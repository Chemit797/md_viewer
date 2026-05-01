# Protenix 推理脚本深度分析报告

本报告旨在详细拆解 `run_protenix_inference.sh` 脚本的完整工作流。该脚本是第四届世界科学智能大赛“生物结构预测赛道”官方提供的一键化自动推理脚本，其核心作用是自动化完成从环境配置、数据读取、AI推理（预测RNA-蛋白复合物三维结构）到最终打包提交文件的全过程。

---

## 一、 脚本开头与全局配置 (Line 1-30)

这一部分主要负责声明脚本的运行环境和核心配置参数。

```bash
#!/bin/bash
# ============================================================
# SAISfold 路线A：Protenix 推理一键脚本
# 用法：bash run_protenix_inference.sh
# 环境：Linux + NVIDIA GPU (>=16GB显存) + CUDA
# 已验证：Protenix 0.5.5 + RTX 4090 D (24GB)
# ============================================================

set -e

# ===================== 配置区 =====================
# 模型名称（必须用 v0.5.0 后缀！v1.0.0 会报 not supported）
MODEL_NAME="protenix_base_default_v0.5.0"
# 赛题JSON所在目录（相对于脚本位置）
SCRIPT_DIR="$(cd "$(dirname "$0")" && pwd)"
JSON_DIR="${SCRIPT_DIR}/赛题"
# 输出目录
OUTPUT_BASE="${SCRIPT_DIR}/protenix_outputs"
# 是否使用MSA（必须关闭，MSA服务器不可达）
USE_MSA=false
# 采样数（赛题2较大，建议1；其余可用默认5）
# 留空则使用Protenix默认值(5)
SAMPLE_NUM=""
# ===================== 配置区结束 =====================

echo "============================================"
echo " SAISfold 路线A - Protenix 推理一键脚本"
echo " 模型: ${MODEL_NAME}"
echo " MSA: ${USE_MSA}"
echo "============================================"
```

> [!NOTE]
> **解读与预测原理：**
> - `set -e`：这是 Shell 脚本的防御机制，遇到任何一个报错立刻停止执行，防止出现因为前一步环境没配好导致后面生成“假数据”的情况。
> - `MODEL_NAME`：指定了模型版本为 `v0.5.0`。不同的版本对应的底层神经网络架构和训练好的权重参数是不同的。
> - `USE_MSA=false`：**非常关键的一点**。蛋白质/RNA 预测常常依赖 **MSA (Multiple Sequence Alignment，多序列比对)**，即寻找自然界中进化相关序列的保守性来辅助判断哪些氨基酸在空间上离得很近。但由于此处 MSA 服务器不可用，脚本选择“单序列（Single Sequence）”预测模式——这无疑极大地提升了预测的难度，完全依赖大模型在大量数据中内化的单序列特征。

---

## 二、 Step 1: 环境检查与准备 (Line 32-52)

AI 推理对硬件和基础软件的要求极高，因此在干活前需要进行严格的前置检查。

```bash
# ---------- Step 1: 环境检查与准备 ----------
echo ""
echo "[Step 1/5] 环境检查..."

# 检查GPU
if command -v nvidia-smi &> /dev/null; then
    GPU_INFO=$(nvidia-smi --query-gpu=name,memory.total --format=csv,noheader 2>/dev/null || echo "unknown")
    echo "  GPU: ${GPU_INFO}"
else
    echo "  ❌ 未检测到 nvidia-smi，必须有 NVIDIA GPU 才能运行！"
    exit 1
fi

# 检查Python
if ! command -v python &> /dev/null; then
    echo "  ❌ 未找到 python，请先安装 Python 3.10+"
    exit 1
fi
PY_VER=$(python -c "import sys; print(f'{sys.version_info.major}.{sys.version_info.minor}')")
echo "  Python: ${PY_VER}"
```

> [!IMPORTANT]
> **硬件要求：**
> 脚本在这里通过调用 `nvidia-smi` 确保系统中有 NVIDIA 显卡。空间结构的预测会涉及到大量张量（Tensor）的矩阵乘法，CPU 是算不动的，只能依赖 GPU。

---

## 三、 Step 2: 安装核心推理库 Protenix (Line 53-100)

在确认底层环境没问题后，脚本自动为你处理复杂的 Python 依赖关系。

```bash
# ---------- Step 2: 安装 Protenix ----------
echo ""
echo "[Step 2/5] 安装 Protenix..."

if python -c "import protenix" 2>/dev/null; then
    PROT_VER=$(python -c "import importlib.metadata; print(importlib.metadata.version('protenix'))" 2>/dev/null || echo "unknown")
    echo "  Protenix 已安装: v${PROT_VER}"
else
    echo "  pip install protenix (首次安装需要几分钟)..."
    pip install protenix
fi

# 卸载 deepspeed（否则 CLI 启动报 ImportError）
if python -c "import deepspeed" 2>/dev/null; then
    echo "  检测到 deepspeed，卸载中（推理不需要，会导致 ImportError）..."
    pip uninstall deepspeed -y
else
    echo "  deepspeed 未安装，无需处理"
fi

# 验证 CLI 可用并自动检测命令格式（不同版本差异很大）
if ! protenix --help &> /dev/null; then
    echo "  ❌ protenix CLI 启动失败！请检查上方错误信息"
    exit 1
fi

# 自动检测 CLI 命令格式
# 新版(如0.5.5)：protenix predict --input --out_dir --model_name --use_msa
# 旧版(如0.3.x)：protenix pred -i -o -n
if protenix predict --help &> /dev/null 2>&1; then
    CLI_CMD="predict"
    FLAG_INPUT="--input"
    FLAG_OUTDIR="--out_dir"
    FLAG_MODEL="--model_name"
    FLAG_MSA="--use_msa"
    FLAG_SAMPLE="--sample"
    echo "  CLI 格式: 新版 (protenix predict --input ...)"
else
    CLI_CMD="pred"
    FLAG_INPUT="-i"
    FLAG_OUTDIR="-o"
    FLAG_MODEL="-n"
    FLAG_MSA=""
    FLAG_SAMPLE="-s"
    echo "  CLI 格式: 旧版 (protenix pred -i ...)"
fi
echo "  protenix CLI 验证通过 ✓"
```

> [!WARNING]
> **排坑与容错：**
> 这里有两个极为巧妙的排坑设计：
> 1. **强制卸载 DeepSpeed**：DeepSpeed 通常被用于大规模分布式训练，但如果在纯推理（Inference）环境导入，经常会引发环境兼容性导致的 `ImportError`，卡死很多新手。
> 2. **自适应版本参数**：Protenix 工具处于高频迭代期，旧版本（v0.3.x）和新版本（v0.5.5）的命令参数前缀（`-i` 与 `--input`）发生了大改版。脚本通过探测功能，自动适配不同版本的指令格式，保证兼容性。

---

## 四、 Step 3: 读取比赛靶点数据 (Line 101-119)

准备将要预测的数据。

```bash
# ---------- Step 3: 检查赛题文件 ----------
echo ""
echo "[Step 3/5] 检查赛题文件..."

if [ ! -d "${JSON_DIR}" ]; then
    echo "  ❌ 赛题目录不存在: ${JSON_DIR}"
    exit 1
fi

JSON_COUNT=$(ls "${JSON_DIR}"/*.json 2>/dev/null | wc -l)
if [ "${JSON_COUNT}" -eq 0 ]; then
    echo "  ❌ 赛题目录中未找到 .json 文件: ${JSON_DIR}"
    exit 1
fi
echo "  找到 ${JSON_COUNT} 个赛题文件:"
for f in "${JSON_DIR}"/*.json; do
    echo "    - $(basename "$f")"
done
```

> [!NOTE]
> **数据输入格式：**
> AI 不需要看到细胞或者真实的生化试剂，它需要的是信息。赛题目录中的 JSON 文件包含着待预测的靶点序列（如 `ATGC...` 等字母组成的文本字符串）。这些字母就是生命基础物质的密码。

---

## 五、 Step 4: 核心预测执行引擎 (Line 120-163)

这是脚本最核心的功能区域。它将前三步准备好的材料“下锅”，开始真正的 AI 推理。

```bash
# ---------- Step 4: 逐个运行推理（串行，避免OOM） ----------
echo ""
echo "[Step 4/5] 运行 Protenix 推理（串行执行）..."
mkdir -p "${OUTPUT_BASE}"

SUCCESS_COUNT=0
FAIL_COUNT=0

for json_file in "${JSON_DIR}"/*.json; do
    [ ! -f "$json_file" ] && continue

    basename_noext=$(basename "$json_file" .json)
    OUT_DIR="${OUTPUT_BASE}/${basename_noext}"

    echo ""
    echo "  ──────────────────────────────────"
    echo "  推理: ${basename_noext}.json"
    echo "  输出: ${OUT_DIR}"
    echo "  ──────────────────────────────────"

    # 构建推理命令（自动适配新旧版本CLI）
    CMD="protenix ${CLI_CMD} ${FLAG_INPUT} ${json_file} ${FLAG_OUTDIR} ${OUT_DIR} ${FLAG_MODEL} ${MODEL_NAME}"
    # MSA 标志（旧版无此参数）
    if [ -n "${FLAG_MSA}" ]; then
        CMD="${CMD} ${FLAG_MSA} ${USE_MSA}"
    fi
    # 如果指定了采样数则加上
    if [ -n "${SAMPLE_NUM}" ]; then
        CMD="${CMD} ${FLAG_SAMPLE} ${SAMPLE_NUM}"
    fi

    echo "  命令: ${CMD}"

    SECONDS=0
    if eval "${CMD}"; then
        ELAPSED=${SECONDS}
        echo "  ✓ ${basename_noext} 推理完成！耗时: $((ELAPSED/60))分$((ELAPSED%60))秒"
        SUCCESS_COUNT=$((SUCCESS_COUNT + 1))
    else
        echo "  ✗ ${basename_noext} 推理失败！"
        FAIL_COUNT=$((FAIL_COUNT + 1))
    fi
done
```

> [!TIP]
> **串行执行防爆显存：**
> 这里采用 `for` 循环一个接一个地预测靶点（串行），而并非采用并行多线程同时预测。由于大分子折叠预测对显存的消耗极大，若同时将多个序列喂入 GPU 计算，瞬间就会引发 OOM (Out Of Memory，显存溢出)。
> **预测发生了什么？**
> 当执行 `$CMD`（即 `protenix predict ...`）时，模型架构接收 1 维的长序列输入，通过其内部的 Transformer 层不断交换氨基酸、核苷酸残基之间的空间信息，最后通过一个坐标投影模块，生成包含了每个原子精确三维空间坐标（X, Y, Z）的 3D 模型结构文件。

---

## 六、 Step 5: 结果收集与打包上传 (Line 164-210)

将分散的中间结构文件进行清洗，提取最优结果打包以供直接提交比赛。

```bash
# ---------- Step 5: 收集输出 CIF 文件，打包提交 ----------
echo ""
echo "[Step 5/5] 收集输出文件，打包提交..."

SUBMIT_DIR="${OUTPUT_BASE}/submit"
mkdir -p "${SUBMIT_DIR}"

for json_file in "${JSON_DIR}"/*.json; do
    [ ! -f "$json_file" ] && continue
    basename_noext=$(basename "$json_file" .json)

    # Protenix 输出的 CIF 文件路径模式：
    # {out_dir}/{name}/seed_101/predictions/{name}_seed_101_sample_0.cif
    # 取 sample_0（最佳采样）作为提交结果
    found_cif=$(find "${OUTPUT_BASE}/${basename_noext}" -name "*_sample_0.cif" -type f 2>/dev/null | head -1)

    if [ -n "$found_cif" ]; then
        cp "${found_cif}" "${SUBMIT_DIR}/${basename_noext}_pred.cif"
        FILE_SIZE=$(du -h "${found_cif}" | cut -f1)
        echo "  ✓ ${basename_noext}_pred.cif (${FILE_SIZE})"
    else
        echo "  ✗ 未找到 ${basename_noext} 的 CIF 输出！"
        echo "    输出目录内容:"
        find "${OUTPUT_BASE}/${basename_noext}" -type f 2>/dev/null | head -10 | sed 's/^/      /'
    fi
done

# 打包成 output.zip
ZIP_PATH="${OUTPUT_BASE}/output.zip"
if ls "${SUBMIT_DIR}"/*.cif &> /dev/null; then
    cd "${SUBMIT_DIR}"
    zip -j "${ZIP_PATH}" *.cif
    cd "${SCRIPT_DIR}"

    echo ""
    echo "============================================"
    echo " 完成！成功: ${SUCCESS_COUNT}, 失败: ${FAIL_COUNT}"
    echo " 提交文件: ${ZIP_PATH}"
    echo " 内容:"
    unzip -l "${ZIP_PATH}"
    echo "============================================"
else
    echo ""
    echo "❌ 没有成功生成任何 CIF 文件，无法打包！"
    exit 1
fi
```

> [!NOTE]
> **最佳结果提取：**
> 在 AI 预测这种具有高度不确定性的多聚物结构时，单次推断往往不够。默认情况下，模型在相同的输入下会通过设置不同的随机种子（seed）采样多种不同的折叠构象方案（例如生成 5 个结构）。
> 模型内部置信度评分系统（Ranking Score / pLDDT 等指标）会对生成的这些结构进行打分排序。
> 脚本代码 `find ... -name "*_sample_0.cif"` 的目的就是精准找到**模型认为得分最高、置信度最好的第一个构象 (sample_0)**，忽略其他置信度较低的结果。
> 最后使用 `zip -j` 指令忽略掉杂乱的文件夹层级，直接把这几个核心的 `.cif` 结构文件打成一个包，参赛者可以直接拿着这个 ZIP 包在平台提交。
