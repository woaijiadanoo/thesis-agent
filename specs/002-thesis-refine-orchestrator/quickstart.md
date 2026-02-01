# Quickstart: thesis-refine-with-latex

**Branch**: `002-thesis-refine-orchestrator` | **Date**: 2026-02-01

## Overview

The `thesis-refine-with-latex` skill helps PhD students revise LaTeX thesis chapters based on supervisor feedback while preserving all LaTeX structural elements and achieving <10% Turnitin AI detection score.

This skill is specialized for LaTeX content. For non-LaTeX content, use the generic `thesis-pipeline` skill.

---

## When to Use This Skill

| Scenario | Use This Skill |
|----------|---------------|
| LaTeX thesis chapter with citations | ✅ Yes |
| LaTeX chapter with equations/figures | ✅ Yes |
| Long LaTeX chapter (>8K tokens) | ✅ Yes (auto-chunking) |
| Plain text thesis content | ❌ Use `thesis-pipeline` |
| Word document conversion | ❌ Use `thesis-pipeline` |

---

## Basic Usage

### Single Paragraph Revision

```
User: 请根据导师意见修改这段 LaTeX 内容：

导师意见：improve clarity and formal tone

LaTeX内容：
\section{Methodology}
We used CNN to classify images. The results showed that our method works well.
This is because CNN is good at finding patterns. \citep{smith2023}
```

**Expected Output**: Revised LaTeX with formal academic tone, all citations preserved.

---

### Full Chapter Processing

```
User: 请使用 thesis-refine-with-latex 处理整个章节，导师要求提升学术性：

[粘贴完整的 .tex 章节内容]
```

The skill will:
1. Detect this is LaTeX content requiring protection
2. Split long chapters into chunks at section boundaries
3. Process each chunk through the pipeline
4. Reassemble and verify integrity

---

## Pipeline Stages

```
Input: LaTeX Chapter + Supervisor Comments
                    │
                    ▼
    ┌───────────────────────────────┐
    │  1. FEEDBACK ANALYSIS         │
    │  Match comments to paragraphs │
    └───────────────────────────────┘
                    │
                    ▼ (if ambiguous)
    ┌───────────────────────────────┐
    │  2. CLARIFICATION (optional)  │
    │  Ask user to specify target   │
    └───────────────────────────────┘
                    │
                    ▼ (if >8K tokens)
    ┌───────────────────────────────┐
    │  3. CHUNKING                  │
    │  Split at section boundaries  │
    └───────────────────────────────┘
                    │
                    ▼
    ┌───────────────────────────────┐
    │  4. LATEX-GUARD (MASK)        │
    │  Protect citations, refs, etc │
    └───────────────────────────────┘
                    │
                    ▼
    ┌───────────────────────────────┐
    │  5. ACADEMIC-POLISHER         │
    │  Passive voice, formal vocab  │
    └───────────────────────────────┘
                    │
                    ▼
    ┌───────────────────────────────┐
    │  6. HUMANIZER (high)          │
    │  Reduce AI patterns (<10%)    │
    └───────────────────────────────┘
                    │
                    ▼
    ┌───────────────────────────────┐
    │  7. VERIFY & SELF-HEAL        │
    │  Check placeholder integrity  │
    │  Recover if needed            │
    └───────────────────────────────┘
                    │
                    ▼
    ┌───────────────────────────────┐
    │  8. LATEX-GUARD (UNMASK)      │
    │  Restore LaTeX elements       │
    └───────────────────────────────┘
                    │
                    ▼
           Output: Polished LaTeX
                 + Change Log
                 + AI Score Estimate
```

---

## Skill Comparison

| Feature | thesis-refine-with-latex | thesis-pipeline |
|---------|-------------------------|-----------------|
| LaTeX protection | ✅ Full (mask/unmask) | ✅ Basic |
| Long document chunking | ✅ Section-based | ❌ No |
| Self-healing | ✅ Placeholder recovery | ❌ No |
| Ambiguous feedback | ✅ Clarification mode | ❌ No |
| Change log | ✅ Structured | ❌ No |
| AI score estimate | ✅ Pattern density | ❌ No |
| Non-LaTeX support | ❌ No | ✅ Future |

---

## Handling Long Chapters

For chapters exceeding 8,000 tokens:

1. **Automatic chunking** at `\section{}` or `\subsection{}` boundaries
2. **Context overlap** (500 tokens) ensures coherent processing
3. **Seamless reassembly** preserves document structure

Example output for chunked processing:

```
Processing chapter (15,234 tokens)...
  Chunk 1/3: Section 4.1-4.2 (5,102 tokens) ✓
  Chunk 2/3: Section 4.3-4.4 (5,890 tokens) ✓
  Chunk 3/3: Section 4.5 (4,742 tokens) ✓
Reassembling... ✓
All 23 LaTeX elements preserved.
```

---

## Ambiguous Feedback Handling

If supervisor feedback doesn't clearly match a specific paragraph:

```
⚠️ Cannot confidently match feedback to source content.

Feedback: "improve the CNN accuracy section"

Candidate paragraphs:
1. Section 4.2 (score: 28%) - "The CNN model achieved..."
2. Section 4.3 (score: 22%) - "Accuracy improvements were..."
3. Section 3.1 (score: 18%) - "The proposed architecture..."

Please specify which paragraph to modify: [1/2/3]
```

---

## Output Format

### Revised LaTeX

```latex
\section{Results and Discussion}
\label{sec:results}

The experimental results demonstrate the effectiveness of the 
proposed methodology. As illustrated in Figure~\ref{fig:results}, 
the classification accuracy achieved 94.5\% on the benchmark 
dataset \citep{smith2023}. These findings align with previous 
research conducted by \citet{wang2021}, who reported similar 
performance improvements.
```

### Change Log

```
## Change Log

1. [academic_polish] Line 15: "We observed" → "It was observed that"
2. [academic_polish] Line 23: "shows" → "demonstrates"
3. [humanize] Line 31: Removed "Furthermore" sentence opener
4. [humanize] Line 45: Restructured rule-of-three pattern
5. [expand] Line 52: Added supporting sentence per supervisor feedback

Status: 5 modifications | All feedback addressed: ✓
```

### AI Score Estimate

```
AI Pattern Analysis:
  - High-frequency AI words: 2 found
  - Em dash usage: 0 found
  - Rule-of-three patterns: 0 found (fixed)
  - Generic conclusions: 0 found

Estimated Turnitin AI Score: ~7% ✓
Target: <10% | Status: PASS
```

---

## Self-Healing Notifications

```
⚠️ Self-Healing Applied:
  - 1 placeholder recovered at line 89
  - Original: \citep{jones2022}
  - Recovery method: Context matching
  
All LaTeX elements verified intact.
```

---

## Tips for Best Results

1. **Provide specific feedback**: "improve clarity in methodology section" works better than "needs improvement"

2. **Use Overleaf-validated LaTeX**: Ensure your content compiles before processing

3. **Mention this skill explicitly**: Say "使用 thesis-refine-with-latex" for complex LaTeX chapters

4. **Review change log**: Use the change log to verify all supervisor feedback was addressed

5. **Check AI score**: If estimate exceeds 10%, review flagged sections manually
