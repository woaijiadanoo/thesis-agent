# 论文润色工作流（LaTeX + 导师意见 + Humanizer）

本 README 说明如何使用本仓库的 skills 对 LaTeX 论文内容进行修改、
润色、降 AI 痕迹，并输出可直接替换的完整 LaTeX。
每个场景均附带可直接复制的请求模板，便于快速发起任务。

## 核心 Skills 与适用场景

- `thesis-pipeline`: 全流程编排器，依次执行：
  `latex-guard` → `academic-polisher` → `humanizer`（可选）。
- `latex-guard`: 保护引用、交叉引用、图表/公式环境、数学表达式、路径。
- `academic-polisher`: 学术语气、被动语态、正式用词、段落结构（至少 3 句）。
- `humanizer`: 降低 AI 写作痕迹，提升自然学术表达。

## 全局规则（始终遵守）

- 不修改 `\cite{}` / `\ref{}` / `\label{}` 等结构性命令。
- 不修改 figure/table/equation 等环境内部内容。
- 不新增或删除引用（除非导师明确要求）。
- 保留 `\includegraphics` / `\input` / `\include` 的路径。
- 输出必须是完整可编译 LaTeX，可直接替换原文。

---

## 场景 1：带导师意见的全章修改

### 适用时机
你有完整章节 + 导师修改意见，需要整体修订并学术润色，可选 humanizer。

### 推荐 skills
`thesis-pipeline`

### 输入
- 导师意见（中/英均可）
- 章节 LaTeX 原文（如 `sample-chapter.tex`）

### 输出
- 完整修订后的 LaTeX（可直接替换）

### 操作步骤
1. 提供导师意见文本。
2. 提供完整 LaTeX 章节内容。
3. 请求：
   - “使用 thesis-pipeline，保护结构，学术润色 + humanizer，输出完整 LaTeX。”
4. 获取完整修订后的 LaTeX。

### 请求模板
```
[导师要求文件]（可选）
@path/to/requirements.md

[需要修改的章节]
Chapter 1

[使用的工具/流程]
- thesis-pipeline（latex-guard → academic-polisher → humanizer）

[导师意见]
1) ...
2) ...

[LaTeX 内容]
\chapter{INTRODUCTION}
...

[任务说明]
使用 thesis-pipeline，保护结构，学术润色 + humanizer，
输出完整 LaTeX，输出到 target/ 下，并创建对应章节目录。

[输出要求]
- 输出文件: target/chapter 1/chapter-1.tex
- 章节目录: target/chapter 1/
- 需要保留: \cite{}, \ref{}, \label{}, figure/table/equation 环境内容
```

---

## 场景 2：只做学术润色（不做 Humanizer）

### 适用时机
你只需要正式学术语气与结构改进。

### 推荐 skills
`latex-guard` + `academic-polisher`

### 输入
- 章节或段落 LaTeX

### 输出
- 学术风格润色后的 LaTeX

### 操作步骤
1. 提供 LaTeX 内容。
2. 请求：
   - “仅使用 latex-guard + academic-polisher，不运行 humanizer。”
3. 获取润色后的 LaTeX。

### 请求模板
```
[导师要求文件]（可选）
@path/to/requirements.md

[需要修改的章节/小节]
Chapter 2, Section 2.1

[使用的工具/流程]
- latex-guard + academic-polisher

[LaTeX 内容]
\section{...}
...

[任务说明]
仅使用 latex-guard + academic-polisher，不运行 humanizer。

[输出要求]
- 输出: 仅返回该小节的修订 LaTeX
- 需要保留: \cite{}, \ref{}, \label{}, figure/table/equation 环境内容
```

---

## 场景 3：无导师意见的完整润色 + Humanizer

### 适用时机
已有章节，想直接润色并降低 AI 痕迹。

### 推荐 skills
`thesis-pipeline`（启用 humanizer）

### 输入
- 章节 LaTeX

### 输出
- 润色 + humanizer 后的完整 LaTeX

### 操作步骤
1. 提供 LaTeX 内容。
2. 请求：
   - “使用 thesis-pipeline，启用 humanizer，输出完整 LaTeX。”
3. 获取修订结果。

### 请求模板
```
[导师要求文件]（可选）
@path/to/requirements.md

[需要修改的章节]
Chapter 3

[使用的工具/流程]
- thesis-pipeline（latex-guard → academic-polisher → humanizer）

[LaTeX 内容]
\chapter{...}
...

[任务说明]
使用 thesis-pipeline，启用 humanizer，输出完整 LaTeX，
输出到 target/ 下，并创建对应章节目录。

[输出要求]
- 输出文件: target/chapter 3/chapter-3.tex
- 章节目录: target/chapter 3/
- 需要保留: \cite{}, \ref{}, \label{}, figure/table/equation 环境内容
```

---

## 场景 4：AI Writing 检查过高，需要降分

### 适用时机
AI 检测工具评分过高，需要针对性降 AI 痕迹。

### 推荐 skills
`humanizer`（若是 LaTeX 内容，配合 `latex-guard`）

### 输入
- 被标红段落或检测报告中的句段（LaTeX）
- 可选：检测报告或提示

### 输出
- 降低 AI 痕迹后的段落

### 操作步骤
1. 提供问题段落（LaTeX）。
2. 说明目标：
   - “仅降低 AI 痕迹，引用/交叉引用保持不变。”
3. 获取优化后的段落。

### 请求模板
```
[导师要求文件]（可选）
@path/to/requirements.md

[需要修改的章节]
Chapter 4

[使用的工具/流程]
- humanizer（LaTeX 内容可配合 latex-guard）

[问题段落]
... \cite{...} ... \ref{...} ...

[任务说明]
仅降低 AI 痕迹，引用/交叉引用保持不变。

[输出要求]
- 输出: 仅返回该段落的修订 LaTeX
- 需要保留: \cite{}, \ref{}, \label{}, figure/table/equation 环境内容
```

---

## 场景 5：Humanizer 效果不理想，需要二次优化

### 适用时机
humanizer 后依旧不自然或检测仍高。

### 推荐 skills
`humanizer`（二次优化），必要时再做 `academic-polisher`

### 输入
- 已 humanizer 的段落（问题句段）
- 可选：检测反馈

### 输出
- 更自然的学术表达

### 操作步骤
1. 提供问题段落。
2. 说明：
   - “请二次优化 humanizer，降低模板化表达。”
3. 获取优化结果。

### 请求模板
```
[导师要求文件]（可选）
@path/to/requirements.md

[需要修改的章节]
Chapter 4

[使用的工具/流程]
- humanizer（二次优化）

[已 humanizer 的段落]
...

[任务说明]
请二次优化 humanizer，降低模板化表达。

[输出要求]
- 输出: 仅返回该段落的修订 LaTeX
- 需要保留: \cite{}, \ref{}, \label{}, figure/table/equation 环境内容
```

---

## 场景 6：只做轻量修改（语法与清晰度）

### 适用时机
只需要修正语法、提高清晰度，不大幅改写。

### 推荐 skills
`latex-guard` + 轻度 `academic-polisher`

### 输入
- LaTeX 段落或章节

### 输出
- 少量改动的 LaTeX

### 操作步骤
1. 提供 LaTeX 内容。
2. 请求：
   - “只做最小改动，修语法与清晰度。”
3. 获取轻量改动结果。

### 请求模板
```
[导师要求文件]（可选）
@path/to/requirements.md

[需要修改的章节/小节]
Chapter 5, Section 5.2

[使用的工具/流程]
- latex-guard + 轻度 academic-polisher

[LaTeX 内容]
...

[任务说明]
只做最小改动，修语法与清晰度。

[输出要求]
- 输出: 仅返回该小节的修订 LaTeX
- 需要保留: \cite{}, \ref{}, \label{}, figure/table/equation 环境内容
```

---

## 场景 7：导师要求改某一段或小节

### 适用时机
只需改动某个段落或小节。

### 推荐 skills
`latex-guard` + (`academic-polisher` 或 `humanizer`)

### 输入
- 指定段落或小节（LaTeX）
- 对应导师意见

### 输出
- 该段落/小节的修订 LaTeX

### 操作步骤
1. 提供段落/小节 LaTeX。
2. 提供导师意见。
3. 请求：
   - “只修改该段落，保持引用与结构不变。”
4. 获取更新段落内容。

### 请求模板
```
[导师要求文件]（可选）
@path/to/requirements.md

[需要修改的章节/小节]
Chapter 6, Section 6.3

[使用的工具/流程]
- latex-guard + academic-polisher（或 humanizer）

[导师意见]
1) ...

[段落/小节 LaTeX]
\subsection{...}
...

[任务说明]
只修改该段落，保持引用与结构不变。

[输出要求]
- 输出: 仅返回该段落/小节的修订 LaTeX
- 需要保留: \cite{}, \ref{}, \label{}, figure/table/equation 环境内容
```

---

## 场景 8：术语一致性优化

### 适用时机
需要统一术语（如 dataset vs data set）。

### 推荐 skills
`latex-guard` + `academic-polisher`

### 输入
- 术语规范列表
- 需要统一的 LaTeX 内容

### 输出
- 术语统一后的 LaTeX

### 操作步骤
1. 提供术语表。
2. 提供 LaTeX 内容。
3. 请求：
   - “按术语表统一表达，结构不变。”
4. 获取统一后的内容。

### 请求模板
```
[导师要求文件]（可选）
@path/to/requirements.md

[需要修改的章节]
Chapter 2

[使用的工具/流程]
- latex-guard + academic-polisher

[术语表]
1) dataset -> data set
2) ...

[LaTeX 内容]
...

[任务说明]
按术语表统一表达，结构不变。

[输出要求]
- 输出: 仅返回该内容的修订 LaTeX
- 需要保留: \cite{}, \ref{}, \label{}, figure/table/equation 环境内容
```

---

## 场景 9：符合马来西亚大学写作标准

### 适用时机
需要 UM/UPM/UTM 论文写作风格。

### 推荐 skills
`academic-polisher`

### 输入
- LaTeX 内容
- 学校标准（UM/UPM/UTM）

### 输出
- 符合指定标准的 LaTeX

### 操作步骤
1. 提供 LaTeX 内容。
2. 指定学校标准：
   - “请按 UM/UPM/UTM 风格润色。”
3. 获取风格一致的结果。

### 请求模板
```
[导师要求文件]（可选）
@path/to/requirements.md

[需要修改的章节]
Chapter 1

[使用的工具/流程]
- academic-polisher（UM/UPM/UTM 风格）

[LaTeX 内容]
...

[任务说明]
请按 UM/UPM/UTM 风格润色。

[输出要求]
- 输出: 仅返回该内容的修订 LaTeX
- 需要保留: \cite{}, \ref{}, \label{}, figure/table/equation 环境内容
```

---

## 场景 10：混合句（文字 + 引用/交叉引用）

### 适用时机
一句话里含 `\ref{}` 或 `\cite{}`，需要润色但不能改结构。

### 推荐 skills
`latex-guard` + `academic-polisher`

### 输入
- 含引用/交叉引用的段落

### 输出
- 只改文字，不改结构的 LaTeX

### 操作步骤
1. 提供混合句段。
2. 请求：
   - “只改文字，引用/交叉引用保持完全不变。”
3. 获取结果。

### 请求模板
```
[导师要求文件]（可选）
@path/to/requirements.md

[需要修改的章节]
Chapter 1

[使用的工具/流程]
- latex-guard + academic-polisher

[混合句段]
The results in Figure~\ref{...} demonstrate ... \cite{...}.

[任务说明]
只改文字，引用/交叉引用保持完全不变。

[输出要求]
- 输出: 仅返回该句/段的修订 LaTeX
- 需要保留: \cite{}, \ref{}, \label{}, figure/table/equation 环境内容
```

---

## 场景 11：需要完整替换章节

### 适用时机
你希望一次性粘贴替换整个章节内容。

### 推荐 skills
`thesis-pipeline`

### 输入
- 完整章节 LaTeX
- 可选：导师意见

### 输出
- 完整章节 LaTeX（可直接替换）

### 操作步骤
1. 提供完整章节 LaTeX。
2. 请求：
   - “只输出完整 LaTeX，不要额外说明。”
3. 获取完整替换内容。

### 请求模板
```
[导师要求文件]（可选）
@path/to/requirements.md

[需要修改的章节]
Chapter 7

[使用的工具/流程]
- thesis-pipeline（latex-guard → academic-polisher → humanizer）

[完整章节 LaTeX]
\chapter{...}
...

[任务说明]
只输出完整 LaTeX，不要额外说明。

[输出要求]
- 输出: 完整章节 LaTeX
- 需要保留: \cite{}, \ref{}, \label{}, figure/table/equation 环境内容
- 若需写文件: target/chapter 7/chapter-7.tex
```

---

## 场景 12：分段逐节处理

### 适用时机
章节很大，需要逐节处理以降低风险。

### 推荐 skills
`latex-guard` + `academic-polisher`（可选 `humanizer`）

### 输入
- 单节 LaTeX
- 对应需求

### 输出
- 该节的修订 LaTeX

### 操作步骤
1. 每次提供一个小节内容。
2. 指明需求：
   - “仅处理这一节，输出完整小节 LaTeX。”
3. 获取该节修改内容。

### 请求模板
```
[导师要求文件]（可选）
@path/to/requirements.md

[需要修改的章节/小节]
Chapter 8, Section 8.1

[使用的工具/流程]
- latex-guard + academic-polisher（可选 humanizer）

[单节 LaTeX]
\section{...}
...

[任务说明]
仅处理这一节，输出完整小节 LaTeX。

[输出要求]
- 输出: 仅返回该小节的修订 LaTeX
- 需要保留: \cite{}, \ref{}, \label{}, figure/table/equation 环境内容
```

---
