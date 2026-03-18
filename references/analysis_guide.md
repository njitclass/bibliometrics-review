# 文献计量分析图表指南

> 最后更新：2026-03-18（v0.10.0 架构重构：工具参数速查已迁移至 `tool_reference.md`，本文件专注于图表菜单）
> 用途：阶段3分析方案规划、阶段4b逐节图表菜单
> 姊妹文件：`references/tool_reference.md`（工具对比 + 参数设置 + 分析策略）

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
- [分析参数速查（→ 跳转至 tool_reference.md）](#分析参数速查)

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

> 完整内容已迁移至 `references/tool_reference.md` → §双规格鲁棒性三角验证策略
>
> **简要**：同一分析跑两套参数配置（如 LCS vs GCS），检验聚类结论是否依赖具体参数选择。适用于投稿 Scientometrics / JoI 等高要求 Q1 期刊时。

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
| 🟡 | Keyword Burst Chart（突变词图谱） | 时序条形图（X轴=时间，Y轴=关键词，条长=突变强度和持续期） | DE/ID 字段 + 年份，使用 Kleinberg's Burst Detection Algorithm 检测（注意：LLR 是聚类标签提取算法，非突变检测算法） | 识别在特定时期**引用/频次骤然飙升**的关键词，捕捉研究前沿演变节点；与 RPYS 互补（RPYS 看被引文献节点，Burst 看关键词爆发） | CiteSpace（Analysis → Burst Detection） | 设置 γ（突变强度阈值，建议 ≥ 1.0）和最短持续期（建议 ≥ 2年）；可据此划分领域发展阶段并用阶段名命名（如"数字化整合期 2018–2022"），命名应基于该阶段突变词的共性主题 |
| 🟡 | Timezone View（时间线图谱） | 时间线网络图（纵轴=关键词聚类，横轴=时间，节点颜色=聚类） | DE/ID 字段聚类结果 + 年份 | 展示各研究主题**何时兴起、如何沿时间轴演化**；是 CiteSpace 对 VOSviewer/Bibliometrix Overlay Map 的替代实现，侧重历时动态而非共时网络结构 | CiteSpace（Visualize → Timezone View） | Timezone View 是 CiteSpace 独有的视图模式，切换至此模式无需重新运行分析；注意与主题演化桑基图（Thematic Evolution Map）的区别：后者按时段聚类，Timezone View 按时间轴连续展示 |

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

> ⚠️ **本章节已迁移至独立文件** → 请查阅 `references/tool_reference.md`
>
> 迁移内容包括：主流工具对比速查（VOSviewer / Bibliometrix / CiteSpace）、各工具参数设置表、聚类质量指标（Q/S）、非等分时间窗口策略、双规格鲁棒性验证、Cohen's κ 判断标准。
>
> **迁移原因**：将"按工具组织的参数速查"与"按论文章节组织的图表菜单"分开管理，减少单文件认知负荷，解决 Skill 阶段编号 vs 论文章节编号的混淆问题。
