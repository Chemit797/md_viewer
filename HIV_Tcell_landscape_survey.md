# HIV × T 细胞计算建模领域概况

**调研范围与定位说明**：本文档是"虚拟T细胞"课题在"摸清家底"阶段产出的一份**领域普查与综述**文档。目的是对 HIV × T 细胞计算建模相关的数据模态、公开数据资源、临床研究主题与代表性文献进行有组织的盘点，**不构成方法选型建议，不预设任何算法框架的优劣，不代表团队在方向上的取舍**。全文遵循"查不到即标注'未核实'，不编造、不use占位符"的原则；对"空白/首次/从未有人做过"类强结论一律回避，改用"在本轮检索范围内未见"的表述。

**检索方法概述**：本轮调研通过三条独立通道进行文献采集——(1) OpenAlex（经官方 REST API，使用注册 API Key 直接访问，覆盖全学科索引）；(2) PubMed（通过 NCBI MCP 检索接口）；(3) arXiv（通过 arXiv 检索接口，聚焦计算/机器学习相关预印本）。检索矩阵覆盖 9 个组学类目（合计 39 条查询）与 7 个临床主题类目（合计 19 条查询），另有 6 条综述类种子查询。在初步检索基础上，选取各类目被引数最高的若干"锚点文献"，通过 OpenAlex 的引用图谱（向前引用 forward citation 与向后引用 references）做了一轮扩展检索，以覆盖种子词未能直接命中但被锚点文献密集引用/被引用的相关工作。检索执行日期为 2026年7月15日；受限于关键词组合与检索窗口，本报告**不代表该领域文献的穷尽枚举**，只是一次覆盖面较广的横断面普查。

---

## Section 1: 领域叙事概况与研究动机

HIV 感染与 T 细胞（尤其是 CD4+ T 细胞）之间的相互作用，是免疫学与病毒学交叉领域中被研究最广泛、数据积累最丰富的方向之一。计算建模在这一领域中的角色大致可以归纳为以下几条脉络（均基于本轮检索到的具体文献支撑，逐条给出参考）：

**(a) 潜伏病毒库（latent reservoir）的建立、维持与定量建模。** 抗逆转录病毒治疗（ART）虽能抑制病毒复制，但无法清除整合入静息记忆 CD4+ T 细胞基因组中的前病毒，这构成了"功能性治愈"的核心障碍。
早期体外模型工作建立了潜伏感染可重复诱导的实验体系（DOI: [10.1093/emboj/cdg188](https://doi.org/10.1093/emboj/cdg188)），随后的研究表明潜伏库中存在大量"非诱导型"但仍具复制能力的前病毒，这些前病毒构成了治愈策略的额外障碍（DOI: [10.1016/j.cell.2013.09.020](https://doi.org/10.1016/j.cell.2013.09.020)），而更精确定量潜伏库规模的方法学工作（如近全长个体前病毒测序）也随之发展（DOI: [10.1038/s41586-019-0898-8](https://doi.org/10.1038/s41586-019-0898-8)）。这一方向目前是 GEO 等公共数据库中 HIV 相关组学数据集最集中的主题（如整合位点专项检索命中 23 条 GEO 记录，详见 Section 2）。

**(b) 免疫重建与 CD4 恢复的异质性。** 部分感染者在 ART 后 CD4 计数恢复不完全（"免疫无应答者"，immunological non-responders），这一现象促使了对 CD4 恢复轨迹的表格化临床数据建模，以及近期以机器学习方法预测免疫重建结局的尝试（ClinicalTrials.gov 检索显示相关注册研究但公开表格化数据集仍然有限，详见 Section 2 临床数据部分）。

**(c) 自发/治疗后病毒控制现象（精英控制者 EC、治疗后控制者 PTC）驱动的免疫机制研究。** 少数感染者无需 ART 即可自发控制病毒复制，或在治疗中断后维持长期病毒学控制，这类"天然实验"为理解何种 T 细胞免疫特征（如 CD8+ T 细胞功能、TCR 特异性）与病毒控制相关提供了独特窗口，相关综述见 Section 4。

**(d) 疫苗设计与广谱中和抗体（bnAb）研发。** HIV 包膜蛋白的高变异性使传统疫苗策略屡屡受挫，计算免疫学（表位预测、抗体谱系追踪）在这一方向的应用有较长历史（相关综述见 Section 4）。

**(e) 耐药性与病毒演化的群体遗传学/系统发育建模。** HIV 的高突变率使其成为病毒演化动力学建模的经典对象，相关的常微分方程/时滞微分方程模型在 arXiv 上有持续但规模不大的产出（如 arXiv:1003.5992, arXiv:1403.4196，详见 Section 3）。

**(f) 系统免疫学建模与多组学整合。** 随着单细胞多组学（CITE-seq、多组学联合分析）技术的普及，近年来出现了将转录组、表观组、代谢组等多层数据整合以刻画 HIV 感染 CD4+ T 细胞异质性的尝试（如 GSE313059 单细胞多组学检测大麻素对HIV感染CD4 T细胞的影响），这是本领域数据模态最新、增长最快但尚未形成成熟标准流程的方向。

**总体特征**：从本轮检索结果看，该领域的数据资源在"转录组学"与"病毒学测序/前病毒库定量"两个模态上最为丰厚且方法学最成熟；"代谢组学"与"影像学"模态公开数据资源相对匮乏；"多组学整合/空间组学"是数据增长最快但方法尚不成熟的前沿方向。临床主题上，"病毒库与潜伏机制"占据绝对主导地位，其余主题（免疫重建、EC/PTC、疫苗、耐药演化）均有可观但规模较小的独立文献体系。

---

## Section 2: 组学类目分类概况

本节是本报告的核心部分，按 9 个组学类目逐一梳理：(a) 类目描述与代表性可核实文献；(b) 相关公开数据资源及具体 accession；(c) 数据丰富度评级；(d) 计算方法成熟度评级。评级为定性判断，依据均在对应小节中列出，供后续团队自行复核。


### 2.1 转录组学（Bulk RNA-seq / 单细胞 scRNA-seq）

**(a) 描述与代表性文献**

- Distinct viral reservoirs in individuals with spontaneous control of HIV-1 (2020). DOI: [10.1038/s41586-020-2651-8](https://doi.org/10.1038/s41586-020-2651-8), PMID:32848246. 被引:421
- Targeting the Latent Reservoir for HIV-1 (2018). DOI: [10.1016/j.immuni.2018.04.030](https://doi.org/10.1016/j.immuni.2018.04.030). 被引:349
- HIV-1 transcription and latency: an update (2013). DOI: [10.1186/1742-4690-10-67](https://doi.org/10.1186/1742-4690-10-67), PMID:23803414. 被引:326
- CD8+ T cells in HIV control, cure and prevention (2020). DOI: [10.1038/s41577-020-0274-9](https://doi.org/10.1038/s41577-020-0274-9), PMID:32051540. 被引:309
- An In-Depth Comparison of Latency-Reversing Agent Combinations in Various In Vitro and Ex Vivo HIV-1 Latency Models Identified Bryostatin-1+JQ1 and Ingenol-B+JQ1 to Potently Reactivate Viral Gene Expression (2015). DOI: [10.1371/journal.ppat.1005063](https://doi.org/10.1371/journal.ppat.1005063). 被引:286
- Single-cell characterization and quantification of translation-competent viral reservoirs in treated and untreated HIV infection (2019). DOI: [10.1371/journal.ppat.1007619](https://doi.org/10.1371/journal.ppat.1007619), PMID:30811499. 被引:238
- Understanding HIV Latency: The Road to an HIV Cure (2015). DOI: [10.1146/annurev-med-092112-152941](https://doi.org/10.1146/annurev-med-092112-152941), PMID:25587657. 被引:219
- Enhanced TLR7-induced interferon responses in women living with HIV (2026). DOI: [10.3389/fimmu.2026.1791579](https://doi.org/10.3389/fimmu.2026.1791579), PMID:42093980. 被引:0
- Modulation of IRF7-driven transcription as a strategy to control HIV-1 latency (2026). DOI: [10.3389/fimmu.2026.1735192](https://doi.org/10.3389/fimmu.2026.1735192), PMID:41918746. 被引:0
- Single cell multiomic analysis of the impact of Delta-9-tetrahydrocannabinol on HIV infected CD4 T cells (2026). DOI: [10.1186/s42238-026-00412-0](https://doi.org/10.1186/s42238-026-00412-0), PMID:41782037. 被引:0
- Viral load-driven systemic immune exhaustion is an enabler of antibody breadth in HIV infection (2026). DOI: [10.64898/2026.06.05.730519](https://doi.org/10.64898/2026.06.05.730519), PMID:42327147. 被引:0
- Excessive reactive oxygen species attenuated IL-17 production in CD161CD8T cell subset via repression of FOS in HIV-infected immunological non-responders (2026). DOI: [10.1186/s12964-026-02792-5](https://doi.org/10.1186/s12964-026-02792-5), PMID:41845347. 被引:0

**(b) 公开数据资源**

- **GEO (Gene Expression Omnibus)**：以 'HIV + scRNA-seq/single cell RNA sequencing + T cell' 检索命中 **128 条**记录（检索日期 2026-07-15）。代表性最新数据集：GSE329693/GSE328611（微生物组代谢物对慢性HIV感染中CD4+T细胞分化的影响, n=36/6）、GSE332711（CD4/CD8比值与疫苗诱导免疫结构重组, n=60）、GSE313059（大麻素对HIV感染CD4 T细胞影响的单细胞多组学, n=16）、GSE324265/324044/321718（CD8 T细胞、中性粒细胞与I型干扰素信号对高炎症反应的贡献, n=125/64/3）。

**(c) 数据丰富度评级：高 (High)**
  依据：GEO 平台上以 'HIV scRNA-seq/single cell RNA sequencing + T cell' 为检索词命中 128 条记录（GSE329693, GSE328611, GSE313059 等均为 2024-2025 年新发布数据集，含 CD4/CD8 T 细胞 scRNA-seq）；OpenAlex/PubMed 联合检索该类目命中相关文献 94 条（长表计数）

**(d) 方法成熟度评级：较成熟 (Moderately mature)**
  依据：Seurat/Scanpy 等通用单细胞分析框架已广泛应用；HIV 特异性场景（潜伏库细胞标记、感染细胞转录特征）已有多篇高被引工作（如 Cell 2013, cited_by=1478 关于潜伏库; Nature 2020 关于精英控制者reservoir, cited_by=421），但专门针对 HIV×T细胞的深度学习/生成模型方法仍较少见于本轮检索范围

---

### 2.2 表观基因组学 / 染色质可及性（ATAC-seq, ChIP-seq, DNA甲基化）

**(a) 描述与代表性文献**

- Replication-Competent Noninduced Proviruses in the Latent Reservoir Increase Barrier to HIV-1 Cure (2013). DOI: [10.1016/j.cell.2013.09.020](https://doi.org/10.1016/j.cell.2013.09.020), PMID:24243014. 被引:1478
- HIV reproducibly establishes a latent infection after acute infection of T cells in vitro (2003). DOI: [10.1093/emboj/cdg188](https://doi.org/10.1093/emboj/cdg188), PMID:12682019. 被引:959
- A quantitative approach for measuring the reservoir of latent HIV-1 proviruses (2019). DOI: [10.1038/s41586-019-0898-8](https://doi.org/10.1038/s41586-019-0898-8). 被引:757
- Stimulation of HIV-1-Specific Cytolytic T Lymphocytes Facilitates Elimination of Latent Viral Reservoir after Virus Reactivation (2012). DOI: [10.1016/j.immuni.2012.01.014](https://doi.org/10.1016/j.immuni.2012.01.014). 被引:707
- Comparative Analysis of Measures of Viral Reservoirs in HIV-1 Eradication Studies (2013). DOI: [10.1371/journal.ppat.1003174](https://doi.org/10.1371/journal.ppat.1003174). 被引:580
- Harnessing the CRISPR/Cas9 system to disrupt latent HIV-1 provirus (2013). DOI: [10.1038/srep02510](https://doi.org/10.1038/srep02510), PMID:23974631. 被引:566
- RNA-directed gene editing specifically eradicates latent and prevents new HIV-1 infection (2014). DOI: [10.1073/pnas.1405186111](https://doi.org/10.1073/pnas.1405186111), PMID:25049410. 被引:536
- Single cell multiomic analysis of the impact of Delta-9-tetrahydrocannabinol on HIV infected CD4 T cells (2026). DOI: [10.1186/s42238-026-00412-0](https://doi.org/10.1186/s42238-026-00412-0), PMID:41782037. 被引:0
- Advancements in single-cell techniques for examining the HIV reservoir: pathways to a cure (2025). DOI: [10.1128/mbio.00655-25](https://doi.org/10.1128/mbio.00655-25), PMID:40488537. 被引:0
- HIV-1 transcription dominates over host gene activity at the HIV-1 integration site (2025). DOI: [10.1128/mbio.02755-25](https://doi.org/10.1128/mbio.02755-25), PMID:41277870. 被引:0
- Single cell multiomic analysis of the impact of Delta-9-tetrahydrocannabinol on HIV infected CD4 T cells (2025). DOI: [10.1101/2025.06.02.657468](https://doi.org/10.1101/2025.06.02.657468), PMID:40502036. 被引:0
- Intracellular HIV-1 Tat regulator induces epigenetic changes in the DNA methylation landscape (2025). DOI: [10.3389/fimmu.2025.1532692](https://doi.org/10.3389/fimmu.2025.1532692), PMID:40103825. 被引:0

**(b) 公开数据资源**

- **GEO**：ATAC-seq/ChIP-seq + HIV + T细胞/CD4 检索命中 **185 条**记录。代表性：GSE318861（ChIP-seq+RNA-seq解析Tat依赖转录, n=52）、GSE306525（病毒/化学暴露下免疫细胞表观基因组动态, n=92）、GSE302221/GSE302199（HIV-1整合位点处转录主导宿主基因活性, ATAC-seq/RNA-seq两个子集, n=120/123）、GSE297327（空间调控CD8+T细胞HLA-E-NKG2A轴驱动HIV持续, n=18）。
- **GEO（甲基化专项）**：命中 **78 条**记录，代表性：GSE291168（HIV-1 m6A表观转录组高分辨率图谱, n=11）、GSE217633（HIV感染与ART起始对全基因组DNA甲基化的影响, n=413，样本量较大）、GSE143942（HIV进展队列表观基因组分析, n=85）。

**(c) 数据丰富度评级：中 (Moderate)**
  依据：GEO 检索 'HIV + ATAC-seq/ChIP-seq + T cell/CD4' 命中185条记录，含 GSE318861（ChIP-seq+RNA-seq）、GSE302221/302199（ATAC-seq整合位点）等；甲基化专项检索命中78条（GSE217633 n=413为较大队列）

**(d) 方法成熟度评级：中等 (Moderate)**
  依据：潜伏库表观遗传调控机制研究历史悠久（如 EMBO J 2003 建立体外潜伏模型, cited_by=959），但整合多组学表观基因组计算建模（如潜伏库表观异质性预测）在本轮检索中数量有限

---

### 2.3 蛋白质组学

**(a) 描述与代表性文献**

- Distinct viral reservoirs in individuals with spontaneous control of HIV-1 (2020). DOI: [10.1038/s41586-020-2651-8](https://doi.org/10.1038/s41586-020-2651-8), PMID:32848246. 被引:421
- The Biology of the HIV-1 Latent Reservoir and Implications for Cure Strategies (2020). DOI: [10.1016/j.chom.2020.03.014](https://doi.org/10.1016/j.chom.2020.03.014). 被引:301
- Phenotypic signatures of immune selection in HIV-1 reservoir cells (2023). DOI: [10.1038/s41586-022-05538-8](https://doi.org/10.1038/s41586-022-05538-8), PMID:36599977. 被引:192
- Current Status of Latency Reversing Agents Facing the Heterogeneity of HIV-1 Cellular and Tissue Reservoirs (2020). DOI: [10.3389/fmicb.2019.03060](https://doi.org/10.3389/fmicb.2019.03060), PMID:32038533. 被引:170
- Anti-apoptotic Protein BIRC5 Maintains Survival of HIV-1-Infected CD4+ T Cells (2018). DOI: [10.1016/j.immuni.2018.04.004](https://doi.org/10.1016/j.immuni.2018.04.004), PMID:29802019. 被引:139
- Antigen-responsive CD4+ T cell clones contribute to the HIV-1 latent reservoir (2020). DOI: [10.1084/jem.20200051](https://doi.org/10.1084/jem.20200051), PMID:32311008. 被引:130
- BCL-2 antagonism sensitizes cytotoxic T cell–resistant HIV reservoirs to elimination ex vivo (2020). DOI: [10.1172/jci132374](https://doi.org/10.1172/jci132374), PMID:32027622. 被引:130
- Sex differences in epigenetic ageing for older people living with HIV (2025). DOI: [10.1016/j.ebiom.2025.105588](https://doi.org/10.1016/j.ebiom.2025.105588), PMID:39923742. 被引:0
- Description of T-Cell and Monocyte Populations in the Circulation of People with HIV Prior to AIDS-NHL Diagnosis (2025). DOI: [10.3390/cells14201608](https://doi.org/10.3390/cells14201608), PMID:41148820. 被引:0
- Disseminated Kaposi sarcoma patients exhibit an expanded population of CD8+CD57+ T cells and an immunosenescence profile (2025). DOI: [10.3389/fimmu.2025.1625386](https://doi.org/10.3389/fimmu.2025.1625386), PMID:41208973. 被引:0
- Impact of hormonal therapy on HIV-1 immune markers in cis women and gender minorities (2024). DOI: [10.1111/hiv.13677](https://doi.org/10.1111/hiv.13677), PMID:38830635. 被引:0
- Distinct immune profiles in children living with HIV based on timing and duration of suppressive antiretroviral treatment (2024). DOI: [10.1016/j.virol.2024.110318](https://doi.org/10.1016/j.virol.2024.110318), PMID:39612623. 被引:0

**(b) 公开数据资源**

- **PRIDE (ProteomeXchange)**：以 'HIV' 关键词检索至少命中 **196 个**项目（100+96，跨两页，可能仍有更多未完全翻页确认）。代表性 accession：PXD077909（HIV-1感染免疫细胞旁分泌信号重编程宫颈癌通路）、PXD077610（微生物组代谢物与CD4+T细胞分化及免疫衰老）、PAD000032（靶向血浆蛋白质组学揭示TNFRSF蛋白在HIV相关病症中的核心作用）、PXD075554（HIV-1 Vif介导的宿主RNA剪接因子SUMO化）、PXD074653（HIV-1异源抗原定量蛋白质组分析）。
- **GEO（蛋白质相关标记检索）**：命中 **9 条**记录，代表性：GSE299125（HIV-1感染免疫细胞旁分泌信号）、GSE306023/306022（HLA-B*57与HLA-E*01限制性CD8 T细胞识别HIV Gag, n=29/9）。

**(c) 数据丰富度评级：中低 (Moderate-low)**
  依据：PRIDE 数据库以关键词 'HIV' 检索命中至少196个蛋白质组学项目（如 PXD077909, PXD077610, PAD000032），但专门聚焦 HIV×T细胞（而非泛HIV蛋白质组）的项目占比需人工进一步甄别

**(d) 方法成熟度评级：早期/发展中 (Emerging)**
  依据：本轮检索到的相关工作以生物学机制发现型研究为主（如 BIRC5 蛋白维持HIV感染CD4 T细胞存活, Immunity 2018, cited_by=139），系统性计算蛋白质组学方法论文较少

---

### 2.4 代谢组学 / 脂质组学

**(a) 描述与代表性文献**

- Cell death by pyroptosis drives CD4 T-cell depletion in HIV-1 infection (2013). DOI: [10.1038/nature12940](https://doi.org/10.1038/nature12940). 被引:1176
- Pathophysiology of CD4+ T-Cell Depletion in HIV-1 and HIV-2 Infections (2017). DOI: [10.3389/fimmu.2017.00580](https://doi.org/10.3389/fimmu.2017.00580). 被引:321
- The Biology of the HIV-1 Latent Reservoir and Implications for Cure Strategies (2020). DOI: [10.1016/j.chom.2020.03.014](https://doi.org/10.1016/j.chom.2020.03.014). 被引:301
- Human Leukocyte Antigen (HLA) and Immune Regulation: How Do Classical and Non-Classical HLA Alleles Modulate Immune Response to Human Immunodeficiency Virus and Hepatitis C Virus Infections? (2017). DOI: [10.3389/fimmu.2017.00832](https://doi.org/10.3389/fimmu.2017.00832). 被引:245
- PD-1 blockade potentiates HIV latency reversal ex vivo in CD4+ T cells from ART-suppressed individuals (2019). DOI: [10.1038/s41467-019-08798-7](https://doi.org/10.1038/s41467-019-08798-7), PMID:30778080. 被引:215
- Cellular Metabolism Is a Major Determinant of HIV-1 Reservoir Seeding in CD4+ T Cells and Offers an Opportunity to Tackle Infection (2018). DOI: [10.1016/j.cmet.2018.11.015](https://doi.org/10.1016/j.cmet.2018.11.015), PMID:30581119. 被引:194
- CD4+ T Cell Depletion in Human Immunodeficiency Virus (HIV) Infection: Role of Apoptosis (2011). DOI: [10.3390/v3050586](https://doi.org/10.3390/v3050586), PMID:21994747. 被引:180
- Metabolic reprogramming of CD4&#x207a; T cells by Zaprinast induces HIV-1 latency reversal ex vivo (2026). DOI: [10.1186/s12977-026-00680-x](https://doi.org/10.1186/s12977-026-00680-x), PMID:42288905. 被引:0
- Lipid and immune dysregulation and risk of metabolic disorders after HCV clearance in HIV/HCV-coinfected participants with cACLD: a retrospective study (2026). DOI: [10.3389/fimmu.2025.1674837](https://doi.org/10.3389/fimmu.2025.1674837), PMID:41601646. 被引:0
- Multi-omics dissection of metabolic dysregulation associated with immune recovery in people living with HIV-1 (2025). DOI: [10.1186/s12967-025-06168-0](https://doi.org/10.1186/s12967-025-06168-0), PMID:39891216. 被引:0
- Metabolic Reprogramming in HIV+ CD4T-Cells: Implications for Immune Dysfunction and Therapeutic Targets inCo-Infection (2025). DOI: [10.3390/metabo15050285](https://doi.org/10.3390/metabo15050285), PMID:40422863. 被引:0
- Retinoic acid enhances HIV-1 reverse transcription and transcription in macrophages via mTOR-modulated mechanisms (2024). DOI: [10.1016/j.celrep.2024.114414](https://doi.org/10.1016/j.celrep.2024.114414), PMID:38943643. 被引:0

**(b) 公开数据资源**

- **Metabolomics Workbench**：以 study_title 含 'HIV' 检索命中 **11 项**研究。全部 accession：ST004931（唾液代谢组学揭示HIV/AIDS相关代谢改变）、ST004746（HIV-感染CD4+T细胞中未靶向代谢物谱与PCS定量）、ST004615（多组学揭示死亡率相关免疫代谢决定因素）、ST004581（母体HIV感染对肠道菌群与代谢组的影响）、ST004210/ST004209/ST004208（男男性行为者HIV-1感染前粪便/口腔/血浆代谢组学谱）、ST002328（HIV+患者口腔黏膜代谢组转录组分析）、ST002133（依非韦伦治疗HIV携带者血清代谢物变化）、ST001750（肠道菌群对HIV及高风险人群代谢疾病的影响）、ST000703（HIV患者短链脂肪酸分析）。规模明显小于转录组学/表观基因组学资源。

**(c) 数据丰富度评级：中低 (Moderate-low)**
  依据：Metabolomics Workbench 以 'HIV' 为study_title检索命中11项研究（ST004931, ST004746, ST004615等，多为2023-2025年新发布），规模远小于转录组/表观组资源

**(d) 方法成熟度评级：早期 (Early-stage)**
  依据：细胞代谢与HIV潜伏库建立/维持的关联已有重要发现（如 Cell Metab 2018, cited_by=194 关于细胞代谢决定reservoir seeding），但系统性代谢组学计算建模工作在本轮检索范围内未见大规模出现

---

### 2.5 免疫组库（TCR/BCR Repertoire）

**(a) 描述与代表性文献**

- HIV-Specific Cd8+ T Cells Produce Antiviral Cytokines but Are Impaired in Cytolytic Function (2000). DOI: [10.1084/jem.192.1.63](https://doi.org/10.1084/jem.192.1.63). 被引:865
- HIV-specific cytotoxic T-cells in HIV-exposed but uninfected Gambian women (1995). DOI: [10.1038/nm0195-59](https://doi.org/10.1038/nm0195-59). 被引:741
- Major expansion of CD8+ T cells with a predominant Vβ usage during the primary immune response to HIV (1994). DOI: [10.1038/370463a0](https://doi.org/10.1038/370463a0). 被引:606
- Broad CTL response is required to clear latent HIV-1 due to dominance of escape mutations (2015). DOI: [10.1038/nature14053](https://doi.org/10.1038/nature14053). 被引:501
- The Neutralization Breadth of HIV-1 Develops Incrementally over Four Years and Is Associated with CD4 <sup>+</sup> T Cell Decline and High Viral Load during Acute Infection (2011). DOI: [10.1128/jvi.00198-11](https://doi.org/10.1128/jvi.00198-11). 被引:472
- Association between Virus-Specific Cytotoxic T-Lymphocyte and Helper Responses in Human Immunodeficiency Virus Type 1 Infection (1999). DOI: [10.1128/jvi.73.8.6715-6720.1999](https://doi.org/10.1128/jvi.73.8.6715-6720.1999). 被引:371
- Suppression of human immunodeficiency virus type 1 replication by CD8+ cells: evidence for HLA class I-restricted triggering of cytolytic and noncytolytic mechanisms (1997). DOI: [10.1128/jvi.71.4.3120-3128.1997](https://doi.org/10.1128/jvi.71.4.3120-3128.1997). 被引:340
- B cell receptor repertoires identified by next-generation sequencing showed signatures associated with incomplete immune reconstitution in people living with HIV (2025). DOI: [10.1016/j.clim.2025.110594](https://doi.org/10.1016/j.clim.2025.110594), PMID:40897246. 被引:0
- HIV infection and ART exposure affect tumor TCR repertoire of diffuse large B cell lymphoma (2024). DOI: [10.1172/jci.insight.180771](https://doi.org/10.1172/jci.insight.180771), PMID:38781015. 被引:0
- RAIN: machine learning-based identification for HIV-1 bNAbs (2024). DOI: [10.1038/s41467-024-49676-1](https://doi.org/10.1038/s41467-024-49676-1), PMID:38914562. 被引:0
- B cell repertoire sequencing of HIV-1 pediatric elite-neutralizers identifies multiple broadly neutralizing antibody clonotypes (2024). DOI: [10.3389/fimmu.2024.1272493](https://doi.org/10.3389/fimmu.2024.1272493), PMID:38433846. 被引:0
- RAIN: a Machine Learning-based identification for HIV-1 bNAbs (2024). DOI: [10.21203/rs.3.rs-4023897/v1](https://doi.org/10.21203/rs.3.rs-4023897/v1), PMID:38903123. 被引:0

**(b) 公开数据资源**

- **GEO（TCR/免疫组库相关，未做HIV特异性过滤）**：检索命中 **702 条**记录（注：该检索词较宽泛，多数记录可能非HIV特异，需人工二次甄别）；HIV特异性代表性：GSE278091（HIV特异性T细胞的克隆替换与分化, n=18）。
- **IEDB (Immune Epitope Database)**：直接通过官方 REST API 核实（查询条件 source_organism_name ilike '*immunodeficiency*'），T细胞相关实验记录 **1365 条**（对应 **462 个不重复表位结构**），B细胞相关实验记录 **1609 条**（查询日期 2026-07-15，API: query-api.iedb.org）。
- **VDJdb**：本轮尝试通过官方 API（vdjdb.cdr3.net）直接核实 HIV 相关 TCR-抗原条目数，但该域名的直接网络请求在本次会话中未能连通（代理层报 403，与已获批准的访问白名单状态不一致，可能是该特定服务临时不可达）——**此项标注为'未核实'**，建议后续人工登陆 vdjdb.cdr3.net 网页界面直接核实条目数。

**(c) 数据丰富度评级：中 (Moderate)**
  依据：GEO 'TCR repertoire' 相关检索命中702条记录（但多数为非HIV特异）；IEDB 数据库中 source_organism 含 'immunodeficiency' 的T细胞表位实验记录1365条（对应462个不重复表位结构），B细胞表位记录1609条；VDJdb 等专用TCR-抗原数据库存在但本轮未能通过API直接核实条目数（网络访问受限）

**(d) 方法成熟度评级：较成熟 (Moderately mature，方法本身in general领域成熟)**
  依据：TCR-表位结合预测的深度学习方法在arXiv发展活跃（如2409.06694, 2509.17305, 2411.17798, 2505.01433, 2310.10893均为2023-2025年发表），但这些方法多为通用TCR-pMHC预测框架，非HIV专门优化；HIV特异性TCR反应历史研究悠久（如 J Exp Med 2000, cited_by=865）

---

### 2.6 病毒学测序 / 前病毒库定量（Reservoir Quantification）

**(a) 描述与代表性文献**

- Replication-Competent Noninduced Proviruses in the Latent Reservoir Increase Barrier to HIV-1 Cure (2013). DOI: [10.1016/j.cell.2013.09.020](https://doi.org/10.1016/j.cell.2013.09.020), PMID:24243014. 被引:1478
- HIV reproducibly establishes a latent infection after acute infection of T cells in vitro (2003). DOI: [10.1093/emboj/cdg188](https://doi.org/10.1093/emboj/cdg188), PMID:12682019. 被引:959
- A quantitative approach for measuring the reservoir of latent HIV-1 proviruses (2019). DOI: [10.1038/s41586-019-0898-8](https://doi.org/10.1038/s41586-019-0898-8). 被引:757
- Rapid seeding of the viral reservoir prior to SIV viraemia in rhesus monkeys (2014). DOI: [10.1038/nature13594](https://doi.org/10.1038/nature13594). 被引:632
- Harnessing the CRISPR/Cas9 system to disrupt latent HIV-1 provirus (2013). DOI: [10.1038/srep02510](https://doi.org/10.1038/srep02510), PMID:23974631. 被引:566
- RNA-directed gene editing specifically eradicates latent and prevents new HIV-1 infection (2014). DOI: [10.1073/pnas.1405186111](https://doi.org/10.1073/pnas.1405186111), PMID:25049410. 被引:536
- Broad CTL response is required to clear latent HIV-1 due to dominance of escape mutations (2015). DOI: [10.1038/nature14053](https://doi.org/10.1038/nature14053). 被引:501
- Considerations and limitations for establishing an Intact Proviral DNA Assay (IPDA) on a chip-based digital PCR system for HIV-1 reservoir quantification (2025). DOI: [10.1016/j.jviromet.2025.115205](https://doi.org/10.1016/j.jviromet.2025.115205), PMID:40553848. 被引:6
- Impact of AGT103-T cell and gene therapy on intact HIV proviral reservoirs (2026). DOI: [10.1097/qad.0000000000004459](https://doi.org/10.1097/qad.0000000000004459), PMID:41670418. 被引:0
- Q4ddPCR: a flexible, 4-target assay for high-resolution HIV reservoir profiling (2026). DOI: [10.1038/s41467-026-69413-0](https://doi.org/10.1038/s41467-026-69413-0), PMID:41720775. 被引:0
- Differential HIV-1 Proviral Defects in Children vs. Adults on Antiretroviral Therapy (2025). DOI: [10.3390/v17070961](https://doi.org/10.3390/v17070961), PMID:40733578. 被引:0
- Integrative Assessment of Total and Intact HIV-1 Reservoir by a 5-Region Multiplexed Rainbow DNA Digital PCR Assay (2025). DOI: [10.1093/clinchem/hvae192](https://doi.org/10.1093/clinchem/hvae192), PMID:39749517. 被引:0

**(b) 公开数据资源**

- **GEO（整合位点专项）**：命中 **23 条**记录。代表性：GSE279615（SETD2和MLL1宿主因子缺失下的HIV-1整合位点, n=8）、GSE302221/GSE302199（同上, ATAC-seq/RNA-seq两个子集）、GSE281027/GSE281026（HIV-1靶向宿主基因组R-loop进行整合, RNA-seq/IS-seq子集, n=5/12）。
- **LANL HIV Sequence Database（Los Alamos National Laboratory）**：长期维护的HIV序列数据库，是本领域病毒基因组学研究的核心公共资源之一；同一机构还维护 CATNAP（中和抗体面板汇编分析工具）。因数据库规模统计页面未被本轮工具直接抓取核实具体条目数，此处仅确认资源存在及其官方地位，**具体条目规模标注为'未核实'**。

**(c) 数据丰富度评级：高 (High)**
  依据：GEO 'integration site' 专项检索命中23条记录（GSE279615, GSE302221/302199, GSE281027/281026）；本领域为HIV治愈研究核心，OpenAlex/PubMed长表命中86条相关文献，含多篇超高被引基础工作（Cell 2013 cited_by=1478; EMBO J 2003 cited_by=959; Nature 2019 cited_by=757）

**(d) 方法成熟度评级：成熟 (Mature)**
  依据：近乎完整前病毒基因组测序（near full-length individual proviral sequencing, FLIPS/related）、整合位点定量分析等方法已形成标准流程，并有CRISPR/Cas9介导潜伏库清除等计算辅助设计工作（Sci Rep 2013 cited_by=566; PNAS 2014 cited_by=536）

---

### 2.7 临床 / 流行病学表格化数据

**(a) 描述与代表性文献**

- Profound phenotypic and epigenetic heterogeneity of the HIV-1-infected CD4+ T cell reservoir (2022). DOI: [10.1038/s41590-022-01371-3](https://doi.org/10.1038/s41590-022-01371-3), PMID:36536105. 被引:101
- Predictions of CD4 lymphocytes’ count in HIV patients from complete blood count (2013). DOI: [10.1186/1756-6649-13-3](https://doi.org/10.1186/1756-6649-13-3), PMID:24034560. 被引:75
- Artificial Intelligence and Machine Learning Based Prediction of Viral Load and CD4 Status of People Living with HIV (PLWH) on Anti-Retroviral Treatment in Gedeo Zone Public Hospitals (2023). DOI: [10.2147/ijgm.s397031](https://doi.org/10.2147/ijgm.s397031), PMID:36760682. 被引:25
- Prediction of CD4+ Cells Counts in HIV/AIDS Patients based on Sets and Probability Theories (2019). DOI: [10.2174/1570162x17666190306125819](https://doi.org/10.2174/1570162x17666190306125819). 被引:8
- Construction of Machine Learning Models to Predict Changes in Immune Function Using Clinical Monitoring Indices in HIV/AIDS Patients After 9.9-Years of Antiretroviral Therapy in Yunnan, China (2022). DOI: [10.3389/fcimb.2022.867737](https://doi.org/10.3389/fcimb.2022.867737), PMID:35646738. 被引:0
- Biomarkers of Progression after HIV Acute/Early Infection: Nothing Compares to CD4&#x207a; T-cell Count? (2018). DOI: [10.3390/v10010034](https://doi.org/10.3390/v10010034), PMID:29342870. 被引:0
- Predicting antiretroviral therapy adherence status of adult HIV-positive patients using machine-learning Northwest, Ethiopia, 2025 (2025). DOI: [10.1186/s12911-025-03106-4](https://doi.org/10.1186/s12911-025-03106-4), PMID:40640758. 被引:0
- Impact of HIV-1 genetic diversity on disease progression: a prospective cohort study in Guangxi (2024). DOI: [10.3389/fcimb.2024.1415123](https://doi.org/10.3389/fcimb.2024.1415123), PMID:38994006. 被引:0
- Pediatric immunotherapy and HIV control (2024). DOI: [10.1097/coh.0000000000000857](https://doi.org/10.1097/coh.0000000000000857), PMID:38841850. 被引:0

**(b) 公开数据资源**

- **ClinicalTrials.gov**（通过官方 REST API v2 直接核实，查询日期 2026-07-15）：'HIV cure reservoir' 相关注册研究 77 项，'HIV therapeutic vaccine' 1123 项，'HIV latency reversal' 14 项，'HIV elite controller' 28 项，'HIV broadly neutralizing antibody' 81 项。**注意**：试验注册记录本身不等同于可下载的个体层面表格化数据集，多数试验的原始数据并不公开。
- **ImmPort**：NIAID维护的免疫学数据公开仓库，托管有超过1000项免疫学研究数据（含部分HIV相关队列），但本轮未能直接通过API核实HIV专项研究的具体数量，**此项标注为'未核实'**，建议后续人工登陆 immport.org 检索确认。

**(c) 数据丰富度评级：中低 (Moderate-low，公开个体层面数据稀缺)**
  依据：ClinicalTrials.gov 检索显示 HIV cure/reservoir相关注册试验77项、therapeutic vaccine 1123项、latency reversal 14项、elite controller 28项，但试验注册本身不等同公开可下载的表格化临床数据集；OpenAlex/PubMed长表命中该类目文献15条

**(d) 方法成熟度评级：早期 (Early-stage，聚焦传统统计+经典ML)**
  依据：已有CD4计数/病毒载量预测的机器学习工作（如 BMC Immunol 2013 cited_by=75 神经网络方法；IJGM 2023 关于AI/ML预测病毒载量与CD4状态），其参考文献回溯显示早在2007-2011年即有SVM/神经网络应用于HIV治疗响应预测（geno2pheno相关工作），但方法总体仍以经典统计/浅层ML为主，深度学习应用有限

---

### 2.8 多组学整合 / 空间组学

**(a) 描述与代表性文献**

- Understanding HIV Latency: The Road to an HIV Cure (2015). DOI: [10.1146/annurev-med-092112-152941](https://doi.org/10.1146/annurev-med-092112-152941), PMID:25587657. 被引:219
- Phenotypic signatures of immune selection in HIV-1 reservoir cells (2023). DOI: [10.1038/s41586-022-05538-8](https://doi.org/10.1038/s41586-022-05538-8), PMID:36599977. 被引:192
- HIV silencing and cell survival signatures in infected T cell reservoirs (2023). DOI: [10.1038/s41586-022-05556-6](https://doi.org/10.1038/s41586-022-05556-6), PMID:36599978. 被引:117
- HIV latency and integration site placement in five cell-based models (2013). DOI: [10.1186/1742-4690-10-90](https://doi.org/10.1186/1742-4690-10-90), PMID:23953889. 被引:116
- Multi-omics analyses reveal that HIV-1 alters CD4+ T cell immunometabolism to fuel virus replication (2021). DOI: [10.1038/s41590-021-00898-1](https://doi.org/10.1038/s41590-021-00898-1), PMID:33767427. 被引:111
- Examining Chronic Inflammation, Immune Metabolism, and T Cell Dysfunction in HIV Infection (2024). DOI: [10.3390/v16020219](https://doi.org/10.3390/v16020219). 被引:89
- The HIV-1 proviral landscape reveals that Nef contributes to HIV-1 persistence in effector memory CD4+ T cells (2022). DOI: [10.1172/jci154422](https://doi.org/10.1172/jci154422). 被引:87
- Local antibody feedback enforces a checkpoint on affinity maturation in the germinal center and promotes epitope spreading (2026). DOI: [10.1016/j.immuni.2026.01.011](https://doi.org/10.1016/j.immuni.2026.01.011), PMID:41690309. 被引:0
- CD8T cells sustain vaccination-induced immunity against dissemination of contained tuberculosis in immunosuppressed hosts (2026). DOI: [10.1038/s41467-026-70911-4](https://doi.org/10.1038/s41467-026-70911-4), PMID:41876499. 被引:0
- BACH2 effector-to-memory switch promotes HIV persistence and CAR-T efficacy (2026). DOI: [10.1097/coh.0000000000001041](https://doi.org/10.1097/coh.0000000000001041), PMID:42130341. 被引:0
- The Characteristics of Peripheral Blood Lymphocyte Subsets in HIV-related Diffuse Large B-cell Lymphoma Patients and Their Impact on Treatment Efficacy (2026). DOI: [10.2174/011570162x369231250818043532](https://doi.org/10.2174/011570162x369231250818043532), PMID:40873272. 被引:0
- Roadmap for spatial transcriptomics of HIV in tissues (2025). DOI: [10.1097/coh.0000000000000961](https://doi.org/10.1097/coh.0000000000000961), PMID:40626838. 被引:0

**(b) 公开数据资源**

- **GEO（CITE-seq/多组学专项）**：命中 **45 条**记录。代表性：GSE307326（持续NRTI类ART诱导的衰老样重编程, n=32）、GSE313059（大麻素对HIV感染CD4 T细胞的单细胞多组学分析, n=16）、GSE297853（cART/SIV/吗啡对脑内髓系细胞影响的单细胞多组学, n=32）、GSE303197（HIV-1潜伏库克隆的动态抗原表达与CTL抗性, n=25）。
- **GEO（空间组学专项）**：命中 **16 条**记录。代表性：GSE274051（HIV相关非霍奇金淋巴瘤的空间转录组学，按EBV状态和细胞来源分层, n=10）、GSE297327（CD8+T细胞HLA-E-NKG2A轴空间调控驱动HIV持续, n=18）。

**(c) 数据丰富度评级：中低 (Moderate-low)**
  依据：GEO CITE-seq/multiome专项检索命中45条记录（GSE307326, GSE313059, GSE297853, GSE303197等，多为2024-2025年新数据）；空间转录组专项检索命中16条（GSE274051针对HIV相关淋巴瘤, GSE297327针对HLA-E-NKG2A轴与HIV持续）

**(d) 方法成熟度评级：早期/快速发展中 (Emerging, rapidly growing)**
  依据：多组学整合方法（如Cell Metabolism 2018关于免疫代谢与reservoir关系, cited_by=194）已有先例，空间技术应用于HIV的工作大多为2023年后新发表，属于该领域最新前沿方向

---

### 2.9 影像学及其他模态

**(a) 描述与代表性文献**

- Autophagy is involved in T cell death after binding of HIV-1 envelope proteins to CXCR4 (2006). DOI: [10.1172/jci26185](https://doi.org/10.1172/jci26185), PMID:16886061. 被引:434
- Microglial Cells: The Main HIV-1 Reservoir in the Brain (2019). DOI: [10.3389/fcimb.2019.00362](https://doi.org/10.3389/fcimb.2019.00362), PMID:31709195. 被引:375
- Quantitative profiling of the full APOBEC3 mRNA repertoire in lymphocytes and tissues: implications for HIV-1 restriction (2010). DOI: [10.1093/nar/gkq174](https://doi.org/10.1093/nar/gkq174), PMID:20308164. 被引:368
- Differences in HIV Burden and Immune Activation within the Gut of HIV‐Positive Patients Receiving Suppressive Antiretroviral Therapy (2010). DOI: [10.1086/656722](https://doi.org/10.1086/656722), PMID:20939732. 被引:292
- Current Status of Latency Reversing Agents Facing the Heterogeneity of HIV-1 Cellular and Tissue Reservoirs (2020). DOI: [10.3389/fmicb.2019.03060](https://doi.org/10.3389/fmicb.2019.03060), PMID:32038533. 被引:170
- HIV infection and latency induce a unique metabolic signature in human macrophages (2019). DOI: [10.1038/s41598-019-39898-5](https://doi.org/10.1038/s41598-019-39898-5), PMID:30850623. 被引:116
- The reservoir of latent HIV (2022). DOI: [10.3389/fcimb.2022.945956](https://doi.org/10.3389/fcimb.2022.945956), PMID:35967854. 被引:95
- Blockade of TGF-β signaling reactivates HIV-1/SIV reservoirs and immune responses in vivo (2022). DOI: [10.1172/jci.insight.162290](https://doi.org/10.1172/jci.insight.162290), PMID:36125890. 被引:26
- The Spatial Biology of HIV Transmission and Infection: Imaging the Female and Male Reproductive Tracts (2026). DOI: [10.1111/aji.70261](https://doi.org/10.1111/aji.70261), PMID:42212707. 被引:0
- Spatial transcriptomic analysis of HIV and tuberculosis coinfection in a humanized mouse model reveals unique transcription patterns, immune responses and early morphological alterations (2025). DOI: [10.1101/2025.01.29.635571](https://doi.org/10.1101/2025.01.29.635571), PMID:39975088. 被引:0
- CCR5-ligand decorated rilpivirine lipid-based nanoparticles for sustained antiretroviral responses (2025). DOI: [10.1038/s41467-024-55544-9](https://doi.org/10.1038/s41467-024-55544-9), PMID:39779664. 被引:0
- CCR5 Decorated Rilpivirine Lipid Nanoparticles Build Myeloid Drug Depots Which Sustains Antiretroviral Activities (2024). DOI: [10.21203/rs.3.rs-4433306/v1](https://doi.org/10.21203/rs.3.rs-4433306/v1), PMID:38883780. 被引:0

**(b) 公开数据资源**

- 本轮检索未发现专门的、大规模的公开 HIV×T细胞影像数据仓库（如公开的显微影像/流式细胞数据集平台）。相关工作多为单篇论文附带的补充材料级别影像数据，未形成如GEO/PRIDE式的集中索引资源。**此项数据资源盘点相对薄弱，建议后续针对性检索 BioImage Archive、Cell Image Library 等专用影像数据库以补充核实。**

**(c) 数据丰富度评级：低-中 (Low-moderate，公开可复用影像数据稀缺)**
  依据：本轮OpenAlex/PubMed检索命中17-22条相关文献（自噬成像、脑内小胶质细胞reservoir定位、APOBEC3表达谱等），未发现专门的公开HIV×T细胞影像数据仓库

**(d) 方法成熟度评级：早期 (Early-stage)**
  依据：多为传统显微成像/流式细胞术为主的机制研究（如 JCI 2006 cited_by=434 关于自噬与T细胞死亡），计算图像分析方法应用有限

---

## Section 3: 按临床/研究主题分类概况

本节按 7 个临床/研究主题对文献进行组织，与 Section 2 的组学模态分类形成正交视角（同一篇文献可能同时归入某个组学类目和某个主题类目，两者的交叉关系见 Section 5）。


### 3.1 病毒库与潜伏机制 (Reservoir & Latency)

- Structure and immune recognition of trimeric pre-fusion HIV-1 Env (2014). DOI: [10.1038/nature13808](https://doi.org/10.1038/nature13808), PMID:25296255. 被引:774
- POPULATION BIOLOGY OF HIV-1 INFECTION: Viral and CD4<sup>+</sup>T Cell Demographics and Dynamics in Lymphatic Tissues (1999). DOI: [10.1146/annurev.immunol.17.1.625](https://doi.org/10.1146/annurev.immunol.17.1.625), PMID:10358770. 被引:547
- HIV Latency (2011). DOI: [10.1101/cshperspect.a007096](https://doi.org/10.1101/cshperspect.a007096), PMID:22229121. 被引:514
- Microglial Cells: The Main HIV-1 Reservoir in the Brain (2019). DOI: [10.3389/fcimb.2019.00362](https://doi.org/10.3389/fcimb.2019.00362), PMID:31709195. 被引:375
- Integrated Single-cell Multiomic Analysis of HIV Latency Reversal Reveals Novel Regulators of Viral Reactivation (2024). DOI: [10.1093/gpbjnl/qzae003](https://doi.org/10.1093/gpbjnl/qzae003), PMID:38902848. 被引:23
- Cognate antigen engagement induces HIV-1 expression in latently infected CD4+ T cells from people on long-term antiretroviral therapy (2024). DOI: [10.1016/j.immuni.2024.11.002](https://doi.org/10.1016/j.immuni.2024.11.002), PMID:39612916. 被引:12
- Clonal heterogeneity and antigenic stimulation shape persistence of the latent reservoir of HIV (2025). DOI: [10.1371/journal.pcbi.1013433](https://doi.org/10.1371/journal.pcbi.1013433), PMID:40953113. 被引:0
- Identification of Inflammation Markers as Novel Potential Predictors of the HIV-DNA Reservoir Size (2025). DOI: [10.3390/ijms26178430](https://doi.org/10.3390/ijms26178430), PMID:40943350. 被引:0

### 3.2 免疫重建 / CD4恢复 (Immune Reconstitution & CD4 Recovery)

- T Cell Activation Is Associated with Lower CD4<sup>+</sup>T Cell Gains in Human Immunodeficiency Virus–Infected Patients with Sustained Viral Suppression during Antiretroviral Therapy (2003). DOI: [10.1086/374786](https://doi.org/10.1086/374786), PMID:12721933. 被引:851
- HIV-Infected Individuals with Low CD4/CD8 Ratio despite Effective Antiretroviral Therapy Exhibit Altered T Cell Subsets, Heightened CD8+ T Cell Activation, and Increased Risk of Non-AIDS Morbidity and Mortality (2014). DOI: [10.1371/journal.ppat.1004078](https://doi.org/10.1371/journal.ppat.1004078), PMID:24831517. 被引:617
- Incomplete Peripheral CD4<sup>+</sup>Cell Count Restoration in HIV‐Infected Patients Receiving Long‐Term Antiretroviral Treatment (2009). DOI: [10.1086/597093](https://doi.org/10.1086/597093), PMID:19193107. 被引:409
- Enhanced CD4+ T-Cell Recovery with Earlier HIV-1 Antiretroviral Therapy (2013). DOI: [10.1056/nejmoa1110187](https://doi.org/10.1056/nejmoa1110187), PMID:23323898. 被引:358
- Immune reconstitution efficacy and associated risk factors for immunological non-response in people living with HIV during long-term antiretroviral therapy: a single-center retrospective cohort study at a tertiary care hospital in China (2026). DOI: [10.3389/fimmu.2026.1776587](https://doi.org/10.3389/fimmu.2026.1776587), PMID:41909684. 被引:0
- Predicting immune reconstitution after antiretroviral therapy in HIV/AIDS using ensemble machine learning: a real-world study (2026). DOI: [10.3389/fimmu.2026.1805202](https://doi.org/10.3389/fimmu.2026.1805202), PMID:42079615. 被引:0
- Single-cell multi-omics profiling uncovers the immune heterogeneity in HIV-infected immunological non-responders (2025). DOI: [10.1016/j.ebiom.2025.105667](https://doi.org/10.1016/j.ebiom.2025.105667), PMID:40184908. 被引:0
- Subset Remodeling of MAIT and NK Cells Correlates With Immune Reconstitution in People Living With HIV Following Four Years of Antiretroviral Therapy (2025). DOI: [10.1002/jmv.70732](https://doi.org/10.1002/jmv.70732), PMID:41317006. 被引:0

### 3.3 自发/治疗后病毒控制（精英控制者 EC、治疗后控制者 PTC）

- Distinct viral reservoirs in individuals with spontaneous control of HIV-1 (2020). DOI: [10.1038/s41586-020-2651-8](https://doi.org/10.1038/s41586-020-2651-8), PMID:32848246. 被引:421
- Microglial Cells: The Main HIV-1 Reservoir in the Brain (2019). DOI: [10.3389/fcimb.2019.00362](https://doi.org/10.3389/fcimb.2019.00362), PMID:31709195. 被引:375
- HIV-1 transcription and latency: an update (2013). DOI: [10.1186/1742-4690-10-67](https://doi.org/10.1186/1742-4690-10-67), PMID:23803414. 被引:326
- Early and nonreversible decrease of CD161++/MAIT cells in HIV infection (2012). DOI: [10.1182/blood-2012-06-436436](https://doi.org/10.1182/blood-2012-06-436436), PMID:23255555. 被引:312
- HIV controllers: hope for a functional cure (2025). DOI: [10.3389/fimmu.2025.1540932](https://doi.org/10.3389/fimmu.2025.1540932), PMID:40070826. 被引:0
- Acute HIV-1 Infection: Paradigm and Singularity (2025). DOI: [10.3390/v17030366](https://doi.org/10.3390/v17030366), PMID:40143294. 被引:0
- HIV Cure: How Far We Have Come? (2024). DOI: [10.1007/s12088-024-01353-z](https://doi.org/10.1007/s12088-024-01353-z), PMID:40655347. 被引:0
- HIV-1 reservoir landscape of post-treatment control (2024). DOI: [10.1097/coh.0000000000000891](https://doi.org/10.1097/coh.0000000000000891), PMID:39484860. 被引:0

### 3.4 疫苗设计与免疫原性 (Vaccine & Immunogenicity)

- Structure and immune recognition of trimeric pre-fusion HIV-1 Env (2014). DOI: [10.1038/nature13808](https://doi.org/10.1038/nature13808), PMID:25296255. 被引:774
- CD8+ T cells in HIV control, cure and prevention (2020). DOI: [10.1038/s41577-020-0274-9](https://doi.org/10.1038/s41577-020-0274-9), PMID:32051540. 被引:309
- The human naive B cell repertoire contains distinct subclasses for a germline-targeting HIV-1 vaccine immunogen (2018). DOI: [10.1126/scitranslmed.aat0381](https://doi.org/10.1126/scitranslmed.aat0381), PMID:29973404. 被引:153
- RAIN: machine learning-based identification for HIV-1 bNAbs (2024). DOI: [10.1038/s41467-024-49676-1](https://doi.org/10.1038/s41467-024-49676-1), PMID:38914562. 被引:0
- Comparing HIV Vaccine Immunogenicity Across Trials With Different Populations and Study Designs (2026). DOI: [10.1002/sim.70495](https://doi.org/10.1002/sim.70495), PMID:41923460. 被引:0
- Multi-Epitope DNA-Based Feline Immunodeficiency Virus Vaccine Construct Designed by Immunoinformatic and Machine Learning Tools as a Surrogate Model for HIV Vaccine Development (2026). DOI: [10.3390/pathogens15030341](https://doi.org/10.3390/pathogens15030341), PMID:41901794. 被引:0
- Profiling of HIV-1 elite neutralizer cohort reveals a CD4bs bnAb for HIV-1 prevention and therapy (2025). DOI: [10.1038/s41590-025-02286-5](https://doi.org/10.1038/s41590-025-02286-5), PMID:41053396. 被引:0
- Isolation and characterization of IgG3 glycan-targeting antibodies with exceptional cross-reactivity for diverse viral families (2024). DOI: [10.1371/journal.ppat.1012499](https://doi.org/10.1371/journal.ppat.1012499), PMID:39292703. 被引:0

### 3.5 耐药性与病毒演化 (Drug Resistance & Viral Evolution)

- The immune response during acute HIV-1 infection: clues for vaccine development (2009). DOI: [10.1038/nri2674](https://doi.org/10.1038/nri2674), PMID:20010788. 被引:847
- Structure and immune recognition of trimeric pre-fusion HIV-1 Env (2014). DOI: [10.1038/nature13808](https://doi.org/10.1038/nature13808), PMID:25296255. 被引:774
- Microglial Cells: The Main HIV-1 Reservoir in the Brain (2019). DOI: [10.3389/fcimb.2019.00362](https://doi.org/10.3389/fcimb.2019.00362), PMID:31709195. 被引:375
- CD8+ T cells in HIV control, cure and prevention (2020). DOI: [10.1038/s41577-020-0274-9](https://doi.org/10.1038/s41577-020-0274-9), PMID:32051540. 被引:309
- A binary trait model reveals the fitness effects of HIV-1 escape from T cell responses (2025). DOI: [10.1073/pnas.2405379122](https://doi.org/10.1073/pnas.2405379122), PMID:39970000. 被引:0
- Quantitative Prediction of Human Immunodeficiency Virus Drug Resistance (2024). DOI: [10.3390/v16071132](https://doi.org/10.3390/v16071132), PMID:39066293. 被引:0
- In-Depth Characterization of Full-Length Archived Viral Genomes after Nine Years of Posttreatment HIV Control (2023). DOI: [10.1128/spectrum.03267-22](https://doi.org/10.1128/spectrum.03267-22), PMID:36692300. 被引:0
- HAMdetector: a Bayesian regression model that integrates information to detect HLA-associated mutations (2022). DOI: [10.1093/bioinformatics/btac134](https://doi.org/10.1093/bioinformatics/btac134), PMID:35238330. 被引:0

### 3.6 T细胞耗竭/功能障碍 (T-cell Exhaustion & Dysfunction)

- Early and nonreversible decrease of CD161++/MAIT cells in HIV infection (2012). DOI: [10.1182/blood-2012-06-436436](https://doi.org/10.1182/blood-2012-06-436436), PMID:23255555. 被引:312
- CD8+ T cells in HIV control, cure and prevention (2020). DOI: [10.1038/s41577-020-0274-9](https://doi.org/10.1038/s41577-020-0274-9), PMID:32051540. 被引:309
- Integrated single-cell analysis of multicellular immune dynamics during hyperacute HIV-1 infection (2020). DOI: [10.1038/s41591-020-0799-2](https://doi.org/10.1038/s41591-020-0799-2), PMID:32251406. 被引:174
- Profound phenotypic and epigenetic heterogeneity of the HIV-1-infected CD4+ T cell reservoir (2022). DOI: [10.1038/s41590-022-01371-3](https://doi.org/10.1038/s41590-022-01371-3), PMID:36536105. 被引:101

### 3.7 系统免疫学建模 (Systems Immunology Modeling)

- The first T cell response to transmitted/founder virus contributes to the control of acute viremia in HIV-1 infection (2009). DOI: [10.1084/jem.20090365](https://doi.org/10.1084/jem.20090365), PMID:19487423. 被引:644
- Fractional modeling dynamics of HIV and CD4+ T-cells during primary infection (2012). DOI: [10.1186/1753-4631-6-1](https://doi.org/10.1186/1753-4631-6-1), PMID:22214194. 被引:162
- Single-cell transcriptome profiling reveals immunological fitness of HIV long-term non-progressors (2025). DOI: [10.1128/jvi.01597-25](https://doi.org/10.1128/jvi.01597-25), PMID:41277843. 被引:0
- Post-treatment control of HIV infection (2015). DOI: [10.1073/pnas.1419162112](https://doi.org/10.1073/pnas.1419162112), PMID:25870266. 被引:0
- Bifurcation and stability analysis of within host HIV dynamics with multiple infections and intracellular delay (2025). DOI: [10.1063/5.0232978](https://doi.org/10.1063/5.0232978), PMID:39792699. 被引:0
- Threshold dynamics of an age-structured HIV model with virus-to-cell, cell-to-cell transmissions, and CTL immune response (2025). DOI: [10.1007/s00285-025-02328-4](https://doi.org/10.1007/s00285-025-02328-4), PMID:41400705. 被引:0
- Immune cell subset profiling and metabolic dysregulation define the divergent immune microenvironments in HIV immunological non-responders (2025). DOI: [10.1002/ctm2.70498](https://doi.org/10.1002/ctm2.70498), PMID:41084320. 被引:0
- Modeling virus-stimulated proliferation of CD4T-cell, cell-to-cell transmission and viral loss in HIV infection dynamics (2024). DOI: [10.1016/j.mbs.2024.109302](https://doi.org/10.1016/j.mbs.2024.109302), PMID:39276975. 被引:0

**补充说明**：

- "病毒库与潜伏机制"（3.1）是本轮检索中文献密度最高、历史最悠久的主题，与 Section 2 中"病毒学测序/前病毒库定量"及"表观基因组学"两个组学类目高度重叠（详见 Section 5 交叉表）。
- "T细胞耗竭/功能障碍"（3.6）在本轮策展中仅保留 4 篇代表性文献（原始检索命中数较少，且许多相关文献来自肿瘤免疫学领域的"耗竭"概念迁移应用，为保持 HIV×T细胞主体性，本报告仅保留明确聚焦 HIV 场景的文献）。
- "疫苗与免疫原性"（3.4）以及"耐药性与病毒演化"（3.5）两个主题在 arXiv 计算文献中均有独立的小规模产出（如 arXiv:1403.4196 关于潜伏库根除治疗结果预测、arXiv:1003.5992 关于HIV感染动力学时滞微分方程模型），详见 Section 4 中 arXiv 预印本清单。

---

## Section 4: 综述 / 方法论 / 基准测评阅读清单

本节汇总两类文献：(1) HIV×T细胞领域内的权威综述文章；(2) 与该领域计算方法相关的通用方法论/基准测评类文献（部分并非HIV专属，但构成本领域计算工作可借鉴的方法基础）。

### 4.1 HIV × T细胞领域综述


- HIV Latency (2011). DOI: [10.1101/cshperspect.a007096](https://doi.org/10.1101/cshperspect.a007096). 被引:514
- T‐cell exhaustion in HIV infection (2019). DOI: [10.1111/imr.12823](https://doi.org/10.1111/imr.12823). 被引:418
- HIV reservoirs as obstacles and opportunities for an HIV cure (2015). DOI: [10.1038/ni.3152](https://doi.org/10.1038/ni.3152). 被引:232
- CD8+ T cells in HIV control, cure and prevention (2020). DOI: [10.1038/s41577-020-0274-9](https://doi.org/10.1038/s41577-020-0274-9). 被引:309
- The causes and consequences of HIV evolution (2004). DOI: [10.1038/nrg1246](https://doi.org/10.1038/nrg1246). 被引:566
- Strategies for HIV-1 vaccines that induce broadly neutralizing antibodies (2022). DOI: [10.1038/s41577-022-00753-w](https://doi.org/10.1038/s41577-022-00753-w). 被引:362
- POPULATION BIOLOGY OF HIV-1 INFECTION: Viral and CD4<sup>+</sup>T Cell Demographics and Dynamics in Lymphatic Tissues (1999). DOI: [10.1146/annurev.immunol.17.1.625](https://doi.org/10.1146/annurev.immunol.17.1.625). 被引:547
- HIV infection (2015). DOI: [10.1038/nrdp.2015.35](https://doi.org/10.1038/nrdp.2015.35). 被引:620

### 4.2 计算方法论 / 单细胞多组学 / 机器学习基准测评（通用方法基础，非HIV专属）


- Eleven grand challenges in single-cell data science (2020). DOI: [10.1186/s13059-020-1926-6](https://doi.org/10.1186/s13059-020-1926-6). 被引:1441
- The technological landscape and applications of single-cell multi-omics (2023). DOI: [10.1038/s41580-023-00615-w](https://doi.org/10.1038/s41580-023-00615-w). 被引:968
- Applications of single-cell RNA sequencing in drug discovery and development (2023). DOI: [10.1038/s41573-023-00688-4](https://doi.org/10.1038/s41573-023-00688-4). 被引:423
- Integrating machine learning and multiscale modeling—perspectives, challenges, and opportunities in the biological, biomedical, and behavioral sciences (2019). DOI: [10.1038/s41746-019-0193-y](https://doi.org/10.1038/s41746-019-0193-y). 被引:632

### 4.3 arXiv 计算/机器学习相关预印本

**检索说明**：直接以 "virtual T cell" 字面检索会被 "virtual memory T cell (TVM)" 这一真实免疫学概念污染，故本轮改用精确短语+领域标签组合检索（如 `abs:"HIV" AND abs:"T cell" AND abs:"machine learning"` 限定 q-bio.QM 分类）。总体来看，**arXiv 上HIV×T细胞计算建模的预印本数量稀少但可通过精确措辞定位**，多集中在群体动力学微分方程建模（较早年份）与近两年新兴的TCR-表位深度学习预测方法（后者多为通用TCR-pMHC预测框架，非HIV专门优化）。

**病毒动力学/潜伏库微分方程建模类**：

- Robustness of a Cellular Automata Model for the HIV Infection (2008). arXiv:[0807.2411](https://arxiv.org/abs/0807.2411)。（细胞自动机模型鲁棒性分析 (HIV感染)）
- Optimal intervention strategies of staged progression HIV infections through an age-structured model with probabilities of ART drop out (2019). arXiv:[1911.06703](https://arxiv.org/abs/1911.06703)。（分阶段进展HIV感染的年龄结构模型与ART脱落概率下的最优干预策略）
- The dynamics of the HIV infection: a time-delay differential equation approach (2010). arXiv:[1003.5992](https://arxiv.org/abs/1003.5992)。（HIV感染动力学的时滞微分方程方法）
- Predicting the outcomes of treatment to eradicate the latent reservoir for HIV-1 (2014). arXiv:[1403.4196](https://arxiv.org/abs/1403.4196)。（预测清除HIV-1潜伏库治疗结果）
- The Effects of Latent Infection on the Dynamics of HIV (2013). arXiv:[1312.3670](https://arxiv.org/abs/1312.3670)。（潜伏感染对HIV动力学的影响）

**TCR-表位结合预测深度学习类（通用方法，非HIV专属，供方法借鉴）**：

- DANCE: Deep Learning-Assisted Analysis of Protein Sequences Using Chaos Enhanced Kaleidoscopic Images (2024). arXiv:[2409.06694](https://arxiv.org/abs/2409.06694)
- Rational Multi-Modal Transformers for TCR-pMHC Prediction (2025). arXiv:[2509.17305](https://arxiv.org/abs/2509.17305)
- DapPep: Domain Adaptive Peptide-agnostic Learning for Universal T-cell Receptor-antigen Binding Affinity Prediction (2024). arXiv:[2411.17798](https://arxiv.org/abs/2411.17798)
- Enhancing TCR-Peptide Interaction Prediction with Pretrained Language Models and Molecular Representations (2025). arXiv:[2505.01433](https://arxiv.org/abs/2505.01433)
- Active Learning Framework for Cost-Effective TCR-Epitope Binding Affinity Prediction (2023). arXiv:[2310.10893](https://arxiv.org/abs/2310.10893)

**免疫组库计算分析综述**：
- Computational strategies for dissecting the high-dimensional complexity of adaptive immune repertoires (2017). arXiv:[1711.11070](https://arxiv.org/abs/1711.11070)

---

## Section 5: 组学模态 × 临床主题 交叉表

下表统计了本轮策展文献集合中，每个"临床主题"类目下的文献同时被标记为某个"组学模态"类目的**数量**（基于检索时的类目标签重叠，而非严格的内容标注复核；数字仅反映检索矩阵设计下的类目共现频次，**非该细分方向绝对文献总量**，仅作为描述性、组织性参考，不构成方法或方向推荐）。


| 主题 \ 模态 | 转录组学 | 表观基因组学 / 染色质可及性 | 蛋白质组学 | 代谢组学 / 脂质组学 | 免疫组库 | 病毒学测序 / 前病毒库定量 | 临床 / 流行病学表格化数据 | 多组学整合 / 空间组学 | 影像学及其他模态 |
|---|---|---|---|---|---|---|---|---|---|
| 病毒库与潜伏机制 | 5 | 6 | 2 | 0 | 0 | 2 | 1 | 3 | 1 |
| 免疫重建 / CD4恢复 | 2 | 1 | 1 | 0 | 0 | 0 | 3 | 0 | 0 |
| 自发/治疗后病毒控制（精英控制者 EC、治疗后控制者 PTC） | 4 | 2 | 1 | 0 | 0 | 3 | 0 | 0 | 1 |
| 疫苗设计与免疫原性 | 1 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 |
| 耐药性与病毒演化 | 1 | 0 | 0 | 0 | 1 | 1 | 0 | 0 | 1 |
| T细胞耗竭/功能障碍 | 3 | 1 | 2 | 0 | 0 | 0 | 1 | 0 | 0 |
| 系统免疫学建模 | 1 | 0 | 0 | 1 | 0 | 0 | 0 | 1 | 0 |

**观察（描述性，非结论性判断）**：

- "病毒库与潜伏机制" × "表观基因组学" 及 × "转录组学" 的交叉计数最高，与 Section 1/Section 2 的定性判断一致——这是本领域数据与方法积累最深厚的交叉格子。
- "疫苗与免疫原性"、"耐药性与演化" 两个主题与"代谢组学/脂质组学"、"影像学"两个模态在本轮策展文献中**未见交叉**（交叉表中对应格子为0）。这**不代表**该交叉方向不存在相关研究——更可能是本轮检索矩阵的查询词组合未能命中，或该交叉方向的文献体量本身很小、需要更细粒度的后续检索来确认。
- "系统免疫学建模"主题与"多组学整合/空间组学"模态出现交叉（计数=1），提示系统建模类工作开始尝试纳入多层数据，但样本量极小，仅作为方向性观察记录。

---

## Section 6: 自我审计（Self-Audit）

### 6.1 DOI / PMID 核实状态

- **核实方法**：全部拟纳入正文（Section 2-4）的 DOI，均通过 CrossRef 官方 REST API（`api.crossref.org/works/{doi}`）逐条直接查询确认可解析，并将返回标题与本地记录标题做字符串相似度比对，排查条目错配。
- **核实结果**：**132/132** 条 curated DOI（Section 2 + Section 3 引用集合）全部通过 CrossRef 解析核实，核实通过率 **100%**。其中 1 条初始比对相似度较低（`10.1016/j.mbs.2024.109302`），经人工检查确认为 CrossRef 返回标题中含 MathML 标记（数学符号渲染差异）导致的字符串相似度算法误判，并非文献错配，已排除。
- 另有 **74 条**来自 PubMed 检索通道的文献，其 PMID 通过 NCBI eutils `esummary` 接口批量核实，**74/74** 全部确认存在（核实通过率 100%）。
- Section 4 的综述/方法论类 DOI（12条）同样全部通过 CrossRef 核实。
- **未直接逐条人工核实"是否被引用文本准确反映论文实际结论"**——本轮核实仅确认"文献真实存在、标题匹配"，不构成对论文内容准确性/文献综述质量的背书；这是文献调研类 agent 工作的固有边界，请后续使用者知悉。

### 6.2 公开数据资源核实状态

| 数据资源 | 核实方式 | 核实状态 |
|---|---|---|
| GEO (Gene Expression Omnibus) | NCBI eutils 直接查询，逐条获取 accession/title/n_samples | 已核实（活查询，非缓存） |
| IEDB (Immune Epitope Database) | query-api.iedb.org 官方 REST API 直接查询 | 已核实（活查询） |
| ClinicalTrials.gov | 官方 REST API v2 直接查询 | 已核实（活查询） |
| PRIDE (ProteomeXchange) | www.ebi.ac.uk/pride 官方 REST API 直接查询 | 已核实（活查询），但总量未完全翻页确认到底 |
| Metabolomics Workbench | 官方 REST API 直接查询 | 已核实（活查询） |
| VDJdb | 尝试通过 vdjdb.cdr3.net 官方 API 核实 | **未核实**——API 请求未能连通（代理层报错），条目规模数字未获得 |
| LANL HIV Sequence Database / CATNAP | 网页检索确认资源存在及官方地位 | **规模数字未核实**——仅确认数据库存在，未获取具体条目计数 |
| ImmPort | 网页检索确认资源存在（NIAID维护，逾1000项免疫学研究） | **HIV专项研究具体数量未核实** |

### 6.3 覆盖面自评估

**检索覆盖广度**：
- OpenAlex 直接 API 检索：9个组学类目（39条查询）+ 7个主题类目（19条查询）+ 6条综述种子查询，合计64条查询，去重后得到 701 篇不重复文献，其中标题级关键词过滤后判定为"HIV×T细胞强相关"的有 146 篇。
- PubMed 检索：覆盖16个细分类目，58条查询，去重后 493 个不重复 PMID，全部成功获取元数据，其中判定为强相关的有 341 篇（PubMed 相关性判定标准较宽，纳入了摘要级别关键词匹配，故绝对数字高于 OpenAlex 标题级过滤结果，两者不可直接横向比较总量）。
- 引用图谱扩展：针对各组学类目被引数最高的锚点文献做前向引用扩展，以及针对部分主题类目关键综述做进一步的引用扩展，共获得 435 条扩展记录，其中 154 篇经相关性判定后新增（部分与前两个通道有重叠）。
- arXiv 检索：通过语义短语+分类标签组合检索，共定位 11 篇强相关计算方法学预印本。
- 三个文献通道去重后的相关文献并集总计 **539 篇不重复 DOI**。

**已知覆盖盲区（本轮检索范围内未见但不代表不存在）**：
- **在本轮检索范围内未见**大规模的、专门针对 HIV×T细胞的**公开影像数据仓库**（Section 2.9）。
- **在本轮检索范围内未见**充分的**空间蛋白质组学**（如 CODEX、MIBI 等技术）应用于 HIV×T细胞场景的文献，多组学空间类工作目前以空间转录组学为主。
- VDJdb 中 HIV 特异性 TCR-抗原条目的具体规模**未核实**，需后续人工确认。
- 本报告的相关性判定主要基于**标题/摘要关键词的规则式匹配**（正则表达式检测"HIV"类词汇 + "T细胞/CD4/CD8/TCR"类词汇同时出现），**并非人工逐篇精读**；虽然对每篇候选文献的标题均做了人工可读的展示，但受限于调研规模，未能对全部539篇候选文献的摘要或全文进行逐篇精读复核，这与需求中"精读阅读"的理想标准存在差距，是本报告在时间/资源约束下的现实简化，**特此明确标注，供后续人工复核参考**。
- arXiv 检索显示 HIV×T细胞计算建模的预印本产出规模明显小于 PubMed/OpenAlex 索引的期刊文献，这与该领域整体上仍以湿实验/生物学期刊发表为主的现状相符，但不能排除存在未被本轮查询词覆盖的预印本。

### 6.4 未核实项清单（Unverified Items）

以下条目在本报告正文中已标注为"未核实"，此处汇总列出，避免遗漏：

1. VDJdb 数据库中 HIV 特异性 TCR-抗原条目的具体数量。
2. LANL HIV Sequence Database 及 CATNAP 的具体序列/数据条目规模。
3. ImmPort 平台中 HIV 专项研究的具体数量。
4. PRIDE 数据库中 HIV 相关蛋白质组学项目的完整总数（本轮仅确认至少196个，翻页未完全穷尽）。
5. 全部539篇候选相关文献中，除本报告正文列出的约150余篇策展文献外，其余文献未经逐篇摘要/全文精读复核，仅完成了标题级相关性规则匹配与DOI存在性核实。

---

*本文档由计算免疫学 + AI4Science 领域文献调研 agent 生成，检索与核实工作于 2026年7月15日完成。如需复核任何具体数字或文献列表，请参照文中列出的 DOI/PMID/accession 直接查询原始来源。*
