# PRD: 论文自动化修改总控 Skill (Thesis-Refine Orchestrator)

## 1. 产品定位

该 Skill 作为一个 **智能中控台** ，负责调度 `latex-guard`、`academic-polisher` 和 `humanizer` 三个原子能力。其核心目标是：在**完全保护 LaTeX 语法**的前提下，根据**导师意见**对论文内容进行**学术化重塑**与 **去 AI 化处理** 。

---

## 2. 核心工作流设计 (Workflow)

整个 Orchestrator 遵循“ **隔离 -> 处理 -> 还原** ”的流水线模式：

| **阶段**          | **动作**                   | **调用 Skill / 逻辑** | **输出物**         |
| ----------------------- | -------------------------------- | --------------------------- | ------------------------ |
| **Stage 1: 解析** | 分析导师意见，定位原文待修改段落 | LLM Reasoning               | 修改任务清单 (Task List) |
| **Stage 2: 屏蔽** | 提取并锁定 LaTeX 敏感语法        | `latex-guard`(Mask)       | 带有占位符的纯文本       |
| **Stage 3: 优化** | 提升学术语气与逻辑连贯性         | `academic-polisher`       | 学术增强文本             |
| **Stage 4: 拟人** | 调整句式权重，消除 AI 痕迹       | `humanizer`               | 最终修正文本             |
| **Stage 5: 还原** | 将占位符替换回原始 LaTeX 语法    | `latex-guard`(Unmask)     | 合法的 LaTeX 代码        |

---

## 3. 功能需求 (Functional Requirements)

### 3.1 上下文感知修改 (Context-Aware Revision)

* **输入：** 必须同时接收 `Original_Content` (LaTeX) 和 `Advisor_Comments` (String/PDF)。
* **逻辑：** 总控需要先判断：导师意见是针对“全局”还是“特定段落”。如果是特定段落，总控需精准提取该段落进行流水线处理。

### 3.2 链式调用约束

* **顺序性：** 严禁在 `latex-guard` 之前执行任何文本改动。
* **幂等性：** 多次执行同一段落，输出的 LaTeX 结构必须保持一致，不能出现标签嵌套错误。

### 3.3 马来西亚学术规范适配 (Localization)

* **拼写检查：** 默认使用 **British English** (马来西亚论文标准)。
* **引用保护：** 强制锁定 `\cite` 和 `\citep`，确保 `humanizer` 不会修改文献引用的作者顺序。

---

## 4. 技术接口定义 (API & Schema)

### 输入参数 (Input Schema)

**JSON**

```
{
  "project_id": "string",
  "source_latex": "string",
  "advisor_feedback": "string",
  "target_style": "Malaysian_Academic_Standard",
  "options": {
    "intensity": "high", // Humanizer 的强度
    "keep_original_meaning": true
  }
}
```

### 输出参数 (Output Schema)

**JSON**

```
{
  "modified_latex": "string",
  "change_log": [
    {"point": "Fixed passive voice according to feedback", "status": "done"}
  ],
  "ai_score_estimate": "number" // 预估的 AI 写作比例
}
```

---

## 5. 异常处理与边界情况 (Edge Cases)

* **长文本溢出：** 如果论文章节过长（超过 8k tokens），总控 Skill 必须支持 **分段处理（Chunking）** 。
* **LaTeX 语法冲突：** 若 `humanizer` 意外删除了占位符，总控需触发 **Self-Healing** 机制，重新对比原文补齐标签。
* **导师意见模糊：** 若导师意见与原文匹配度低于 30%，总控应返回“提问模式”，要求用户确认修改范围。

---

## 6. 测试用例 (Test Cases)

1. **基础测试：** 修改一个包含 `\begin{equation}` 的段落，确认公式在润色后完全未变。
2. **压力测试：** 输入一段典型的 AI 生成文本（如大量使用 "In conclusion", "Furthermore"），测试 `humanizer` 后 AI 检测率的下降程度。
3. **引用测试：** 确认 `academic-polisher` 不会将 `et al.` 改为其他形式。
