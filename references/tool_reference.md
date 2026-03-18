# 分析工具参数速查

> 最后更新：2026-03-18（v0.10.0 从 analysis_guide.md 拆分独立：工具对比+参数速查+分析策略集中管理）
> 用途：阶段3分析方案中的工具选择与参数设置、阶段4b图表操作指引、方法节撰写中的参数报告

---

## 目录
- [主流工具对比速查](#主流工具对比速查)
- [VOSviewer 常用参数设置](#vosviewer-常用参数设置)
- [Bibliometrix 常用函数速查](#bibliometrix-常用函数速查)
- [CiteSpace 常用参数设置](#citespace-常用参数设置)
- [聚类质量指标：Modularity Q + Silhouette S](#聚类质量指标modularity-q--silhouette-s)
- [多期时序共词分析：非等分时间窗口策略](#多期时序共词分析非等分时间窗口策略)
- [双规格鲁棒性三角验证策略](#双规格鲁棒性三角验证策略)
- [Cohen's κ 判断标准](#cohens-κ-判断标准)

---

## 主流工具对比速查

> 来源：综合多篇参考文献（Chen 2025, Thakur 2024, Trojanowski 2025, 肖永慧 2025）

| 工具 | 开发机构 | 运行环境 | 核心优势 | 独有功能 |
|------|---------|---------|---------|---------|
| **VOSviewer** | CWTS, 莱顿大学 | Windows/Mac（免费） | 直观网络可视化，适合共被引/共现/合著网络 | Overlay Visualization（时间叠加着色） |
| **Bibliometrix / Biblioshiny** | 那不勒斯大学 | R + Rstudio（开源）；Biblioshiny 为无代码 GUI | 全流程一站式分析；RPYS、主题演化、战略坐标图 | RPYS 光谱分析；thematicEvolution |
| **CiteSpace** | Drexel 大学 Chaomei Chen | Java（免费，需安装 JRE） | 知识演化与研究前沿检测；擅长时序动态分析 | **突变词检测（Burst Detection）**；**时间线图谱（Timezone View）**；Modularity Q/S 聚类质量报告 |

> **选择建议**：
> - 初学者 / 快速可视化 → **VOSviewer**（上手最快）
> - 完整方法论 / 可复现报告 → **Bibliometrix / Biblioshiny**（功能最全）
> - 时序演化 / 中文学者 / CNKI 数据 → **CiteSpace**（对 CNKI 格式支持好，突变词和时间线是独有优势）
> - **可以组合使用**：用 VOSviewer 做共现网络可视化 + Bibliometrix 做主题图 + CiteSpace 做突变词分析，三者并不互斥

---

## VOSviewer 常用参数设置

| 分析类型 | 最小阈值建议 | 归一化方法 | 聚类算法 |
|---------|------------|---------|---------|
| 关键词共现 | 最小共现次数：3–5（视样本量调整） | Association Strength | Leiden |
| 共被引（文献） | 最小共被引次数：5–10 | Association Strength | Leiden |
| 共被引（作者） | 最小共被引次数：3–5 | Association Strength | Leiden |
| 合著（作者） | 最小发文量：2–5 | Association Strength | Leiden |
| 合著（国家） | 最小发文量：1–3 | Association Strength | Leiden |
| 书目耦合（文献） | 最小共享参考文献数：5 | Association Strength | Leiden |

---

## Bibliometrix 常用函数速查

> **工具选择提示**：
> - 会写 R 代码 → 使用 **Bibliometrix R 包**（灵活性最高，可重现）
> - 不会写代码 → 使用 **Biblioshiny**（Bibliometrix 的网页 GUI 版，在 R 中运行 `biblioshiny()` 即可打开，无需编写代码，支持95%以上的分析功能）
>
> 两者底层算法完全相同，产出结果一致。Biblioshiny 适合快速探索和非编程用户；R 代码更适合需要精确参数控制和可重现报告的正式分析（Trojanowski & Barmentloo 2025 全程使用 Biblioshiny）。

| 功能 | R 函数 | Biblioshiny 路径 | 主要参数 |
|------|--------|----------------|---------|
| 读取数据 | `convert2df()` | 首页→上传文件 | `format="wos"` 或 `"scopus"` |
| 描述性分析 | `biblioAnalysis()` + `summary()` | Overview→Main Results | — |
| 年产出图 | `plot(M, "production")` | Overview→Annual Production | — |
| 主题图 | `thematicMap()` | Clustering→Thematic Map | `field="DE"`, `n=250`, `minfreq=5` |
| 主题演化 | `thematicEvolution()` | Clustering→Thematic Evolution | `years=c(2000,2010,2023)` |
| 国家合作地图 | `countryCollaboration()` + `worldMap()` | Networks→Collaboration→Country | — |
| 历史引用网络 | `histNetwork()` + `histPlot()` | Networks→Historical Direct Citation | `min.citations=3` |
| 作者合著网络 | `biblioNetwork(analysis="collaboration")` | Networks→Collaboration→Authors | `network="authors"` |
| RPYS 光谱分析 | `rpys()` | Extra→Reference Publication Year Spectroscopy | `sep=";"` |

---

## CiteSpace 常用参数设置

> **运行环境**：Java 11+（推荐 JRE 11 或 OpenJDK 17）；需在 [CiteSpace 官网](https://citespace.podia.com/) 注册免费账号后下载。
> **数据导入**：支持 WoS（Plain Text）、Scopus（CSV）、CNKI（Refworks）、PubMed 等格式（Data → Import/Export）

**Step 1 — Time Slicing（时间切片）**

| 参数 | 说明 | 建议值 |
|------|------|--------|
| Time Span | 分析的起止年份 | 与检索时间窗口一致 |
| Years Per Slice | 每个时间切片的年数 | 1年（精细）或 2–3年（样本量小时合并） |

**Step 2 — Node Types（节点类型选择）**

| 节点类型 | 对应分析 | 用途 |
|---------|---------|------|
| Keyword | 关键词共现 | 主题结构、突变词检测、Timezone View |
| Reference | 共被引分析 | 知识基础聚类 |
| Author | 作者合著 | 合作网络 |
| Institution | 机构合著 | 机构合作格局 |
| Cited Author | 被引作者共被引 | 核心学者影响力 |

> 每次分析建议只选择**一种**节点类型，避免网络过于复杂。

**Step 3 — Selection Criteria（节点筛选标准）**

| 方法 | 含义 | 建议值 |
|------|------|--------|
| Top N | 每个时间切片中选取频次最高的前 N 个节点 | 30–50（样本量 <500）；50–100（样本量 >500） |
| Top N% | 每个切片选取频次排名前 N% 的节点 | 10%–20% |
| g-index (k) | 每个切片按 g-index 筛选（k 值越大，纳入节点越多） | k=25（默认，适用大多数场景） |
| Threshold | 按绝对频次阈值筛选 | 视分析类型调整（关键词共现 ≥3；共被引 ≥5） |

**Step 4 — Pruning（网络修剪）**

| 算法 | 用途 | 适用场景 |
|------|------|---------|
| Pathfinder | 保留最重要的连接路径，消除冗余边 | **推荐默认使用**——网络更清晰，聚类更稳定 |
| Minimum Spanning Tree (MST) | 保留最小生成树 | 网络极度密集时使用 |
| None | 不修剪 | 仅在需要查看完整连接密度时使用 |

**Step 5 — Visualization（可视化模式）**

| 模式 | 功能 | 适用场景 |
|------|------|---------|
| Cluster View | 按聚类着色，节点大小=频次 | 展示网络聚类结构（最常用） |
| **Timezone View** | 纵轴=聚类，横轴=时间轴 | 展示主题历时演化（CiteSpace 独有） |
| Timeline View | 与 Timezone 类似，但横轴为连续时间线 | 细粒度时间演化 |

**CiteSpace 方法节报告模板**：

> "Co-occurrence analysis of author keywords was performed using CiteSpace (version 6.3.R1; Chen, 2006). The time span was set to [YYYY]–[YYYY] with 1-year slices. Nodes were selected using the g-index method (k=25) with Pathfinder network pruning. Burst detection was performed using Kleinberg's algorithm (γ=1.0, minimum duration=2 years) to identify rapidly emerging keywords. The resulting network comprised N nodes and M links, with a modularity Q of 0.XX and a mean silhouette score of 0.XX, indicating [significant/reliable] cluster structure."

---

## 聚类质量指标：Modularity Q + Silhouette S

> 来源：肖永慧 & 张庆龙 (2025)；仅适用于 CiteSpace 输出的聚类结果

在 CiteSpace 运行关键词共现或共被引聚类后，系统自动输出两个聚类质量指标。报告这两个指标是 CiteSpace 研究的规范要求：

| 指标 | 全称 | 计算含义 | 判断标准 |
|------|------|---------|---------|
| **Modularity Q** | 模块度 | 衡量网络划分为聚类的结构显著性（聚类内连接密度 vs 聚类间连接密度的比值） | Q > 0.3：聚类结构显著，网络划分有效 |
| **Silhouette S** | 轮廓系数 | 衡量聚类内部同质性（每个节点距自身聚类重心 vs 距最近外部聚类重心的比值） | S > 0.5：聚类可信；S > 0.7：聚类高度显著 |

**在方法节报告规范**：

> "The keyword co-occurrence network was clustered using CiteSpace's built-in algorithm. The clustering solution yielded a modularity Q value of 0.XX (> 0.3, indicating significant network structure) and a mean silhouette score of 0.XX (> 0.5, indicating reliable cluster quality), confirming the validity of the identified thematic groupings."

> **注意**：VOSviewer 使用 Leiden/Modularity 算法但不直接输出 Q 和 S 值；Bibliometrix 也不提供同等格式的 Q/S 报告。以上两个指标是 **CiteSpace 特有**的输出格式，使用其他工具时无需（也无法）报告这两个值，可改为报告网络密度（Network density）或聚类数量。

---

## 多期时序共词分析：非等分时间窗口策略

> 来源：Thakur & Kushwaha (2024)

传统时序分析将研究时间段均等划分（如 2000–2010, 2011–2020），但对发展不均匀的领域，**非等分时间窗口**更能捕捉领域演化的真实拐点。

**建议策略**：

| 领域发展阶段 | 推荐时间窗口设计 |
|------------|---------------|
| 萌芽期（文献稀少，年均发文<10篇） | 合并为一个较长窗口（如 2000–2014，14年） |
| 快速增长期（发文量出现拐点） | 设为独立中间窗口（如 2015–2019，5年） |
| 成熟/近期期 | 设为最新窗口（如 2020–2024，5年） |

**实践步骤**：
1. 先绘制年度发文量折线图（§3.1），识别发文量的**拐点年份**
2. 以拐点年份为界划分时间段（通常 2–3 段）
3. 在每段内独立运行共词分析或主题演化分析
4. 对比各段聚类结构的变化，在 Discussion 解释主题演化的驱动力

**Bibliometrix 实现代码**：

```r
# 划分时间段（以发文量拐点为依据）
M1 <- M[M$PY <= 2014, ]                     # 萌芽期
M2 <- M[M$PY >= 2015 & M$PY <= 2019, ]    # 快速增长期
M3 <- M[M$PY >= 2020, ]                    # 近期

# 方法一：分段独立运行主题图
map1 <- thematicMap(M1, field="DE", n=250, minfreq=3)
map2 <- thematicMap(M2, field="DE", n=250, minfreq=5)
map3 <- thematicMap(M3, field="DE", n=250, minfreq=5)

# 方法二：主题演化（直接传入时间节点）
thematicEvolution(M, years=c(2014, 2019, 2024), field="DE")
```

> **方法节说明规范**：需明确写出时间窗口的划分依据（如"基于年度发文量折线图识别的拐点，本研究将研究时段划分为萌芽期（XXXX–XXXX）、增长期（XXXX–XXXX）和近期（XXXX–XXXX）三个阶段"），避免被审稿人质疑为主观划分或事后调整。

---

## 双规格鲁棒性三角验证策略

> 来源：Trojanowski & Barmentloo (2025)

**核心思想**：同一种网络分析（如书目耦合聚类）运行两次，每次仅改变**一个参数维度**，对比结果是否一致。若主要结论稳定 → 结果是规格无关的（可信）；若结论随规格变化 → 需在 Discussion 解释差异来源（比如"GCS 放大了被高度引用的全球热点论文，而 LCS 更聚焦领域内部的知识流动"）。

**推荐的双规格配置（参考 Trojanowski & Barmentloo 2025）**：

| 参数维度 | 主规格（Analysis 1） | 比较规格（Analysis 2） | 目的 |
|---------|---------------------|----------------------|------|
| **影响力度量** | 本地引用分 LCS（语料库内被引次数） | 全局引用分 GCS（数据库总被引次数） | 检验聚类结构是否依赖引用来源 |
| **标签来源** | 数据库索引词（Index Keywords / ID 字段） | 作者自选关键词（Authors' Keywords / DE 字段） | 检验主题命名是否依赖术语来源 |
| **耦合方式**（可选） | 文献级书目耦合 | 关键词共现 | 检验聚类层级一致性 |

**操作步骤**：
1. 确定主规格配置（如 LCS + Index Keywords），完整运行并记录聚类结构（聚类数、主题标签、中心度排名）
2. 仅改变一个参数（如 LCS → GCS，其他不变），再次运行
3. 对比两套结果：聚类数是否稳定？核心主题排名是否一致？少数聚类的命名是否有明显差异？
4. 在方法节声明："To verify the robustness of our findings, we replicated the analysis using [Alternative Spec]. The cluster structure remained stable across both specifications (see Appendix), confirming the reliability of the reported thematic patterns."
5. 将两套结果的对比表格放入 Appendix，Discussion 中用一段话解释任何实质性差异

> **什么时候必须做**：若期刊为 Scientometrics / JoI / IJIM 等高要求 Q1，或审稿意见中出现"robustness check"字样时，建议加做双规格验证。

---

## Cohen's κ 判断标准

| κ 值范围 | 一致性水平 | 发表建议 |
|---------|----------|---------|
| < 0.20 | 微弱 | 不可接受，需重新培训编码员 |
| 0.21–0.40 | 一般 | 勉强，需说明原因 |
| 0.41–0.60 | 中等 | 可接受（最低标准） |
| 0.61–0.80 | 良好 | 符合发表要求 |
| 0.81–1.00 | 极佳 | 优秀 |

> B类综述的 κ 建议达到 ≥ 0.61，并在 Methodology 中明确报告。
