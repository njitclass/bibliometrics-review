# 文献计量分析图表指南

> 最后更新：2026-03-17（从参考文献 Chen et al., 2025, npj Digital Medicine 更新）
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

| 档位 | 图表名称 | 类型 | 所需数据 | 功能定位 | 推荐工具 | 参数说明 |
|------|---------|------|---------|---------|---------|---------|
| 🟢 | Top 10 Most Cited Documents | 表格（文章标题 + 作者 + 年份 + 被引次数） | WoS TC 字段 | 识别领域奠基性文献，展示知识基础 | Excel | — |
| 🟢 | Top 10 Most Cited Authors | 表格（作者 + 总被引量） | WoS TC+AU 字段 | 识别最具影响力的学者 | Excel | — |
| 🟡 | Co-citation Network of References | 网络图 | WoS CR 字段，最小共被引≥5 | 揭示领域知识基础的聚类结构，识别研究流派 | VOSviewer（Type: Citation，Unit: Cited References） | 归一化：Association Strength；聚类：Leiden algorithm |
| 🟡 | Co-citation Network of Authors | 网络图 | WoS CR 字段提取作者，最小共被引≥3 | 识别相互引用的核心学者群体 | VOSviewer（Type: Citation，Unit: Cited Authors） | 同上 |
| 🟡 | Bibliographic Coupling Network of Documents | 网络图 | WoS CR 字段，最小共享参考文献≥5 | 识别当前研究前沿的相似研究集群 | VOSviewer（Type: Bibliographic Coupling，Unit: Documents） | 适合展示近5年研究趋势 |
| 🔴 | Historiograph (Direct Citation Network) | 时间线网络图（纵轴=年份，横轴=引用关系） | WoS CR 字段，直接引用关系链 | 呈现知识演化的历史路径与奠基文献传承关系 | R `bibliometrix` `histNetwork`，可视化用 `histPlot` | 建议筛选被引≥3次的文献 |
| 🔴 | Overlay Visualization (Citation Time Map) | 时间叠加网络图（节点颜色代表年份） | VOSviewer 导出 + 时间字段 | 在共被引网络上叠加时间维度，展示研究焦点的演化 | VOSviewer（Overlay Visualization 模式，Score: Year） | 颜色冷暖代表发表时间早晚；蓝=早期，橙/红=近期；Chen et al. 2025 用此图展示眼科AI伦理研究热点从"respect/benefit"演化到"privacy/security/trust" |

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

| 功能 | 函数 | 主要参数 |
|------|------|---------|
| 读取数据 | `convert2df()` | `format="wos"` 或 `"scopus"` |
| 描述性分析 | `biblioAnalysis()` + `summary()` | — |
| 年产出图 | `plot(M, "production")` | — |
| 主题图 | `thematicMap()` | `field="DE"`, `n=250`, `minfreq=5` |
| 主题演化 | `thematicEvolution()` | `years=c(2000,2010,2023)` |
| 国家合作地图 | `countryCollaboration()` + `worldMap()` | — |
| 历史引用网络 | `histNetwork()` + `histPlot()` | `min.citations=3` |
| 作者合著网络 | `biblioNetwork(analysis="collaboration")` | `network="authors"` |

### Cohen's κ 判断标准

| κ 值范围 | 一致性水平 | 发表建议 |
|---------|----------|---------|
| < 0.20 | 微弱 | 不可接受，需重新培训编码员 |
| 0.21–0.40 | 一般 | 勉强，需说明原因 |
| 0.41–0.60 | 中等 | 可接受（最低标准） |
| 0.61–0.80 | 良好 | 符合发表要求 |
| 0.81–1.00 | 极佳 | 优秀 |

> B类综述的 κ 建议达到 ≥ 0.61，并在 Methodology 中明确报告。
