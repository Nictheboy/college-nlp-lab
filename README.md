# NLP Course Project — Topic 9

**From Code Assistants to Code Guardians: Real-Time Hallucination Detection for
AI-Generated Code in CI/CD Pipelines**

课程：NLP（2026 秋）小组作业
题目来源：[openi.pcl.ac.cn/luckh2/nlp26projects](https://openi.pcl.ac.cn/luckh2/nlp26projects)（题目九）
小组成员：李甘、张星烁、连瑾昭

## 题目简介

现有研究主要关注自然语言的事实性幻觉，而"代码幻觉"——LLM 生成的代码看似正确，
实则存在逻辑漏洞、资源泄漏或依赖过时/不存在的 API——检测研究仍属空白。题目九要求
开发一个轻量级代码验证器，集成到 CI/CD 流水线中，在 AI 生成代码被合并前进行
静态分析 + 动态沙箱测试，并在检测覆盖率与执行速度之间取得平衡。

## 当前具体研究方向

在完成文献调研后，我们把切口收窄为一个更具体的问题：**当 AI 生成的代码改动被合并
时，如何让受影响的模块文档和测试同步更新，并判断这种更新是否需要传播到其他关联
模块。** 方法概览：

1. **离线抽取整个仓库的架构**——识别有哪些组件、每个组件对应哪些目录/文件、
   组件之间的依赖关系
2. **diff → 模块归属**——给定一次代码改动，依据架构图判断它属于哪个/哪些模块
3. **模块级 agent 更新**——为受影响模块启动一个 agent，读取该模块已有文档，
   更新文档并同步更新/新增测试
4. **级联传播决策**——agent 依据架构图中的依赖关系，自主判断是否需要对其他
   关联模块也做同样处理

详见 [`slides/`](slides/) 中的汇报材料（第 9-13 页：问题重新聚焦、最相关的已有工作、
方法、创新点对比、研究规划）。

## 仓库结构

- [`literature/`](literature/) — 相关文献 PDF 及文献综述索引（`literature/README.md`）
- [`slides/`](slides/) — 第一次个人汇报 PPT（`.pptx` 源文件 + 导出的 `.pdf`）
