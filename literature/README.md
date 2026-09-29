# 相关文献 (Related Literature)

题目九：From Code Assistants to Code Guardians: Real-Time Hallucination Detection for
AI-Generated Code in CI/CD Pipelines

以下文献围绕三个核心问题收集：(1) 代码幻觉的定义与分类，(2) 静态检测方法及其局限，
(3) 动态/沙箱验证与 CI/CD 集成。本地已下载 PDF 的文献见下表对应文件；另外两篇因平台
版权限制（USENIX / Springer 付费墙）未能直接下载全文 PDF，已附链接与详细摘要。

| # | 文件 | 标题 | 作者 | 年份/venue | 关键贡献 |
|---|------|------|------|-----------|----------|
| 1 | `01_CodeHalu_2405.00253.pdf` | CodeHalu: Investigating Code Hallucinations in LLMs via Execution-based Verification | Tian, Yan, Yang, Zhao, Chen, Wang, Luo, Ma, Song | AAAI 2025 (arXiv:2405.00253) | 提出四类代码幻觉分类体系（mapping / naming / resource / logic），构建 CodeHaluEval 基准（8,883 样本 / 699 任务），评测 17 个主流 LLM |
| 2 | `02_RefusingTheImpossible_2609.03267.pdf` | Refusing the Impossible: A Taxonomy and Benchmark for Code Hallucination in Large Language Models | Dasu, Kundu, Tan | arXiv:2609.03267 (2026) | 从 groundedness / manifestation level / behavioral pattern 三维度定义"不可能任务"上的幻觉；构造 270 条对抗性提示 + 91 条可解对照，测试 12 个开源模型 |
| 3 | `03_StaticAnalysis_LibraryHallucinations_2604.07755.pdf` | An Empirical Analysis of Static Analysis Methods for Detection and Mitigation of Code Library Hallucinations | Miranda-Pena, Reeson, Paris, Poon, Kummerfeld | arXiv:2604.07755 (2026) | 实测纯静态分析工具只能识别 16%-70% 的错误、14%-85% 的库幻觉，证明静态方法覆盖率有理论上限（48.5%-77%），单独使用不足以解决问题——为"混合验证"提供动机 |
| 4 | `04_StaticPassDynamicFail_2609.10762.pdf` | Beyond Static Guarantees: Measuring the Static-Pass Dynamic-Fail Gap in Security-Sensitive and LLM-Generated Python Code | Pourleyli, Das Urmi, Melo | arXiv:2609.10762 (2026) | 提出 "Static-Pass Dynamic-Fail" 现象：654 个通过 Bandit/Semgrep 静态扫描的样本中，动态沙箱执行 + LLM 驱动的 CWE 推理发现 95 个仍可被利用，证明静态通过和运行时安全是两个层级 |
| 5 | `05_SandboxEval_2504.00018.pdf` | SandboxEval: Towards Securing Test Environment for Untrusted Code | Rabin, Hostetler, McGregor, Weir, Judd | arXiv:2504.00018 (2025) | 面向"执行 LLM 生成代码"场景设计沙箱安全测试集，覆盖敏感信息泄露、文件系统篡改、外部通信等风险，指出现有沙箱基础设施的薄弱点 |
| 6 | `06_LLMHallucinationSurvey_2510.06265.pdf` | Large Language Models Hallucination: A Comprehensive Survey | (综述, arXiv:2510.06265) | arXiv:2510.06265 (2025) | 通用 LLM 幻觉综述（定义/成因/分类/检测/缓解），为"代码幻觉"提供上位概念与术语基础 |

## 补充文献：架构感知的文档/测试维护（支撑第二次汇报的新方向）

在第一次汇报后，我们将研究角度从"通用代码幻觉检测"收窄为一个更具体的问题：**当 AI
生成的代码改动被合并时，如何让受影响的模块文档和测试同步更新，并判断这种更新是否需要
传播到其他关联模块。** 为此新增以下 4 篇最相关的已有工作，用于定位我们方法的创新点：

| # | 文件 | 标题 | 作者 | 年份/venue | 与本项目的关系 |
|---|------|------|------|-----------|----------------|
| 7 | `07_RepoAgent_2402.16667.pdf` | RepoAgent: An LLM-Powered Open-Source Framework for Repository-level Code Documentation Generation | Luo et al. | arXiv:2402.16667 (2024) | 通过 git pre-commit hook 检测代码变更，定位受影响的对象及其双向引用，仅更新"最小受影响范围"内的文档。**局限**：粒度停留在函数/对象级 docstring，没有显式的模块级架构图，也不更新测试 |
| 8 | `08_DocAgent_2504.08725.pdf` | DocAgent: A Multi-Agent System for Automated Code Documentation Generation | (Meta/FAIR 团队) | arXiv:2504.08725 (2025) | Reader/Searcher/Writer/Verifier/Orchestrator 多智能体协作，拓扑顺序逐步生成文档，并给出 Completeness/Helpfulness/Truthfulness 评测框架。**局限**：面向"从零生成文档"，不是"给定 diff 决定是否级联更新其他模块" |
| 9 | `09_CASCADE_2604.19400.pdf` | CASCADE: Detecting Inconsistencies between Code and Documentation with Automatic Test Generation | Kiecker et al. | arXiv:2604.19400 (2026) | 用文档生成单测、用代码生成参照实现，双向交叉验证以检测代码-文档不一致，在真实仓库中发现 13 个此前未知的问题。**局限**：面向单个函数/文件级别的一致性检测，没有仓库级架构图，也没有跨模块传播机制 |
| 10 | `10_RepositoryIntelligenceGraph_2601.10112.pdf` | Repository Intelligence Graph: Deterministic Architectural Map for LLM Code Assistants | Cherny-Shahar, Yehudai | arXiv:2601.10112 (2026) | 从构建系统（如 CMake）中抽取确定性的仓库架构图（可构建组件、聚合器、测试、外部依赖等），提供给编码 agent 后平均准确率提升 12.2%、完成时间减少 53.9%。**局限**：架构图仅用于辅助单次编码任务，不用于"diff→模块归属→级联决策"的文档/测试维护流程 |

这四篇是目前检索到与我们新方法**最接近**的已有工作，因此也是论证创新点时最需要
对比的基线。

## 未能下载全文的补充文献（付费墙，仅附链接与摘要）

**We Have a Package for You! A Comprehensive Analysis of Package Hallucinations by
Code Generating LLMs.** Joseph Spracklen, Raveen Wijewickrama, A.H.M. Nazmus Sakib,
Anindya Maiti, Bimal Viswanath, Murtuza Jadliwala. *USENIX Security Symposium 2025*.
https://www.usenix.org/publications/loginonline/we-have-package-you-comprehensive-analysis-package-hallucinations-code

测试 16 个代码模型（Python/JavaScript），发现"包幻觉"（推荐不存在的依赖包）平均发生率
19.6%（开源模型约 21%，商业模型约 5%），生成了超过 20.5 万个独特的虚构包名，其中约
45% 在重复查询中持续出现——这为攻击者发布"投毒包"（slopsquatting）提供了可乘之机，
是"API/依赖误用"这一幻觉子类的重要实证支撑。

**Hallucination detection in LLM code generation: A sampling-based consensus
verification approach.** *Automated Software Engineering (Springer), 2026*.
https://link.springer.com/article/10.1007/s10515-026-00605-0

提出基于多次采样一致性的幻觉检测方法：对同一 prompt 多次采样生成代码，通过结果间的
一致性/分歧来估计幻觉概率，无需外部 oracle，可作为静态 AST 匹配和沙箱执行之外的第三
种轻量检测思路。

## 文献如何支撑题目九的三个创新点

- **创新点一（代码幻觉分类体系）**：文献 1、2 提供了两套互补的分类框架（执行结果导向
  的 mapping/naming/resource/logic 四分类，以及 groundedness/manifestation/behavior
  三维分类），可作为本项目分类体系设计的直接参考基线。
- **创新点二（静态-动态混合验证）**：文献 3 证明纯静态方法覆盖率有限，文献 4 证明"静
  态通过"不等于"运行时安全"，两者共同说明单一手段不够，必须结合 AST 模式匹配（快）
  与沙箱执行（准）；文献 5 提供了安全沙箱设计的具体测试维度。
- **创新点三（CI/CD 原生集成与结构化反馈）**：文献 4、5 的流水线设计（静态扫描 →
  LLM 推理 → 沙箱验证 → 报告）可直接映射为 CI/CD 中的多阶段 gate，用于设计本项目的
  系统架构。
