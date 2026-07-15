# 虚拟 T 细胞(HIV × T 细胞 计算建模)——独立文献测绘与问题图谱

> **本轮定位**:独立、脱钩的领域测绘。本文档全部分类、大问题、小问题均归纳自本轮实际检索并经 PubMed 逐条核实的文献,未读取、未引用、未参照本项目任何既往产出(报告/idea 清单/打分表/场景清单/summary/extraction),亦未以记忆中的既往方向为起点。

> **检索与核实**:主力检索与核实通道为 PubMed(`search_articles` + `get_article_metadata`);每条参考的 PMID 均实测返回题目,DOI 与 PubMed 记录逐条比对(**206 条参考、DOI 比对零冲突**)。OpenAlex 连接器本轮不可用(见 Part V),arXiv 受限流限制,故 NeurIPS/ICML 等纯 ML 会议预印本未纳入——这会低估"最前沿深度模型"一端,已在 Part V 如实记录。

> **检索陷阱规避**:全程未使用字面词 “virtual T cell”(避免被真实免疫学概念 *virtual memory T cell, TVM* 污染),改用具体组学/方法/机制关键词的交叉组合。

> **规模**:去重后共 **206** 条经核实参考(各部分标签计数 Part I 38 · Part II-A 47 · II-B 40 · II-C 31 · Part III 新增源 52,和为 208;其中 2 条被跨部分/跨模块标注、按去重只计一次,故去重后总数为 206);Part III 采集 **64** 个原子问题,归纳为 **5** 个大问题、**23** 个小问题 + 2 个独立条目。远超"Part I+II+III 合计 ≥60 篇"底线。

> **立场红线**:本轮不做优劣评判、不给战略建议、不推荐优先级、不预判任何特定框架(含超图神经网络)是否适用;Part IV 的"gap"只描述"有没有",不判断"该不该"。


*生成日期:2026-07-15;检索/核实工具:PubMed E-utilities(经连接器)。*


---

# Part I — 领域基座:虚拟细胞 / 虚拟免疫细胞作为一个研究范式

> 本章为独立检索测绘,所有条目均经 PubMed 实际检索并逐条核实(题目 + DOI/PMID 均返回)。检索刻意避开字面词 "virtual T cell"(易被真实生物学概念 virtual memory T cell 污染),改用具体的组学 / 方法 / 机制关键词组合(AI virtual cell、foundation model single-cell、digital twin immune、generative perturbation prediction、in silico immune modeling、LLM agent biology 等),年份跨度 2018–2026。本轮共纳入 38 篇有区分度的文献:30 篇综述 / 展望 / 评测类(含 1 篇地基展望),8 篇被反复引用、构成方法学地基的原创论文(module='地基方法')。

## 1. 概念版图:什么是"虚拟细胞"

"虚拟细胞"并非单一技术,而是一族在不同社区、以不同名字发展起来的建模范式。本轮检索显示,至少存在四条彼此交叠但出发点不同的脉络:

**(a) AI 虚拟细胞(AI Virtual Cell, AIVC)——大型神经网络作为通用细胞表征与模拟器。** 这一脉络最具纲领性的文本是 Bunne、Roohani 等联合 CZI / Stanford / Genentech 提出的路线图,把 AIVC 定义为一个多尺度、多模态的大型神经网络,既提供跨分子—细胞—组织尺度的"通用表征(universal representation)",又能执行"in silico 虚拟实验(可查询、可扰动)"[Cell 2024]。随后一批综述沿此展开并各有侧重:Ma 等强调临床前研究中的技术路径、验证机制与转化潜力[npj Digit Med 2025];多篇 2026 年综述分别从多尺度耦合(Brief Bioinform)、临床视角(J Int Med Res)、以及药物发现中的"情境依赖"难题(Br J Pharmacol)切入。

**(b) 数字孪生(Digital Twin)——从工程学移植到医学的个体化动态模型。** 这条脉络把"孪生"从工业系统移植到细胞乃至整个患者。Lancet Digit Health 指出该领域尚缺乏对数字孪生"构成要素"的共识,需回到工程学范式澄清;Genome Med 则把数字孪生上升为"全局学习型健康 / 疾病模型";生成式 AI 被视为让数字孪生可跨尺度模拟的引擎(Expert Opin Drug Discov)。在免疫方向,npj Syst Biol Appl 专门综述了"免疫数字孪生"的应用、局限与挑战。

**(c) 基础模型 / 单细胞语言模型——把细胞当作"语言"来预训练。** 这是当前最活跃的技术底座。多篇方法学综述(Natl Sci Rev、Comput Biol Med、J Transl Med、Exp Mol Med)系统梳理了从 NLP 迁移到细胞 / 分子"语言"的预训练框架,并把评测与可解释性列为共同短板。

**(d) 机制建模 / 系统免疫学——数据驱动之外的另一半。** Trends Immunol、Nat Immunol、eLife(肿瘤系统免疫学)等提醒:数据驱动与简约机制建模是互补而非替代关系;Nat Biotechnol(2026)以"Toward mechanistic virtual immune cells"为题提出机制性虚拟免疫细胞的展望(该文 PubMed 未返回摘要,此处仅据标题概括,正文论点未经核实)。

值得注意的是,本轮已检到一篇直接把虚拟细胞与 HIV/AIDS 治疗关联的综述(Microb Pathog 2026),它把 VC 定位为模拟 HIV 感染细胞行为、辅助治疗探索的计算范式——这为本课题("虚拟 T 细胞" HIV × T 细胞建模)提供了一个明确的领域接口。

## 2. 免疫特化:虚拟免疫细胞与 T 细胞

在通用虚拟细胞之上,免疫方向已有自身的问题谱系与瓶颈判断:

- **T 细胞特异性预测**是免疫虚拟细胞最硬的骨头。Hudson 等(Nat Rev Immunol 2023)以蛋白结构预测的突破为参照,判断 TCR-pMHC 识别预测远未达到"AlphaFold 时刻",数据偏倚与泛化到未见表位是核心障碍;Front Immunol(2023)从定量方法角度呼应了这一诊断。
- **系统 / 分布式视角**:Nat Immunol 的"systems-level immunomics"指南提供了免疫系统"状态空间"的框架——成百上千细胞状态并行、通路动态协同,这是任何虚拟免疫细胞都要面对的复杂度基线。
- **应用出口**:CAR-T 工程(Phys Life Rev 2026)、"in silico 患者"预测个体化药物响应(Biochem Pharmacol 2026)、AI 虚拟类器官(Bioact Mater 2025)代表了虚拟(免疫)细胞走向转化的三个不同尺度。

## 3. 方法学地基:被反复引用的原创工作

围绕上述综述反复出现、构成"地基"的原创方法论文(以本轮实际检索到的为准),可归为三类:

1. **概率 / 生成式表征**:scVI(Nat Methods 2018)把变分推断引入单细胞,是概率建模的基石;深度生成模型综述(Comput Biol Med 2024)对这一支做了系统化。
2. **单细胞基础模型**:Geneformer(Nature 2023,迁移学习)、scGPT(Nat Methods 2024,生成式 Transformer)、scFoundation(Nat Methods 2024,大规模)、UCE(Nature 2026,跨物种通用表征)、EpiAgent(Nat Methods 2025,表观模态)共同勾勒出"单细胞语言模型"从可行性到多模态扩展的轨迹。
3. **可执行虚拟实验(in silico 扰动)**:CellOracle(Nature 2023,GRN + TF 扰动)、GEARS(Nat Biotechnol 2023,图神经网络预测多基因组合扰动)、以及"扰动细胞与组织图谱"路线(Cell 2024)把"虚拟实验"从愿景落到可计算的机制工具。

## 4. 冷静的对照:能力评测与批判

领域并非一味乐观。两篇 2025 年 Nat Methods 评测提供了必要的对照:其一发现"基于深度学习的基因扰动效应预测尚未超越刻意简单的线性基线",直接对虚拟细胞"预测扰动"这一核心卖点提出冷静评估;其二系统评测可泛化的单细胞扰动响应预测,指出泛化到未见 / 组合扰动是主要瓶颈。这两篇提示:**虚拟(免疫)细胞的每一项"能力"都应配强基线与泛化测试来验证**,而非仅报告拟合精度。

## 5. 对"虚拟细胞该怎么建"的收敛判断(基于本轮文献)

综合本轮检索,领域内反复出现、相对收敛的判断有:
1. **通用表征 + 可执行虚拟实验**是两大核心能力(Bunne 等的双支柱)。
2. **多模态、多尺度**是共识方向,但**跨尺度耦合(分子↔细胞↔组织)**被普遍列为最大难点。
3. **数据驱动与机制建模互补**,纯黑箱不足以支撑免疫等强机制系统(机制性虚拟免疫细胞、系统免疫学两条脉络的共同主张)。
4. **验证机制、强基线与泛化评测**是可信度前提,而非事后补充。
5. **情境依赖(context-dependence)**是把虚拟细胞用于药物发现 / 免疫治疗的中心难题。

---
*检索方法说明:PubMed 为主力检索源;OpenAlex 本轮未接入、arXiv 限流,故 ML 会议论文若 PubMed 无记录则未纳入(未编造 DOI)。所有 38 条均 verified=true(题目 + DOI/PMID 经 get_article_metadata 返回确认)。*

### Part I 参考文献一览(全部 PMID+DOI 经 PubMed 核实)

| Key | 题目 | 期刊/会议 | 年 | DOI | PMID |
|---|---|---|---|---|---|
| scvi2018 | Deep generative modeling for single-cell transcriptomics. | Nat Methods | 2018 | https://doi.org/10.1038/s41592-018-0229-2 | 30504886 |
| elife2020cancersysimm | Cancer systems immunology. | Elife | 2020 | https://doi.org/10.7554/eLife.53839 | 32657757 |
| ni2022immunomics | A guide to systems-level immunomics. | Nat Immunol | 2022 | https://doi.org/10.1038/s41590-022-01309-9 | 36138185 |
| hudson2023tcellspec | Can we predict T cell specificity with digital biology and machine learning? | Nat Rev Immunol | 2023 | https://doi.org/10.1038/s41577-023-00835-3 | 36755161 |
| ti2023sysimmdt | Towards systems immunology of critical illness at scale: from single cell 'omics to digital twins. | Trends Immunol | 2023 | https://doi.org/10.1016/j.it.2023.03.004 | 36967340 |
| fi2023tcrspec | Quantitative approaches for decoding the specificity of the human T cell repertoire. | Front Immunol | 2023 | https://doi.org/10.3389/fimmu.2023.1228873 | 37781387 |
| geneformer2023 | Transfer learning enables predictions in network biology. | Nature | 2023 | https://doi.org/10.1038/s41586-023-06139-9 | 37258680 |
| celloracle2023 | Dissecting cell identity via network inference and in silico gene perturbation. | Nature | 2023 | https://doi.org/10.1038/s41586-022-05688-9 | 36755098 |
| gears2023 | Predicting transcriptional outcomes of novel multigene perturbations with GEARS. | Nat Biotechnol | 2023 | https://doi.org/10.1038/s41587-023-01905-6 | 37592036 |
| bunne2024virtualcell | How to build the virtual cell with artificial intelligence: Priorities and opportunities. | Cell | 2024 | https://doi.org/10.1016/j.cell.2024.11.015 | 39672099 |
| cbm2024deepgen | Deep generative models in single-cell omics. | Comput Biol Med | 2024 | https://doi.org/10.1016/j.compbiomed.2024.108561 | 38749321 |
| cell2024aiagents | Empowering biomedical discovery with AI agents. | Cell | 2024 | https://doi.org/10.1016/j.cell.2024.09.022 | 39486399 |
| npjsba2024immdt | Immune digital twins for complex human pathologies: applications, limitations, and challenges. | NPJ Syst Biol Appl | 2024 | https://doi.org/10.1038/s41540-024-00450-5 | 39616158 |
| csbj2024perturbmini | A mini-review on perturbation modelling across single-cell omic modalities. | Comput Struct Biotechnol J | 2024 | https://doi.org/10.1016/j.csbj.2024.04.058 | 38721585 |
| eodd2024gendt | Generative artificial intelligence empowers digital twins in drug discovery and clinical trials. | Expert Opin Drug Discov | 2024 | https://doi.org/10.1080/17460441.2023.2273839 | 37887266 |
| scgpt2024 | scGPT: toward building a foundation model for single-cell multi-omics using generative AI. | Nat Methods | 2024 | https://doi.org/10.1038/s41592-024-02201-0 | 38409223 |
| scfoundation2024 | Large-scale foundation model on single-cell transcriptomics. | Nat Methods | 2024 | https://doi.org/10.1038/s41592-024-02305-7 | 38844628 |
| perturbcellatlas2024 | Toward a foundation model of causal cell and tissue biology with a Perturbation Cell and Tissue Atlas. | Cell | 2024 | https://doi.org/10.1016/j.cell.2024.07.035 | 39178831 |
| ma2025aivirtualcell | AI-driven virtual cell models in preclinical research: technical pathways, validation mechanisms, and clinical translation potential. | NPJ Digit Med | 2025 | https://doi.org/10.1038/s41746-025-02198-6 | 41381900 |
| nsr2025foundbioinf | Foundation models in bioinformatics. | Natl Sci Rev | 2025 | https://doi.org/10.1093/nsr/nwaf028 | 40078374 |
| jtm2025scomicsfm | Transformative advances in single-cell omics: a comprehensive review of foundation models, multimodal integration and computational ecosystems. | J Transl Med | 2025 | https://doi.org/10.1186/s12967-025-07091-0 | 41146276 |
| ldh2025meddt | Medical digital twins: enabling precision medicine and medical artificial intelligence. | Lancet Digit Health | 2025 | https://doi.org/10.1016/j.landig.2025.02.004 | 40518342 |
| gm2025dtwins | Digital twins as global learning health and disease models for preventive and personalized medicine. | Genome Med | 2025 | https://doi.org/10.1186/s13073-025-01435-7 | 39920778 |
| bam2025aivo | Artificial Intelligence Virtual Organoids (AIVOs). | Bioact Mater | 2025 | https://doi.org/10.1016/j.bioactmat.2025.12.030 | 41536916 |
| natm2025perturbnooutperform | Deep-learning-based gene perturbation effect prediction does not yet outperform simple linear baselines. | Nat Methods | 2025 | https://doi.org/10.1038/s41592-025-02772-6 | 40759747 |
| natm2025perturbbench | Benchmarking algorithms for generalizable single-cell perturbation response prediction. | Nat Methods | 2025 | https://doi.org/10.1038/s41592-025-02980-0 | 41381899 |
| epiagent2025 | EpiAgent: foundation model for single-cell epigenomics. | Nat Methods | 2025 | https://doi.org/10.1038/s41592-025-02822-z | 40999099 |
| beusch2026mechvic | Toward mechanistic virtual immune cells. | Nat Biotechnol | 2026 | https://doi.org/10.1038/s41587-026-03139-8 | 42350645 |
| multiscale2026vc | Multiscale predictive cellular modeling: integrating hypothesis grammars, digital twins, and multi-omics for In silico oncology and precision theranostics. | Funct Integr Genomics | 2026 | https://doi.org/10.1007/s10142-026-01890-4 | 42213163 |
| bib2026multiscalevc | Artificial intelligence-enabled multi-scale virtual cell: perspective, challenges, and opportunities. | Brief Bioinform | 2026 | https://doi.org/10.1093/bib/bbag104 | 41795653 |
| jimr2026virtualcell | Virtual cell: Current perspectives and future prospects. | J Int Med Res | 2026 | https://doi.org/10.1177/03000605261425080 | 42200280 |
| bjp2026vcdrug | Virtual cell construction for artificial intelligence-driven drug discovery. | Br J Pharmacol | 2026 | https://doi.org/10.1111/bph.70585 | 42429061 |
| emm2026llmbiochem | A survey on large language models in biology and chemistry. | Exp Mol Med | 2026 | https://doi.org/10.1038/s12276-025-01583-1 | 41258076 |
| bib2026llmagents | Large language model agents for biological intelligence across genomics, proteomics, spatial biology, and biomedicine. | Brief Bioinform | 2026 | https://doi.org/10.1093/bib/bbag110 | 41883029 |
| bcp2026insilicopat | Integrating single-cell atlases and machine learning to construct 'in silico patients' for predicting individualized drug responses. | Biochem Pharmacol | 2026 | https://doi.org/10.1016/j.bcp.2026.117873 | 41796725 |
| plr2026cart | AI-driven cellular immunotherapy: transforming CAR-T engineering and translation. | Phys Life Rev | 2026 | https://doi.org/10.1016/j.plrev.2026.06.007 | 42349054 |
| micpath2026hivvc | Virtual cell/virtual cell like: The key to unlocking a new era of HIV/AIDS treatment ? | Microb Pathog | 2026 | https://doi.org/10.1016/j.micpath.2026.108459 | 41912072 |
| uce2026 | Universal cell embedding provides a foundation model for cell biology. | Nature | 2026 | https://doi.org/10.1038/s41586-026-10689-z | 42420460 |


---

## Part II — T 细胞免疫学的机器学习图景(按组学模块整理)

> 每个模块内部由大到小:先通用 T 细胞/免疫 ML 图景,再聚焦 HIV;每模块含代表文献(PMID+DOI 均核实)、公开数据资源、HIV 数据丰度评级、方法学成熟度评级。

### Part II · 模块组 A:转录组学 / 表观基因组学 / 蛋白质组学

# Part II 模块 A:转录组学 / 表观基因组学 / 蛋白质组学
**T 细胞相关机器学习 / 计算工作梳理(以 HIV × T 细胞为重点,不排他)**

> **检索与核实说明**:本节全部条目来自本轮针对 PubMed 的独立检索,并逐条经 `get_article_metadata` 核实(PMID + DOI + 期刊 + 年份均成功返回者才标 `verified=true`)。检索刻意避开字面词 “virtual T cell”(以免被 “virtual memory T cell / TVM” 概念污染),改用具体组学 / 方法 / 机制关键词组合,多角度、多措辞、跨年份(2014–2026)分别检索。本轮 OpenAlex 未接入 key、arXiv 限流,故以 PubMed 为主力;纯机器学习会议论文若 PubMed 未收录则本轮未纳入,不编造 DOI。结论用词从严:凡未经多轮多角度确认者一律表述为“在本轮检索范围内”。

---

## 模块 1 · 转录组学(bulk RNA-seq / 单细胞 scRNA-seq)

### 1.1 方法图景:由大到小

**大的一端(T 细胞 / 免疫学一般语境):** 转录组机器学习已形成较完整层级——(a)**降维与生成建模**:变分自编码器(VAE)系是单细胞转录组主流表征工具,既做降维也做可解释因子建模(线性解码 VAE / scVI 系),并延伸到用 VAE 对转录动力学作生物物理建模;(b)**数据整合与细胞类型标注**:半监督深度生成模型(scANVI 类)做概率性跨数据集整合与标注,大规模监督式注释模型已覆盖数百种人类细胞类型并向跨组织统一注释扩展,针对强批次效应的整合算法亦是活跃基准方向;(c)**基因调控网络(GRN)**:SCENIC 系(regulon 推断)是从 scRNA-seq 联合刻画转录因子调控程序、据此定义细胞状态的经典方法;(d)**T 细胞 / TCR 专用建模**:面向单个 T 细胞转录组的可解释深度框架(MIST),以及将 TCR 库用于癌症早筛或预测肿瘤反应性受体的深度模型。

**小的一端(HIV):** scRNA-seq 已成为解剖 HIV 潜伏库与免疫功能障碍的核心手段——单细胞刻画感染者免疫细胞耗竭图谱、平行分析单个前病毒的转录/整合/序列、组织(如胃肠道)储存库异质性、影响结局的单核细胞表达谱等,均在本轮检索中出现。

### 1.2 代表性工作

**通用 / 免疫学方法端:**
- **[Svensson2020]** LDVAE/scVI 系变分自编码器,用可解释线性解码器对 scRNA-seq 做因子建模,兼顾降维与因子可解释性。 — *Interpretable factor models of single-cell RNA-seq via variational autoencoders.* (Bioinformatics (Oxford, England), 2020; PMID 32176273, DOI: 10.1093/bioinformatics/btaa169)
- **[Xu2021]** scANVI:深度生成模型对单细胞转录组做概率性数据整合与细胞类型标注(半监督)。 — *Probabilistic harmonization and annotation of single-cell transcriptomics data with deep generative models.* (Molecular systems biology, 2021; PMID 33491336, DOI: 10.15252/msb.20209620)
- **[Aibar2017]** SCENIC:从 scRNA-seq 联合推断转录因子调控网络(regulon)并据此聚类细胞状态,经典 GRN 方法。 — *SCENIC: single-cell regulatory network inference and clustering.* (Nature methods, 2017; PMID 28991892, DOI: 10.1038/nmeth.4463)
- **[Dong2024]** 跨 265 种人类细胞类型的深度学习单细胞注释模型,展示大规模监督式细胞类型识别。 — *Single-cell type annotation with deep learning in 265 cell types for humans.* (Bioinformatics advances, 2024; PMID 38645719, DOI: 10.1093/bioadv/vbae054)
- **[Fischer2023]** 可扩展的跨组织单细胞注释模型,面向大型细胞图谱做统一标注。 — *Scaling cross-tissue single-cell annotation models.* (bioRxiv : the preprint server for biology, 2023; PMID 37873298, DOI: 10.1101/2023.10.07.561331)
- **[Hrovatin2024]** 针对存在显著批次效应的 scRNA-seq 数据集的整合方法(基准与算法)。 — *Integrating single-cell RNA-seq datasets with substantial batch effects.* (bioRxiv : the preprint server for biology, 2024; PMID 37961672, DOI: 10.1101/2023.11.03.565463)
- **[Lai2025]** MIST:面向单个 T 细胞转录组的可解释、灵活深度学习框架。 — *MIST: An interpretable and flexible deep learning framework for single-T cell transcriptome and receptor analysis.* (Science advances, 2025; PMID 40184452, DOI: 10.1126/sciadv.adr7134)
- **[Cai2024]** iCanTCR:用 T 细胞受体库(TCR)做早期癌症检测的深度学习框架。 — *The Deep Learning Framework iCanTCR Enables Early Cancer Detection Using the T-cell Receptor Repertoire in Peripheral Blood.* (Cancer research, 2024; PMID 38536129, DOI: 10.1158/0008-5472.can-23-0860)
- **[Tan2024]** 从 scRNA-seq 预测肿瘤反应性 T 细胞受体,用于个性化 T 细胞治疗。 — *Prediction of tumor-reactive T cell receptors from scRNA-seq data for personalized T cell therapy.* (Nature biotechnology, 2024; PMID 38454173, DOI: 10.1038/s41587-024-02161-y)
- **[Carilli2023]** 变分自编码器做双模态单细胞 RNA 的生物物理建模(转录动力学)。 — *Biophysical modeling with variational autoencoders for bimodal, single-cell RNA sequencing data.* (bioRxiv : the preprint server for biology, 2023; PMID 36712140, DOI: 10.1101/2023.01.13.523995)

**HIV 端:**
- **[Wang2020]** 单细胞测序构建 HIV 感染者免疫细胞耗竭图谱,刻画外周 T 细胞耗竭异质性。 — *An atlas of immune cell exhaustion in HIV-infected individuals revealed by single-cell transcriptomics.* (Emerging microbes & infections, 2020; PMID 32954948, DOI: 10.1080/22221751.2020.1826361)
- **[Einkauf2022]** 单个 HIV 前病毒的转录、整合位点与序列平行分析(单细胞多维定位潜伏库)。 — *Parallel analysis of transcription, integration, and sequence of single HIV-1 proviruses.* (Cell, 2022; PMID 35026153, DOI: 10.1016/j.cell.2021.12.011)
- **[Iyer2025]** 综述:单细胞转录组测序对 HIV-1 持续/潜伏库认识的最新进展。 — *Current insight into HIV-1 persistence from single-cell transcriptome profiling in acutely treated cohorts of infection.* (Current opinion in HIV and AIDS, 2025; PMID 40638066, DOI: 10.1097/coh.0000000000000962)
- **[Peterson2025]** 单细胞刻画胃肠道 HIV 储存库,揭示组织内异质性。 — *Single-cell characterization of the gastrointestinal HIV reservoir reveals heterogeneous cellular phenotypes.* (The Journal of clinical investigation, 2025; PMID 41433124, DOI: 10.1172/jci196536)
- **[Ehrenberg2025]** 单细胞分析识别影响 HIV 结局的单核细胞基因表达谱。 — *Single-cell analyses identify monocyte gene expression profiles that influence HIV-1 reservoir size in acutely treated cohorts.* (Nature communications, 2025; PMID 40442100, DOI: 10.1038/s41467-025-59833-9)
- **[Kulkarni2023]** HIV 合并感染的单细胞转录组学分析。 — *Single-Cell Transcriptomics of/HIV Co-Infection.* (Cells, 2023; PMID 37759517, DOI: 10.3390/cells12182295)

### 1.3 代表性公开数据资源

- **GEO(Gene Expression Omnibus)**:bulk 与单细胞 RNA-seq 的主入口,T 细胞/HIV 相关系列极多(检索 “CD4 HIV scRNA-seq” 可得数百个 GSE 系列);量级:全库数百万样本级。
- **SRA / ENA**:原始测序读段归档,HIV 感染 CD4/PBMC 的 raw reads 多在此。
- **Human Cell Atlas(HCA)Data Portal**:大规模人类单细胞图谱(含免疫/T 细胞图谱),百万细胞级。
- **CELLxGENE Discover(CZ)**:标准化单细胞表达矩阵浏览与下载,含多套 T 细胞/PBMC 数据集。
- **ImmPort**:免疫学研究(含 HIV 队列)转录组与临床元数据共享平台。
- **专题 HIV 库/图谱**:上述潜伏库单细胞研究多把矩阵存放于 GEO(如 Einkauf/Collora/Wei 等对应 GSE)。

### 1.4 HIV 语境数据丰度评估:**中等偏充裕**。HIV 单细胞转录组近 5 年快速增长(潜伏库、组织储存库、合并感染),但受限于储存库细胞极稀有、样本可及性与伦理,单个研究细胞数常偏少,“真感染/前病毒阳性”细胞的标注数据仍稀缺。

### 1.5 方法学成熟度:**较成熟(深度学习 + 经典 ML 并存)**。通用单细胞侧深度生成模型/整合/注释已工业化;HIV 侧仍以差异表达、聚类、轨迹等经典分析为主,深度学习专门化模型(HIV 特异)在本轮检索范围内仍较少,机制性建模(把转录状态与前病毒命运耦合)刚起步。


---

## 模块 2 · 表观基因组学 / 染色质可及性(ATAC-seq, ChIP-seq, DNA 甲基化)

### 2.1 方法图景:由大到小

**大的一端:**(a)**染色质可及性的序列深度学习**:碱基分辨率、去偏模型(ChromBPNet)与调控变异效应预测模型(AlphaGenome),把 DNA 序列直接映射到可及性/调控信号;(b)**单细胞表观分析**:chromVAR 从 scATAC-seq 推断转录因子相关可及性偏差,是经典工具;(c)**多组学 GRN**:SCENIC+ 联合 scATAC+scRNA 推断增强子与调控网络,并延伸到从 ATAC-seq 识别差异活跃转录因子;(d)**T 细胞衰老/状态的表观特征**:刻画 T 细胞衰老保守表观遗传特征、以及用转录因子协同逻辑做 T 细胞状态工程;(e)**DNA 甲基化时钟**:与年龄相关疾病/死亡关联的甲基化时钟,以及对免疫细胞组成稳健的改进时钟。

**小的一端(HIV):** 表观层面聚焦潜伏机制——染色质对 HIV-1 潜伏影响的多维视角、潜伏与激活 CD4 T 细胞的单细胞表观+转录+蛋白联合谱、单细胞多组学揭示前病毒在细胞毒性 T 细胞中的持续、储存库细胞免疫选择的表型/整合景观、HIV 感染中 DNA 甲基化改变与表观遗传衰老性别差异等。

### 2.2 代表性工作

**通用 / 免疫学方法端:**
- **[Schep2017]** chromVAR:从单细胞 ATAC-seq 推断转录因子相关的可及性偏差,经典单细胞表观分析工具。 — *chromVAR: inferring transcription-factor-associated accessibility from single-cell epigenomic data.* (Nature methods, 2017; PMID 28825706, DOI: 10.1038/nmeth.4401)
- **[Pampari2025]** ChromBPNet:碱基分辨率、去偏的染色质可及性深度学习模型(序列→可及性)。 — *ChromBPNet: bias factorized, base-resolution deep learning models of chromatin accessibility reveal cis-regulatory sequence syntax, transcription factor footprints and regulatory variants.* (bioRxiv : the preprint server for biology, 2025; PMID 39829783, DOI: 10.1101/2024.12.25.630221)
- **[Avsec2026]** AlphaGenome:面向调控变异效应预测的序列深度学习模型,推进调控基因组预测。 — *Advancing regulatory variant effect prediction with AlphaGenome.* (Nature, 2026; PMID 41606153, DOI: 10.1038/s41586-025-10014-0)
- **[Bravo2023]** SCENIC+:单细胞多组学联合推断增强子与基因调控网络。 — *SCENIC+: single-cell multiomic inference of enhancers and gene regulatory networks.* (Nature methods, 2023; PMID 37443338, DOI: 10.1038/s41592-023-01938-4)
- **[Gerbaldo2024]** 从 ATAC-seq 识别差异活跃转录因子的方法。 — *On the identification of differentially-active transcription factors from ATAC-seq data.* (PLoS computational biology, 2024; PMID 39441876, DOI: 10.1371/journal.pcbi.1011971)
- **[Mi2024]** 刻画 T 细胞衰老在免疫与恶性肿瘤中保守的表观遗传特征。 — *Conserved epigenetic hallmarks of T cell aging during immunity and malignancy.* (Nature aging, 2024; PMID 38867059, DOI: 10.1038/s43587-024-00649-5)
- **[Tomusiak2024]** 构建对免疫细胞组成变化稳健的表观遗传时钟(甲基化年龄)。 — *Development of an epigenetic clock resistant to changes in immune cell composition.* (Communications biology, 2024; PMID 39095531, DOI: 10.1038/s42003-024-06609-4)
- **[Yang2020]** 与年龄相关疾病和死亡率关联的 DNA 甲基化时钟(可被加速)。 — *A DNA methylation clock associated with age-related illnesses and mortality is accelerated in men with combat PTSD.* (Molecular psychiatry, 2020; PMID 32382136, DOI: 10.1038/s41380-020-0755-z)
- **[Savage2026]** 转录因子协同作用实现精确 T 细胞状态工程(调控逻辑建模)。 — *Transcription factor collaboration enables precise T cell state engineering.* (bioRxiv : the preprint server for biology, 2026; PMID 42079248, DOI: 10.64898/2026.04.20.718569)
- **[Han2025]** UUATAC-seq 结合深度学习建模脊椎动物调控序列图景。 — *Modeling the vertebrate regulatory sequence landscape by UUATAC-seq and deep learning.* (Cell, 2025; PMID 40633538, DOI: 10.1016/j.cell.2025.06.020)

**HIV 端:**
- **[Arumugam2021]** 综述/分析:解读 HIV 感染中的 DNA 甲基化改变。 — *Deciphering DNA Methylation in HIV Infection.* (Frontiers in immunology, 2021; PMID 34925380, DOI: 10.3389/fimmu.2021.795121)
- **[Wei2023]** 对潜伏与激活 CD4 T 细胞做单细胞表观遗传、转录与蛋白联合谱分析(HIV)。 — *Single-cell epigenetic, transcriptional, and protein profiling of latent and active HIV-1 reservoir revealed that IKZF3 promotes HIV-1 persistence.* (Immunity, 2023; PMID 37922905, DOI: 10.1016/j.immuni.2023.10.002)
- **[Collora2022]** 单细胞多组学揭示 HIV-1 在扩增的细胞毒性 T 细胞中的持续存在。 — *Single-cell multiomics reveals persistence of HIV-1 in expanded cytotoxic T cell clones.* (Immunity, 2022; PMID 35320704, DOI: 10.1016/j.immuni.2022.03.004)
- **[Jones2025]** 综述:染色质对 HIV-1 潜伏影响的多维视角。 — *Impact of chromatin on HIV-1 latency: a multi-dimensional perspective.* (Epigenetics & chromatin, 2025; PMID 40055755, DOI: 10.1186/s13072-025-00573-x)
- **[Zhao2021]** 整合单细胞分析定义 HIV-1 潜伏逆转的机制。 — *Leveraging Novel Integrated Single-Cell Analyses to Define HIV-1 Latency Reversal.* (Viruses, 2021; PMID 34206546, DOI: 10.3390/v13071197)
- **[Johnston2025]** 老年 HIV 感染者表观遗传衰老的性别差异。 — *Sex differences in epigenetic ageing for older people living with HIV.* (EBioMedicine, 2025; PMID 39923742, DOI: 10.1016/j.ebiom.2025.105588)
- **[Sun2023]** HIV-1 储存库细胞中免疫选择的表型特征(前病毒整合/表观景观)。 — *Phenotypic signatures of immune selection in HIV-1 reservoir cells.* (Nature, 2023; PMID 36599977, DOI: 10.1038/s41586-022-05538-8)

### 2.3 代表性公开数据资源

- **ENCODE**:ATAC-seq / ChIP-seq / DNase 等调控基因组数据的主库,含大量免疫细胞系与原代 CD4/CD8 T 细胞实验。
- **Roadmap Epigenomics**:127 种参考表观组(含 T 细胞子集)的组蛋白修饰/甲基化/可及性图谱。
- **GEO / SRA**:HIV 潜伏相关 ATAC-seq、CUT&RUN、WGBS/EPIC 甲基化芯片数据的主要归档处。
- **JASPAR / UniBind / ENCODE cCREs**:转录因子结合基序与顺式调控元件参考,用于 ATAC/ChIP 下游 motif 分析。
- **ImmGen / DICE**:免疫细胞表观+表达参考(DICE 含人 T 细胞亚群)。
- **Illumina 甲基化芯片队列(如 GEO 上的 HIV 队列 450K/EPIC 数据)**:用于表观遗传时钟/甲基化差异分析。

### 2.4 HIV 语境数据丰度评估:**中等**。HIV 甲基化(芯片队列)与近年单细胞多组学潜伏库数据在增长,但染色质可及性/ChIP 层面因需分选稀有储存库细胞、样本量小,专门针对 HIV 的高质量 ATAC/ChIP 数据仍相对有限。

### 2.5 方法学成熟度:**通用侧成熟、HIV 侧起步**。序列深度学习(ChromBPNet/AlphaGenome)与单细胞多组学 GRN 已相当成熟;HIV 侧多为描述性表观分析与整合,专门的机制性/预测性建模(如从染色质状态预测潜伏逆转)在本轮检索范围内仍处早期。


---

## 模块 3 · 蛋白质组学

### 3.1 方法图景:由大到小

**大的一端:**(a)**从转录组插补/预测表面蛋白**:集成学习与深度学习从 CITE-seq/单细胞转录组预测数千种表面蛋白丰度,是连接转录组与蛋白组的活跃方向;(b)**免疫肽组学(immunopeptidomics)+ 深度学习**:深度学习显著提升质谱免疫肽鉴定灵敏度(DeepRescore、灵敏度提升方法),几何深度学习提升 MHC 结合肽预测泛化;(c)**T 细胞蛋白组统计/ML 分析**:对人 CD4 T 细胞蛋白组谱的统计与机器学习分析;(d)**TCR 信号磷酸化蛋白组学**:早期 TCR 信号磷酸化位点动力学的时间分辨定量。

**小的一端(HIV):** 质谱刻画 HIV-1 感染 CD4 T 细胞蛋白组变化、超急性期血浆蛋白组动态、可预测结局的血浆蛋白组特征(炎症/B 细胞活化)、免疫代谢受损宿主血浆微环境、以及 HIV 合并感染的血浆蛋白组学。

### 3.2 代表性工作

**通用 / 免疫学方法端:**
- **[Xu2020]** 集成学习模型从单细胞多模态(CITE-seq)预测表面蛋白丰度。 — *Ensemble learning models that predict surface protein abundance from single-cell multimodal omics data.* (Methods (San Diego, Calif.), 2020; PMID 33039573, DOI: 10.1016/j.ymeth.2020.10.001)
- **[Chen2024]** cTP-net/类似:从单细胞转录组插补 2500+ 种表面蛋白丰度的深度学习方法。 — *Imputing abundance of over 2,500 surface proteins from single-cell transcriptomes with context-agnostic zero-shot deep ensembles.* (Cell systems, 2024; PMID 39243755, DOI: 10.1016/j.cels.2024.08.006)
- **[Qian2023]** 用深度神经网络在多模态单细胞数据中识别细胞类型特异基因/蛋白。 — *Identification of cell-type-specific genes in multimodal single-cell data using deep neural network algorithm.* (Computers in biology and medicine, 2023; PMID 37738895, DOI: 10.1016/j.compbiomed.2023.107498)
- **[Wilhelm2021]** 深度学习显著提升质谱免疫肽组学(immunopeptidomics)的灵敏度。 — *Deep learning boosts sensitivity of mass spectrometry-based immunopeptidomics.* (Nature communications, 2021; PMID 34099720, DOI: 10.1038/s41467-021-23713-9)
- **[Marzella2024]** 几何深度学习提升 MHC 结合肽预测的泛化能力。 — *Geometric deep learning improves generalizability of MHC-bound peptide predictions.* (Communications biology, 2024; PMID 39702482, DOI: 10.1038/s42003-024-07292-1)
- **[Li2020]** DeepRescore:用深度学习改进免疫肽组学的肽段鉴定。 — *DeepRescore: Leveraging Deep Learning to Improve Peptide Identification in Immunopeptidomics.* (Proteomics, 2020; PMID 32864883, DOI: 10.1002/pmic.201900334)
- **[Suomi2022]** 用统计与机器学习方法研究人 CD4 T 细胞蛋白组谱。 — *Statistical and machine learning methods to study human CD4T cell proteome profiles.* (Immunology letters, 2022; PMID 35381305, DOI: 10.1016/j.imlet.2022.03.006)
- **[Chylek2014]** 早期 T 细胞受体信号传导的磷酸化位点动力学(磷酸化蛋白组学)。 — *Phosphorylation site dynamics of early T-cell receptor signaling.* (PloS one, 2014; PMID 25147952, DOI: 10.1371/journal.pone.0104240)
- **[Vo2025]** 综述:人工智能与免疫肽组学不断演进的研究图景。 — *Artificial Intelligence and the Evolving Landscape of Immunopeptidomics.* (Proteomics. Clinical applications, 2025; PMID 40741879, DOI: 10.1002/prca.70018)

**HIV 端:**
- **[Nemeth2017]** 质谱蛋白组学分析 HIV-1 感染的人 CD4 T 细胞蛋白组变化。 — *andProteome Analysis of Human Immunodeficiency Virus (HIV)-1-infected, Human CD4T Cells.* (Molecular & cellular proteomics : MCP, 2017; PMID 28223351, DOI: 10.1074/mcp.m116.065235)
- **[Nazziwa2024]** 超急性期 HIV-1 感染中血浆蛋白组的动态变化。 — *Dynamics of the blood plasma proteome during hyperacute HIV-1 infection.* (Nature communications, 2024; PMID 39632834, DOI: 10.1038/s41467-024-54848-0)
- **[Kusejko2025]** 炎症与 B 细胞活化定义可预测结局的 HIV 血浆蛋白组特征。 — *Inflammation and B cell activation define a plasma proteome signature predicting tuberculosis in people with HIV.* (mBio, 2025; PMID 40874618, DOI: 10.1128/mbio.01585-25)
- **[Mikaeloff2025]** 免疫代谢受损 HIV 感染的宿主血浆微环境蛋白组学。 — *Host Plasma Microenvironment in Immunometabolically Impaired HIV Infection Leads to Dysregulated Monocyte Function and Synaptic Transmission Ex Vivo.* (Advanced science (Weinheim, Baden-Wurttemberg, Germany), 2025; PMID 40013867, DOI: 10.1002/advs.202416453)
- **[Zhang2025]** HIV 合并 SARS-CoV-2 住院患者的血浆蛋白组学谱。 — *Plasma proteomic profiling of hospitalized patients co-infected with HIV and SARS-CoV-2.* (Frontiers in immunology, 2025; PMID 40568587, DOI: 10.3389/fimmu.2025.1601672)

### 3.3 代表性公开数据资源

- **PRIDE(ProteomeXchange)**:质谱蛋白组/磷酸化蛋白组原始与处理数据的主库,含 T 细胞信号与 HIV 相关项目。
- **MassIVE / jPOST / iProX**:ProteomeXchange 联盟其他质谱数据仓库。
- **IEDB**:免疫表位数据库,含 MHC 结合/T 细胞表位实验数据,用于免疫肽组学建模。
- **HLA Ligand Atlas**:良性组织 HLA 呈递肽参考,用于免疫肽组学/新抗原对照。
- **CPTAC**:临床蛋白组肿瘤图谱(方法参考,含免疫浸润相关蛋白组)。
- **CITE-seq 数据(GEO)**:表面蛋白+转录组多模态数据集,支撑蛋白丰度预测模型训练。

### 3.4 HIV 语境数据丰度评估:**中等偏稀缺**。HIV 血浆/PBMC 蛋白组学近年有稳定产出(尤以血浆生物标志物为主),但针对纯化 T 细胞亚群、储存库细胞的深度蛋白组与磷酸化蛋白组数据明显稀少;单细胞蛋白组学(HIV 特异)在本轮检索范围内很少。

### 3.5 方法学成熟度:**分化明显**。免疫肽组学/MHC 预测侧深度学习成熟且竞争激烈;从转录组预测表面蛋白的多模态方法快速成熟;而 HIV 蛋白组多停留在质谱差异分析 + 经典统计/ML 生物标志物筛选,机制性或深度学习专门建模在本轮检索范围内仍薄弱。


---

## 覆盖度与丰度/成熟度小结

**检索覆盖:** 三模块均达到目标篇数(转录组 16、表观 17、蛋白 14,共 47 篇,均 PMID+DOI 双核实)。可能偏薄之处:(1)纯 ML 会议论文(NeurIPS/ICML 等)因 PubMed 不收录、本轮 OpenAlex/arXiv 不可用而未纳入,方法学"最前沿深度模型"一端可能低估;(2)HIV 特异的表观染色质可及性(ATAC/ChIP)与单细胞蛋白组数据本就稀少,非检索遗漏。

| 模块 | HIV 数据丰度 | 方法学成熟度 |
|---|---|---|
| 转录组学 | 中等偏充裕(单细胞近 5 年快速增长,但储存库细胞稀有、真感染标注稀缺) | 较成熟:通用侧深度生成/整合/注释工业化;HIV 侧仍以经典分析为主,专门深度模型少 |
| 表观基因组学 | 中等(甲基化芯片队列 + 近年单细胞多组学在增长;ATAC/ChIP 仍有限) | 通用侧成熟(ChromBPNet/AlphaGenome/SCENIC+);HIV 侧多描述性,机制预测起步 |
| 蛋白质组学 | 中等偏稀缺(血浆蛋白组较多;纯化 T 细胞/储存库深度蛋白组与磷酸化稀少) | 分化:免疫肽组学/MHC 深度学习成熟;HIV 侧以质谱差异+经典 ML 生标筛选为主 |

**共性判断(限本轮检索范围):** 三模态在 T 细胞/免疫学"大"语境下方法学均已进入深度学习阶段;但在 HIV"小"语境下,普遍停留在描述性组学 + 经典统计/ML,面向 HIV 的机制性、跨模态、预测性建模仍是明显空档——此判断仅基于本轮检索,未作"从未有人做"式强结论。

### Part II · 模块组 B:代谢组学/脂质组学 / 免疫组库 / 病毒学测序

# Part II 模块 B — 代谢/脂质组学 · 免疫组库(TCR/BCR-seq)· 病毒学测序

> 本章为"虚拟T细胞(HIV × T细胞 计算建模)"课题的文献测绘,覆盖 3 个组学/测序模块。所有 DOI/PMID 均经 PubMed 元数据接口实测确认(verified=true)。检索跨度 2014–2026,多角度多措辞组合;避免使用字面词 "virtual T cell"。ML 会议/预印本若 PubMed 不可核实则如实标注。

---

## 模块 1 — 代谢组学 / 脂质组学

### (1) 一般语境:ML 与代谢/脂质组学的方法图景
在非 HIV 语境下,代谢组学/脂质组学与机器学习的结合已相对成熟:主流范式是以质谱(LC-MS/GC-MS)获取的靶向/非靶向代谢物谱作为特征,训练分类器或回归器用于疾病诊断、分型与治疗反应预测。方法学关注点集中在特征选择、批次效应校正、缺失值处理与模型可解释性。在 T 细胞免疫代谢方向,单细胞层面的代谢 profiling 工具正在补齐"从群体谱到单细胞状态"的分辨率缺口——代表性方法包括基于流式的能量代谢功能剖析 [met08] 与单细胞代谢质谱 profiling [met07],以及用同位素示踪刻画 CD8 T 细胞分化/耗竭代谢检查点的通量分析 [met09]。这些方法为"T 细胞代谢状态→功能/命运"的计算建模提供了可训练的单细胞特征层。

### (2) HIV 具体工作
在 HIV 语境下,血浆/血清代谢组与脂质组已被用于刻画治疗后免疫恢复、慢性炎症与储存库活性:磷脂类代谢物被发现与治疗中断后病毒反弹时间相关 [met01];致病性 SIV 感染模型的血浆脂质组动态为 HIV 临近模型提供参照 [met02];网络化多组学整合在治疗人群中界定"代谢高危"亚型 [met03];多组学解析免疫重建相关的代谢失调 [met04];跨队列证据显示长期成功治疗向谷氨酰胺分解方向的代谢重编程 [met05];免疫重建不良者具有独特血浆代谢物谱 [met06]。病毒脂质组学的综述 [met10] 概括了病毒-宿主互作层面的方法进展。

### (3) 验证文献(带 DOI/PMID + 一句话)
1. **[met01]** Phospholipid Metabolism Is Associated with Time to HIV Rebound upon Treatment Interruption. — Giron et al., *mBio* (2021). DOI: 10.1128/mBio.03444-20 · PMID: 33622719。发现血浆磷脂类代谢物与治疗中断后病毒反弹时间相关,提示脂质代谢可作为储存库活性的预测特征。
2. **[met02]** Plasma lipidomic alterations during pathogenic SIV infection with and without antiretroviral therapy. — Sivanandham et al., *Frontiers in immunology* (2025). DOI: 10.3389/fimmu.2025.1475160 · PMID: 40129985。在致病性SIV感染(含/不含抗病毒治疗)中刻画血浆脂质组的动态改变,是HIV临近模型的脂质组学参照。
3. **[met03]** Network-based multi-omics integration reveals metabolic at-risk profile within treated HIV-infection. — Mikaeloff et al., *eLife* (2023). DOI: 10.7554/eLife.82785 · PMID: 36794912。用网络化多组学整合(含代谢组)在治疗后HIV人群中界定'代谢高危'亚型。
4. **[met04]** Multi-omics dissection of metabolic dysregulation associated with immune recovery in people living with HIV-1. — Wan et al., *Journal of translational medicine* (2025). DOI: 10.1186/s12967-025-06168-0 · PMID: 39891216。多组学解析治疗后HIV-1人群免疫重建相关的代谢失调,含分类/关联建模。
5. **[met05]** Trans cohort metabolic reprogramming towards glutaminolysis in long-term successfully treated HIV-infection. — Mikaeloff et al., *Communications biology* (2022). DOI: 10.1038/s42003-021-02985-3 · PMID: 35017663。跨队列证据显示长期成功治疗的HIV感染向谷氨酰胺分解方向进行代谢重编程。
6. **[met06]** HIV-Infected Individuals on ART With Impaired Immune Recovery Have Altered Plasma Metabolite Profiles. — Nystr&#xf6;m et al., *Open forum infectious diseases* (2021). DOI: 10.1093/ofid/ofab288 · PMID: 34258318。免疫重建不良的ART患者具有独特的血浆代谢物谱,用于区分免疫应答表型。
7. **[met07]** Single-cell metabolic profiling of human cytotoxic T cells. — Hartmann et al., *Nature biotechnology* (2020). DOI: 10.1038/s41587-020-0651-8 · PMID: 32868913。建立单细胞代谢profiling方法刻画人细胞毒T细胞代谢异质性,为T细胞免疫代谢建模提供单细胞层数据。
8. **[met08]** SCENITH: A Flow Cytometry-Based Method to Functionally Profile Energy Metabolism with Single-Cell Resolution. — Arg&#xfc;ello et al., *Cell metabolism* (2020). DOI: 10.1016/j.cmet.2020.11.007 · PMID: 33264598。SCENITH:基于流式的单细胞能量代谢功能profiling方法,广泛用于免疫细胞代谢通路依赖度量化。
9. **[met09]** C tracer analysis reveals the landscape of metabolic checkpoints in human CD8T cell differentiation and exhaustion. — Kirchmair et al., *Frontiers in immunology* (2023). DOI: 10.3389/fimmu.2023.1267816 · PMID: 37928527。用¹³C示踪代谢流分析绘制人CD8 T细胞分化与耗竭过程中的代谢检查点全景。
10. **[met10]** Unraveling virus-host interactions: Current advances in viral lipidomics. — Requena et al., *iScience* (2025). DOI: 10.1016/j.isci.2025.113750 · PMID: 41210968。综述病毒-宿主互作中的病毒脂质组学最新进展,覆盖方法与分析框架。
11. **[met11]** Metabolomics Workbench: An international repository for metabolomics data and metadata, metabolite standards, protocols, tutorials and training, and analysis tools. — Sud et al., *Nucleic acids research* (2015). DOI: 10.1093/nar/gkv1042 · PMID: 26467476。Metabolomics Workbench:国际化代谢组学数据与元数据、代谢物标准的公共仓库(数据资源)。
12. **[met12]** MetaboLights: open data repository for metabolomics. — Yurekten et al., *Nucleic acids research* (2024). DOI: 10.1093/nar/gkad1045 · PMID: 37971328。MetaboLights:开放的代谢组学数据仓库(数据资源)。

### (4) 公开数据资源
- **Metabolomics Workbench**(NIH,含 REST API 与 mwTab 格式)— 国际代谢组学数据/元数据/代谢物标准仓库,accession 形如 `ST######`(研究)与 `PR######`(项目)[met11]。
- **MetaboLights**(EMBL-EBI)— 开放代谢组学数据仓库,accession 形如 `MTBLS####` [met12]。
- 补充(本轮检索命中但未列为主参考):DDBJ **MetaboBank**(代谢组学数据与元数据,PMID 37971299)。

### (5) HIV 数据丰度 + 方法学成熟度小结
HIV 血浆/CSF 代谢组与脂质组研究数量可观(本轮命中数十篇,横跨心血管风险、神经认知、免疫重建、储存库等),数据丰度**中等偏上**;但绝大多数为关联/分型研究,真正把代谢/脂质特征喂入"T 细胞状态"级机器学习模型的工作**相对稀薄**,单细胞免疫代谢与 HIV 的交叉尤其少。方法学成熟度:通用代谢组学 ML 管线成熟;单细胞代谢 profiling 成熟中;两者与 HIV×T 细胞建模的直接结合仍是开放空间(在本轮检索范围内)。

---

## 模块 2 — 免疫组库(TCR-seq / BCR-seq)

### (1) 一般语境:ML 与免疫组库的方法图景
免疫组库测序(AIRR:TCR/BCR-seq)与深度学习结合是当前活跃度极高的方向。两条主线清晰:一是**仓库层面表征与诊断**——用深度学习从整个 TCR/BCR 仓库中学习序列概念、做免疫状态分类(代表:DeepTCR [rep01]、ML 方法综述 [rep06]);二是**TCR-表位/pMHC 结合特异性预测**——从序列注意力模型到基准评测框架不断迭代(TITAN [rep02]、NetTCR-2.1 [rep03]、双α链解析 [rep04]、系统基准 ePytope-TCR [rep05])。本轮命中还包含大量 Transformer/蛋白语言模型/图神经网络变体,显示该子领域方法极密集但基准与泛化(尤其对未见表位)仍是核心挑战。

### (2) HIV 具体工作
HIV 语境的免疫组库工作既有 TCR 也有 BCR 侧:TCR 侧包括慢性 HIV 感染及 ART 后 TCR 仓库动态扰动 [rep14]、以及对保守 HIV 特异性 TCR 识别谱(含与细菌肽交叉反应)的解析 [rep10];BCR 侧集中在广谱中和抗体(bNAb)谱系——儿童精英中和者的 BCR 仓库测序鉴定多个 bNAb [rep11]、HIV 控制者 B 细胞的独特克隆演化 [rep13]、以及用机器学习识别 HIV-1 bNAb 的 RAIN 方法 [rep12]。

### (3) 验证文献(带 DOI/PMID + 一句话)
1. **[rep01]** DeepTCR is a deep learning framework for revealing sequence concepts within T-cell repertoires. — Sidhom et al., *Nature communications* (2021). DOI: 10.1038/s41467-021-21879-w · PMID: 33707415。DeepTCR:从TCR序列中揭示序列概念的深度学习框架(表征学习+仓库分析)。
2. **[rep02]** TITAN: T-cell receptor specificity prediction with bimodal attention networks. — Weber et al., *Bioinformatics (Oxford, England)* (2021). DOI: 10.1093/bioinformatics/btab294 · PMID: 34252922。TITAN:双模态注意力网络预测TCR-表位特异性,支持对未见表位的泛化。
3. **[rep03]** NetTCR-2.1: Lessons and guidance on how to develop models for TCR specificity predictions. — Montemurro et al., *Frontiers in immunology* (2022). DOI: 10.3389/fimmu.2022.1055151 · PMID: 36561755。NetTCR-2.1:TCR特异性预测模型的开发经验与指导,序列基线方法。
4. **[rep04]** Deep learning predictions of TCR-epitope interactions reveal epitope-specific chains in dual alpha T cells. — Croce et al., *Nature communications* (2024). DOI: 10.1038/s41467-024-47461-8 · PMID: 38615042。深度学习预测TCR-表位互作,并揭示双α T细胞中表位特异性链。
5. **[rep05]** Benchmarking of T cell receptor-epitope predictors with ePytope-TCR. — Drost et al., *Cell genomics* (2025). DOI: 10.1016/j.xgen.2025.100946 · PMID: 40628266。ePytope-TCR:对TCR-表位预测器进行系统基准评测,评估方法学成熟度。
6. **[rep06]** Machine Learning Approaches to TCR Repertoire Analysis. — Katayama et al., *Frontiers in immunology* (2022). DOI: 10.3389/fimmu.2022.858057 · PMID: 35911778。综述机器学习方法在TCR仓库分析中的应用(方法学图景)。
7. **[rep07]** VDJdb: a curated database of T-cell receptor sequences with known antigen specificity. — Shugay et al., *Nucleic acids research* (2018). DOI: 10.1093/nar/gkx760 · PMID: 28977646。VDJdb:已知抗原特异性的TCR序列策展数据库(数据资源,含HIV表位)。
8. **[rep08]** The Immune Epitope Database (IEDB): 2024 update. — Vita et al., *Nucleic acids research* (2025). DOI: 10.1093/nar/gkae1092 · PMID: 39558162。IEDB 2024更新:免疫表位数据库,收录T/B细胞表位及受体数据(数据资源)。
9. **[rep09]** iReceptor: A platform for querying and analyzing antibody/B-cell and T-cell receptor repertoire data across federated repositories. — Corrie et al., *Immunological reviews* (2018). DOI: 10.1111/imr.12666 · PMID: 29944754。iReceptor:查询与分析抗体/BCR与TCR仓库数据(AIRR)的平台(数据资源)。
10. **[rep10]** Interrogating the recognition landscape of a conserved HIV-specific TCR reveals distinct bacterial peptide cross-reactivity. — Mendoza et al., *eLife* (2020). DOI: 10.7554/eLife.58128 · PMID: 32716298。解析一个保守HIV特异性TCR的识别谱,揭示其与细菌肽的交叉反应(HIV具体TCR特异性)。
11. **[rep11]** B cell repertoire sequencing of HIV-1 pediatric elite-neutralizers identifies multiple broadly neutralizing antibody clonotypes. — Kumar et al., *Frontiers in immunology* (2024). DOI: 10.3389/fimmu.2024.1272493 · PMID: 38433846。对HIV-1儿童精英中和者进行BCR仓库测序,鉴定多个广谱中和抗体。
12. **[rep12]** RAIN: machine learning-based identification for HIV-1 bNAbs. — Foglierini et al., *Nature communications* (2024). DOI: 10.1038/s41467-024-49676-1 · PMID: 38914562。RAIN:基于机器学习识别HIV-1广谱中和抗体(bNAb)。
13. **[rep13]** Distinct clonal evolution of B-cells in HIV controllers with neutralizing antibody breadth. — Cizmeci et al., *eLife* (2021). DOI: 10.7554/eLife.62648 · PMID: 33843586。HIV控制者中具中和广度的B细胞呈现独特克隆演化(BCR仓库纵向分析)。
14. **[rep14]** Dynamic Perturbations of the T-Cell Receptor Repertoire in Chronic HIV Infection and following Antiretroviral Therapy. — Heather et al., *Frontiers in immunology* (2016). DOI: 10.3389/fimmu.2015.00644 · PMID: 26793190。刻画慢性HIV感染及抗病毒治疗后TCR仓库的动态扰动。

### (4) 公开数据资源
- **VDJdb** — 已知抗原特异性的 TCR 序列策展库,含 HIV 表位条目 [rep07]。
- **IEDB**(Immune Epitope Database,2024 更新)— T/B 细胞表位及受体数据,含 HIV 表位与受体 [rep08]。
- **iReceptor / AIRR Data Commons** — 联邦式查询与分析 BCR/TCR 仓库数据的平台 [rep09_res=iReceptor,见 rep 列表第 9 项]。
- 补充命中:AIRR Community 数据共享规范(PMID 29144493);epiTCR/其它预测器多以 VDJdb+IEDB 为训练底座。

### (5) HIV 数据丰度 + 方法学成熟度小结
通用 TCR/BCR-seq 的 ML 方法与公开数据库**非常成熟且密集**(VDJdb/IEDB/iReceptor 生态完善)。但 HIV 特异条目在这些库中占比有限,HIV-specific TCR 特异性建模的专门工作**中等偏稀薄**;HIV bNAb 的 BCR 谱系分析相对丰富(疫苗学驱动)。方法学成熟度:预测模型成熟但泛化/基准仍在演进;HIV×仓库的深度学习专用工作仍有拓展空间(在本轮检索范围内)。

---

## 模块 3 — 病毒学测序(整合位点 / 前病毒 / 近全长测序 / IPDA)

### (1) 一般语境:测序技术与计算分析图景
HIV 储存库的病毒学测序有几条成熟技术线:**整合位点分析**(integration site,映射前病毒在宿主基因组的落点与克隆扩增)、**近全长单基因组测序**(near-full-length,判断前病毒基因组完整/缺陷)、**完整前病毒 DNA 测定**(IPDA,基于数字 PCR 定量完整 vs 缺陷前病毒),以及配套的**生物信息学管线与完整性推断工具**。计算侧从比对/映射管线到深度学习(如整合位点偏好建模)均有覆盖。

### (2) HIV 具体工作(本模块即以 HIV 为主体)
奠基性整合位点全景 [vir02] 与区分治疗后控制者的前病毒图谱 [vir03] 构成基础;深度学习理解整合位点的 DeepHINT [vir01] 是"整合位点×ML"的代表;近全长测序方法学协议 [vir04][vir05] 与完整性推断工具 HIVIntact [vir06] 支撑前病毒完整性判定;IPDA 奠基与大队列基准 [vir07][vir08]、整合位点/序列联合分析重建病毒动态 [vir10]、单细胞层面刻画完整可诱导前病毒 [vir11] 与单细胞多组学揭示 HIV 在扩增 T 细胞克隆中持续 [vir12];计算方法侧还有整合位点映射管线 [vir09]、贝叶斯整合日期估计 bayroot [vir13] 与条形码 HIV 追踪克隆增殖 [vir14]。

### (3) 验证文献(带 DOI/PMID + 一句话)
1. **[vir01]** DeepHINT: understanding HIV-1 integration via deep learning with attention. — Hu et al., *Bioinformatics (Oxford, England)* (2019). DOI: 10.1093/bioinformatics/bty842 · PMID: 30295703。DeepHINT:带注意力机制的深度学习理解HIV-1整合位点(整合位点×深度学习核心工作)。
2. **[vir02]** HIV-1 integration landscape during latent and active infection. — Cohn et al., *Cell* (2015). DOI: 10.1016/j.cell.2015.01.020 · PMID: 25635456。绘制潜伏与活跃感染下HIV-1整合位点全景,是整合位点研究的奠基性图谱。
3. **[vir03]** HIV-1 proviral landscapes distinguish posttreatment controllers from noncontrollers. — Sharaf et al., *The Journal of clinical investigation* (2018). DOI: 10.1172/JCI120549 · PMID: 30024859。HIV-1前病毒整合位点/基因组图谱区分治疗后控制者与非控制者。
4. **[vir04]** Near-Full-Length Single-Genome HIV-1 DNA Sequencing. — Lee et al., *Methods in molecular biology (Clifton, N.J.)* (2022). DOI: 10.1007/978-1-0716-1871-4_23 · PMID: 34985675。近全长单基因组HIV-1 DNA测序的标准方法(方法学协议)。
5. **[vir05]** Amplification of Near Full-length HIV-1 Proviruses for Next-Generation Sequencing. — Hiener et al., *Journal of visualized experiments : JoVE* (2018). DOI: 10.3791/58016 · PMID: 30394382。近全长HIV-1前病毒扩增用于二代测序的方法(方法学协议)。
6. **[vir06]** HIVIntact: a python-based tool for HIV-1 genome intactness inference. — Wright et al., *Retrovirology* (2021). DOI: 10.1186/s12977-021-00561-5 · PMID: 34176496。HIVIntact:基于Python推断HIV-1基因组完整性的工具(前病毒完整性分析软件)。
7. **[vir07]** A quantitative approach for measuring the reservoir of latent HIV-1 proviruses. — Bruner et al., *Nature* (2019). DOI: 10.1038/s41586-019-0898-8 · PMID: 30700913。提出定量测量潜伏HIV-1前病毒储存库的方法(IPDA思路的奠基工作)。
8. **[vir08]** Intact proviral DNA assay analysis of large cohorts of people with HIV provides a benchmark for the frequency and composition of persistent proviral DNA. — Simonetti et al., *Proceedings of the National Academy of Sciences of the United States of America* (2020). DOI: 10.1073/pnas.2006816117 · PMID: 32690683。在大队列中用完整前病毒DNA测定(IPDA)提供储存库频率基准。
9. **[vir09]** An analytical pipeline for identifying and mapping the integration sites of HIV and other retroviruses. — Wells et al., *BMC genomics* (2020). DOI: 10.1186/s12864-020-6647-4 · PMID: 32151239。识别与定位HIV及其他逆转录病毒整合位点的分析流程(生信管线)。
10. **[vir10]** Combined HIV-1 sequence and integration site analysis informs viral dynamics and allows reconstruction of replicating viral ancestors. — Patro et al., *Proceedings of the National Academy of Sciences of the United States of America* (2019). DOI: 10.1073/pnas.1910334116 · PMID: 31776247。联合HIV-1序列与整合位点分析刻画病毒动态并重建复制起源。
11. **[vir11]** Phenotypic characterization of single CD4+ T cells harboring genetically intact and inducible HIV genomes. — Dufour et al., *Nature communications* (2023). DOI: 10.1038/s41467-023-36772-x · PMID: 36849523。对携带完整可诱导HIV基因组的单个CD4 T细胞进行表型刻画(单细胞×前病毒完整性)。
12. **[vir12]** Single-cell multiomics reveals persistence of HIV-1 in expanded cytotoxic T cell clones. — Collora et al., *Immunity* (2022). DOI: 10.1016/j.immuni.2022.03.004 · PMID: 35320704。单细胞多组学揭示HIV-1在扩增的细胞毒T细胞克隆中持续存在。
13. **[vir13]** bayroot: Bayesian sampling of HIV-1 integration dates by root-to-tip regression. — Ferreira et al., *Virus evolution* (2022). DOI: 10.1093/ve/veac120 · PMID: 36632480。bayroot:用根到尖回归的贝叶斯方法采样HIV-1整合日期(计算方法)。
14. **[vir14]** Barcoded HIV-1 reveals viral persistence driven by clonal proliferation and distinct epigenetic patterns. — Zhang et al., *Nature communications* (2025). DOI: 10.1038/s41467-025-56771-4 · PMID: 39952916。用条形码HIV-1揭示由克隆增殖和表观遗传模式驱动的病毒持续。

### (4) 公开数据资源
- **LANL HIV Sequence Database**(Los Alamos)— HIV 序列主库;本轮以关键词命中大量基于其序列的分型/耐药分析(如 alignment-free 分型 PMID 31683009),但 LANL 数据库本身的方法学引文未在 PubMed 以可核实 DOI 形式稳定命中,故不单列为 verified 参考,标注为"数据资源、非文献验证"。
- **LANL HIV Immunology Database** — HIV 表位/免疫数据(同上,资源指引,本轮未获稳定可核实文献条目)。
- 通用逆转录病毒整合位点分析管线亦见于 [vir09] 及 VISPA2(PMID 29178837,载体整合位点,非 HIV 特异)。

### (5) HIV 数据丰度 + 方法学成熟度小结
HIV 病毒学测序是本模块中数据与方法**最丰富**的部分:整合位点、近全长测序、IPDA、单细胞储存库刻画均有大量高质量原始工作与标准化协议;计算工具(HIVIntact、映射管线、bayroot、条形码追踪)较成熟。相对薄弱处是**深度学习**在该模块的渗透——除 DeepHINT 等少数工作外,把测序数据接入现代表征学习/生成模型的尝试仍有限(在本轮检索范围内)。整体方法学成熟度:实验+生信管线成熟;深度学习结合尚处早期。

### Part II · 模块组 C:多组学整合/空间组学 / 临床表格数据

# Part II 模块 C:多组学整合 / 空间组学 + 临床表格数据(HIV × T 细胞视角)

> 本章为本轮独立检索结果。所有 DOI/PMID 均经 PubMed 元数据实际核实;凡预印本或非期刊来源均在条目内标注。强结论一律限定为"在本轮检索范围内"。

---

## 模块 1:多组学整合 / 空间组学

**1. 一般语境 ML 图景(方法层)**
免疫单细胞多组学整合已形成较成熟的方法家族:变分/深度生成模型(totalVI 联合建模 RNA+蛋白;MultiVI 跨 RNA/ATAC/蛋白并可补全缺失模态)、图嵌入整合(GLUE 将不同组学映射到共享隐空间并推断调控)、以及多层图谱聚类、稀疏偏最小二乘等潜因子/结构化整合方法(MOFA 类思路)。这批方法多为通用框架,并非 HIV 专用,但可直接迁移。

**2. 空间组学与空间蛋白组学(方法+免疫应用)**
空间转录组学与单细胞分辨的多模态空间蛋白组学已在肿瘤、肝病、自身免疫等组织免疫微环境中落地,用于原位刻画免疫细胞组成与空间邻域关系。这些工作提供了可迁移到淋巴组织免疫空间分析的实验/计算范式。

**3. HIV 具体工作 —— 空间维度**
HIV 领域的空间组学仍处于成型阶段:已有综述系统梳理淋巴结中评估 HIV-1 储存库及其微环境的空间技术,给出组织空间转录组学的方法路线图,并覆盖淋巴组织、CNS/CSF 等多组织维度。提示"HIV × 空间"是活跃但尚未饱和的方向。

**4. HIV 具体工作 —— 单细胞多组学储存库**
单细胞多组学已用于从表观/转录/蛋白多层次解析 HIV-1 潜伏储存库,揭示感染 CD4 T 细胞的深刻表型与表观异质性,并结合潜伏激活策略做多组学分析。这是把"多组学整合"直接嵌入 HIV×T 细胞建模的核心实证入口。

**5. 公开数据资源与丰度/成熟度评估**
- **可用数据入口(通用):** Human Cell Atlas(HCA data portal)、10x Genomics 公开数据集(CITE-seq / Visium / Xenium)、CELLxGENE、GEO/SRA(多组学与空间数据)、ImmPort(免疫学数据)。
- **HIV 数据丰度:** 通用多组学/空间方法与非 HIV 免疫组织数据充沛;**HIV 特异**的空间/多组学公开数据集相对有限,多分散于单项研究的 GEO 附属数据,尚无统一大规模 HIV 空间图谱(本轮检索范围内)。
- **方法学成熟度:** 多组学整合方法本身成熟(有基准与通用工具链);HIV 空间组学处于早期路线图阶段,应用深度与样本量仍受限。

---

## 模块 2:临床表格数据(CD4 计数、病毒载量、队列变量)

> 说明:此层不属严格分子组学,但 HIV 领域大量 ML 工作直接建立在临床/实验室表格变量上,单列一类以免遗漏。

**1. 一般语境 ML 图景**
在临床表格数据上,树模型(随机森林、梯度提升)与逻辑回归仍是主力,深度/序列模型(LSTM)用于纵向电子病历。系统综述与文献计量显示,HIV 领域 AI/ML 已从零散探索走向体系化,近年研究数量与方法多样性明显增加。

**2. 结局预测:病毒载量 / CD4 / 病毒学抑制与失败**
已有多项工作用临床表格变量预测在治患者的病毒载量与 CD4 状态、病毒学抑制、以及病毒学失败,覆盖多个国家队列(埃塞俄比亚、中国新疆十年队列等),常配合列线图等可解释输出。

**3. 纵向/合并症与诊断预测**
深度序列模型(LSTM)用于结构化 EMR 预测 HIV 患者合并结核;机器学习也用于基于问卷/临床变量预测重点人群(MSM)的 HIV/STI 诊断;血浆糖组/代谢等可测生物标志物用于区分停药后病毒控制者。

**4. 耐药与 bnAb 中和预测(基因型/序列→表型的表格化)**
从基因型/序列特征计算预测 HIV 耐药有成熟的方法综述;深度学习(含注意力)用于理解整合位点;序列+深度学习预测对单抗/bnAb(如 VRC01、联合方案)的中和敏感性,直接对接 CATNAP 型中和数据库。

**5. 公开数据资源与丰度/成熟度评估**
- **可用数据入口:** Stanford HIVDB(HIV Drug Resistance Database,耐药基因型/表型)、LANL CATNAP(中和抗体×病毒中和数据)、LANL HIV Sequence Database、各类临床队列(如 CAPRISA、CHAVI/相关联盟队列)、以及以受控访问为主的大型队列(需申请)。
- **HIV 数据丰度:** 序列/耐药/中和类结构化数据(HIVDB、CATNAP、LANL)公开且丰富;临床结局队列(CD4/病毒载量/依从性)大量存在但**多为受控访问或机构内部**,公开可直接下载的完整临床表格相对稀薄(本轮检索范围内)。
- **方法学成熟度:** 表格 ML(树模型/GBM)在 HIV 结局预测上成熟且已多队列验证;序列→表型(耐药/中和)预测成熟度高;深度学习在临床 EMR 上仍属新兴,外部验证与前瞻评估偏少。

---

*引用文献见 part2c_refs.json;每条含 DOI/PMID 与一句话概括,verified 字段标注核实状态。*

### 模块参考文献一览(全部 PMID+DOI 经 PubMed 核实)

| Key | 题目 | 期刊 | 年 | DOI | PMID | 一句话 |
|---|---|---|---|---|---|---|
| vir01 | DeepHINT: understanding HIV-1 integration via deep learning with attention. | Bioinformatics (Oxford, Engl | 2019 | https://doi.org/10.1093/bioinformatics/bty842 | 30295703 | DeepHINT:带注意力机制的深度学习理解HIV-1整合位点(整合位点×深度学习核心工作)。 |
| totalVI2021 | Joint probabilistic modeling of single-cell multi-omic data with totalVI | Nat Methods | 2021 | https://doi.org/10.1038/s41592-020-01050-x | 33589839 | 用变分自编码器联合建模 CITE-seq 的 RNA 与蛋白模态,是免疫单细胞多模态整合的代表方法。 |
| MultiVI2023 | MultiVI: deep generative model for the integration of multimodal data | Nat Methods | 2023 | https://doi.org/10.1038/s41592-023-01909-9 | 37386189 | 深度生成模型联合整合 RNA/ATAC/蛋白多模态并可补全缺失模态,是当前多组学整合的通用框架。 |
| GLUE2022 | Multi-omics single-cell data integration and regulatory inference with graph-lin | Nat Biotechnol | 2022 | https://doi.org/10.1038/s41587-022-01284-4 | 35501393 | 用图连接嵌入把不同组学映射到共享隐空间并推断调控关系,适合无配对多组学的整合。 |
| SpectralMO2022 | Spectral clustering of single-cell multi-omics data on multilayer graphs | Bioinformatics | 2022 | https://doi.org/10.1093/bioinformatics/btac378 | 35652725 | 把多模态单细胞数据建成多层图做谱聚类,是多模态联合分群的一类方法。 |
| mssPLS2020 | Multiset sparse partial least squares path modeling for high dimensional omics d | BMC Bioinformatics | 2020 | https://doi.org/10.1186/s12859-019-3286-3 | 31918677 | 面向高维多组学的稀疏偏最小二乘路径建模,属于潜因子型整合方法家族(MOFA 类思路)。 |
| CITEtopic2023 | Single-cell multi-omics topic embedding reveals cell-type-specific and COVID-19  | Cell Rep Methods | 2023 | https://doi.org/10.1016/j.crmeth.2023.100563 | 37671028 | 用主题嵌入整合单细胞多组学,在感染(COVID-19)免疫严重度中识别细胞型特异信号,是免疫多组学应用范例。 |
| CITEdynsyn2025 | Dynamic Synthesis of Multi-Modal Representations for CITE-seq Data Integration a | Adv Sci | 2025 | https://doi.org/10.1002/advs.202509247 | 40917001 | 近期 CITE-seq 深度学习整合方法,动态合成多模态表示以改进联合分析。 |
| HIVspatialtech2024 | Spatial technologies to evaluate the HIV-1 reservoir and its microenvironment in | mBio | 2024 | https://doi.org/10.1128/mbio.01909-24 | 39058091 | 综述淋巴结中评估 HIV-1 储存库及其微环境的空间组学技术,是 HIV×空间的直接落点。 |
| HIVspatialroadmap2025 | Roadmap for spatial transcriptomics of HIV in tissues | Curr Opin HIV AIDS | 2025 | https://doi.org/10.1097/COH.0000000000000961 | 40626838 | 为组织中 HIV 空间转录组学给出方法路线图,提示该方向仍在成型阶段。 |
| HIVlymphoid2025 | Illuminating lymphoid tissue HIV reservoirs: advanced assays and their relevance | Curr Opin HIV AIDS | 2025 | https://doi.org/10.1097/COH.0000000000000974 | 40891589 | 综述照亮淋巴组织 HIV 储存库的先进检测(含空间/单细胞),关联治愈目标。 |
| HIVcns2025 | Single cell analyses of the HIV reservoir in the CNS and CSF: recent insights an | Curr Opin HIV AIDS | 2025 | https://doi.org/10.1097/COH.0000000000000958 | 40742782 | 综述中枢神经系统/脑脊液 HIV 储存库的单细胞分析进展,拓展了组织维度。 |
| HIVmultiomicRev2023 | Single-cell multiomic understanding of HIV-1 reservoir at epigenetic, transcript | Curr Opin HIV AIDS | 2023 | https://doi.org/10.1097/COH.0000000000000809 | 37535039 | 综述从表观/转录/蛋白多层次用单细胞多组学理解 HIV-1 储存库。 |
| HIVreservoirNI2022 | Profound phenotypic and epigenetic heterogeneity of the HIV-1-infected CD4 T cel | Nat Immunol | 2022 | https://doi.org/10.1038/s41590-022-01371-3 | 36536105 | 单细胞多组学揭示 HIV-1 感染 CD4 T 细胞储存库的表型与表观异质性,是关键实证数据来源。 |
| HIVtatNP2023 | Potent latency reversal by Tat RNA-containing nanoparticle enables multi-omic an | Nat Commun | 2023 | https://doi.org/10.1038/s41467-023-44020-5 | 38110433 | 以潜伏激活配合多组学解析 HIV-1 储存库,示范了多组学在储存库研究中的用法。 |
| SpatProtPanc2024 | Multimodal single cell-resolved spatial proteomics reveal pancreatic tumor heter | Nat Commun | 2024 | https://doi.org/10.1038/s41467-024-54438-0 | 39572534 | 单细胞分辨的多模态空间蛋白组学解析肿瘤异质性,可迁移到免疫组织空间蛋白分析。 |
| SpatProtNASH2023 | Spatial proteomics of immune microenvironment in nonalcoholic steatohepatitis-as | Hepatology | 2023 | https://doi.org/10.1097/HEP.0000000000000591 | 37733002 | 空间蛋白组学刻画组织免疫微环境,方法学可借鉴于淋巴组织免疫空间分析。 |
| MLvlcd42023 | Artificial Intelligence and Machine Learning Based Prediction of Viral Load and  | Int J Gen Med | 2023 | https://doi.org/10.2147/IJGM.S397031 | 36760682 | 基于临床表格变量用 AI/ML 预测在治患者的病毒载量与 CD4 状态,是本课题核心表格预测范例。 |
| MLviralsupp2025 | Using Machine Learning Techniques to Predict Viral Suppression Among People With | J Acquir Immune Defic Syndr | 2025 | https://doi.org/10.1097/QAI.0000000000003561 | 39561000 | 用机器学习从队列表格变量预测病毒学抑制(viral suppression)。 |
| MLvirfail2023 | Machine learning to predict virological failure among HIV patients on ART (Gonda | BMC Med Inform Decis Mak | 2023 | https://doi.org/10.1186/s12911-023-02167-7 | 37085851 | 以临床/实验室变量训练 ML 预测抗病毒治疗患者的病毒学失败。 |
| MLnomogram2025 | Predicting disease progression in people living with HIV using machine learning  | BMJ Open | 2025 | https://doi.org/10.1136/bmjopen-2025-105026 | 41248391 | 基于十年队列结合 ML 与列线图预测 HIV 疾病进展。 |
| LSTMtbhiv2024 | LSTM-Based Prediction Model for Tuberculosis Among HIV-Infected Patients Using S | J Multidiscip Healthc | 2024 | https://doi.org/10.2147/JMDH.S467877 | 39070689 | 用 LSTM 在结构化电子病历上预测 HIV 患者合并结核,示范深度学习用于纵向表格/EMR。 |
| MLstimsm2020 | Predicting the diagnosis of HIV and sexually transmitted infections among MSM us | J Infect | 2020 | https://doi.org/10.1016/j.jinf.2020.11.007 | 33189772 | 用机器学习基于问卷/临床表格变量预测 MSM 人群 HIV/STI 诊断。 |
| GlycomicPTC2021 | Non-invasive plasma glycomic and metabolic biomarkers of post-treatment control  | Nat Commun | 2021 | https://doi.org/10.1038/s41467-021-24077-w | 34188039 | 以血浆糖组/代谢等表格化生物标志物区分停药后病毒控制者,属临床可测变量建模。 |
| AIhivreview2025 | Artificial intelligence for HIV care: a global systematic review of current stud | J Int AIDS Soc | 2025 | https://doi.org/10.1002/jia2.70045 | 40990267 | 系统综述 HIV 照护中 AI 的现状与趋势,可作为方法学成熟度全局评估的锚点。 |
| BigdataHIV2021 | Emergence and evolution of big data science in HIV research: Bibliometric analys | Int J Med Inform | 2021 | https://doi.org/10.1016/j.ijmedinf.2021.104558 | 34481301 | 文献计量分析 HIV 研究中大数据科学的兴起,勾勒数据/方法演化脉络。 |
| DRreview2021 | Drug resistance mutations in HIV: new bioinformatics approaches and challenges | Curr Opin Virol | 2021 | https://doi.org/10.1016/j.coviro.2021.09.009 | 34597873 | 综述 HIV 耐药突变的新生物信息学方法与挑战(基因型→表型)。 |
| DRcomp2016 | Current Approaches in Computational Drug Resistance Prediction in HIV | Curr HIV Res | 2016 | https://doi.org/10.2174/1570162x14666160321120232 | 26996942 | 综述从基因型表格特征计算预测 HIV 耐药的经典方法。 |
| DLmab2022 | Prediction of HIV sensitivity to monoclonal antibodies using aminoacid sequences | Bioinformatics | 2022 | https://doi.org/10.1093/bioinformatics/btac530 | 35876860 | 用氨基酸序列 + 深度学习预测 HIV 对单抗的敏感性,连接 CATNAP 型中和数据。 |
| VRC01pred2019 | Prediction of VRC01 neutralization sensitivity by HIV-1 gp160 sequence features | PLoS Comput Biol | 2019 | https://doi.org/10.1371/journal.pcbi.1006952 | 30933973 | 基于 gp160 序列特征预测对 VRC01 的中和敏感性,是 bnAb 中和预测的表格化建模。 |
| bNAbcombo2023 | Predicting neutralization susceptibility to combination HIV-1 monoclonal broadly | bioRxiv (preprint) | 2023 | https://doi.org/10.1101/2023.12.14.571616 | 38168308 | 预测对联合 bnAb 方案的中和敏感性;来源为 bioRxiv 预印本(未同行评审)。 |


---

## Part III — HIV × T 细胞问题图谱(归纳式构建)

> **构建方法**:严格按四步执行。**第一步**从 19 个组合检索角度(HIV × 各类组学/方法词交叉,非预设临床类别出发)采集 **64 个原子问题**,每个原子问题对应一篇经核实的具体研究实际回答的问题(见 §III.0)。**第二步**在积累完成后才观察聚类。**第三步**用聚类内文献自身语言命名,并逐簇做"是否无意识套用教科书分型"的核查(见 §III.2 及 Part V)。**第四步**无法自然归入者保留为独立条目(AQ08、AQ53)。**归纳结果**:5 个大问题、23 个小问题、2 个独立条目。

### III.0 原子问题清单(64 条,全部源自本轮核实文献)

> 采集顺序即检索浮现顺序;`from_seed=True` 表示该研究亦见于 Part I/II 的核实集,其余 52 条为 Part III 定向检索新增。

| QID | 原子问题 | 来源 PMID | 检索角度 | 模块 | 新增 |
|---|---|---|---|---|---|
| AQ01 | BACH2 驱动的组织驻留记忆(TRM)程序如何促进 CD4 T 细胞中 HIV-1 的持续存在? | 39763845 | HIV_scRNA_reservoir | 转录组 | 新 |
| AQ02 | HIV 感染怎样将 CD4 T 细胞重编程为静息状态并进入前病毒潜伏? | 41006834 | HIV_scRNA_reservoir | 转录组 | 新 |
| AQ03 | 早期 ART 治疗的 HIV 感染者中,HIV 持续存在如何在不同 T 细胞谱系间分布与追踪? | 40044684 | HIV_scRNA_reservoir | 转录组 | 新 |
| AQ04 | 单细胞多组学如何刻画 HIV 潜伏逆转过程并识别新的逆转相关标志? | 38902848 | HIV_scRNA_reservoir | 多组学/空间 | 新 |
| AQ05 | 单细胞转录组能否揭示 HIV 长期不进展者的免疫适应度特征? | 41277843 | HIV_scRNA_reservoir | 转录组 | 新 |
| AQ06 | 通过让 HIV 储存库对细胞死亡敏化,能否促进储存库清除? | 40726975 | HIV_scRNA_reservoir | 转录组 | 新 |
| AQ07 | 公共型(public)TCR 是否赋予 HIV 控制者高亲和力的 CD4 T 细胞应答? | 27111229 | HIV_TCR_epitope | 免疫组库 | 新 |
| AQ08 | HIV-1 表位变异性与 T 细胞受体库不稳定性之间存在怎样的关联? | 28592539 | HIV_TCR_epitope | 免疫组库 | 新 |
| AQ09 | 慢性 HIV 感染中 Gag 特异性 CD8 T 细胞应答的克隆型结构是怎样的? | 34369597 | HIV_TCR_epitope | 免疫组库 | 新 |
| AQ10 | 初始病毒血症持续时间如何调节 HIV 特异性 T 细胞的功能特性? | 41676665 | HIV_TCR_epitope | 免疫组库 | 新 |
| AQ11 | TCR 接触残基的疏水性是否可作为 CD8 T 细胞表位免疫原性的判别标志? | 25831525 | HIV_TCRpMHC_prediction | 免疫组库 | 新 |
| AQ12 | 能否根据序列预测 HIV 储存库对广谱中和抗体的敏感性? | 31484826 | HIV_bnab_sequence_ML | 病毒学测序 | 新 |
| AQ13 | 如何对临床 HIV-1 分离株的抗体耐药性进行准确预测? | 31604961 | HIV_bnab_sequence_ML | 病毒学测序 | 新 |
| AQ14 | SLAPNAP 容器化工具如何从序列预测中和抗体谱的敏感性? | 34021743 | HIV_bnab_sequence_ML | 病毒学测序 | 新 |
| AQ15 | BRAVE 语言模型方法能否高精度预测 HIV-1 抗体耐药性? | 40970138 | HIV_bnab_sequence_ML | 病毒学测序 | 新 |
| AQ16 | 整合结构信息的模型能否改进抗体-抗原(HIV)中和预测? | 42015414 | HIV_bnab_sequence_ML | 病毒学测序 | 新 |
| AQ17 | 单细胞层面深入分析可翻译 HIV-1 储存库能识别出哪些特征? | 34140517 | HIV_integration_clonal | 病毒学测序 | 新 |
| AQ18 | 如何构建刻画克隆扩增与病毒反弹的多维 HIV-1 持续存在模型? | 35475216 | HIV_integration_clonal | 病毒学测序 | 新 |
| AQ19 | HIV DNA 整合到 STAT3 如何驱动 T 细胞持续存在并成为 HIV 相关病变模型? | 40236153 | HIV_integration_clonal | 病毒学测序 | 新 |
| AQ20 | 缺陷型前病毒如何通过启动子外显子化(exaptation)导致 T 细胞重编程? | 41040144 | HIV_integration_clonal | 病毒学测序 | 新 |
| AQ21 | HIV-1 整合位点如何决定被感染 T 细胞的转录命运与持续存在? | 41509258 | HIV_integration_clonal | 病毒学测序 | 新 |
| AQ22 | 急性期与 AIDS 期启动 ART 对 HIV-1 整合位点与克隆扩增有何不同影响? | 39788938 | HIV_integration_clonal | 病毒学测序 | 新 |
| AQ23 | 基线代谢组学特征能否预测 ART 后 CD4 T 细胞的免疫学恢复? | 29280761 | HIV_metabolome_recovery | 代谢/脂质 | 新 |
| AQ24 | 谷氨酰胺分解与脂蛋白是否是成功抑制病毒者晚期免疫恢复的关键因素? | 30952809 | HIV_metabolome_recovery | 代谢/脂质 | 新 |
| AQ25 | 血浆酰基肉碱蓄积是否与 HIV 感染者免疫恢复不良相关? | 34384363 | HIV_metabolome_recovery | 代谢/脂质 | 新 |
| AQ26 | 哪些宿主表观遗传标记可预测 HIV 储存库大小及其对逆转的响应性? | 34482353 | HIV_methylation_latency | 表观 | 新 |
| AQ27 | 女性 HIV 感染者中调控 CD4 T 细胞储存库的基因存在哪些异常 DNA 甲基化? | 40070009 | HIV_methylation_latency | 表观 | 新 |
| AQ28 | UHRF1 在潜伏 HIV-1 的表观遗传抑制中发挥怎样的新作用? | 35429693 | HIV_methylation_latency | 表观 | 新 |
| AQ29 | 表达型 HIV 储存库大小能否预测治疗中断后病毒反弹的时间? | 26588174 | HIV_rebound_predict | 临床表格 | 新 |
| AQ30 | 纳入储存库测量的模型能否预测 ART 中断后病毒反弹的时间? | 31339888 | HIV_rebound_predict | 临床表格 | 新 |
| AQ31 | 哪些循环免疫与血浆生物标志物可预测 HIV 控制者的病毒反弹时间? | 38979421 | HIV_rebound_predict | 蛋白 | 新 |
| AQ32 | 早期病毒动力学能否预测 HIV 治疗后控制(post-treatment control)? | 39513745 | HIV_rebound_predict | 临床表格 | 新 |
| AQ33 | 感染前 PBMC 中 FAM26F 转录水平能否预测 HIV 疾病进展结局? | 27902344 | HIV_elite_controller_transcriptome | 转录组 | 新 |
| AQ34 | 代谢通路激活如何区分 HIV 控制者与进展者 CD8 T 细胞的转录特征? | 30289807 | HIV_elite_controller_transcriptome | 转录组 | 新 |
| AQ35 | miR-19b 高表达是否通过靶向 PTEN 增强 HIV 感染中 CD8 T 细胞功能? | 30687333 | HIV_elite_controller_transcriptome | 转录组 | 新 |
| AQ36 | 多组学整合能否揭示与 HIV 病毒载量相关的机制与潜在靶点? | 40766151 | HIV_viralload_ML | 多组学/空间 | 新 |
| AQ37 | 机器学习能否在低资源环境下对 HIV 病毒载量抑制状态进行分类? | 42011437 | HIV_viralload_ML | 临床表格 | 新 |
| AQ38 | 增强型语言模型能否预测并解释 HIV 护理脱失(care disengagement)? | 41565873 | HIV_viralload_ML | 临床表格 | 新 |
| AQ39 | 如何用随机动力学模型刻画 HIV 感染中潜伏感染细胞储存库的变化? | 30298198 | HIV_math_model_dynamics | 临床表格 | 新 |
| AQ40 | 温和的 HIV 特异性选择压力叠加在自然 CD4 T 细胞动力学上能否解释储存库结构? | 40987290 | HIV_math_model_dynamics | 临床表格 | 新 |
| AQ41 | 数学建模如何评估自体中和抗体对治疗中断后病毒反弹的影响? | 37502921 | HIV_math_model_dynamics | 临床表格 | 新 |
| AQ42 | 如何在人体中精准靶向 HIV 广谱中和抗体的前体(germline precursor)? | 40373114 | HIV_env_structure_design | 病毒学测序 | 新 |
| AQ43 | 结合 cryoEM 与机器学习能否解码 HIV Env 的表位免疫优势(immunodominance)? | 41959402 | HIV_env_structure_design | 病毒学测序 | 新 |
| AQ44 | 探索性算法能否通过分析 HIV 蛋白设计多表位亚单位疫苗? | 40014623 | HIV_env_structure_design | 病毒学测序 | 新 |
| AQ45 | 基于序列熵分析能否识别 HIV-1 蛋白中的保守区域用于疫苗/靶点设计? | 42278661 | HIV_env_structure_design | 病毒学测序 | 新 |
| AQ46 | 深度学习能否基于 HIV-1 序列数据预测药物耐药性? | 32438586 | HIV_drugresist_deeplearning | 临床表格 | 新 |
| AQ47 | 如何提升对新型 HIV-1 蛋白酶抑制剂药物耐药性的预测效能? | 39393002 | HIV_drugresist_deeplearning | 临床表格 | 新 |
| AQ48 | 血浆蛋白质组学能否识别 CD33 作为自然控制 HIV 的标志物? | 37506557 | HIV_proteome_biomarker | 蛋白 | 新 |
| AQ49 | HLA-E–NKG2A 轴上 CD8 T 细胞的空间调控如何驱动淋巴组织中 HIV 的持续存在? | 40849901 | HIV_spatial_lymphnode | 多组学/空间 | 新 |
| AQ50 | CD8 T 细胞干性(stemness)是否先于干预后 HIV 病毒血症的控制? | 41326735 | HIV_CD8_exhaustion_sc | 转录组 | 新 |
| AQ51 | 长期 ART 后 CD8 T 细胞库经历怎样的克隆更替(clonal succession)与再生? | 39179934 | HIV_CD8_exhaustion_sc | 免疫组库 | 新 |
| AQ52 | 单细胞如何刻画 HIV-1 感染者 CD8 T 细胞的图谱与受体库? | 42252444 | HIV_CD8_exhaustion_sc | 转录组 | 新 |
| AQ53 | 单细胞转录组能否构建 HIV 感染者免疫细胞耗竭的图谱并刻画外周 T 细胞异质性? | 32954948 | seed_scRNA | 转录组 | 种子 |
| AQ54 | 如何对单个 HIV-1 前病毒同时平行分析其转录、整合位点与序列? | 35026153 | seed_multimodal | 转录组 | 种子 |
| AQ55 | 单细胞分析能否揭示胃肠道 HIV 储存库的异质性细胞表型? | 41433124 | seed_tissue | 转录组 | 种子 |
| AQ56 | 单细胞表观-转录-蛋白联合谱分析能否证明 IKZF3 促进 HIV-1 持续存在? | 37922905 | seed_multiomics | 表观 | 种子 |
| AQ57 | 单细胞多组学能否证明 HIV-1 持续存在于扩增的细胞毒性 CD4 T 细胞中? | 35320704 | seed_multiomics | 表观 | 种子 |
| AQ58 | 如何解析一个保守 HIV 特异性 TCR 的识别景观(recognition landscape)? | 32716298 | seed_TCR | 免疫组库 | 种子 |
| AQ59 | RAIN 机器学习方法能否用于识别 HIV-1 广谱中和抗体? | 38914562 | seed_bnab | 免疫组库 | 种子 |
| AQ60 | 磷脂代谢是否与 ART 中断后 HIV 反弹时间相关? | 33622719 | seed_metabolome | 代谢/脂质 | 种子 |
| AQ61 | HIV-1 储存库细胞的表型特征能否反映免疫选择(immune selection)的印记? | 36599977 | seed_reservoir | 表观 | 种子 |
| AQ62 | 条形码化 HIV-1 能否揭示由克隆增殖驱动的病毒持续存在? | 39952916 | seed_barcode | 病毒学测序 | 种子 |
| AQ63 | 能否根据 HIV-1 gp160 序列预测 VRC01 中和敏感性? | 30933973 | seed_bnab | 病毒学测序 | 种子 |
| AQ64 | 基于网络的多组学整合能否揭示 HIV 感染中的代谢风险谱? | 36794912 | seed_multiomics | 代谢/脂质 | 种子 |

### III.1 两级问题树(大问题 → 小问题,含全字段)

**受控词汇**:互补=覆盖同一主题不同侧面;顺序依赖=一者输出喂给另一者或须先解决其一;竞争性表述=两种几乎同问一事的不同问法(标"可能可合并");粒度嵌套=同一任务在更粗/更细分辨率的版本。


#### 大问题 A:「是什么决定了哪些 T 细胞成为、并长期维持 HIV 持续储存库?」

- **统摄对象**:持续/潜伏储存库细胞本身(被感染 CD4 T 细胞及其克隆)
- **拆解轴**:沿"决定持续性的分子层次"裂开:基因组整合位置 → 克隆增殖动力学 → 细胞状态/谱系程序 → 解剖分布 → 群体时间动力学。理由:本支原子问题反复围绕"哪一层决定了这些细胞不被清除",层次由微观基因组到宏观组织再到时间维度自然铺开。
- **蕴含类型**:实例化式:每个子问题是"储存库如何被建立与维持"在某一分子层次/解剖部位上的具体化,而非彼此相加才回答母题。
- **与同级大问题的关系**:与 B 的关系:顺序依赖 — 必须先刻画"哪些细胞、为何持续"(A),才能问"潜伏状态能否被撬动/清除"(B)。

- **小问题 A.1:「HIV-1 整合位点的基因组位置如何决定被感染 T 细胞的转录命运与持续性?」**
  - I/O:输入:单细胞/单基因组整合位点坐标+局部转录状态 → 输出:该整合位点与细胞持续/潜伏命运的关联
  - 模块:病毒学测序、转录组
  - 表示需求:整合位点的基因组坐标+染色质/转录语境(位置-序列-表达三元组)
  - 数据现状:LANL HIV Sequence DB / HIV Immunology DB(序列/表位;DB 本身方法学引文本轮未稳定核实);GEO/SRA/ENA(公开;HIV scRNA/bulk 系列众多,GSE 级);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:来源方法本身(整合位点-命运关联分析)构成 baseline;未见统一外部 baseline 数字
  - 同父下关系:A.2 顺序依赖:整合位点(A.1)是克隆能否扩增(A.2)的上游决定因素之一
  - 跨支关联:与 E 支共享 LANL 序列数据
  - 支撑原子问题:AQ21、AQ19、AQ54
- **小问题 A.2:「克隆增殖如何驱动 HIV 储存库的扩增与病毒反弹?」**
  - I/O:输入:整合位点/条形码标记的克隆谱系纵向计数 → 输出:克隆扩增速率与反弹贡献
  - 模块:病毒学测序
  - 表示需求:克隆谱系的纵向计数(整合位点或条形码作克隆身份)
  - 数据现状:LANL HIV Sequence DB / HIV Immunology DB(序列/表位;DB 本身方法学引文本轮未稳定核实);barcode/整合位点纵向数据;叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:多维持续性模型(AQ18)、条形码克隆模型(AQ62)为可比方法
  - 同父下关系:A.5 粒度嵌套:克隆动力学(A.2)是储存库群体动力学(A.5)在克隆分辨率上的版本
  - 跨支关联:与 D.1 共享"储存库大小/克隆"测量,喂给反弹预测
  - 支撑原子问题:AQ18、AQ22、AQ62
- **小问题 A.3:「哪些细胞状态/谱系转录程序使 CD4 T 细胞倾向于携带并维持前病毒?」**
  - I/O:输入:感染/储存库细胞单细胞转录(±表观、蛋白)谱 → 输出:与持续性相关的细胞状态/TF 程序
  - 模块:转录组、表观、多组学/空间
  - 表示需求:单细胞多模态状态向量(转录+可及性+表面蛋白)
  - 数据现状:GEO/SRA/ENA(公开;HIV scRNA/bulk 系列众多,GSE 级);ENCODE + GEO(ATAC/ChIP/甲基化芯片;HIV 专门 ATAC/ChIP 有限);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:各来源自身的差异状态分析;未见跨研究统一 baseline
  - 同父下关系:A.1 互补:细胞状态(A.3)与整合位点(A.1)是持续性的两个不同侧面
  - 跨支关联:与 B.1 共享单细胞多组学潜伏数据
  - 支撑原子问题:AQ01、AQ02、AQ20、AQ57、AQ56
- **小问题 A.4:「HIV 储存库在不同组织/解剖部位与 T 细胞谱系间如何分布?」**
  - I/O:输入:多组织/多谱系单细胞或空间取样 → 输出:储存库的解剖-谱系分布图
  - 模块:转录组、多组学/空间
  - 表示需求:带空间/组织坐标与谱系标签的细胞图谱
  - 数据现状:GEO/SRA/ENA(公开;HIV scRNA/bulk 系列众多,GSE 级);HCA / 10x 公开集 / CELLxGENE(通用充沛;HIV 空间专门集有限);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:组织特异储存库刻画为描述性,未见预测 baseline
  - 同父下关系:A.3 互补:分布(A.4)与状态(A.3)互补刻画储存库
  - 跨支关联:与 C 支共享淋巴组织单细胞数据(AQ49 空间同时涉及 CD8 调控)
  - 支撑原子问题:AQ03、AQ55、AQ49
- **小问题 A.5:「可翻译/完整前病毒储存库在单细胞层面有哪些可识别特征,群体动力学如何随时间演变?」**
  - I/O:输入:单细胞翻译能力/完整性读出 + 纵向储存库测量 → 输出:可翻译储存库特征谱 / 随机动力学参数
  - 模块:病毒学测序、转录组
  - 表示需求:完整性/翻译能力的单细胞离散标签;群体规模的时间序列(随机过程状态)
  - 数据现状:LANL HIV Sequence DB / HIV Immunology DB(序列/表位;DB 本身方法学引文本轮未稳定核实);IPDA 类测量;叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:随机潜伏细胞动力学模型(AQ39)、选择力叠加模型(AQ40)为机制 baseline
  - 同父下关系:A.2 粒度嵌套:群体动力学(A.5)是克隆动力学(A.2)的粗粒度版本
  - 跨支关联:与 D.1 共享储存库规模测量
  - 支撑原子问题:AQ17、AQ39、AQ40
- **小问题 A.6:「储存库细胞的表型是否携带免疫选择的印记?」**
  - I/O:输入:储存库 vs 非储存库细胞表型/序列谱 → 输出:免疫选择特征(如被 CTL 压力塑形的印记)
  - 模块:表观、转录组
  - 表示需求:储存库细胞的表型/序列特征向量 + 选择信号
  - 数据现状:GEO/SRA/ENA(公开;HIV scRNA/bulk 系列众多,GSE 级);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:来源研究(免疫选择签名)自身为 baseline
  - 同父下关系:A.3 互补:选择印记(A.6)补充细胞状态(A.3)的"为何是这些细胞存活"侧面
  - 跨支关联:与 C 支共享"CTL 选择压力"概念(顺序依赖于 CD8 应答)
  - 支撑原子问题:AQ61


#### 大问题 B:「HIV 潜伏状态如何被表观遗传/转录网络锁定,又能否被定向逆转或清除?」

- **统摄对象**:前病毒的潜伏转录开关(latency switch)及其可操作性
- **拆解轴**:沿"从锁定潜伏的分子机制 → 预测/逆转/清除的可操作性"裂开。理由:本支原子问题一端问"什么把潜伏锁死"(甲基化、UHRF1、宿主表观标记),另一端问"能否撬开或让其死亡",构成机制→干预的连续谱。
- **蕴含类型**:聚合式:机制端(锁定)与操作端(逆转/清除)的子问题合起来,才回答"潜伏能否被工程化解除"这一母题。
- **与同级大问题的关系**:与 A 的关系:顺序依赖(A→B);与 C 的关系:互补 — B 操作潜伏细胞,C 提供清除所需的效应 T 细胞。

- **小问题 B.1:「单细胞多组学能否刻画潜伏逆转过程并识别新的逆转相关标志?」**
  - I/O:输入:逆转刺激前后单细胞表观+转录+蛋白谱 → 输出:逆转轨迹与新标志基因/因子
  - 模块:多组学/空间、转录组、表观
  - 表示需求:逆转过程的单细胞多模态时序状态
  - 数据现状:GEO/SRA/ENA(公开;HIV scRNA/bulk 系列众多,GSE 级);ENCODE + GEO(ATAC/ChIP/甲基化芯片;HIV 专门 ATAC/ChIP 有限);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:来源多组学逆转研究(AQ04)自身为 baseline
  - 同父下关系:B.2 顺序依赖:识别逆转标志(B.1)先于据其预测逆转响应(B.2)
  - 跨支关联:与 A.3 共享单细胞多组学潜伏数据
  - 支撑原子问题:AQ04
- **小问题 B.2:「哪些宿主表观遗传标记可预测储存库大小及其对逆转的响应性?」**
  - I/O:输入:宿主(甲基化等)表观标记 → 输出:储存库大小/逆转响应性的预测
  - 模块:表观
  - 表示需求:宿主表观标记特征(甲基化 β 值等)向量
  - 数据现状:GEO 上 450K/EPIC 甲基化队列(公开);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:候选宿主表观标记研究(AQ26)为 baseline
  - 同父下关系:B.3 互补:宿主标记(B.2)与病毒侧甲基化机制(B.3)互补
  - 跨支关联:与 D 支共享"储存库大小"作为可预测量
  - 支撑原子问题:AQ26
- **小问题 B.3:「哪些 DNA 甲基化/表观机制在锁定 HIV 潜伏中起作用?」**
  - I/O:输入:潜伏 vs 激活细胞的甲基化/表观修饰谱(±UHRF1 等因子扰动) → 输出:锁定潜伏的表观机制
  - 模块:表观
  - 表示需求:位点分辨率甲基化/组蛋白修饰谱 + 关键因子活性
  - 数据现状:GEO 上 450K/EPIC 甲基化队列(公开);ENCODE + GEO(ATAC/ChIP/甲基化芯片;HIV 专门 ATAC/ChIP 有限);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:UHRF1 机制(AQ28)、女性队列异常甲基化(AQ27)为机制 baseline
  - 同父下关系:B.2 互补:病毒/宿主甲基化机制(B.3)补充 B.2 的预测视角
  - 支撑原子问题:AQ27、AQ28
- **小问题 B.4:「能否通过让储存库对细胞死亡敏化来促进其清除?」**
  - I/O:输入:敏化干预 + 储存库细胞存活读出 → 输出:清除效率/敏化机制
  - 模块:转录组、病毒学测序
  - 表示需求:干预-存活的因果读出(扰动响应表征)
  - 数据现状:GEO/SRA/ENA(公开;HIV scRNA/bulk 系列众多,GSE 级);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:敏化促清除研究(AQ06)为 baseline
  - 同父下关系:B.1 顺序依赖:逆转标志(B.1)与敏化清除(B.4)构成"激活-清除"序列
  - 跨支关联:与 C 支互补:清除常需 CD8 效应功能
  - 支撑原子问题:AQ06


#### 大问题 C:「抗病毒 T 细胞应答的哪些特征区分免疫控制与疾病进展?」

- **统摄对象**:抗病毒(主要 CD8,兼及 CD4)T 细胞应答的功能质量
- **拆解轴**:沿"从识别层 → 克隆结构/动力学 → 转录/代谢功能程序 → 与控制结局的关联"裂开。理由:本支原子问题从 TCR 如何识别表位,到克隆如何随时间更替,到功能程序(干性/代谢)如何决定控制,层层递进。
- **蕴含类型**:实例化式:每个子问题在"T 细胞应答质量"这一对象的某一功能维度上具体化。
- **与同级大问题的关系**:与 A 的关系:互补(储存库细胞生物学 vs 效应 T 细胞生物学);与 D 的关系:顺序依赖 — C 的功能签名常被 D 用作预测轨迹的输入特征。

- **小问题 C.1:「T 细胞受体的识别特性(公共型、亲和力、疏水性)如何决定 HIV 特异性应答质量?」**
  - I/O:输入:TCR 序列/结构 + 表位 → 输出:识别质量(亲和力/免疫原性/公共性)
  - 模块:免疫组库、蛋白
  - 表示需求:TCR 序列(±结构)与 pMHC 的配对表征
  - 数据现状:VDJdb + IEDB + AIRR/iReceptor(TCR/表位;HIV 条目占比有限);LANL HIV Sequence DB / HIV Immunology DB(序列/表位;DB 本身方法学引文本轮未稳定核实)(免疫库);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:公共 TCR 高亲和(AQ07)、疏水性免疫原性标志(AQ11)、保守 TCR 识别景观(AQ58)为 baseline
  - 同父下关系:C.2 顺序依赖:识别质量(C.1)是克隆能否扩增维持(C.2)的上游
  - 跨支关联:与 E 支共享"序列→表型"建模范式(TCR vs 抗体)
  - 支撑原子问题:AQ07、AQ11、AQ58、AQ09
- **小问题 C.2:「HIV 特异 CD8 T 细胞库的克隆结构如何随感染与 ART 演变?」**
  - I/O:输入:纵向 TCR-seq(±功能) → 输出:克隆更替/再生/克隆型结构轨迹
  - 模块:免疫组库、转录组
  - 表示需求:纵向克隆频率轨迹 + 表型标签
  - 数据现状:VDJdb + IEDB + AIRR/iReceptor(TCR/表位;HIV 条目占比有限);GEO/SRA/ENA(公开;HIV scRNA/bulk 系列众多,GSE 级);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:克隆更替再生(AQ51)、CD8 图谱+受体库(AQ52)、Gag 克隆型结构(AQ09)为 baseline
  - 同父下关系:C.1 顺序依赖(承 C.1);与 C.3 互补
  - 跨支关联:与 A.2 共享"克隆动力学"表征(储存库克隆 vs 效应克隆)
  - 支撑原子问题:AQ51、AQ52、AQ10
- **小问题 C.3:「哪些转录/代谢功能程序(干性、代谢通路、miRNA)区分控制者与进展者的 CD8 应答?」**
  - I/O:输入:CD8 单细胞/bulk 转录±代谢读出,分组=控制/进展 → 输出:区分性功能签名
  - 模块:转录组、代谢/脂质
  - 表示需求:CD8 功能程序的高维签名(转录+代谢轴)
  - 数据现状:GEO/SRA/ENA(公开;HIV scRNA/bulk 系列众多,GSE 级);Metabolomics Workbench(ST######/PR######)、MetaboLights(MTBLS####);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:CD8 干性先于控制(AQ50)、代谢通路区分(AQ34)、miR-19b/PTEN(AQ35)为 baseline
  - 同父下关系:C.2 互补:功能程序(C.3)补充克隆结构(C.2)
  - 跨支关联:与 D.3 共享代谢特征(CD8 代谢 vs 血浆代谢组)
  - 支撑原子问题:AQ50、AQ34、AQ35、AQ05
- **小问题 C.4:「感染前/早期的宿主转录状态能否预示 HIV 疾病进展?」**
  - I/O:输入:感染前或早期 PBMC 转录 → 输出:疾病进展结局预测
  - 模块:转录组
  - 表示需求:感染前/早期转录快照
  - 数据现状:GEO/SRA/ENA(公开;HIV scRNA/bulk 系列众多,GSE 级);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:感染前 FAM26F 预测进展(AQ33)为 baseline
  - 同父下关系:C.3 竞争性表述(可能可合并):C.4 与 C.3 中"控制者转录签名"部分重叠,均问"转录特征↔结局";C.4 特指感染前时点
  - 跨支关联:与 D 支顺序依赖:预示进展的特征可并入轨迹预测
  - 支撑原子问题:AQ33


#### 大问题 D:「能否从分子/临床特征预测 HIV 感染者的病毒学与免疫学轨迹?」

- **统摄对象**:个体未来的病毒学/免疫学轨迹(反弹时间、治疗后控制、免疫重建、病毒抑制状态)
- **拆解轴**:沿"预测的结局类型"(反弹时间 / 治疗后控制 / 免疫恢复 / 病毒抑制)×"输入特征模态"(储存库测量 / 代谢-蛋白组 / 临床表格)两维裂开。理由:原子问题天然按"预测什么结局"聚团,且每团内部又按输入模态分化。
- **蕴含类型**:实例化式:每个子问题是"预测轨迹"在某一结局×某一输入模态上的具体化。
- **与同级大问题的关系**:与 C 的关系:顺序依赖(C 供特征→D 预测);与 E 的关系:互补(D 预测宿主轨迹,E 预测病毒表型)。

- **小问题 D.1:「表达型/整合型储存库大小能否预测 ART 中断后病毒反弹时间?」**
  - I/O:输入:储存库大小测量(±克隆) → 输出:反弹时间(生存/回归)
  - 模块:病毒学测序、临床表格
  - 表示需求:储存库定量标量 + 时间-事件结构
  - 数据现状:LANL HIV Sequence DB / HIV Immunology DB(序列/表位;DB 本身方法学引文本轮未稳定核实);IPDA/储存库测量;叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:表达型储存库预测反弹(AQ29)、含储存库测量的反弹模型(AQ30)为 baseline
  - 同父下关系:D.2 竞争性表述(可能可合并):AQ29 与 AQ30 几乎同问"储存库大小↔反弹时间",可能可合并
  - 跨支关联:与 A.2/A.5 共享储存库/克隆测量(顺序依赖)
  - 支撑原子问题:AQ29、AQ30
- **小问题 D.2:「哪些循环免疫/血浆生物标志物与早期病毒动力学可预测反弹时间或治疗后控制?」**
  - I/O:输入:血浆免疫/蛋白标志物、早期 VL 动力学 → 输出:反弹时间 / PTC 概率
  - 模块:蛋白、临床表格、代谢/脂质
  - 表示需求:血浆标志物面板 + 早期动力学参数
  - 数据现状:PRIDE/ProteomeXchange、MassIVE(质谱;含 HIV 项目);临床队列(CD4/VL/依从性)多为受控访问或机构内部;公开完整表格相对稀薄;叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:反弹生物标志(AQ31)、早期动力学预测 PTC(AQ32)、自体 NAb 反弹模型(AQ41)为 baseline
  - 同父下关系:D.1 互补:生物标志(D.2)与储存库大小(D.1)是反弹预测的不同输入
  - 跨支关联:与 E 支共享抗体(NAb)数据(AQ41 与 E)
  - 支撑原子问题:AQ31、AQ32、AQ41、AQ60
- **小问题 D.3:「基线代谢组/脂质组/蛋白组特征能否预测 ART 后免疫学恢复?」**
  - I/O:输入:基线代谢/脂质/蛋白组 → 输出:CD4 免疫恢复好坏
  - 模块:代谢/脂质、蛋白
  - 表示需求:代谢/脂质/蛋白组高维谱
  - 数据现状:Metabolomics Workbench(ST######/PR######)、MetaboLights(MTBLS####);PRIDE/ProteomeXchange、MassIVE(质谱;含 HIV 项目);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:基线代谢签名(AQ23)、谷氨酰胺分解/脂蛋白(AQ24)、酰基肉碱(AQ25)、CD33 蛋白标志(AQ48)为 baseline
  - 同父下关系:D.2 互补:免疫恢复(D.3)与反弹(D.1/2)是不同结局,共享组学输入
  - 跨支关联:与 C.3 共享代谢特征
  - 支撑原子问题:AQ23、AQ24、AQ25、AQ48
- **小问题 D.4:「多组学整合能否揭示与 HIV 病毒载量相关的机制与风险谱?」**
  - I/O:输入:多组学(代谢+其它)整合数据 → 输出:与 VL 相关的机制模块/风险谱
  - 模块:多组学/空间、代谢/脂质
  - 表示需求:跨组学联合隐表示/网络
  - 数据现状:Metabolomics Workbench(ST######/PR######)、MetaboLights(MTBLS####);HCA / 10x 公开集 / CELLxGENE(通用充沛;HIV 空间专门集有限);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:组学整合揭示 VL 机制(AQ36)、网络多组学代谢风险谱(AQ64)为 baseline
  - 同父下关系:D.3 互补:VL 机制谱(D.4)与免疫恢复(D.3)共享组学整合方法
  - 跨支关联:与 A 支互补(机制发现 vs 储存库)
  - 支撑原子问题:AQ36、AQ64
- **小问题 D.5:「机器学习能否从临床表格变量预测病毒抑制/失败与护理脱失?」**
  - I/O:输入:临床/实验室表格变量(CD4、VL、依从性、人口学) → 输出:抑制/失败/脱失分类
  - 模块:临床表格
  - 表示需求:结构化表格特征(混合类别/数值)
  - 数据现状:临床队列(CD4/VL/依从性)多为受控访问或机构内部;公开完整表格相对稀薄;叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:低资源 VL 抑制分类(AQ37)、语言模型预测脱失(AQ38)为 baseline
  - 同父下关系:D.1 互补:临床表格预测(D.5)与分子特征预测(D.1-4)是不同输入模态的同类轨迹预测
  - 支撑原子问题:AQ37、AQ38


#### 大问题 E:「能否从病毒序列/结构预测中和、耐药与免疫原性表型,以指导抗体与疫苗设计?」

- **统摄对象**:HIV 病毒基因型/结构 → 表型(中和敏感性、药物耐药、表位免疫原性)映射
- **拆解轴**:沿"被预测/设计的表型类型"裂开:bNAb 中和敏感性 / 药物耐药 / 表位免疫优势与疫苗靶点。理由:原子问题按"预测哪种病毒表型"清晰聚团。
- **蕴含类型**:聚合式:各表型预测子问题合起来,才构成"病毒序列-结构→功能表型"的完整映射与设计闭环。
- **与同级大问题的关系**:与 D 的关系:互补(病毒表型 vs 宿主轨迹);与 C 的关系:互补(抗体识别 vs T 细胞识别,同为序列→识别建模)。注:本支落点偏体液免疫/抗病毒药物,与"T 细胞"锁的关联为间接(T 细胞辅助 bNAb 成熟、疫苗中的 T 细胞表位),在验证段如实标注。

- **小问题 E.1:「能否从病毒序列预测 HIV 对广谱中和抗体(bNAb)的中和敏感性?」**
  - I/O:输入:病毒 Env/gp160 序列 → 输出:对特定 bNAb 的中和敏感性(IC50/分类)
  - 模块:病毒学测序
  - 表示需求:病毒序列特征(位点/基序);中和数据作标签
  - 数据现状:LANL CATNAP(病毒×中和抗体数据)、Stanford HIVDB(耐药基因型/表型);LANL HIV Sequence DB / HIV Immunology DB(序列/表位;DB 本身方法学引文本轮未稳定核实);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:VRC01 从 gp160 预测(AQ63)、储存库 bNAb 敏感性(AQ12)、SLAPNAP 工具(AQ14)为 baseline
  - 同父下关系:E.2 竞争性表述(可能可合并):中和敏感性(E.1)与抗体耐药(E.2)在部分表述上几乎同问"序列↔中和",可能可合并;E.3 粒度嵌套:VRC01(AQ63)是 E.1 在单抗粒度的实例
  - 跨支关联:与 D.2 共享抗体/中和数据
  - 支撑原子问题:AQ12、AQ63、AQ14
- **小问题 E.2:「能否准确预测临床 HIV-1 分离株对抗体的耐药性?」**
  - I/O:输入:病毒序列(±结构) → 输出:抗体耐药性预测
  - 模块:病毒学测序
  - 表示需求:序列(±结构)特征 → 耐药标签
  - 数据现状:LANL CATNAP(病毒×中和抗体数据)、Stanford HIVDB(耐药基因型/表型);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:准确抗体耐药预测(AQ13)、BRAVE 语言模型(AQ15)、整合结构信息(AQ16)为 baseline
  - 同父下关系:E.1 竞争性表述(见 E.1);AQ13/AQ15 竞争性表述(同任务不同模型,可能可合并),AQ16 互补(加入结构)
  - 支撑原子问题:AQ13、AQ15、AQ16、AQ59
- **小问题 E.3:「深度学习能否从 HIV-1 序列预测抗病毒药物耐药性?」**
  - I/O:输入:蛋白酶/RT 等序列 → 输出:药物耐药表型
  - 模块:临床表格、病毒学测序
  - 表示需求:病毒蛋白序列特征 → 耐药表型
  - 数据现状:Stanford HIVDB;LANL HIV Sequence DB / HIV Immunology DB(序列/表位;DB 本身方法学引文本轮未稳定核实);叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:DL 序列预测耐药(AQ46)、蛋白酶抑制剂预测改进(AQ47)为 baseline
  - 同父下关系:E.1 互补:药物耐药(E.3)与抗体中和(E.1)同为序列→表型但表型不同
  - 支撑原子问题:AQ46、AQ47
- **小问题 E.4:「能否解码 Env 表位免疫优势/免疫原性并据此设计多表位疫苗与保守靶点?」**
  - I/O:输入:Env 序列/cryoEM 结构、序列熵 → 输出:免疫优势/免疫原性排序、疫苗表位集/保守区
  - 模块:病毒学测序、蛋白
  - 表示需求:序列+结构联合表征;表位免疫原性标签
  - 数据现状:LANL CATNAP(病毒×中和抗体数据)、Stanford HIVDB(耐药基因型/表型);LANL HIV Sequence DB / HIV Immunology DB(序列/表位;DB 本身方法学引文本轮未稳定核实);IEDB;叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)
  - baseline:germline 前体靶向(AQ42)、cryoEM+ML 免疫优势(AQ43)、探索算法多表位疫苗(AQ44)、熵分析保守区(AQ45)为 baseline
  - 同父下关系:E.1 顺序依赖:免疫原性/靶点设计(E.4)可上游于中和敏感性评估(E.1)
  - 跨支关联:与 C.1 互补:疫苗 T 细胞表位与 TCR 识别
  - 支撑原子问题:AQ42、AQ43、AQ44、AQ45

### III.2 独立条目(第四步:不强并入任何聚类)

- **AQ08:「HIV-1 表位变异性与 TCR 库不稳定性之间存在怎样的关联?」** — 保留理由:跨支桥接:同时涉及 C 支(TCR 库)与 E 支(病毒表位变异),问的是"病毒逃逸变异如何反过来扰动宿主 TCR 库"这一共演化关系,不落在任一叶子的单一 I/O 上。(模块:免疫组库、病毒学测序;来源 PMID 28592539)
- **AQ53:「单细胞转录组能否构建 HIV 感染者免疫细胞耗竭图谱并刻画外周 T 细胞异质性?」** — 保留理由:描述性泛耗竭图谱,横跨 A.3(细胞状态)与 C.3(功能程序),但既非"促持续性状态"也非"控制者vs进展者签名",作为独立地标保留,不强并入任一叶。(模块:转录组;来源 PMID 32954948)

### III.3 分类合理性自查(第三步要求,结果如实汇总)

- **大问题 A**:聚类 A(储存库建立与维持)确由 AQ01/02/03/17/18/19/20/21/22/54/55/57/56/62/39/40/61 等原子问题支撑,这些问题共享同一目标对象(被感染/持续细胞)。风险自查:'储存库'是 HIV 领域高频术语,易让人以为在套用现成分型。核查结果:本支的"拆解轴"(整合位点→克隆→状态→分布→动力学)不是任何标准教科书分型,而是从原子问题实际关注的分子层次归纳出来的;未套用如"中枢/效应记忆"等既有免疫学分型。判定:归纳支撑成立。
- **大问题 B**:聚类 B(潜伏锁定与逆转)由 AQ04/06/26/27/28 支撑。风险自查:'shock and kill / block and lock' 是 HIV 治愈领域的知名口号,须警惕无意识套用。核查结果:本轮原子问题里并未出现以该口号为框架的表述;B 支是围绕"表观机制↔可操作性"归纳,B.1/B.4 恰好一个偏激活标志、一个偏敏化清除,但我没有用 'shock and kill' 命名,也没有据该口号预设子问题。判定:命名与结构来自原子问题本身,未套用口号式分型。
- **大问题 C**:聚类 C(T 细胞应答质量)由 AQ07/09/10/11/34/35/50/51/52/05/33/58 支撑。风险自查:'耗竭 vs 记忆 vs 干性' 是免疫学教科书轴,易被套用。核查结果:C 支的轴(识别→克隆结构→功能程序→结局关联)是从原子问题的实际提问归纳的;虽然 C.3 涉及"干性",但那是 AQ50 原文(stemness)本身的用词,属"用聚类内文献自身语言命名",而非我外加教科书轴。判定:成立;C.4 与 C.3 存在竞争性表述已如实标注。
- **大问题 D**:聚类 D(轨迹预测)由 AQ23/24/25/29/30/31/32/36/37/38/41/48/60/64 支撑。风险自查:'反弹/免疫重建/病毒抑制' 是 HIV 临床结局的常见分类,须核查是否只是把临床结局清单搬过来。核查结果:这些结局不是我预设的类别,而是每篇预测类研究"实际预测的那个量"聚起来后自然分出的组;拆解轴(结局类型×输入模态)也是观察原子问题后描述的,符合"从组合检索词出发让问题浮现"的要求。判定:成立,但须承认这些结局名与常见临床结局重合——重合是因为文献本身就在预测这些量,而非我复用记忆分类。
- **大问题 E**:聚类 E(病毒序列/结构→表型)由 AQ12/13/14/15/16/42/43/44/45/46/47/59/63 支撑。风险自查:是否偏离了"T 细胞"锁?核查结果:E 支多数落在体液免疫(bNAb/中和)与抗病毒药物耐药,与 T 细胞的关联是间接的(T 细胞辅助抗体成熟、疫苗中的 T 细胞表位)。如实标注:E 支是本轮组合检索(HIV×序列×ML)自然浮现的强聚类,但其与"HIV × T 细胞"主锁的贴合度弱于 A–D;保留但在 Part IV/V 标注其"T 细胞相关性为间接"。判定:聚类本身由原子问题强支撑,主题贴合度需打折说明。
- **独立条目**:AQ08、AQ53 未强并入任何叶(见 Part III 独立条目)。自查:这不是遗漏,而是刻意执行第四步——两者要么跨支桥接(AQ08),要么是泛描述图谱(AQ53),并入任一叶都会破坏该叶的一句话 I/O 闭环。


---

## Part IV — 交叉与综合(描述性,不做战略判断)

### IV.1 组学模块 × 问题树分支 对照矩阵

> 单元格 = 该分支下"用到该模块"的小问题数(一个小问题可跨多模块计数)。

| 模块＼分支 | A 储存库 | B 潜伏 | C 应答质量 | D 轨迹预测 | E 序列→表型 | 行合计 |
|---|---|---|---|---|---|---|
| 转录组 | 5 | 2 | 3 | 0 | 0 | 10 |
| 表观 | 2 | 3 | 0 | 0 | 0 | 5 |
| 蛋白 | 0 | 0 | 1 | 2 | 1 | 4 |
| 代谢/脂质 | 0 | 0 | 1 | 3 | 0 | 4 |
| 免疫组库 | 0 | 0 | 2 | 0 | 0 | 2 |
| 病毒学测序 | 3 | 1 | 0 | 1 | 4 | 9 |
| 多组学/空间 | 2 | 1 | 0 | 1 | 0 | 4 |
| 临床表格 | 0 | 0 | 0 | 3 | 1 | 4 |
| **列合计** | 12 | 7 | 7 | 10 | 6 | — |

**密集处**:病毒学测序(行合计 9)集中支撑 A、E 两支;转录组(10)集中在 A、B、C;A 支(储存库,列合计 12)与 D 支(轨迹,10)承接模块最多。
**稀薄处**:免疫组库仅支撑 C 支(2);蛋白与代谢/脂质仅零星进入 C、D、E;B 支(潜伏)几乎只靠表观+转录+单细胞多组学,无临床表格/免疫组库/代谢介入;E 支(序列→表型)完全不涉转录/表观/免疫组库层。

**各模块 HIV 语境数据丰度(承 Part II 评级)**:
- 转录组:充裕
- 表观:中等
- 蛋白:中等
- 代谢/脂质:中等
- 免疫组库:中等偏稀薄(HIV 特异 TCR;bNAb BCR 较丰富)
- 病毒学测序:充裕(HIV 最丰富模块)
- 多组学/空间:稀薄(无统一 HIV 空间图谱)
- 临床表格:表面丰富但多受控访问

### IV.2 领域基座技术(Part I) × HIV × T 细胞应用现状(Part III)

> 逐条核对 Part I 出现过的、在更广虚拟细胞/免疫建模领域已被验证或广泛采用的技术路线,是否在本轮 Part III 的 HIV × T 细胞语料里出现同类应用。**只标事实分布(已出现/部分出现/未出现),不判断是否该做、不给优先级。**

| Part I 技术路线 | 所属脉络 | HIV 应用现状 | 事实依据(本轮语料) |
|---|---|---|---|
| 单细胞基础模型 / 细胞语言模型(scGPT/Geneformer 类:大规模预训练细胞表征) | 基础模型/单细胞语言模型 | **未出现** | 本轮 HIV × T 细胞语料中未见将单细胞基础模型(预训练 foundation model)直接用于 HIV 数据的研究;HIV scRNA 工作多用常规降维/聚类/差异分析(AQ01-05,AQ50-57)。仅在通用/方法学综述(Part I/II-A)出现,HIV 侧本轮检索范围内未见。 |
| 生成式扰动预测(in silico perturbation:预测未测扰动下的细胞状态) | AI 虚拟细胞 | **部分出现** | HIV 侧有"潜伏逆转""敏化清除"等扰动-响应研究(AQ04,AQ06),但为实测扰动的描述性分析,未见"用生成模型预测未测扰动"的虚拟实验式建模。 |
| 序列→功能深度学习(语言模型/注意力用于生物序列表型预测) | 基础模型(迁移到序列) | **已出现** | HIV 侧广泛出现:BRAVE 语言模型预测抗体耐药(AQ15)、DeepHINT 注意力预测整合(vir01)、DL 预测药物耐药(AQ46/47)、bNAb 中和序列预测(AQ12/14/63)。 |
| 多模态/多组学联合表征学习(totalVI/MultiVI/GLUE 类跨模态隐空间) | AI 虚拟细胞(多模态表征) | **部分出现** | HIV 侧有单细胞多组学联合谱(AQ56/57,B.1)与网络多组学整合(AQ36/64),但多用通用工具做联合分析/整合,未见专为 HIV 训练的跨模态表征模型;方法多为应用而非新表征学习。 |
| 机制性/系统建模(ODE、随机过程、机制虚拟免疫细胞) | 机制建模/系统免疫学 | **已出现** | HIV 侧有随机潜伏细胞动力学(AQ39)、选择力叠加自然 CD4 动力学(AQ40)、自体 NAb 反弹数学模型(AQ41)、多维持续性模型(AQ18)。 |
| 数字孪生(个体化动态患者/细胞模型,可模拟干预) | 数字孪生 | **未出现** | 本轮 HIV × T 细胞语料中未见以"数字孪生"为框架、可模拟个体干预轨迹的模型;反弹/恢复预测(D 支)为统计/ML 预测,非孪生式动态仿真。本轮检索范围内未见。 |
| 通用细胞表征的跨数据集迁移/图谱级整合(reference mapping) | AI 虚拟细胞(通用表征) | **部分出现** | HIV 侧有组织/谱系图谱构建(AQ03/52/53,A.4)与 CD8 图谱,属图谱级刻画,但未见借助大规模通用参考(如 HCA 级基础模型)做迁移映射的 HIV 研究。 |
| 结构感知建模(cryoEM/结构信息融入预测,AlphaFold 类结构先验) | 地基方法(结构预测外溢) | **已出现** | HIV 侧有 cryoEM+ML 解码 Env 免疫优势(AQ43)、整合结构信息改进中和预测(AQ16)、germline 前体结构靶向(AQ42)。 |
| LLM/agent 驱动的生物学推理(把大语言模型用作分析/预测 agent) | AI 虚拟细胞(LLM agent) | **部分出现** | HIV 侧仅见"增强语言模型预测护理脱失"(AQ38)这一临床文本/表格向 LLM 的应用;未见把 LLM 作 agent 编排多步生物学推理的 HIV × T 细胞研究。 |
| T 细胞特异性/TCR-pMHC 识别预测(免疫虚拟细胞最难问题) | 免疫特化(Hudson 等诊断) | **部分出现** | HIV 侧有公共 TCR 亲和(AQ07)、疏水性免疫原性标志(AQ11)、保守 TCR 识别景观(AQ58)、Gag 克隆型(AQ09),但多为特定表位/TCR 的实验刻画,未见泛化到未见 HIV 表位的通用 TCR-pMHC 预测器(与 Hudson 诊断一致)。 |

**分布小结(仅描述)**:已出现 3 项(序列→功能 DL、机制/系统建模、结构感知建模),部分出现 5 项,未出现 2 项(单细胞基础模型直接用于 HIV 数据、数字孪生式个体动态仿真)——均限"本轮检索范围内"。

### IV.3 完整问题树(缩进式,标注数据丰度 / 跨支连线 / 竞争性表述节点对)

> 叶后标注:`【数据就绪度】`(Part V 分类)· `↔跨支` · `⚠竞争性表述/可能可合并`。

```
● 大问题 A:是什么决定了哪些 T 细胞成为、并长期维持 HIV 持续储存库?
  ├─ A.1 HIV-1 整合位点的基因组位置如何决定被感染 T 细胞的转录命运与持续性?
  │       【有数据就能推进】  ↔与 E 支共享 LANL 序列数据
  ├─ A.2 克隆增殖如何驱动 HIV 储存库的扩增与病毒反弹?
  │       【有数据就能推进】  ↔与 D.1 共享"储存库大小/克隆"测量,喂给反弹预测
  ├─ A.3 哪些细胞状态/谱系转录程序使 CD4 T 细胞倾向于携带并维持前病毒?
  │       【有数据就能推进】  ↔与 B.1 共享单细胞多组学潜伏数据
  ├─ A.4 HIV 储存库在不同组织/解剖部位与 T 细胞谱系间如何分布?
  │       【有数据就能推进】  ↔与 C 支共享淋巴组织单细胞数据(AQ49 空间同时涉及 CD8 调控)
  ├─ A.5 可翻译/完整前病毒储存库在单细胞层面有哪些可识别特征,群体动力学如何随时间演变?
  │       【只差算法设计】  ↔与 D.1 共享储存库规模测量
  ├─ A.6 储存库细胞的表型是否携带免疫选择的印记?
  │       【有数据就能推进】  ↔与 C 支共享"CTL 选择压力"概念(顺序依赖于 CD8 应答)
│
● 大问题 B:HIV 潜伏状态如何被表观遗传/转录网络锁定,又能否被定向逆转或清除?
  ├─ B.1 单细胞多组学能否刻画潜伏逆转过程并识别新的逆转相关标志?
  │       【有数据就能推进】  ↔与 A.3 共享单细胞多组学潜伏数据
  ├─ B.2 哪些宿主表观遗传标记可预测储存库大小及其对逆转的响应性?
  │       【有数据就能推进】  ↔与 D 支共享"储存库大小"作为可预测量
  ├─ B.3 哪些 DNA 甲基化/表观机制在锁定 HIV 潜伏中起作用?
  │       【有数据就能推进】
  ├─ B.4 能否通过让储存库对细胞死亡敏化来促进其清除?
  │       【数据和方法都还没有】  ↔与 C 支互补:清除常需 CD8 效应功能
│
● 大问题 C:抗病毒 T 细胞应答的哪些特征区分免疫控制与疾病进展?
  ├─ C.1 T 细胞受体的识别特性(公共型、亲和力、疏水性)如何决定 HIV 特异性应答质量?
  │       【有数据就能推进】  ↔与 E 支共享"序列→表型"建模范式(TCR vs 抗体)
  ├─ C.2 HIV 特异 CD8 T 细胞库的克隆结构如何随感染与 ART 演变?
  │       【有数据就能推进】  ↔与 A.2 共享"克隆动力学"表征(储存库克隆 vs 效应克隆)
  ├─ C.3 哪些转录/代谢功能程序(干性、代谢通路、miRNA)区分控制者与进展者的 CD8 应答?
  │       【有数据就能推进】  ↔与 D.3 共享代谢特征(CD8 代谢 vs 血浆代谢组)
  ├─ C.4 感染前/早期的宿主转录状态能否预示 HIV 疾病进展?
  │       【只差算法设计】  ⚠竞争性表述  ↔与 D 支顺序依赖:预示进展的特征可并入轨迹预测
│
● 大问题 D:能否从分子/临床特征预测 HIV 感染者的病毒学与免疫学轨迹?
  ├─ D.1 表达型/整合型储存库大小能否预测 ART 中断后病毒反弹时间?
  │       【有数据就能推进】  ⚠竞争性表述  ↔与 A.2/A.5 共享储存库/克隆测量(顺序依赖)
  ├─ D.2 哪些循环免疫/血浆生物标志物与早期病毒动力学可预测反弹时间或治疗后控制?
  │       【有数据就能推进】  ↔与 E 支共享抗体(NAb)数据(AQ41 与 E)
  ├─ D.3 基线代谢组/脂质组/蛋白组特征能否预测 ART 后免疫学恢复?
  │       【有数据就能推进】  ↔与 C.3 共享代谢特征
  ├─ D.4 多组学整合能否揭示与 HIV 病毒载量相关的机制与风险谱?
  │       【有数据就能推进】  ↔与 A 支互补(机制发现 vs 储存库)
  ├─ D.5 机器学习能否从临床表格变量预测病毒抑制/失败与护理脱失?
  │       【有数据就能推进】
│
● 大问题 E:能否从病毒序列/结构预测中和、耐药与免疫原性表型,以指导抗体与疫苗设计?
  ├─ E.1 能否从病毒序列预测 HIV 对广谱中和抗体(bNAb)的中和敏感性?
  │       【有数据就能推进】  ⚠竞争性表述  ↔与 D.2 共享抗体/中和数据
  ├─ E.2 能否准确预测临床 HIV-1 分离株对抗体的耐药性?
  │       【有数据就能推进】  ⚠竞争性表述
  ├─ E.3 深度学习能否从 HIV-1 序列预测抗病毒药物耐药性?
  │       【有数据就能推进】
  ├─ E.4 能否解码 Env 表位免疫优势/免疫原性并据此设计多表位疫苗与保守靶点?
  │       【只差算法设计】  ↔与 C.1 互补:疫苗 T 细胞表位与 TCR 识别
│
● 独立条目(未归簇)
  ├─ AQ08 HIV-1 表位变异性与 TCR 库不稳定性之间存在怎样的关联?
  ├─ AQ53 单细胞转录组能否构建 HIV 感染者免疫细胞耗竭图谱并刻画外周 T 细胞异质性?
```

**被标记"竞争性表述、可能可合并"的节点对**:
- **D.1 内 AQ29 ↔ AQ30**:均问"储存库大小 ↔ 反弹时间",几乎同一任务不同队列/模型,可能可合并。
- **C.4 ↔ C.3**:"感染前/早期转录预示进展"与"控制者 vs 进展者转录签名"在"转录特征↔结局"上高度重叠,C.4 特指感染前时点。
- **E.1 ↔ E.2**:"中和敏感性预测"与"抗体耐药预测"在部分表述上几乎同问"序列↔中和",可能可合并。
- **E.2 内 AQ13 ↔ AQ15**:同为抗体耐药预测,分别用经典/语言模型方法,任务相同、方法不同,可能可合并。

**主要跨支连线(数据/方法共享)**:
- A.1 ↔ E 支:共享 LANL 病毒序列数据。
- A.2 ↔ D.1:储存库/克隆测量作为反弹预测的输入(顺序依赖)。
- A.3 ↔ B.1:共享单细胞多组学潜伏数据。
- C.1 ↔ E:同为"序列→识别"建模范式(TCR 识别 vs 抗体中和)。
- C.3 ↔ D.3:共享代谢特征(CD8 细胞内代谢 vs 血浆代谢组)。
- C.4/C 支 ↔ D 支:功能/转录签名作为轨迹预测输入(顺序依赖)。
- E.4 ↔ C.1:疫苗 T 细胞表位设计与 TCR 识别互补。


---

## Part V — 自审与不确定清单

### V.1 全文 DOI / accession 核实状态

- **DOI/PMID**:全文共 **206** 条参考,每条 PMID 均经 PubMed `get_article_metadata` 实测返回题目;所报 DOI 与 PubMed 记录逐条比对,**DOI 冲突 0 条、题目实质不符 0 条**(3 例题目相似度低仅因子代理缩写标题,经人工核对为同一文献)。核实状态:**全部通过**。
- **叶级 accession**:Part III 各小问题的"数据现状"给出的是**模块级已核实公开资源**(如 GEO/SRA、ENCODE、PRIDE、Metabolomics Workbench(ST######/PR######)、MetaboLights(MTBLS####)、VDJdb、IEDB、LANL、CATNAP、Stanford HIVDB);这些资源实体在 Part II 检索中确认存在。**但每个小问题项下的具体单个 accession(某个 GSE/某个 ST 编号)本轮未逐一点名核实**——已在每条数据现状标注"叶级具体 accession 本轮未逐一核实(来源研究 PMID 已核实)",避免给出格式看似正确但未实测的编号。
- **数据库自身文献条目**:LANL HIV Sequence/Immunology Database 的方法学引文在 PubMed 未以稳定可核实 DOI 命中,故作为"资源指引"列出而**不计入核实参考条数**,已如实注明。

### V.2 Part III 分类合理性自查汇总(第三步)

五个聚类逐一核查"是否无意识复用教科书式分型",结论:
- **A / B / C**:拆解轴均由原子问题的实际分子层次归纳,未套用"记忆/效应/耗竭"等既有免疫学分型;C.3"干性"用词直接取自来源文献 AQ50(stemness),属"用聚类内文献自身语言命名"。
- **B**:特别核查了是否无意识套用治愈领域口号"shock and kill / block and lock"——原子问题中无该框架表述,B 支按"表观机制↔可操作性"归纳,**未套用口号**。
- **D**:结局名(反弹/免疫恢复/病毒抑制)与常见临床结局重合,**核查结论:重合是因为文献本身就在预测这些量,而非复用记忆分类**;拆解轴(结局类型×输入模态)为归纳后描述。
- **E**:如实标注其落点偏体液免疫/抗病毒药物,与"HIV × T 细胞"主锁关联为**间接**(T 细胞辅助抗体成熟、疫苗 T 细胞表位);聚类由原子问题强支撑但主题贴合度需打折。
- **独立条目**:AQ08、AQ53 刻意不并簇(第四步),理由见 §III.2。

### V.3 小问题推进状态分类(有数据就能推进 / 只差算法设计 / 数据和方法都还没有)

23 个小问题分类计数:**有数据就能推进 19**、**只差算法设计 3**、**数据和方法都还没有 1**。

**有数据就能推进:**
- A.1(「HIV-1 整合位点的基因组位置如何决定被感染 T 细胞的转录命运与持续…」):整合位点+单细胞转录数据已存在(LANL/GEO),已有位点-命运关联分析;可直接建模。
- A.2(「克隆增殖如何驱动 HIV 储存库的扩增与病毒反弹?…」):整合位点/条形码克隆纵向数据+已发表多维/条形码模型均在;数据与 baseline 齐备。
- A.3(「哪些细胞状态/谱系转录程序使 CD4 T 细胞倾向于携带并维持前病毒?…」):单细胞多模态潜伏数据充裕(GEO),已有差异状态分析;推进主要靠更好表征而非缺数据。
- A.4(「HIV 储存库在不同组织/解剖部位与 T 细胞谱系间如何分布?…」):多组织/谱系单细胞数据存在(部分见 GEO/HCA);描述性刻画已有,可扩展。
- A.6(「储存库细胞的表型是否携带免疫选择的印记?…」):储存库表型/序列数据存在,已有免疫选择签名研究作 baseline。
- B.1(「单细胞多组学能否刻画潜伏逆转过程并识别新的逆转相关标志?…」):逆转前后单细胞多组学数据已发表(AQ04),可复用扩展。
- B.2(「哪些宿主表观遗传标记可预测储存库大小及其对逆转的响应性?…」):宿主甲基化队列数据(GEO 芯片)+候选标记 baseline 已在。
- B.3(「哪些 DNA 甲基化/表观机制在锁定 HIV 潜伏中起作用?…」):甲基化/表观机制数据与 UHRF1 等机制 baseline 已在。
- C.1(「T 细胞受体的识别特性(公共型、亲和力、疏水性)如何决定 HIV 特异性…」):TCR 序列/表位数据(VDJdb/IEDB)+多篇识别质量 baseline 已在。
- C.2(「HIV 特异 CD8 T 细胞库的克隆结构如何随感染与 ART 演变?…」):纵向 TCR-seq 数据与克隆更替 baseline 已在。
- C.3(「哪些转录/代谢功能程序(干性、代谢通路、miRNA)区分控制者与进展者的…」):CD8 单细胞转录+代谢数据与多篇区分性签名 baseline 已在。
- D.1(「表达型/整合型储存库大小能否预测 ART 中断后病毒反弹时间?…」):储存库大小测量+反弹时间队列与多篇 baseline 已在(AQ29/30)。
- D.2(「哪些循环免疫/血浆生物标志物与早期病毒动力学可预测反弹时间或治疗后控制?…」):血浆标志物/早期动力学数据与反弹/PTC baseline 已在。
- D.3(「基线代谢组/脂质组/蛋白组特征能否预测 ART 后免疫学恢复?…」):基线代谢/脂质/蛋白组数据(MW/PRIDE)与多篇免疫恢复 baseline 已在。
- D.4(「多组学整合能否揭示与 HIV 病毒载量相关的机制与风险谱?…」):多组学整合数据与网络整合 baseline 已在。
- D.5(「机器学习能否从临床表格变量预测病毒抑制/失败与护理脱失?…」):临床表格 ML 有多篇 baseline;但注意数据多为受控访问,"能推进"以获授权为前提。
- E.1(「能否从病毒序列预测 HIV 对广谱中和抗体(bNAb)的中和敏感性?…」):CATNAP 中和数据+序列(LANL)公开,多篇 bNAb 预测 baseline 已在。
- E.2(「能否准确预测临床 HIV-1 分离株对抗体的耐药性?…」):抗体耐药预测数据+多篇 baseline(含 BRAVE)已在。
- E.3(「深度学习能否从 HIV-1 序列预测抗病毒药物耐药性?…」):Stanford HIVDB 耐药数据公开+多篇 DL baseline 已在。

**只差算法设计:**
- A.5(「可翻译/完整前病毒储存库在单细胞层面有哪些可识别特征,群体动力学如何随时…」):可翻译/完整性单细胞读出较稀、随机动力学参数需从有限纵向数据反推;机制模型有,但单细胞完整性大规模数据偏少,方法整合仍待设计。
- C.4(「感染前/早期的宿主转录状态能否预示 HIV 疾病进展?…」):感染前/早期纵向样本稀少(需 pre-infection 队列),FAM26F 单篇 baseline;数据窗口窄,主要缺能在小样本上稳健的预测方法。
- E.4(「能否解码 Env 表位免疫优势/免疫原性并据此设计多表位疫苗与保守靶点?…」):Env 序列/cryoEM 结构数据存在,但"免疫优势/多表位疫苗设计"多为探索性算法,缺统一 baseline 与标准化免疫原性标签;数据在、方法待成型。

**数据和方法都还没有:**
- B.4(「能否通过让储存库对细胞死亡敏化来促进其清除?…」):敏化-清除多为单项干预研究,缺乏可复用的公开扰动-存活配对数据集与预测 baseline;既缺标准化数据也缺预测方法。

### V.4 覆盖充分性诚实评估

**本轮覆盖较充分的部分:**
- 病毒学测序(整合位点、克隆扩增、近全长/完整性测序、bNAb 序列预测)——HIV 最丰富模块,多角度检索均达满额,A/E 支证据密集。
- 单细胞转录组下的储存库/潜伏/CD8 应答刻画——数据与文献充裕。
- 序列→表型深度学习(耐药、中和、整合)——baseline 多、可核实。
- 临床表格 ML 预测(病毒抑制/失败/反弹)——文献量足。

**可能有遗漏 / 偏薄的部分(如实记录):**
- **纯 ML 会议文献(NeurIPS/ICML/ICLR 等)**:PubMed 不收录,而本轮 **OpenAlex 连接器不可用、arXiv 受限流**,故"最前沿深度模型"一端(含 Part I 校准示例里 ImmunoFoundation 这类 ICML 工作)**系统性缺席**;这是本轮工具层的确定性缺口,非领域本身空白。
- **scATAC-seq × HIV**:定向检索几无新增独立可核实条目;HIV 专门的染色质可及性数据在本轮检索范围内确实稀薄(已多角度重搜)。
- **HIV 空间转录组/统一空间图谱**:多为组织病毒群体演化,真正空间组学 HIV 数据集少,无统一大规模图谱(本轮检索范围内)。
- **单细胞层面蛋白质组 biomarker**:定向检索新增极少。
- **代谢组 × T 细胞 ML 的交叉**:HIV 代谢组多为血浆层面关联,与"T 细胞"直接绑定的 ML 工作偏少。
- 非英文文献、预印本、以及未被 PubMed 索引的方法学工具论文可能有遗漏。

### V.5 存疑判断与未能核实项清单

- **Beusch et al., "Toward mechanistic virtual immune cells", Nat Biotechnol 2026**(Part I 校准示例之一):PubMed 未返回摘要,Part I 相应表述**仅据标题概括,正文论点未经核实**,已在 Part I 正文标注。
- beusch2026mechvic(PMID 42350645):PubMed 未返回摘要(A: Abstract not available);one_line 仅据标题推断,核心论点未经正文核实
- **OpenAlex 不可用**:本轮尝试 OpenAlex 连接器,已获取 API key 但连接器持续返回 `openalex_key_required`(4 次重试失败),判定为连接器未正确装载密钥,需在 设置→连接器 重新启用。**后果**:无法用 OpenAlex 的引文网络"顺藤摸瓜"扩展,Part I"被反复引用的地基论文"识别改为依据综述正文的点名 + PubMed 检索,可能低估某些高被引但未在综述正文点名的方法论文。
- **arXiv 限流**:多次触发 ReadTimeout / HTTP 429,预印本仅零星可查,未纳入正式参考。
- **叶级具体 accession**:如 V.1 所述,模块级资源已核实,单条 accession 未逐一点名,标"未逐一核实"。
- **E 支主题贴合度**:E 支与"T 细胞"的关联为间接,是否应计入"HIV × T 细胞"主线存在判断空间,已在 §III.3 与 V.2 标注,不下强结论。
- **样本量/量级数字**:正文未逐条给出各研究样本量;凡未实际核实的量级一律未写入,不使用占位符。

---

*全文参考合计 206 条(去重、PMID+DOI 经 PubMed 核实);原子问题 64;大问题 5、小问题 23、独立条目 2。检索横跨 2015–2026(个别地基方法早至 2015 以前),来源以 PubMed 为主。*