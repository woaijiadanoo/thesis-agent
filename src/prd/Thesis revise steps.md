以下是我修改一章论文的工作流

[输入]

* 导师的意见
* 需要修改的论文

[目的]

按照导师的意见完成论文修改

[使用的工具/流程]

1. 使用 `latex-guard`: 保护 LaTex 引用和标记
2. 按照导师的论文修改要求完成论文修改
3. `使用 academic-polisher` 检查和润色论文内容
4. 使用 `humanizer` 降低 AI 写作痕迹，提升自然学术表达

[输出要求]

- 需要输出可以直接使用的 LaTex 的论文内容
- 输出位置：target/修改的章节名/修改的章节名.tex, 例如修改 Chapter 1, target/Chapter 1/Chapter 1.tex

[规则文件]
src\rag\terminology.md
src\rag\latex.md
