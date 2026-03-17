# 各章节写作简报与示范

> 最后更新：2026-03-17（从参考文献 Chen et al., 2025, npj Digital Medicine 更新）
> 用途：阶段4b逐节撰写前的简报内容，提供底层逻辑与优秀标准

---

## 目录
- [Abstract（摘要）](#abstract摘要)
- [1. Introduction（引言）](#1-introduction引言)
- [2. Methodology（方法论）](#2-methodology方法论)
- [3.1 Publication Trends（发表趋势）](#31-publication-trends发表趋势)
- [3.2 Productive Sources（高产来源）](#32-productive-sources高产来源)
- [3.3 Citation Analysis（引用结构）](#33-citation-analysis引用结构)
- [3.4 Co-word & Thematic Analysis（共词与主题）](#34-co-word--thematic-analysis共词与主题)
- [4. Discussion（讨论）](#4-discussion讨论)
- [5. Conclusion（结论）](#5-conclusion结论)

---

## Abstract（摘要）

### 底层逻辑
摘要是编辑和审稿人对文章的第一印象，也是数据库检索时读者决定是否阅读全文的唯一依据。它必须在约200词内完整传达：做了什么、怎么做的、发现了什么、有什么意义。文献计量综述摘要的特殊性在于，它要明确说明数据来源和分析规模，让读者即使不看方法节也能评估研究的覆盖范围。

### 优秀标准
- ✓ 结构化（Background / Purpose / Methods / Results / Conclusions），Q1期刊普遍要求
- ✓ 精确报告数据规模（如"X篇文献，来自Y个数据库，时间跨度Z年"）
- ✓ Results部分列出2–4个最核心发现，用具体数字而非泛泛描述
- ✓ 最后一句说明研究贡献或实践意义，不是重复上文
- ✓ 字数控制在150–300词，关键词4–8个

### 常见失分点
- ✗ Results 仅说"进行了多项分析"而不说发现了什么
- ✗ 缺少具体数字（文献数量、时间范围、主要指标）
- ✗ 摘要与正文结论不一致
- ✗ 关键词与标题单词完全重复（损失检索覆盖）

### 衔接逻辑
摘要独立成节，需与 Introduction 的 RQ 和 Conclusion 的贡献声明完全对应。

### 示范段落

**Background & Purpose:**
> "The global transition toward renewable energy has generated substantial academic interest over the past two decades. However, a quantitative mapping of this research landscape — including its intellectual structure, thematic evolution, and collaborative networks — remains lacking. This study addresses this gap by conducting a systematic bibliometric analysis of the renewable energy literature."

**Methods:**
> "A total of 4,832 documents published between 2000 and 2023 were retrieved from the Web of Science Core Collection. Bibliometric analyses, including publication trend analysis, co-citation network analysis, keyword co-occurrence mapping, and thematic evolution analysis, were performed using VOSviewer (v1.6.20) and Bibliometrix (v4.1.3) in R."

**Results:**
> "Findings reveal a threefold increase in annual publications since 2015, driven primarily by Chinese and European institutions. Co-citation analysis identified five foundational knowledge clusters, while keyword analysis revealed a shift in research focus from 'solar energy efficiency' toward 'energy storage systems' and 'hydrogen production' after 2018."

---

## 1. Introduction（引言）

### 底层逻辑
引言的核心任务是回答三个问题：（1）这个领域为什么重要？（2）现有综述留下了什么缺口？（3）本研究如何填补这个缺口？文献计量综述引言的特殊难点在于：你需要论证"为什么用文献计量方法（而不是叙述性综述）来研究这个问题是合适的"。这是审稿人常常追问的点。

### 优秀标准
- ✓ 开篇以数据或现象引入，而不是"近年来，X领域受到广泛关注"这类空洞表述
- ✓ 研究缺口（Gap）论证具体：列出已有同类综述，说明它们的局限（时间/范围/方法/视角）
- ✓ 明确说明使用文献计量方法的理由（大样本、客观性、量化趋势等）
- ✓ RQ清晰列出（通常2–4个），逻辑上从宏观到微观递进
- ✓ 最后一段概述文章结构（"The remainder of this paper is organized as follows..."）
- ✓ 字数通常800–1200词

### 常见失分点
- ✗ Gap 论证不充分（仅说"尚无综述"而未引证）
- ✗ RQ 与后续 Results 节不对应
- ✗ 未说明文献计量方法相对于传统综述的优势
- ✗ 引言过长（超过1500词），喧宾夺主

### 衔接逻辑
↑ 无（第一节）
↓ 引出 Methodology：引言末段可以"To address these RQs, we employed a systematic bibliometric approach..."过渡

### 研究缺口论证示范

> "Several bibliometric studies have examined adjacent topics, including renewable energy policy (Smith et al., 2021; n=1,200 documents) and solar photovoltaic technology (Liu et al., 2022; n=892 documents). However, these studies are limited in three respects: (1) they focused on specific sub-technologies rather than the broader renewable energy transition; (2) the most recent analysis was conducted in 2021, missing the post-pandemic recovery period; and (3) none employed thematic evolution analysis to track shifting research priorities. The present study addresses these limitations by..."

### RQ 列举示范（A类）

> "This study is guided by the following research questions:
> RQ1: What are the temporal and geographic patterns of renewable energy research output from 2000 to 2023?
> RQ2: What is the intellectual structure of this field, as revealed by co-citation and bibliographic coupling analyses?
> RQ3: What are the emerging and declining research themes, as identified through keyword co-occurrence and thematic evolution analysis?"

---

## 2. Methodology（方法论）

### 底层逻辑
方法节是可复现性的核心保证。它必须让任何读者能够根据文中描述，重现你的检索过程并得到基本相同的结果集。审稿人（尤其是 Scientometrics 和 JoI 的审稿人）会逐字检查方法节，寻找模糊或不可复现之处。文献计量方法节有标准四段式结构：数据库选择 → 检索策略 → 纳入排除标准 → PRISMA流程。

### 优秀标准
- ✓ 给出**完整布尔检索式**（不能只说"使用关键词X和Y"）
- ✓ 精确到**检索执行日期**（"The search was conducted on [date]"）
- ✓ PRISMA 流程图（或流程描述）精确报告各阶段数量
- ✓ 分析工具版本号（VOSviewer 1.6.20, Bibliometrix 4.1.3, R 4.3.0）
- ✓ 网络图参数（最小阈值、归一化方法、聚类算法）逐一说明
- ✓ B类额外：编码方案开发过程、编码员培训说明、κ值报告

### 常见失分点
- ✗ 只提数据库名，不给检索式
- ✗ 未报告检索日期
- ✗ PRISMA 各阶段数字对不上（初检总数≠各库之和）
- ✗ 未说明去重方法
- ✗ 网络分析参数缺失（"used VOSviewer for visualization"一句带过）

### 衔接逻辑
↑ 承接 Introduction（RQ对应所选分析类型）
↓ 引出 Results（"Based on the methodology described above, the following section presents the results..."）

### 检索策略描述示范

> "The search was conducted on November 15, 2023, using the following Boolean query applied to the Title, Abstract, and Keywords fields:
> TS=("renewable energy" OR "solar energy" OR "wind energy" OR "hydropower") AND TS=("bibliometric*" OR "scientometric*" OR "systematic review")
> The search was restricted to Articles and Reviews published in English between 2000 and 2023. A total of 5,214 records were initially retrieved, of which 382 duplicates were removed using the R `deduplication` function in Bibliometrix, yielding 4,832 unique records for analysis."

### 分析工具声明示范

> "Co-occurrence analysis of author keywords was performed using VOSviewer (version 1.6.20; van Eck & Waltman, 2010). Keywords appearing fewer than three times were excluded, resulting in a network of 187 keywords from an initial 2,341 unique terms. The Association Strength normalization method was applied, and clusters were identified using the Leiden algorithm (resolution = 1.0). Bibliometric analyses, including thematic mapping and historical citation network analysis, were conducted using the Bibliometrix package (version 4.1.3) in R (version 4.3.0; R Core Team, 2023)."

### 可复现性声明示范（高分必备，Nature 系列期刊尤其重视）

可复现性声明（Reproducibility Statement）写在 Methods 节末尾，通常一句话，表明其他研究者可用相同方法重现结果：

> "Researchers with access to the Web of Science Core Collection and Scopus databases can replicate this analysis using the search terms and screening strategy provided in the Supplementary Materials."

**为什么重要**：审稿人需要确认你的数据不是"黑箱"。提供完整检索式（Supplementary Table）+ 工具版本 + 可复现声明，是 Nature Portfolio、Elsevier 旗下 Q1 期刊对文献计量研究的隐性要求。

### B类双流方法节结构模板

当文章同时包含标准文献计量（流一）和综合内容分析（流二）时，方法节建议按以下逻辑组织：

```
2.1 数据库选择与检索策略
    ├── 数据库选择理由（为什么选 WoS + Scopus 而非单一数据库）
    ├── 完整布尔检索式（Supplementary 附录）
    └── 检索执行日期

2.2 纳入排除标准与双编码筛查
    ├── 纳入标准（建议精确到"必须同时涉及X/Y/Z三个主题"，交集而非并集）
    ├── 排除标准（逐条列出，通常5条）
    ├── 双编码员流程（两名独立编码员 + 第三方裁决不一致项）
    └── PRISMA 流程（精确报告各阶段排除数量及原因）

2.3 流一：标准文献计量分析
    ├── Performance Analysis（发表趋势/高产来源）
    ├── Co-authorship Analysis（合著网络）
    └── Co-occurrence Analysis（共词网络，说明节点阈值和聚类参数）

2.4 流二：综合文本分析
    ├── 主题分类框架来源（基于已有文献构建编码表，列于 Supplementary Table）
    ├── 编码程序（两名编码员独立编码 + 不一致项第三方裁决）
    └── 趋势分析（时序追踪，建议以2–5年为粒度）
```

---

## Results 节写作纪律：描述与解释的边界

> **来源**：Chen et al. (2025) 的分析提供了一个清晰范本——Results 节维持严格的描述性姿态，所有因果解释均推迟到 Discussion 节进行。

这是文献计量综述中最容易犯错的地方：**在 Results 里过早解释**，导致 Discussion 无话可说，也让 Results 读起来像个人观点而非客观报告。

### Results 节标准句式（正确示范）

| 场景 | 错误写法（含解释） | 正确写法（纯描述） |
|------|-----------------|-----------------|
| 报告某主题占比高 | "Privacy emerged as a major concern because retinal imaging is highly sensitive biometric data." | "Privacy and data security was identified in 14.5% of publications, with a notable increase observed after 2021." |
| 报告国家排名 | "The US leads due to its substantial NIH funding." | "Publications from the United States (n=X) ranked first, followed by China (n=Y) and the UK (n=Z)." |
| 报告趋势转变 | "This shift reflects growing societal concerns about AI governance." | "From 2020 to 2022, the focus shifted from 'traditional ethics concepts (respect, benefit)' toward 'AI-specific concerns (privacy, security, trust)', as evidenced by the overlay visualization." |

### 合法的"比较性陈述"（可写入 Results）

比较性陈述是陈述事实，不是因果解释，可以保留在 Results 中：
- ✓ "Ophthalmology ranked second among 16 medical sub-disciplines, exceeding oncology in annual publications by 2022."
- ✓ "The exponential growth model (Y=20.06e^0.4039x) yielded an excellent fit (R²=0.97)."

---

## 3.1 Publication Trends（发表趋势）

### 底层逻辑
这是 Results 部分的"全局地图"，为读者建立对研究规模和时间脉络的基本认知。其功能不是单纯堆砌数字，而是通过趋势描述揭示领域的发展节律——哪些年份是拐点，为什么？审稿人在这节主要评估：样本量是否充分、时间跨度是否合理、数字描述是否精确。

### 优秀标准
- ✓ 不只说"增加了"，要说增加了多少（CAGR 或具体倍数）
- ✓ 识别并解释增长拐点（结合领域重大事件、政策变化、技术突破）
- ✓ 图文互补：文字不重复图中已有数据，而是提炼趋势解读
- ✓ 将本研究样本量与同类综述横向比较（体现充分性）
- ✓ 参考字数：300–500词

### 常见失分点
- ✗ "2015年发表了X篇，2016年发表了Y篇……"逐年罗列，无分析
- ✗ 图表和文字重复（图已展示数据，文字又列一遍）
- ✗ 未解释拐点，仅描述"快速增长"

### 衔接逻辑
↑ 承接 Methodology（数据来源与时间范围已在此说明）
↓ 引出 3.2（"Having established the overall research output, we next examine which journals, authors, and countries have contributed most to this growth."）

### 拐点解释示范

> "Publication output showed a marked acceleration after 2015, coinciding with the adoption of the Paris Agreement and increased national renewable energy targets. The compound annual growth rate (CAGR) between 2015 and 2023 was 18.3%, compared to 6.7% in the preceding decade (2005–2014), suggesting that international climate policy served as a significant catalyst for research activity in this domain."

---

## 3.2 Productive Sources（高产来源）

### 底层逻辑
这一节回答"谁在做这个研究"，从期刊、作者、国家/机构三个维度建立对领域研究力量格局的认识。它与 3.1 形成互补：3.1 说明"研究有多活跃"，3.2 说明"活跃在哪里"。

### 优秀标准
- ✓ 三个维度（期刊、作者、国家）均有呈现，通常每个维度一段
- ✓ 高产作者分析需结合其研究方向，不只是排名
- ✓ 国家分析需区分产出量和影响力（发文量 vs. 被引量/篇均被引）
- ✓ 合著网络分析需解读集群的实质意义（哪些机构/国家在合作）
- ✓ 参考字数：600–900词

### 常见失分点
- ✗ 只列 Top 10 表格，无任何文字解读
- ✗ 国家分析仅谈发文量，忽略影响力差异（发展中国家发文多但引用少的讨论）
- ✗ 合著网络仅描述"形成了X个聚类"，不说聚类代表什么

### 衔接逻辑
↑ 承接 3.1（研究规模建立后，深入识别核心贡献者）
↓ 引出 3.3（"Beyond identifying productive sources, we next examine the citation structure to uncover the intellectual foundations of the field."）

---

## 3.3 Citation Analysis（引用结构）

### 底层逻辑
引用分析揭示的是"这个领域站在谁的肩膀上"——知识的根基在哪里，哪些理论框架被反复引用，哪些研究形成了知识流派。共被引分析（Co-citation）展示知识基础，书目耦合（Bibliographic Coupling）展示研究前沿，两者结合形成对领域知识结构的完整刻画。

### 优秀标准
- ✓ 说明每个共被引聚类的实质内容（不只是"聚类1包含X篇文献"）
- ✓ 为每个聚类命名（基于其主要文献的研究主题）
- ✓ 解读最高被引文献的地位（为什么这篇文章被引用最多，它代表什么）
- ✓ 区分共被引（过去的知识基础）和书目耦合（当前研究前沿）的不同功能
- ✓ 参考字数：600–1000词

### 常见失分点
- ✗ 仅列出被引次数，不解释文献内容或其对领域的贡献
- ✗ 混淆共被引和书目耦合的含义（需在方法节明确区分）
- ✗ 网络图中节点过多（>200个），可读性差

### 聚类解读示范

> "Co-citation analysis identified four distinct knowledge clusters (Figure 3). Cluster 1 (red, 47 nodes), centered on seminal works by Sovacool (2009) and REN21 (2019), represents the **policy and governance** knowledge base, focusing on renewable energy transition frameworks and international climate policy. Cluster 2 (green, 38 nodes), anchored by Jacobson & Delucchi (2011) and Lund & Mathiesen (2009), constitutes the **100% renewable energy systems** stream, debating the technical feasibility of complete decarbonization. Clusters 3 and 4 capture the **economic modeling** and **social acceptance** knowledge bases, respectively."

---

## 3.4 Co-word & Thematic Analysis（共词与主题）

### 底层逻辑
如果引用分析回答"这个领域研究了什么（从引用的文献看）"，那么共词分析回答"这个领域研究了什么（从作者自己的关键词看）"。两者视角不同，相互印证。战略坐标图（Strategic Diagram）是文献计量综述的标志性图表，它不只是描述"哪些主题热"，而是评估各主题的成熟度和战略重要性。

### 优秀标准
- ✓ 关键词网络图必须解读聚类实质，给每个聚类命名
- ✓ 战略坐标图需解释四个象限的含义，并结合具体主题讨论
  - Motor themes（高中心度+高密度）= 核心且成熟，领域主流
  - Niche themes（低中心度+高密度）= 专业化但孤立，细分方向
  - Basic themes（高中心度+低密度）= 基础性但不成熟，跨领域融合
  - Emerging themes（低中心度+低密度）= 新兴边缘，潜在未来方向
- ✓ 主题演化图（Thematic Evolution）需解释主题的"继承"与"分化"
- ✓ 参考字数：700–1000词

### 常见失分点
- ✗ 战略坐标图只有图没有解读
- ✗ 将"低中心度+低密度"（Emerging）一律标注为"有潜力"，缺乏辨别
- ✗ 关键词网络图中包含过多低频词，稀释核心信息

### 战略坐标图解读示范

> "The strategic diagram (Figure 5) maps research themes across four quadrants. The motor themes quadrant is dominated by **energy storage**, **grid integration**, and **photovoltaic efficiency** — topics that are both central to the field and internally cohesive, indicating mature and well-connected research streams. In the niche themes quadrant, **offshore wind turbine design** and **tidal energy systems** represent highly developed but relatively self-contained specializations, suggesting these are important sub-fields with limited cross-fertilization with the broader literature. Emerging themes include **green hydrogen production** and **vehicle-to-grid technology**, reflecting nascent but growing research directions that may become motor themes in subsequent periods."

---

## 4. Discussion（讨论）

### 底层逻辑
Discussion 是文章最能体现研究者学术判断力的部分。它的任务不是重复 Results，而是做三件事：（1）解释发现背后的原因；（2）将本研究发现与已有文献对话；（3）说明这些发现对理论和实践意味着什么。文献计量综述的 Discussion 有一个特殊难点：如何从"图谱上的聚类"跳跃到"对领域发展有意义的洞察"——这需要研究者对领域的实质性理解。

### 三层叙事结构（优秀 Discussion 的骨架）

每个核心发现的讨论应按此三层展开：
1. **本研究发现**：简述关键结论（一句话，不重复Results）
2. **已有文献对话**：与相关文献比较（"这与 X 等人的发现一致/不一致，原因可能是..."）
3. **理论/实践意义**：这个发现意味着什么（"This suggests that..."）

### 优秀标准
- ✓ 每段讨论一个核心主题，不杂糅多个发现
- ✓ 每段均有文献引用支撑（不是"我认为"，而是"这与X的研究一致"）
- ✓ "Theoretical Contributions"和"Practical Implications"各自成段或成子节
- ✓ "Limitations"诚实列出（至少3–4条），不回避
- ✓ 局限性描述精确（"本研究仅检索了英文文献，可能遗漏了中文/西班牙语等发表的相关研究"）
- ✓ 参考字数：1000–1500词

### 常见失分点
- ✗ 用 Discussion 重复 Results（每句都是"我们发现了X，Y，Z"）
- ✗ 局限性过于宽泛（"本研究可能存在一定局限"）
- ✗ 无文献引用支撑，变成个人观点陈述
- ✗ Practical Implications 仅一句"对政策制定者有参考价值"

### 衔接逻辑
↑ 承接 Results（"The preceding results section identified key structural and thematic patterns. This section interprets these findings in light of existing scholarship."）
↓ 引出 Conclusion（"Building on these discussions, the following section summarizes the contributions of this study and outlines a research agenda."）

### Limitations 示范

> "This study has several limitations that should be acknowledged. First, the analysis was restricted to documents indexed in the Web of Science Core Collection and Scopus, potentially excluding relevant publications in other databases, gray literature, and non-English sources — introducing a language and database coverage bias. Second, as a snapshot analysis with a search cutoff of November 2023, it does not capture publications from late 2023 onward. Third, the bibliometric approach analyzes metadata rather than full-text content, meaning that the thematic conclusions reflect keyword patterns rather than in-depth conceptual analysis; future research combining bibliometric and systematic content analysis could provide richer insights (B类综述可删除此条)."

---

## 5. Conclusion（结论）

### 底层逻辑
结论是文章的最后印象。它需要在300–500词内完成三件事：（1）直接回答引言中提出的每一个 RQ；（2）简洁概括最重要的贡献；（3）为未来研究指明具体方向。结论的"坏"版本是把 Abstract 或 Discussion 复制一遍；"好"版本是让读者读完结论后感到"这篇文章值得"。

### 优秀标准
- ✓ 第一段按 RQ 顺序逐一回答，每个 RQ 1–2句
- ✓ 明确声明理论贡献（"This study contributes to the literature by..."）
- ✓ 明确声明实践贡献（对谁有用，具体在哪方面）
- ✓ Future Research 部分提出3–5个具体的研究问题，而不是笼统的"未来可以做更多研究"
- ✓ 字数：300–500词

### 常见失分点
- ✗ 仅重复 Abstract 或 Discussion 内容
- ✗ 未逐一回应 RQ
- ✗ Future Directions 过于笼统（"Future studies should explore more topics"）
- ✗ 结尾句过于夸张（"This study will revolutionize our understanding of..."）

### 衔接逻辑
↑ 承接 Discussion（贡献声明基于 Discussion 中的分析）
↓ 无（最后一节）

### Future Research Directions 示范

> "Based on the findings of this study, we propose the following directions for future research:
> (1) **Longitudinal impact studies**: Future research should investigate whether the emerging themes identified in this analysis — particularly green hydrogen and vehicle-to-grid technology — consolidate into mainstream research streams over the next five years.
> (2) **Cross-database comparative analysis**: Given the coverage limitations of WoS and Scopus, future studies should incorporate databases such as Dimensions or OpenAlex to capture a broader range of publications, particularly from emerging research economies.
> (3) **Mixed-method integration**: The citation network structures identified here could be further enriched through systematic content analysis of the foundational documents in each cluster, revealing the conceptual mechanisms linking the identified knowledge bases."
