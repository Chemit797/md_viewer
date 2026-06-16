# Tfh 细胞特异性代谢特征与 Human-GEM/ftINIT 任务设计

## 摘要

Tfh 细胞的代谢建模不应只用“Warburg effect”作为活化锚点，因为文献显示 Tfh 分化还依赖 ICOS-mTOR 介导的葡萄糖摄取与脂质合成、谷氨酰胺/谷氨酸代谢、MTHFD2 线粒体一碳代谢，以及胆碱-Kennedy pathway 介导的磷脂酰胆碱合成。ICOS 可通过 mTORC1/mTORC2 同时驱动糖酵解和 lipogenesis，Glut1 介导的葡萄糖代谢促进 Tfh 反应，这直接支持“glucose to fatty acid”类任务作为 Tfh active-state anchor ([Immunity 2016](https://pmc.ncbi.nlm.nih.gov/articles/PMC5050556/))。与之相对，Treg 经典上更偏向低 Glut1、高 lipid oxidation 的代谢程序，因此用 anabolic lipogenesis、glutaminolysis、one-carbon metabolism 和 phosphatidylcholine synthesis 作为 Tfh 强制任务，可以比单纯乳酸外排更有助于拉开 Tfh 与 Treg 的网络拓扑差异 ([Journal of Immunology 2011](https://pmc.ncbi.nlm.nih.gov/articles/PMC3198034/))。

本文将前两次结果合并为两层输出：第一层是可解释的 Tfh 代谢特征与文献依据，第二层是可直接转换为 RAVEN/ftINIT 任务文件的 Human-GEM metabolite ID 表。Human-GEM 的反应、代谢物和基因注释位于 `model/` 目录中的 `reactions.tsv`、`metabolites.tsv` 和 `genes.tsv`，本文所有 MAM 代谢物 ID 均按当前 `metabolites.tsv` 校验 ([Human-GEM GitHub](https://github.com/SysBioChalmers/Human-GEM), [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv))。

## 建模目标与使用原则

这些任务的目标不是构造新的伪反应，而是给 ftINIT/RAVEN 提供“参考网络必须能完成的生物学功能约束”。Human-GEM 原生 metabolic task 文件包含 `IN`、`OUT` 和 `EQU` 等列，因此下表的 `IN` 与 `OUT` 可对应底物可用性和产物生成约束，`EQUATION` 列则应理解为任务净流向说明，而非要加入模型的严格元素平衡反应 ([Human-GEM metabolicTasks_Essential.txt](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/data/metabolicTasks/metabolicTasks_Essential.txt))。

一个重要 ID 修正是：Human-GEM 中 D-glucose 的 extracellular ID 是 `MAM01965[e]`，而 `MAM01974[e]` 是 L-glutamate，不是 glucose ([Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv))。如果 RAVEN 模型对象内部使用无括号 ID，则 `MAM01965[e]` 需要转换为 `MAM01965e`，其余 compartments 同理 ([Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv))。

## Tfh 特异性代谢特征汇总

| 优先级 | Specific metabolic pathway | Key distinguishing feature vs Treg | Key enzymes/genes for GPR | Actionable GEM task | Primary literature source |
|---|---|---|---|---|---|
| 1 | ICOS-mTOR 介导的葡萄糖摄取、糖酵解与 de novo lipogenesis | Tfh 在 ICOS 刺激下通过 mTORC1/mTORC2 增强 glycolysis 和 lipogenesis，Glut1 上调促进 Tfh/GC response；经典 Treg 更偏低 Glut1 与 lipid oxidation | SLC2A1/GLUT1, MTOR, RPTOR, RICTOR, MYC, ACLY, ACACA/ACC1, FASN, SCD | consume extracellular glucose, produce cytosolic palmitate and optional extracellular CO2/lactate | “mTORC1 and mTORC2 Kinase Signaling and Glucose Metabolism Drive Follicular Helper T Cell Differentiation”, Immunity ([Immunity 2016](https://pmc.ncbi.nlm.nih.gov/articles/PMC5050556/)); Treg contrast from “Cutting Edge: Distinct Glycolytic and Lipid Oxidative Metabolic Programs Are Essential for Effector and Regulatory CD4+ T Cell Subsets”, Journal of Immunology ([Journal of Immunology 2011](https://pmc.ncbi.nlm.nih.gov/articles/PMC3198034/)) |
| 2 | Glutaminolysis to alpha-ketoglutarate and enhanced glutamate metabolism | Lupus-prone pathogenic Tfh 显示增强 glutamate metabolism、malate-aspartate shuttle、ammonia recycling，并伴随 glutamine transporter 程序增强；Treg 方向通常不以 glutamine-to-aKG anaplerosis 作为核心区分任务 | SLC1A5, SLC38A2, SLC38A6, GLS, GLUD1/2, GOT1/2, MDH1/2 | consume extracellular glutamine, produce mitochondrial alpha-ketoglutarate and ammonium | “Transcriptional and metabolic programs promote the expansion of follicular helper T cells in lupus-prone mice”, iScience ([iScience 2023](https://pmc.ncbi.nlm.nih.gov/articles/PMC10197114/)) |
| 3 | MTHFD2-driven mitochondrial one-carbon metabolism | CD4+ T to Tfh differentiation中，一碳代谢显著上调；serine/methionine/glycine supplementation 促进 Tfh differentiation，MTHFD2 inhibition 或 CD4 T cell-specific knockout 抑制 Tfh 与 tertiary lymphoid organ formation；MTHFD2 deficiency 更偏向增强 Treg/FoxP3 方向 | MTHFD2, SHMT2, MTHFD1L, SLC1A4, SLC36A1, MTHFD1, TYMS | consume extracellular serine, produce mitochondrial glycine and cytosolic formate | “Mitochondrial 1-Carbon Metabolism Drives CD34-Lineage Cells to Differentiate Into T Follicular Helper Cells to Form Tertiary Lymphoid Organs in Transplant Arteriosclerosis”, Circulation ([Circulation 2025](https://www.ahajournals.org/doi/10.1161/CIRCULATIONAHA.125.073691)); “MTHFD2 is a Metabolic Checkpoint Controlling Effector and Regulatory T Cell Fate and Function”, Immunity ([Immunity 2021](https://pmc.ncbi.nlm.nih.gov/articles/PMC8755618/)) |
| 4 | Kennedy pathway for phosphatidylcholine synthesis | Tfh-derived AITL cells highly依赖 Kennedy pathway 的 choline lipid branch 来合成 phosphatidylcholine，human AITL Tfh 程序也显示 choline pathway 上调；这比一般 Warburg task 更接近 membrane biogenesis 和 Tfh-like proliferative state | SLC44A1, SLC44A4, SLC5A7, CHKA/CHKB, PCYT1A, CEPT1, CHPT1, LPCAT1 | consume extracellular choline, CTP, ATP and DAG, produce cytosolic phosphatidylcholine, CMP, ADP and PPi | “Inhibition of choline metabolism in an angioimmunoblastic T-cell lymphoma preclinical model reveals a new metabolic vulnerability as possible target for treatment”, Journal of Experimental & Clinical Cancer Research ([JECCR 2024](https://jeccr.biomedcentral.com/articles/10.1186/s13046-024-02952-w)) |
| 5 | FXR/cholesterol-associated pathogenic Tfh response | 该方向更适合作为后续候选任务或调控层特征，因为最新文献提示 FXR inhibition 可作为 pathogenic Tfh response 的 checkpoint，但其与 Human-GEM 代谢任务的直接底物-产物约束仍需更谨慎定义 | NR1H4/FXR, cholesterol/bile acid metabolism genes, context-dependent ABC transporters | optional: cholesterol/bile acid handling task, not recommended as top forced task without context-specific evidence | “FXR inhibition functions as a checkpoint blockade of the pathogenic Tfh cell response in lupus”, Cellular & Molecular Immunology ([Cellular & Molecular Immunology 2025](https://www.nature.com/articles/s41423-025-01309-3)) |
| 6 | cTfh17 glucose-dependent activation | cTfh17 比 cTfh1/cTfh2 显示更高 glycolytic activity，glucose deprivation 会降低 costimulatory molecule expression、cytokine production 和 B cell activation capacity；该特征可作为 Tfh subset-specific glycolysis task，而不是 pan-Tfh task | glycolysis-related genes, SLC2A family, HK2, PFK, LDHA, activation markers ICOS/PDCD1 | optional: extracellular glucose to lactate plus ATP demand, cTfh17-specific | “Metabolic pathways within cTfh subsets and glucose-dependent activation of cTfh17 in SLE and healthy individuals”, JCI Insight ([JCI Insight 2025](https://insight.jci.org/articles/view/189858)) |

## Top 4 强制 ftINIT 任务设计

### Task 01: Glucose-derived anabolic lipogenesis

该任务用于强制 Tfh 模型保留从 extracellular glucose 到 cytosolic palmitate 的 anabolic carbon flow。ICOS-mTOR 论文显示，ICOS stimulation 同时促进 glycolysis 和 lipogenesis，Raptor/Rictor deficiency 会削弱这些代谢增强，Glut1-mediated glucose metabolism 促进 Tfh response ([Immunity 2016](https://pmc.ncbi.nlm.nih.gov/articles/PMC5050556/))。

推荐将该任务作为 Tfh active-state 的核心 anabolic task，而不是仅要求 glucose to lactate。Treg 对比依据是 FoxP3+ Treg 经典上 Glut1 较低且 lipid oxidation 较高，因此 palmitate synthesis 比单纯 aerobic glycolysis 更能体现 Tfh 的 anabolic membrane/growth demand ([Journal of Immunology 2011](https://pmc.ncbi.nlm.nih.gov/articles/PMC3198034/))。

### Task 02: Glutaminolysis to mitochondrial alpha-ketoglutarate

该任务用于强制保留 glutamine uptake、glutaminase 和 glutamate dehydrogenase/transaminase 相关 anaplerotic route。iScience 2023 的 lupus-prone Tfh 数据显示，TC Tfh cells 具有增强的 glutamate metabolism、malate-aspartate shuttle 和 ammonia recycling，并且多个 glutamine transporter 在 Tfh 中上调，包括 Slc1a5、Slc38a2 和 Slc38a6 ([iScience 2023](https://pmc.ncbi.nlm.nih.gov/articles/PMC10197114/))。

GEM 中建议把 extracellular glutamine 到 mitochondrial alpha-ketoglutarate 和 ammonium 作为任务终点。这样会比“消耗 glutamine 生成 biomass precursor”更具体，也更容易在 Tfh 与 Treg 的 topology graph 中形成可解释子网络。

### Task 03: MTHFD2-driven mitochondrial one-carbon metabolism

该任务用于强制 serine-derived mitochondrial one-carbon flux，核心净流向是 serine 进入线粒体一碳代谢，产生 glycine 与 formate。Circulation 2025 研究显示，CD4+ T 到 Tfh differentiation 过程中一碳代谢显著上调，deuterium-labeled serine 证明 mitochondrial 1-carbon pathway 占主导，MTHFD2 inhibition 或 CD4+ T cell-specific MTHFD2 knockout 会显著抑制 Tfh numbers 和 tertiary lymphoid organ formation ([Circulation 2025](https://www.ahajournals.org/doi/10.1161/CIRCULATIONAHA.125.073691))。

MTHFD2 也是 effector versus regulatory fate 的关键代谢 checkpoint。Immunity 2021 研究显示，MTHFD2 deficiency 会削弱 Teff proliferation 与 inflammatory cytokine production，并促进 Treg/FoxP3 方向，因此该任务特别适合用来区分 Tfh-like effector fate 与 Treg fate ([Immunity 2021](https://pmc.ncbi.nlm.nih.gov/articles/PMC8755618/))。

### Task 04: Kennedy pathway phosphatidylcholine synthesis

该任务用于强制 choline uptake/activation、CDP-choline branch 和 phosphatidylcholine production。JECCR 2024 研究显示，AITL 的 malignant driver 是 CD4+ Tfh cells，mAITL Tfh cells 高度依赖 Kennedy pathway 的 choline lipid branch 生成 phosphatidylcholine，human AITL Tfh cells 也显示 choline lipid pathway upregulation ([JECCR 2024](https://jeccr.biomedcentral.com/articles/10.1186/s13046-024-02952-w))。

虽然 AITL 是 malignant Tfh context，但它对“高度活跃 Tfh-like state 的 membrane lipid dependency”非常有用。对于 Human-GEM/ftINIT，建议用 choline + CTP + DAG 到 phosphatidylcholine + CMP 的任务净流向来强制保留 Kennedy pathway 拓扑。

## Human-GEM metabolite ID 对照

| Metabolite | Human-GEM ID with compartment | BiGG-like label in Human-GEM | 任务用途 | Source |
|---|---|---|---|---|
| D-glucose extracellular | MAM01965[e] | glc__D | Task 01 IN | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| ATP cytosol | MAM01371[c] | atp | Task 01/04 IN | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| NADPH cytosol | MAM02555[c] | nadph | Task 01 IN | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| Palmitate cytosol | MAM02674[c] | hdca | Task 01 OUT | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| Carbon dioxide extracellular | MAM01596[e] | co2 | Task 01 OUT | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| L-glutamine extracellular | MAM01975[e] | gln__L | Task 02 IN | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| Alpha-ketoglutarate mitochondria | MAM01306[m] | akg | Task 02 OUT | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| Ammonium extracellular | MAM02579[e] | nh4 | Task 02 OUT | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| L-serine extracellular | MAM02896[e] | ser__L | Task 03 IN | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| Glycine mitochondria | MAM01986[m] | gly | Task 03 OUT | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| Formate cytosol | MAM01833[c] | for | Task 03 OUT | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| Choline extracellular | MAM01513[e] | chol | Task 04 IN | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| CTP cytosol | MAM01623[c] | ctp | Task 04 IN | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| Diacylglycerol cytosol | MAM00240[c] | dag_hs | Task 04 IN | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| Phosphatidylcholine cytosol | MAM02684[c] | pchol_hs | Task 04 OUT | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| CMP cytosol | MAM01590[c] | cmp | Task 04 OUT | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |
| Pyrophosphate cytosol | MAM02759[c] | ppi | Task 04 OUT | [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv) |

## RAVEN/ftINIT-compatible task table

下表保留用户指定的六列格式，`Mandatory` 全部设为 `TRUE`。`EQUATION` 是用于解释任务净流向的简化式；在 RAVEN task 文件中，更稳妥的做法是用 `IN` 和 `OUT` 设置可行性约束，让 Human-GEM 内部已有反应来完成严格的化学计量与 compartment transport ([Human-GEM metabolicTasks_Essential.txt](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/data/metabolicTasks/metabolicTasks_Essential.txt))。

| Task_ID | Description | IN | OUT | EQUATION | Mandatory |
|---|---|---|---|---|---|
| Tfh_Task_01 | Glucose-derived anabolic lipogenesis, forcing extracellular glucose into cytosolic palmitate production | MAM01965[e]; MAM01371[c]; MAM02555[c] | MAM02674[c]; MAM01596[e]; MAM01285[c]; MAM02751[c]; MAM02554[c] | 4 MAM01965[e] + 7 MAM01371[c] + 14 MAM02555[c] -> MAM02674[c] + 8 MAM01596[e] + 7 MAM01285[c] + 7 MAM02751[c] + 14 MAM02554[c] | TRUE |
| Tfh_Task_02 | Glutaminolysis to mitochondrial alpha-ketoglutarate, forcing glutamine anaplerosis through GLS/GLUD-like topology | MAM01975[e]; MAM02040[m]; MAM02552[m] | MAM01306[m]; MAM02579[e]; MAM02553[m]; MAM02039[m] | MAM01975[e] + 2 MAM02040[m] + MAM02552[m] -> MAM01306[m] + 2 MAM02579[e] + MAM02553[m] + MAM02039[m] | TRUE |
| Tfh_Task_03 | MTHFD2-linked mitochondrial one-carbon metabolism, forcing serine catabolism to glycine plus exported formate | MAM02896[e]; MAM02040[m]; MAM02552[m] | MAM01986[m]; MAM01833[c]; MAM02553[m]; MAM02039[m] | MAM02896[e] + MAM02040[m] + MAM02552[m] -> MAM01986[m] + MAM01833[c] + MAM02553[m] + MAM02039[m] | TRUE |
| Tfh_Task_04 | Kennedy pathway phosphatidylcholine synthesis, forcing choline plus DAG conversion into cytosolic phosphatidylcholine | MAM01513[e]; MAM01371[c]; MAM01623[c]; MAM00240[c] | MAM02684[c]; MAM01285[c]; MAM02759[c]; MAM01590[c] | MAM01513[e] + MAM01371[c] + MAM01623[c] + MAM00240[c] -> MAM02684[c] + MAM01285[c] + MAM02759[c] + MAM01590[c] | TRUE |

## TSV-ready version

```tsv
Task_ID	Description	IN	OUT	EQUATION	Mandatory
Tfh_Task_01	Glucose-derived anabolic lipogenesis, forcing extracellular glucose into cytosolic palmitate production	MAM01965[e]; MAM01371[c]; MAM02555[c]	MAM02674[c]; MAM01596[e]; MAM01285[c]; MAM02751[c]; MAM02554[c]	4 MAM01965[e] + 7 MAM01371[c] + 14 MAM02555[c] -> MAM02674[c] + 8 MAM01596[e] + 7 MAM01285[c] + 7 MAM02751[c] + 14 MAM02554[c]	TRUE
Tfh_Task_02	Glutaminolysis to mitochondrial alpha-ketoglutarate, forcing glutamine anaplerosis through GLS/GLUD-like topology	MAM01975[e]; MAM02040[m]; MAM02552[m]	MAM01306[m]; MAM02579[e]; MAM02553[m]; MAM02039[m]	MAM01975[e] + 2 MAM02040[m] + MAM02552[m] -> MAM01306[m] + 2 MAM02579[e] + MAM02553[m] + MAM02039[m]	TRUE
Tfh_Task_03	MTHFD2-linked mitochondrial one-carbon metabolism, forcing serine catabolism to glycine plus exported formate	MAM02896[e]; MAM02040[m]; MAM02552[m]	MAM01986[m]; MAM01833[c]; MAM02553[m]; MAM02039[m]	MAM02896[e] + MAM02040[m] + MAM02552[m] -> MAM01986[m] + MAM01833[c] + MAM02553[m] + MAM02039[m]	TRUE
Tfh_Task_04	Kennedy pathway phosphatidylcholine synthesis, forcing choline plus DAG conversion into cytosolic phosphatidylcholine	MAM01513[e]; MAM01371[c]; MAM01623[c]; MAM00240[c]	MAM02684[c]; MAM01285[c]; MAM02759[c]; MAM01590[c]	MAM01513[e] + MAM01371[c] + MAM01623[c] + MAM00240[c] -> MAM02684[c] + MAM01285[c] + MAM02759[c] + MAM01590[c]	TRUE
```

## ftINIT 实施建议

优先把四个任务都设置为 mandatory，并先在 full Human-GEM 上单独测试 feasibility。若某个任务失败，优先检查 compartment transport、exchange reaction、cofactor availability 和 task bounds，而不是立刻放弃该生物学假设，因为 Human-GEM metabolic tasks 本身就是通过 `IN`、`OUT` 和 `EQU` 组合来测试网络可行性 ([Human-GEM metabolicTasks_Essential.txt](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/data/metabolicTasks/metabolicTasks_Essential.txt))。

对于 GNN 任务，建议将这四个任务映射到四个 pathway-level subgraph labels：glycolysis-lipogenesis、glutaminolysis-aKG、mitochondrial one-carbon metabolism 和 Kennedy phosphatidylcholine synthesis。这四类 subgraph 分别对应 carbon source usage、anaplerotic nitrogen/carbon flow、folate-coupled biosynthesis 和 membrane phospholipid synthesis，因此比单一 Warburg task 更适合捕捉 Tfh 与 Treg differentiation fate 的拓扑差异。

## 关键参考文献与用途

- “mTORC1 and mTORC2 Kinase Signaling and Glucose Metabolism Drive Follicular Helper T Cell Differentiation”, Immunity, 2016：支持 ICOS-mTOR、Glut1、glycolysis 和 lipogenesis 作为 Tfh 正向代谢轴 ([Immunity 2016](https://pmc.ncbi.nlm.nih.gov/articles/PMC5050556/))。
- “Transcriptional and metabolic programs promote the expansion of follicular helper T cells in lupus-prone mice”, iScience, 2023：支持 Tfh 中 glutamate metabolism、malate-aspartate shuttle、ammonia recycling 和 glutamine transporter 程序增强 ([iScience 2023](https://pmc.ncbi.nlm.nih.gov/articles/PMC10197114/))。
- “Mitochondrial 1-Carbon Metabolism Drives CD34-Lineage Cells to Differentiate Into T Follicular Helper Cells to Form Tertiary Lymphoid Organs in Transplant Arteriosclerosis”, Circulation, 2025：支持 MTHFD2 与 mitochondrial one-carbon metabolism 直接促进 Tfh differentiation ([Circulation 2025](https://www.ahajournals.org/doi/10.1161/CIRCULATIONAHA.125.073691))。
- “MTHFD2 is a Metabolic Checkpoint Controlling Effector and Regulatory T Cell Fate and Function”, Immunity, 2021：支持 MTHFD2 作为 effector versus Treg fate checkpoint，并解释为什么该任务可帮助区分 Tfh 与 Treg ([Immunity 2021](https://pmc.ncbi.nlm.nih.gov/articles/PMC8755618/))。
- “Inhibition of choline metabolism in an angioimmunoblastic T-cell lymphoma preclinical model reveals a new metabolic vulnerability as possible target for treatment”, Journal of Experimental & Clinical Cancer Research, 2024：支持 Tfh-derived AITL 对 Kennedy pathway 和 phosphatidylcholine synthesis 的依赖 ([JECCR 2024](https://jeccr.biomedcentral.com/articles/10.1186/s13046-024-02952-w))。
- “Cutting Edge: Distinct Glycolytic and Lipid Oxidative Metabolic Programs Are Essential for Effector and Regulatory CD4+ T Cell Subsets”, Journal of Immunology, 2011：提供 Tfh-like effector metabolism 与 Treg lipid oxidation/OXPHOS 方向的基础对比 ([Journal of Immunology 2011](https://pmc.ncbi.nlm.nih.gov/articles/PMC3198034/))。
- Human-GEM 官方仓库与 `metabolites.tsv`：支持 MAM ID、compartment ID 和 annotation 的校验 ([Human-GEM GitHub](https://github.com/SysBioChalmers/Human-GEM), [Human-GEM metabolites.tsv](https://raw.githubusercontent.com/SysBioChalmers/Human-GEM/main/model/metabolites.tsv))。
