# Quickstart: LaTeX Thesis Proofreading Skills

**Feature**: 001-latex-thesis-skills  
**Date**: 2026-01-31

## Overview

This project provides three independent Cursor Skills for PhD thesis proofreading:

| Skill | Purpose | When to Use |
|-------|---------|-------------|
| **latex-guard** | Protect LaTeX structure during edits | Always (foundational) |
| **academic-polisher** | Malaysian academic style compliance | Style improvements |
| **humanizer** | Reduce AI writing patterns | After AI-assisted editing |

## Quick Usage

### Single Skill Invocation

Reference your chapter file and request a specific skill:

```
@Chapter_4.tex

Please apply the latex-guard skill to protect all LaTeX structural 
elements while improving the prose in this chapter.
```

Or for academic style:

```
@Chapter_4.tex

Please apply the academic-polisher skill to convert first-person 
pronouns to passive voice and ensure formal academic tone.
```

### Combined Pipeline

For full processing, reference all needed files:

```
@Chapter_4.tex @Supervisor_Comments.pdf

Please process this chapter using the thesis pipeline:
1. Protect LaTeX structure (latex-guard)
2. Apply Malaysian academic style (academic-polisher)
3. Reduce AI patterns (humanizer)

Address the supervisor comments while maintaining all citations.
```

### With Terminology Reference

For cross-chapter consistency, include a terminology file:

```
@Chapter_5.tex @terminology.md

Please polish this chapter following the terminology conventions
in the reference file. Ensure abbreviations match previous chapters.
```

## Skill Descriptions

### latex-guard (Skill A)

**Purpose**: Protect all LaTeX structural elements during text editing.

**Protects**:
- Citations: `\cite{}`, `\citep{}`, `\citet{}`
- References: `\ref{}`, `\label{}`
- Environments: figure, table, equation, algorithm
- Math: `$...$`, `\[...\]`
- File paths: `chapter_X/filename.jpg`

**Input**: LaTeX chapter content  
**Output**: Modified LaTeX with all protected elements intact

### academic-polisher (Skill B)

**Purpose**: Apply Malaysian university academic writing standards.

**Applies**:
- First-person → passive voice conversion
- Paragraph length enforcement (≥3 sentences)
- Informal → formal vocabulary upgrades
- Logical flow improvements

**Input**: LaTeX chapter (after latex-guard)  
**Output**: Academically polished LaTeX

### humanizer (Skill C - Existing)

**Purpose**: Remove AI writing patterns from text.

**Applies**:
- Sentence structure variation
- Formulaic transition replacement
- AI vocabulary word removal
- Natural rhythm and voice

**Input**: Polished text  
**Output**: Human-sounding text

## Terminology Reference File Format

Create a `terminology.md` file for thesis-wide consistency:

```markdown
# Thesis Terminology Reference

## Abbreviations

| Full Form | Abbreviation | First Use Chapter |
|-----------|--------------|-------------------|
| Convolutional Neural Network | CNN | Chapter 2 |
| Natural Language Processing | NLP | Chapter 1 |
| Application Programming Interface | API | Chapter 3 |

## Key Terms

- **deep learning** (not "Deep Learning" or "DL" in prose)
- **dataset** (one word, not "data set")
- **real-time** (hyphenated as adjective)

## Chapter Notes

- Chapter 1: Introduce all core abbreviations
- Chapter 4: First use of CNN architecture details
```

## Common Workflows

### Workflow 1: Quick Grammar Fix

```
@section_4.2.tex

Fix grammar and improve clarity. Protect all citations.
```

### Workflow 2: Supervisor Revision

```
@Chapter_3.tex @supervisor_comments.txt

Address these supervisor comments:
1. "Expand discussion on data preprocessing"
2. "Add more detail to Section 3.2"

Maintain all existing citations and figures.
```

### Workflow 3: Full Chapter Polish

```
@Chapter_5.tex @terminology.md

Full chapter revision:
1. Fix all first-person usage
2. Ensure formal academic tone
3. Expand short paragraphs
4. Humanize any AI-sounding sections

Reference the terminology file for consistency.
```

## Output Format

All skills output complete LaTeX code that can directly replace the original:

```latex
\section{Results and Discussion}
\label{sec:results}

The experimental results demonstrate significant improvements 
in classification accuracy. As shown in Figure~\ref{fig:results}, 
the proposed method achieved 94.5\% accuracy on the benchmark 
dataset \citep{smith2023}...
```

## Validation

After processing, verify in Overleaf:
1. Document compiles without errors
2. All citations resolve correctly
3. All figure/table references work
4. No broken cross-references
