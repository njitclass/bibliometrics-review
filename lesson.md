# Bibliometrics Review Skill — Lesson Log

> 本文件由 Skill 自动维护，记录用户在交互中提出的修改建议与偏好。
> 每个新项目启动时读取，使 Skill 从第一轮对话起即更贴合用户习惯。
> 最后更新：2026-03-18（v0.10.1 改进建议 F/G/I 实施后）

---

## 写作风格偏好

| 日期 | 原始建议 | 提炼规则 | 适用范围 |
|------|---------|---------|---------|
| — | — | — | — |

---

## 章节结构偏好

| 日期 | 原始建议 | 提炼规则 | 适用范围 |
|------|---------|---------|---------|
| — | — | — | — |

---

## 图表风格偏好

| 日期 | 原始建议 | 提炼规则 | 适用范围 |
|------|---------|---------|---------|
| — | — | — | — |

---

## 工具与技术偏好

| 日期 | 原始建议 | 提炼规则 | 适用范围 |
|------|---------|---------|---------|
| — | — | — | — |

---

## 方法论偏好

| 日期 | 原始建议 | 提炼规则 | 适用范围 |
|------|---------|---------|---------|
| — | — | — | — |

---

## 期刊与领域规范

| 日期 | 原始建议 | 提炼规则 | 适用范围 |
|------|---------|---------|---------|
| — | — | — | — |

---

## 工作流偏好

| 日期 | 原始建议 | 提炼规则 | 适用范围 |
|------|---------|---------|---------|
| — | — | — | — |

---

## 参考文献学习记录

| 日期 | 文章来源（DOI/标题） | 更新内容 | 更新位置 |
|------|-------------------|---------|---------|
| 2026-03-17 | Chen et al. (2025). Current status and solutions for AI ethics in ophthalmology: a bibliometric analysis. npj Digital Medicine. https://doi.org/10.1038/s41746-025-01976-6 | ① 双流研究设计框架（B类）；② 学科定位对比图 + 指数增长拟合图（含Price曲线框架）；③ 时序叠加可视化（Overlay，蓝→橙/红色谱代表年份演化）；④ 跨维度交叉分析图（伦理主题×数据模态，分组柱状图）；⑤ Results/Discussion分界原则（严格描述性Results）；⑥ B类方法节可复现性声明范式；⑦ npj Digital Medicine 期刊档案（IF≈15.2，Q1，医疗AI方向） | analysis_guide.md（研究框架+4个新图表条目）；writing_examples.md（Results边界原则+B类方法节模板+可复现声明）；journal_standards.md（新增npj Digital Medicine档案）；SKILL.md（B类双流设计说明） |
| 2026-03-18 | Thakur, M., & Kushwaha, A.K. (2024). [Title: Science mapping/bibliometric analysis of a management/information field]. Global Business and Organizational Excellence (GBOE). | ① 共被引 vs 书目耦合决策框架：成熟领域优先共被引（知识根基），新兴领域优先书目耦合（研究前沿），两者互补说明；② 非等分时间窗口策略：以发文量拐点为界划分时间段，萌芽期设较长窗口，快速增长期和近期各设独立短窗口；③ 本地引用 vs 全局引用区分：Top Cited Documents 报告全局引用，共被引网络使用本地引用（避免领域外文献主导网络）；④ Results 压轴综合汇总表（Capstone Summary Table）：按 RQ 组织，同时呈现定量证据（数字）和定性结论（一句话），置于 Results 末尾、Discussion 之前 | analysis_guide.md（§3.3新增共被引 vs 书目耦合决策框架、本地/全局引用区分；§分析参数速查新增非等分时间窗口策略）；writing_examples.md（新增 Results 压轴综合汇总表写法章节） |
| 2026-03-18 | Trojanowski, M., & Barmentloo, E. (2025). Convergence of marketing technologies and artificial intelligence: A bibliometric review (1987–2025). Engineering Management in Production and Services, 17(4), 29–51. doi:10.2478/emj-2025-0025 | ① 双数据库遴选协议（5步量化选库）：同时检索 WoS+Scopus，用关键词覆盖率比较决定主库，将选库变为可核实的客观决策；② 双规格鲁棒性三角验证：同一分析跑两套参数配置（主规格：LCS+索引词；比较规格：GCS+作者词），验证结论的规格稳健性；③ RPYS（参考文献发表年光谱分析）：分析语料库中被引文献的出版年分布，用5年滚动中位数识别领域知识突破节点，Bibliometrix `rpys()` 实现；④ Citations/Year 年化归一化：Top Cited Documents 表格额外报告"总被引 ÷ 发表年数"，使新老文献可比；⑤ 关键词轨迹推演表（Keyword Trajectory Inference Table）：在战略坐标图基础上，对每个关键词基于其当前中心度-密度位置做出前瞻性演化推断（"Authors posit that..."），链接 Results 与 Discussion；⑥ Biblioshiny 作为 Bibliometrix 的无代码 GUI 替代方案 | analysis_guide.md（§3.3新增 RPYS 图表条目、Citations/Year 标注、双规格鲁棒性验证策略；§分析参数速查新增 Biblioshiny 工具路径列）；writing_examples.md（§2新增双数据库选库协议；§3.4新增关键词轨迹推演表写法） |
| 2026-03-18 | 肖永慧 & 张庆龙 (2025). 数字化时代的财务共享：现实、挑战与未来发展——基于CiteSpace的可视化分析. 《财会通讯》2025年第4期. DOI: 10.16144/j.cnki.issn1002-8072.2025.04.003 | ① CiteSpace 工具条目：新增主流工具对比速查表（VOSviewer / Bibliometrix-Biblioshiny / CiteSpace 三强对比），CiteSpace 独有优势为突变词检测+时间线图谱，对 CNKI 格式支持最好；② CNKI 主库使用规范（特殊情形）：聚焦中文学界时以 CNKI（CSSCI+北大核心）为主库，补充 CNKI 导出格式、字段映射、去重规范及双库方法节报告模板；③ 突变词图谱（Keyword Burst Chart）：新增图表条目，使用 LLR 算法识别特定时期骤然飙升的关键词，可据此划分领域发展阶段；与 RPYS 互补（RPYS 看被引文献节点，Burst 看关键词爆发）；④ 时间线图谱（Timezone View）：CiteSpace 独有视图，纵轴按聚类分层、横轴按时间排列，展示主题历时演化；与 Overlay Map 目标类似但视觉逻辑不同；⑤ Q/S 聚类质量指标：CiteSpace 特有输出（Modularity Q > 0.3 + Silhouette S > 0.5 / 0.7），是聚类结果有效性的标准报告格式，附方法节报告范式；⑥ 中外文献对比表（Bilateral Literature Comparison Table）：双库研究新写法，将 CNKI Top-5 与 WoS Top-5 关键词聚类并排呈现，揭示中外学界系统性差异，附引导段写法示范 | analysis_guide.md（§分析参数速查新增主流工具对比表；§3.4共词与主题分析新增突变词图谱和Timezone View两个图表条目；§分析参数速查新增聚类质量指标Q/S章节）；writing_examples.md（§2数据库遴选协议新增CNKI主库特殊情形；§3.4新增中外文献对比表写法） |

---

## 待观察模式

> 单次出现、尚未确认是否为稳定偏好的反馈。累计出现2次后升级为对应分类的正式规则。

| 日期 | 建议内容 | 出现次数 | 状态 |
|------|---------|---------|------|
| — | — | — | — |
