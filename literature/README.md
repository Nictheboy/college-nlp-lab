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
