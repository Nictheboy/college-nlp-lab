# NLP Course Project — Topic 9

**From Code Assistants to Code Guardians: Real-Time Hallucination Detection for
AI-Generated Code in CI/CD Pipelines**

课程：NLP（2026 秋）小组作业
题目来源：[openi.pcl.ac.cn/luckh2/nlp26projects](https://openi.pcl.ac.cn/luckh2/nlp26projects)（题目九）
小组成员：李甘、张星烁、连瑾昭

## 题目简介

现有研究主要关注自然语言的事实性幻觉，而"代码幻觉"——LLM 生成的代码看似正确，
实则存在逻辑漏洞、资源泄漏或依赖过时/不存在的 API——检测研究仍属空白。本项目计划
开发一个轻量级代码验证器，集成到 CI/CD 流水线中，在 AI 生成代码被合并前进行
静态分析 + 动态沙箱测试，检测潜在的运行时错误和 API 兼容性问题，并在检测覆盖率
与执行速度之间取得平衡。

三个创新点：
1. **代码幻觉分类体系**：系统性定义 LLM 生成代码的幻觉类型（API 误用、逻辑短路、
   资源泄漏、安全漏洞等）
2. **静态-动态混合验证**：AST 模式匹配（快）+ 轻量级沙箱执行（准）
3. **CI/CD 原生集成**：结构化反馈 + 一键修正建议

## 仓库结构

- [`literature/`](literature/) — 相关文献 PDF 及文献综述索引（`literature/README.md`）
- [`slides/`](slides/) — 第一次个人汇报 PPT（`.pptx` 源文件 + 导出的 `.pdf`）
