# 文献计量分析图表指南

> 最后更新：2026-03-18（从参考文献 Trojanowski & Barmentloo, 2025, EMPS 更新：新增 RPYS 图表条目、Citations/Year 年化归一化、双规格鲁棒性三角验证策略、Biblioshiny 无代码工具路径）
> 用途：阶段3分析方案规划、阶段4b逐节图表菜单

---

## 研究设计框架：单流 vs 双流文献计量

在规划分析方案前，先确定文章的方法论框架是**单流（Standard）**还是**双流（Hybrid）**：

| 框架 | 适用场景 | 分析流 |
|------|---------|-------|
| **单流（A类标准）** | 纯文献计量，不进行内容编码 | 一条流：量化文献特征 |
| **双流混合（B类进阶）** | 在标准计量基础上叠加主题内容分析 | 流一：标准文献计量（发表趋势/高产来源/引用结构/共词）<br>流二：综合文本分析（编码主题频次/模态分析/策略分类/时序演化）|

> **双流设计建议**（参考 Chen et al., 2025）：
> - 流一（Common Bibliometric Analysis）：Performance Analysis → Co-authorship Analysis → Co-occurrence Analysis
> - 流二（Comprehensive Analysis）：Frequencies Analysis → Trend Analysis（对全文人工编码的主题/类别进行频次统计和时序追踪）
> - 论文结构中建议用方法论流程图（Fig.1）可视化两条流的分工，帮助读者理解研究设计逻辑

---

## 档位说明

| 档位 | 标识 | 目标用户 | 工具门槛 | 产出时间 |
|------|------|---------|---------|---------|
| 基础 | 🟢 | 会用 Excel/WPS | 低 | <30分钟/图 |
| 进阶 | 🟡 | 会用 R / VOSviewer / Bibliometrix | 中 | 1–3小时/图 |
| 高阶 | 🔴 | 熟悉 R/Python 编程 | 高 | 3小时+/图 |

---

## 目录
- [3.1 发表趋势](#31-发表趋势-publication-trends)
- [3.2 高产来源分析](#32-高产来源分析-productive-sources)
- [3.3 引用结构分析](#33-引用结构分析-citation-analysis)
- [3.4 共词与主题分析](#34-共词与主题分析-co-word-analysis)
- [B类专属：内容分析结果](#b类专属内容分析结果)
- [分析参数速查](#分析参数速查)

---

## 3.1 发表趋势（Publication Trends）

| 档位 | 图表名称 | 类型 | 所需数据 | 功能定位 | 推荐工具 | 备注 |
|------|---------|------|---------|---------|---------|------|
| 🟢 | Annual Publication Volume | 柱状图或折线图 | 年份列 + 文章计数 | 展示领域整体增长态势，建立研究规模基准 | Excel / WPS | 最基础图，通常为 Fig.1 |
| 🟢 | Summary Statistics Table | 描述性统计表 | 总文献数、时间跨度、国家数、期刊数、作者数 | 快速呈现数据集规模，辅助样本充分性判断 | Word 表格 | 常作为 Table 1 |
| 🟡 | Annual Publications and Citations Over Time | 双轴折线图 | 年份 + 发文量（左轴）+ 被引量（右轴） | 同时呈现产出规模与知识影响力的时序变化 | R `ggplot2` / Bibliometrix `annualProduction` | 注意标注两轴单位 |
| 🟡 | Document Types Distribution | 饼图/环形图 | 文档类型（Article/Review/...）+ 占比 | 展示文献质量结构 | R `ggplot2` / Excel | 纳入标准验证用 |
| 🟡 | Disciplinary Positioning Comparison | 柱状图+折线叠加，多学科并排 | 本领域在 N 个学科中的发文量/被引量排名 | 论证本领域在上位学科中的地位（"名列第X"），为研究选题提供宏观战略依据 | Excel（多系列柱状图）/ R `ggplot2` | 适合学科交叉选题；数据来自跨学科检索；Chen et al. 2025 中用此图确认眼科在医学AI伦理中排第二位 |
| 🟡 | Exponential Growth Curve Fit | 散点+指数拟合曲线 | 年份 + 发文量 + 拟合公式（如 Y=a·e^(bx)）+ R² | 量化领域发展阶段：婴儿期→指数增长期→成熟期（Price 曲线框架）；提供 R² 值证明拟合优度 | GraphPad Prism / R `nls()` + `ggplot2` | 需在文中报告完整公式和 R²（如"Y=20.06e^0.4039x, R²=0.97"）；建议同时报告 CAGR 以便读者比较 |
| 🔴 | Publication Growth Rate with Trend Projection | 折线图+预测置信区间 | 年份 + 发文量 + CAGR 计算 | 预判领域所处发展阶段（成长期/成熟期/衰退期） | R `forecast` 或 Python `statsmodels` | 需说明预测模型 |
| 🔴 | Bradford's Law Visualization | 散点+拟合曲线 | 核心期刊 + 累计文章数 | 验证布拉德福定律，识别核心区/散射区期刊 | R `bibliometrix` `bradford` | 可选，增强方法论厚度 |

---

## 3.2 高产来源分析（Productive Sources）

### 3.2.1 期刊分析

| 档位 | 图表名称 | 类型 | 所需数据 | 功能定位 | 推荐工具 |
|------|---------|------|---------|---------|---------|
| 🟢 | Top 10 Most Productive Journals | 横向柱状图 | 期刊名 + 发文量（降序） | 识别领域核心发表期刊 | Excel |
| 🟡 | Source Growth Over Time (Top 5 Journals) | 多折线图 | 年份 + 各期刊年发文量 | 追踪主要期刊对领域的贡献演变 | R `ggplot2` |
| 🔴 | Bradford Zone Classification Table | 表格+散点图 | 期刊 + 累计发文量 + 区域划分 | 区分核心/相关/边缘期刊，辅助文献来源评估 | R `bibliometrix` |

### 3.2.2 作者分析

| 档位 | 图表名称 | 类型 | 所需数据 | 功能定位 | 推荐工具 |
|------|---------|------|---------|---------|---------|
| 🟢 | Top 10 Most Productive Authors | 横向柱状图 | 作者名 + 发文量 | 识别领域核心研究者 | Excel |
| 🟡 | Co-authorship Network (Author Level) | 网络图 | WoS/Scopus AU 字段，最小合著次数≥2 | 识别核心研究团队与合作群体 | VOSviewer（Type: Co-authorship，Unit: Authors） |
| 🔴 | Lotka's Law Fit | 散点+拟合曲线 | 作者 + 发文量分布 | 验证洛特卡定律，评估作者贡献分布规律 | R `ggplot2`（手动拟合）|

### 3.2.3 国家/机构分析

| 档位 | 图表名称 | 类型 | 所需数据 | 功能定位 | 推荐工具 |
|------|---------|------|---------|---------|---------|
| 🟢 | Top Countries by Publication Output | 表格（国家/地区 + 发文量 + 被引量 + H指数） | C1字段提取的国家信息 | 呈现研究的地理分布与影响力 | Excel |
| 🟢 | Top 10 Institutions | 横向柱状图 | 机构名 + 发文量 | 识别领域核心研究机构 | Excel |
| 🟡 | Country Collaboration World Map | 地图热力图 + 连线 | 国家发文量 + 合作关系 | 可视化国际合作格局与研究中心 | Bibliometrix `worldMap` + `countryCollaboration` |
| 🟡 | Co-authorship Network (Country Level) | 网络图 | WoS C1 字段，最小发文量≥1 | 识别国家间合作集群 | VOSviewer（Type: Co-authorship，Unit: Countries） |

---

## 3.3 引用结构分析（Citation Analysis & Intellectual Structure）

### 方法选择决策框架：共被引 vs 书目耦合

> 来源：Thakur & Kushwaha (2024)

这是引用结构分析中最常见的决策困惑。两种方法基于不同的"共享关系"，揭示领域知识结构的不同侧面：

| 维度 | 共被引分析（Co-citation） | 书目耦合（Bibliographic Coupling） |
|------|--------------------------|----------------------------------|
| **共享关系** | 两篇文献被第三篇文献同时引用 | 两篇文献引用了相同的参考文献 |
| **揭示内容** | 知识基础（Intellectual Base）：领域的经典文献与理论根基 | 研究前沿（Research Front）：当前研究的相似性与新兴趋势 |
| **分析单位** | 通常为被引文献（较早发表） | 通常为施引文献（较新发表） |
| **适用场景** | 领域历史较长、有清晰经典文献积累 | 领域较新、近年论文增长快、关注最新研究聚类 |
| **局限性** | 对新兴领域（经典文献少）结果不稳定 | 不能反映历史知识根基 |

**决策建议**：
- **成熟领域**（发文 10 年以上，有明确奠基文献）：优先使用**共被引**揭示知识基础，辅以**书目耦合**描述当前研究前沿
- **新兴领域**（发文不足 5 年，经典文献稀少）：优先使用**书目耦合**；共被引结果因样本不足可能不稳定
- **完整分析**：两者兼用，分别报告，在 Discussion 中说明两张图的互补关系（"共被引图揭示知识根基，书目耦合图呈现当前研究聚类"）

---

### 本地引用 vs 全局引用（Local vs Global Citations）

> 来源：Thakur & Kushwaha (2024)

在文献计量分析中，"被引次数"有两种来源，混淆使用是常见的方法论错误：

| 类型 | 定义 | 用途 |
|------|------|------|
| **全局引用（Global Citations）** | 数据库（WoS/Scopus）记录的总被引次数，包含来自语料库以外文献的引用 | 排列最具影响力文献（Top Cited Documents 表格）；反映文献对整个学科的外部影响力 |
| **本地引用（Local Citations）** | 语料库内文献互相引用的次数（仅计算分析集内的引用） | 构建共被引网络；识别在**本研究领域**（而非学科整体）最具核心性的文献 |

**操作规则**：
- **Top Cited Documents 表格**：报告全局引用（体现领域对外影响力）
- **共被引网络**：使用本地引用构建（避免领域外高被引文献（如通用方法论综述）主导网络，遮蔽领域内真正的核心文献）
- 若两个指标的 Top 排名存在显著差异，在方法节或 Results 中注明（如"本地引用 Top 5 与全局引用 Top 5 存在部分差异，表明部分奠基文献在本领域以外也具有广泛影响力"）

---

### 图表清单

| 档位 | 图表名称 | 类型 | 所需数据 | 功能定位 | 推荐工具 | 参数说明 |
|------|---------|------|---------|---------|---------|---------|
| 🟢 | Top 10 Most Cited Documents | 表格（文章标题 + 作者 + 年份 + 被引次数 + **Citations/Year**） | WoS TC 字段 + 发表年份 | 识别领域奠基性文献，展示知识基础；Citations/Year = 总被引 ÷ 发表至今年数，用于新旧文献公平比较 | Excel | 同时报告总引用和Citations/Year两列：总引用=绝对影响力；Citations/Year=增长速度（如近三年发表但Citations/Year极高，说明该文献快速获得认可，是新兴奠基文）|
| 🟢 | Top 10 Most Cited Authors | 表格（作者 + 总被引量） | WoS TC+AU 字段 | 识别最具影响力的学者 | Excel | — |
| 🟡 | Co-citation Network of References | 网络图 | WoS CR 字段，最小共被引≥5 | 揭示领域知识基础的聚类结构，识别研究流派 | VOSviewer（Type: Citation，Unit: Cited References） | 归一化：Association Strength；聚类：Leiden algorithm |
| 🟡 | Co-citation Network of Authors | 网络图 | WoS CR 字段提取作者，最小共被引≥3 | 识别相互引用的核心学者群体 | VOSviewer（Type: Citation，Unit: Cited Authors） | 同上 |
| 🟡 | Bibliographic Coupling Network of Documents | 网络图 | WoS CR 字段，最小共享参考文献≥5 | 识别当前研究前沿的相似研究集群 | VOSviewer（Type: Bibliographic Coupling，Unit: Documents） | 适合展示近5年研究趋势 |
| 🔴 | Historiograph (Direct Citation Network) | 时间线网络图（纵轴=年份，横轴=引用关系） | WoS CR 字段，直接引用关系链 | 呈现知识演化的历史路径与奠基文献传承关系 | R `bibliometrix` `histNetwork`，可视化用 `histPlot` | 建议筛选被引≥3次的文献 |
| 🔴 | Overlay Visualization (Citation Time Map) | 时间叠加网络图（节点颜色代表年份） | VOSviewer 导出 + 时间字段 | 在共被引网络上叠加时间维度，展示研究焦点的演化 | VOSviewer（Overlay Visualization 模式，Score: Year） | 颜色冷暖代表发表时间早晚；蓝=早期，橙/红=近期；Chen et al. 2025 用此图展示眼科AI伦理研究热点从"respect/benefit"演化到"privacy/security/trust" |
| 🔴 | RPYS (Reference Publication Year Spectroscopy) | 折线图（X轴=被引文献出版年，Y轴=被引频次 + 5年滚动中位数偏差） | WoS/Scopus CR 字段，提取所有被引文献的出版年 | 识别领域知识基础的"突破年份"——哪些年份发表的方法/理论论文在后期被大量引用，是理解领域发展节点的独特视角 | R `bibliometrix` `rpys()` / Biblioshiny | 用5年滚动中位数作为基线，偏差（deviation）显著高于零的年份 = 领域知识突破节点；Trojanowski & Barmentloo 2025 发现 2016–2019 年峰值对应深度学习和 NLP 的突破 |

---

### 双规格鲁棒性三角验证策略

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

## 3.4 共词与主题分析（Co-word Analysis & Thematic Mapping）

| 档位 | 图表名称 | 类型 | 所需数据 | 功能定位 | 推荐工具 | 参数说明 |
|------|---------|------|---------|---------|---------|---------|
| 🟢 | Top 20 Author Keywords by Frequency | 横向柱状图 | DE 字段（Author Keywords）+ 频次 | 直观呈现高频研究主题，辅助读者快速了解领域热点 | Excel | 使用作者关键词（DE），非数据库关键词（ID） |
| 🟢 | Top Keywords Word Cloud | 词云图 | DE 字段 + 频次 | 视觉化呈现关键词重要性（美观但信息密度低） | WordArt.com / Python `wordcloud` | 可作为封面图，不建议作为主图 |
| 🟡 | Keyword Co-occurrence Network | 网络图 | DE 字段，最小共现次数≥3 | 揭示关键词聚类结构，识别研究主题群及其关联 | VOSviewer（Type: Co-occurrence，Unit: All Keywords） | 归一化：Association Strength；建议展示≥5个聚类 |
| 🟡 | Strategic Diagram (Thematic Map) | 四象限散点图（X轴=中心度，Y轴=密度） | Bibliometrix 计算的主题密度和中心度 | 评估各研究主题的战略地位（Motor/Niche/Basic/Emerging） | R `bibliometrix` `thematicMap` | 建议4–6个主题；需解释各象限含义 |
| 🟡 | Trending Topics (Word Dynamics Over Time) | 多折线图或气泡图 | DE 字段 + 年份 + 频次 | 追踪关键词热度随时间的变化，识别新兴主题 | R `bibliometrix` `fieldByYear` | 选取频次 Top 10–15 关键词 |
| 🔴 | Thematic Evolution Map | 桑基图/Alluvial图（节点=主题，箭头=时间流向） | 分时段关键词聚类结果 | 展示研究主题随时间的演化、合并与分裂 | R `ggalluvial` / Bibliometrix `thematicEvolution` | 建议分2–3个时间段；需预先定义时间窗口 |
| 🔴 | Topic Modeling Visualization (LDA) | 气泡图或热力图 | 全文摘要（Abstract 字段） | 基于文本内容的主题发现，补充关键词分析 | R `topicmodels` + `ggplot2` / Python `gensim` | 超出标准文献计量范畴，适合 B 类综述 |

---

## B类专属：内容分析结果

| 档位 | 图表名称 | 类型 | 所需数据 | 功能定位 | 推荐工具 |
|------|---------|------|---------|---------|---------|
| 🟢 | Coding Category Distribution | 频率表格（类别 + 频次 + 占比%） | 内容编码结果表 | 呈现各编码类别的分布，回答内容层面的描述性 RQ | Excel |
| 🟢 | Research Method Classification Table | 表格（方法类别 + 文章数 + 代表文献） | 内容编码（研究方法维度） | 展示领域研究方法多样性 | Word/Excel |
| 🟡 | Theoretical Frameworks Over Time (Heatmap) | 热力图（X轴=年份，Y轴=理论框架，颜色深浅=频次） | 编码结果（框架维度）+ 年份 | 展示理论框架使用的时序变化规律 | R `ggplot2` / Python `seaborn` |
| 🟡 | Research Focus Distribution (Grouped Bar) | 分组柱状图 | 多个编码维度的频次 | 多维度对比不同研究特征的分布 | R `ggplot2` / Excel |
| 🔴 | Inter-rater Reliability Report | 表格（编码员 + 维度 + κ值 + 一致率） + 方法说明 | 双编码员独立编码结果 | 证明内容编码的客观性与可重复性（B类方法论必需项） | R `irr` 包（`kappa2`函数）/ SPSS / Krippendorff's Alpha |
| 🟡 | Cross-dimensional Theme × Category Chart | 分组柱状图（X轴=类别1，分组色=类别2）或矩阵热力图 | 两个编码维度的交叉频次表（如"伦理主题 × 数据模态"）| 揭示不同子类别之间的差异化内容规律（如不同数据模态对应不同伦理优先项）；是双流B类文章的核心贡献图表 | Excel（分组柱状图）/ R `ggplot2` | 参考 Chen et al. 2025 Fig.4b：用9个伦理主题×10个数据模态的交叉分析，揭示底眼成像→重解释性、面部摄影→重隐私的规律 |
| 🔴 | Content-Bibliometrics Integration Matrix | 矩阵热力图（X轴=计量聚类，Y轴=内容主题） | 文献的计量聚类标签 + 内容编码标签 | 桥接计量分析与内容分析，揭示聚类的实质内容 | R `pheatmap` / Python `seaborn` |

---

## 分析参数速查

### VOSviewer 常用参数设置

| 分析类型 | 最小阈值建议 | 归一化方法 | 聚类算法 |
|---------|------------|---------|---------|
| 关键词共现 | 最小共现次数：3–5（视样本量调整） | Association Strength | Leiden |
| 共被引（文献） | 最小共被引次数：5–10 | Association Strength | Leiden |
| 共被引（作者） | 最小共被引次数：3–5 | Association Strength | Leiden |
| 合著（作者） | 最小发文量：2–5 | Association Strength | Leiden |
| 合著（国家） | 最小发文量：1–3 | Association Strength | Leiden |
| 书目耦合（文献） | 最小共享参考文献数：5 | Association Strength | Leiden |

### Bibliometrix 常用函数速查

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

### 多期时序共词分析：非等分时间窗口策略

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

### Cohen's κ 判断标准

| κ 值范围 | 一致性水平 | 发表建议 |
|---------|----------|---------|
| < 0.20 | 微弱 | 不可接受，需重新培训编码员 |
| 0.21–0.40 | 一般 | 勉强，需说明原因 |
| 0.41–0.60 | 中等 | 可接受（最低标准） |
| 0.61–0.80 | 良好 | 符合发表要求 |
| 0.81–1.00 | 极佳 | 优秀 |

> B类综述的 κ 建议达到 ≥ 0.61，并在 Methodology 中明确报告。
