# Cyber-Repair-Manual — Q&A 准备 / Q&A Preparation

中英对照，按主题分类，回答尽量简洁。标 ⚠️ 的是"尖锐问题"——如果被问到，坦诚承认比硬撑更安全。

Bilingual, grouped by topic, answers kept short. Questions marked ⚠️ are "hard questions" — if asked, an honest answer is safer than overselling.

---

## A. 检索机制 / Retrieval Mechanics

**Q1. 系统是怎么检索到答案的？**
**How does the system retrieve an answer?**
> 把用户query和语料库里每条故障的12-15个口语化释义做匹配，用BM25（关键词重合）和另一路语义信号分别打分，再用RRF把两个排名融合成最终排名。
> It matches the query against 12–15 colloquial paraphrases per fault using BM25 (lexical overlap) and a second semantic signal, then fuses both rankings with Reciprocal Rank Fusion (RRF).

**Q2. 为什么同时用BM25和语义模型，只用一个不行吗？**
**Why combine BM25 with a semantic model instead of using just one?**
> BM25单独用会漏掉同义表达；语义模型单独用会丢失精确关键词的可靠性。两者互补。
> BM25 alone misses synonymous phrasing; a semantic-only model loses the reliability of exact keyword matches. They're complementary.

**Q3. RRF具体怎么算？**
**How exactly is RRF computed?**
> 每个候选文档在两路排名里各取 1/(k+名次)，相加即为RRF分数，k=60是平滑常数，降低名次微小差异带来的分数剧烈波动。
> For each candidate, sum 1/(k+rank) across both rankings; k=60 smooths out large score swings from small rank differences.

**Q4. 为什么不用更先进的向量数据库/dense retrieval？**
**Why not use a vector database or more advanced dense retrieval?**
> 项目要求可解释、无需训练的统计方法为主；BM25/TF-IDF是完全透明的加权公式，符合"每个分数都能手算复现"的目标。
> The project prioritizes interpretable, training-free methods; BM25/TF-IDF are fully transparent formulas, matching our goal that every score is manually reproducible.

**Q5. 用户输错字怎么办？**
**What if the user makes a typo?**
> 目前主要靠语料库里丰富的口语化释义覆盖常见说法，对真正拼写错误容错有限，报告里列为未来工作（加入字符n-gram）。
> Robustness mainly comes from broad paraphrase coverage; real misspellings have limited tolerance today — character n-grams are listed as future work.

**Q6. Cascade（级联）检索是什么，为什么最后没选它？**
**What is cascade retrieval, and why wasn't it chosen?**
> 先用BM25筛出Top-K候选再重排序，若BM25第一步漏掉正确答案就无法挽回。我们测K=10/20/50结果一样，说明当前语料规模下瓶颈已不存在，所以全量RRF更完整、没有额外代价。
> BM25 pre-filters Top-K candidates before reranking; unrecoverable if BM25 misses the answer at step one. Testing K=10/20/50 gave identical results, so the bottleneck no longer applies — full RRF fusion is equally cheap and more complete.

---

## B. "生成" 与模板渲染 / Generation vs. Templating

**Q7. 系统是怎么"生成"维修步骤的？**
**How does the system "generate" repair steps?**
> 其实没有生成——维修步骤、工具、安全提示全是人工预写在语料库里的字段，系统只是把检索到的记录填进固定Markdown模板，一个字都不是现场编的。
> It doesn't generate anything — steps, tools, and safety notes are pre-written corpus fields. The system fills a fixed Markdown template with the retrieved entry; nothing is produced on the fly.

**Q8. "生成式AI"在项目里到底用在哪？**
**Where, if anywhere, is generative AI actually used?**
> 除了实验对照组里的Sentence-Transformer（只打相似度分数，不生成文本）外，整条链路没有生成式组件——没有生成，就没有编造的空间。
> Aside from Sentence-Transformer in the experimental configuration (scores similarity, doesn't produce text), there's no generative component anywhere — no generation, no room to fabricate.

**Q9. 语料库没覆盖到的故障，系统会瞎编答案吗？**
**If a fault isn't covered in the corpus, will the system make something up?**
> 不会。所有候选分数都低于阈值时，DecisionGate直接判定low_confidence，只列出最接近的候选供参考，绝不编造新答案。
> No. If all candidates score below threshold, DecisionGate returns low_confidence and only lists the closest existing candidates — it never invents a new answer.

---

## C. 决策与安全 / Decision Logic & Safety

**Q10. confident / need_clarify / low_confidence 是怎么判断的？**
**How are the three decision states determined?**
> 看两点：第一名分数是否≥60%门槛，以及第一、二名分差是否≥1.5%安全边际。两者都满足才confident；分够但差距不够就反问；分数不够直接拒绝。
> Two checks: does the top score clear a 60% floor, and does the gap to #2 clear a 1.5-point margin. Both pass → confident; good score but small gap → clarify; low score → refuse.

**Q11. 这两个阈值(60%、1.5%)怎么定出来的？**
**How were the 60% and 1.5% thresholds chosen?**
> 在236条测试集上反复调参得出的，目标是尽量减少误判前提下覆盖合理比例的查询（报告Table 2：不设门槛答对212/错24；设门槛后答对125/错约1）。
> Tuned empirically on the 236-query test set to minimize false positives while still answering a reasonable share (Table 2: ungated ~212 correct/24 wrong; gated ~125 correct/~1 wrong).

**Q12. 为什么"宁可少答也不要答错"？**
**Why prioritize "fewer answers" over "more coverage"?**
> 因为一次错误的DIY指导可能导致触电或火灾，误判代价远高于"没有答案"，所以设计哲学是precision over recall。
> Because a wrong DIY instruction risks shock or fire; a false positive costs far more than "no answer" — our philosophy is precision over recall.

**Q13. 安全熔断机制具体怎么实现的？**
**How is the safety circuit breaker actually implemented?**
> 渲染时检查severity字段，若为"Requires Professional Service"，渲染器架构上就不打印solution_steps和tools，只输出诊断和安全警告——是代码里的硬分支，不是提示词。
> At render time, the code checks the severity field; if "Requires Professional Service," the renderer architecturally skips printing steps/tools, showing only diagnosis and warnings — a hard code branch, not a soft prompt.

**Q14. 完全无关的query（比如问汽车）会怎样？**
**What happens with a completely unrelated query (e.g. about a car)?**
> 解析器识别不出11类家电中任何一类时，系统在检索前就直接拒绝，不会在全库里瞎撞出一个不相关的"自信"答案。
> If the parser can't match any of the 11 device categories, the system refuses before searching at all, instead of stumbling onto an unrelated "confident" match.

---

## D. 语料库与数据 / Corpus & Data

**Q15. 语料库是爬虫爬来的吗？**
**Was the corpus scraped from the web?**
> 不是，全部人工编写：11类家电、86种故障，每种配12-15条口语化说法，全部团队手写，保证内容和安全提示可控。
> No — entirely hand-written: 11 categories, 86 fault types, 12–15 paraphrases each, all authored by the team for controllable accuracy.

**Q16. 为什么写12-15个同义句，而不训练模型去"理解"？**
**Why write 12–15 paraphrases instead of training a model to "understand" meaning?**
> 这是核心设计决策：把用户可能的说法预先写进语料库，让统计方法靠词汇重合直接命中——把语义匹配问题转化成词汇覆盖问题，用人工写作代替模型训练。
> This is the core design choice: pre-write likely phrasings so a purely statistical method finds matches via lexical overlap — turning semantic matching into a vocabulary-coverage problem, writing instead of training.

**Q17. 语料库质量怎么保证，会不会有错？** ⚠️
**How is corpus quality guaranteed — could it contain mistakes?**
> 目前是团队内部编写和检查，没有专业维修人员审核，这是潜在准确性风险，也是报告里提到的改进方向。
> Currently written and checked internally only, without professional-technician review — a real accuracy risk we acknowledge as future work.

**Q18. 训练集/测试集怎么划分的？**
**How is the corpus split into training/test data?**
> 86条语料本身既是索引库；测试集是单独写的236条自然语言query，各标注gold_entry_id和真实设备，用来算P@1/P@3/MRR，两者语句不重叠。
> The 86-entry corpus is the indexed knowledge base; a separate 236-query test set (each labeled with gold_entry_id and true device) is used for P@1/P@3/MRR — no overlap between the two.

---

## E. 评估方法与结果 / Evaluation & Results

**Q19. 最后准确率是多少，怎么算的？**
**What's the final accuracy, and how is it computed?**
> RRF Fusion在236条测试query上P@1=93.64%，MRR=0.9626，即93.64%的查询里系统给出的第一候选就是标注正确答案。
> RRF Fusion reaches P@1 = 93.64%, MRR = 0.9626 on 236 test queries — the top candidate matched the labeled answer 93.64% of the time.

**Q20. Round 1到Round 2的"反转"是什么意思？**
**What does the Round 1 → Round 2 "reversal" mean?**
> 第一轮语料小（每故障1种表达）时RRF表现最差(64%)；扩充到12-15条释义后，同样算法RRF从垫底变第一(93.64%)——说明瓶颈在语料覆盖度，不在算法。
> With a small corpus (1 phrasing/fault), RRF performed worst (64%); after expanding to 12–15 paraphrases, the same algorithm went from worst to best (93.64%) — proving the bottleneck was corpus coverage, not the algorithm.

**Q21. 哪些设备/故障表现最差，为什么？**
**Which devices/faults perform worst, and why?**
> Coffee Machine(72.2%)和Kettle(68.4%)最弱，因为同设备不同故障共享太多相同词汇("water"、"leak"、"noise")，导致向量太相似难区分。
> Coffee Machine (72.2%) and Kettle (68.4%) are weakest — different faults on the same device share too much vocabulary ("water," "leak," "noise"), making their vectors too similar to distinguish.

**Q22. 评估时是不是"作弊"了，比如直接告诉系统设备类型？** ⚠️
**Does the evaluation "cheat" by telling the system the device type directly?**
> 是的，需要坦诚说明：evaluate.py算P@1/MRR时，直接用测试集自带的真实设备标签做过滤，没有经过真实的SymptomParser识别。报告里的准确率反映的是检索算法本身的上限，不完全等于端到端产品体验（含解析错误）的准确率。
> Honestly, yes: evaluate.py passes the test set's ground-truth device label directly to the retriever, bypassing live SymptomParser detection. The reported accuracy reflects the retrieval algorithm's ceiling, not full end-to-end accuracy including parsing mistakes.

---

## F. 系统架构与工程 / Architecture & Engineering

**Q23. 技术栈是什么？**
**What's the tech stack?**
> Python后端(rank_bm25、scikit-learn、sentence-transformers、jieba分词)，Streamlit做本地网页界面，全程本地运行不依赖云服务。
> Python backend (rank_bm25, scikit-learn, sentence-transformers, jieba), Streamlit for the local web UI, everything runs locally with no cloud dependency.

**Q24. 为什么选Streamlit而不是Flask/Django？**
**Why Streamlit instead of Flask/Django?**
> Streamlit能用很少代码快速搭出可交互网页界面，适合课程项目demo，不需要单独写前后端API。
> Streamlit builds an interactive UI with minimal code, fitting a course project's demo needs without a separate frontend/backend API.

**Q25. 设备识别是怎么做的，为什么不用NER模型？**
**How is device recognition done — why not a trained NER model?**
> 要识别的实体是封闭有限集合(11种设备、约30个症状词)，用jieba配合自定义词典做字典匹配就够了，且完全可追溯、可解释。
> The entities form a small closed set (11 devices, ~30 symptom terms); dictionary matching via jieba is sufficient and keeps detection fully traceable.

---

## G. 局限性与未来工作 / Limitations & Future Work

**Q26. 双语支持真的做到了吗？** ⚠️
**Is bilingual support actually implemented?**
> 目前设备词典和症状词典只收录英文关键词，中文输入无法被正确识别成设备类别，这是未来工作，不是这次demo展示的能力。
> Currently the dictionaries only contain English keywords; Chinese input can't be mapped to a device category yet. It's future work, not a demoed capability.

**Q27. 系统能推广到其他领域吗？**
**Can this generalize to other domains?**
> 理论上可以，核心方法(BM25+TF-IDF+RRF+DecisionGate)是领域无关的，换领域只需重写语料库和词典，不用改检索算法。
> In principle yes — the core method is domain-agnostic; porting to a new domain only needs a new corpus and dictionaries, not algorithm changes.

**Q28. 未来最想优先解决什么？**
**What's the top priority for future work?**
> 扩大每个设备的故障覆盖种类(6-10种→15-20种)，因为错误分析显示大部分剩余错误是语料没覆盖到，而不是算法排错。
> Expanding fault coverage per device (6–10 → 15–20 types), since error analysis shows most remaining mistakes come from missing corpus coverage, not ranking errors.

---

## H. 尖锐质疑类问题 / Hard Challenge Questions

**Q29. 报告说生产默认用纯统计方法，但代码里rrf_fusion默认用了Sentence-Transformer，矛盾吗？** ⚠️
**The report claims a pure-statistical production default, but the code's rrf_fusion default uses Sentence-Transformer — isn't that a contradiction?**
> 确实需要坦诚承认：rrf_fusion是app.py当前的默认配置，用了ST作为一路排序信号，因为它综合准确率最高(93.64%)。我们也评估并保留了完全无神经网络的BM25-only/TF-IDF-only配置(约89%)作为合规备选方案；报告应更明确说明这是权衡，而非两者互斥。
> Fair to admit directly: rrf_fusion is the current default and does use ST, chosen because it scored highest overall (93.64%). We also evaluated and kept fully neural-network-free BM25-only/TF-IDF-only configs (~89%) as compliant alternatives — the report should state this trade-off more explicitly.

**Q30. 为什么不干脆用ChatGPT/大模型API，效果不是更好？**
**Why not just use ChatGPT/an LLM API — wouldn't it perform better?**
> 效果好不等于安全可信；大模型会产生无法追溯来源的幻觉，在可能涉及触电/火灾的场景里这个风险不可接受。我们用可解释、可追溯、离线的检索方法，换取100%可验证的输出。
> Fluent isn't the same as trustworthy; an LLM can hallucinate ungrounded content, an unacceptable risk where wrong advice risks shock or fire. We trade some general capability for fully verifiable, offline, interpretable output.

**Q31. 这个系统跟RAG(检索增强生成)有什么区别？**
**How is this different from RAG (retrieval-augmented generation)?**
> RAG最后还是靠语言模型重新组织语言输出答案，仍有生成幻觉风险；我们是"检索+模板填充"，检索到答案后直接摘录原文拼进模板，完全没有生成步骤，从架构上杜绝幻觉。
> RAG still has a generation step that can hallucinate. We do "retrieval + template filling" — the retrieved text is copied directly into a template with no generation step, ruling out hallucination architecturally, not just mitigating it.
