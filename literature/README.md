# 相关文献 (Related Literature)

题目九：From Code Assistants to Code Guardians: Real-Time Hallucination Detection for
AI-Generated Code in CI/CD Pipelines

**选文标准（第二次修订）**：只保留 2025 年及以后、且明确面向"软件工程实践"的文献——
静态/动态验证工具、仓库级文档与测试维护、AI 时代软件工程方法论、以及大仓库/长时间跨度
的 agent benchmark。删除了早于 2025 年的文献，以及泛泛而谈"LLM 生成代码存在幻觉"这一
现象本身、但不落到具体软件工程问题/工具/benchmark 上的文献（例如通用幻觉分类与综述）。

## 一、静态/动态验证 与 沙箱安全（幻觉在“单次生成”阶段如何被检测）

| # | 文件 | 标题 | 作者 | 年份/venue | 关键贡献 |
|---|------|------|------|-----------|----------|
| 1 | `01_StaticAnalysis_LibraryHallucinations_2604.07755.pdf` | An Empirical Analysis of Static Analysis Methods for Detection and Mitigation of Code Library Hallucinations | Miranda-Pena, Reeson, Paris, Poon, Kummerfeld | arXiv:2604.07755 (2026) | 实测纯静态分析工具只能识别 16%-70% 的错误、14%-85% 的库幻觉，证明静态方法覆盖率有理论上限（48.5%-77%） |
| 2 | `02_StaticPassDynamicFail_2609.10762.pdf` | Beyond Static Guarantees: Measuring the Static-Pass Dynamic-Fail Gap in Security-Sensitive and LLM-Generated Python Code | Pourleyli, Das Urmi, Melo | arXiv:2609.10762 (2026) | 三阶段流水线（静态扫描→LLM 驱动 CWE 推理→Docker 沙箱验证）证明"静态通过"与"运行时安全"是两个层级 |
| 3 | `03_SandboxEval_2504.00018.pdf` | SandboxEval: Towards Securing Test Environment for Untrusted Code | Rabin, Hostetler, McGregor, Weir, Judd | arXiv:2504.00018 (2025) | 面向"执行不可信 LLM 生成代码"场景设计安全测试集，覆盖敏感信息泄露、文件系统篡改等风险 |
| — | *(无 PDF，付费墙)* | We Have a Package for You! A Comprehensive Analysis of Package Hallucinations by Code Generating LLMs | Spracklen et al. | USENIX Security 2025 | 16 个代码模型的"包幻觉"（推荐不存在依赖包）实证研究，平均发生率 19.6%，揭示 slopsquatting 供应链攻击面 |

## 二、仓库级文档/测试自动维护（与本项目方法最直接相关）

| # | 文件 | 标题 | 作者 | 年份/venue | 关键贡献 |
|---|------|------|------|-----------|----------|
| 4 | `04_DocAgent_2504.08725.pdf` | DocAgent: A Multi-Agent System for Automated Code Documentation Generation | (Meta/FAIR 团队) | arXiv:2504.08725 (2025) | Reader/Searcher/Writer/Verifier/Orchestrator 多智能体拓扑式生成文档，提出 Completeness/Helpfulness/Truthfulness 评测框架 |
| 5 | `05_CASCADE_2604.19400.pdf` | CASCADE: Detecting Inconsistencies between Code and Documentation with Automatic Test Generation | Kiecker, Sparka, Reuter, Ziegler, Grunske | arXiv:2604.19400 (2026) | 用文档生成单测、用代码生成参照实现，双向交叉验证检测代码-文档不一致，在真实仓库中发现 13 个未知问题 |
| 6 | `06_RepositoryIntelligenceGraph_2601.10112.pdf` | Repository Intelligence Graph: Deterministic Architectural Map for LLM Code Assistants | Cherny-Shahar, Yehudai | arXiv:2601.10112 (2026) | 从构建系统抽取确定性仓库架构图（可构建组件/聚合器/测试/依赖），喂给编码 agent 后平均准确率提升 12.2%、耗时减少 53.9% |
| 7 | `10_ReCite_2608.03734.pdf` | We Must Have Missed This Comment: Detecting and Repairing Stale Function References in Linux Kernel Comments | Sun, Lyu, Ma, Kuang, Widyasari, Zhang, Ma, Lawall, Lo | arXiv:2608.03734, ASE 2026 | 在 Linux 内核（v6.18-rc1）真实大仓库中，三阶段方法（检测失效符号引用→追溯 Git 历史→LLM 生成修复建议）发现 869 处过时注释，89.0% 的修复建议有用，已被上游接受 50 个补丁 |

## 三、AI 时代软件工程方法论 与 大仓库/长时间跨度 Agent Benchmark

| # | 文件 | 标题 | 作者 | 年份/venue | 关键贡献 |
|---|------|------|------|-----------|----------|
| 8 | `07_SWEMilestone_2603.13428.pdf` | SWE-Milestone: Evaluating AI Agents on Continuous Software Evolution | Deng et al. | arXiv:2603.13428 (2026) | 从真实提交历史构造"里程碑 DAG"，评测 agent 在**连续**任务序列（而非孤立任务）下的表现：分数从孤立任务的 >80% 骤降到连续场景的 38.03%，暴露长期维护与错误级联的短板 |
| 9 | `08_SWEEVO_2512.18470.pdf` | SWE-EVO: Benchmarking Coding Agents in Long-Horizon Software Evolution Scenarios | Le, Thai, Manh, Nhat, Bui | arXiv:2512.18470 (2025) | 基于 7 个成熟 Python 开源项目的 release notes 构造 48 个任务，平均涉及 21 个文件、874 个测试；GPT-5.4+OpenHands 仅拿到 25%（对比 SWE-Bench Verified 上的 72.80%），证明多文件长时程推理仍是短板 |
| 10 | `09_RoadmapBench_2605.15846.pdf` | RoadmapBench: Evaluating Long-Horizon Agentic Software Development Across Version Upgrades | Xu et al. | arXiv:2605.15846 (2026) | 17 个仓库、5 种语言、115 个跨版本升级任务（平均改动 3,700 行/51 个文件），最强模型也只解决 39.1% |
| 11 | `11_AgenticSE_Roadmap_2509.06216.pdf` | Agentic Software Engineering: Foundational Pillars and a Research Roadmap | Hassan, Li, Lin, Adams, Chen, Kashiwa, Qiu | arXiv:2509.06216 (2025) | 提出 "SE for Humans / SE for Agents" 双框架与 Structured Agentic Software Engineering (SASE) 概念体系，重新定义 AI 时代软件工程的角色/流程/工具/产物 |
| 12 | `12_AgenticCodeReview_2605.17548.pdf` | Rethinking Code Review in the Age of AI: A Vision for Agentic Code Review | Kamalı, Tuna, Haratian, Tüzün | arXiv:2605.17548 (2026) | 提出五阶段 agentic code review 流程（PR 创建→增强→评审者选择→AI 辅助评审→复盘），人类转为"agent 的监督操作员" |
| 13 | `13_DependencyUpgradeAgents_2510.03480.pdf` | LLM Agents for Automated Dependency Upgrades | Tawosi, Alamir, Liu, Veloso | arXiv:2510.03480 (2025) | Summary/Control/Code 三 agent 协作，结合迁移文档自动定位并修复 Java 代码中的依赖升级问题，工业案例精度 71.4% |

## 文献如何支撑本项目的新方法（架构感知的模块级文档/测试同步 Agent）

- **为什么"文档/测试同步"值得单独研究**：第二组文献里，DocAgent/CASCADE/Repository
  Intelligence Graph/ReCite 各自解决了问题的一部分（生成文档、检测不一致、抽取架构图、
  修复过时引用），但都局限在函数/文件级别或单次任务，没有一个把"仓库级架构图 + diff
  归属到模块 + 模块级 agent 更新文档和测试 + 依架构图决定是否级联"整套流程打通——这正是
  我们方法的切入点（详见 PPT 第 10 页"最相关的已有工作"）。
- **为什么要强调"大仓库、长时间跨度"**：第三组文献（SWE-Milestone、SWE-EVO、
  RoadmapBench）用不同方式证明同一件事——现有 agent 在**孤立、单次**任务上表现尚可，
  但放到**连续演化、跨多文件、跨版本**的真实场景下性能大幅下降（38.03% vs 80%+；
  25% vs 72.80%；39.1% 封顶）。这说明我们的方法必须在"长时间跨度、持续演化"的仓库上
  验证，而不能只用一次性的、静态的 diff 样例来评估。
- **为什么需要"AI 时代软件工程"的方法论支撑**：Agentic SE Roadmap 与 Agentic Code
  Review 两篇提供了"人类作为 agent 监督者"的流程范式，为我们方法中"agent 自主判断是否
  级联"这一设计提供了合理性依据（而不是纯粹自动化、无人把关）；Dependency Upgrade
  Agents 则提供了一个已验证可行的、"多 agent 协作 + 现有文档作为上下文"的工程范式参考。
