---
description: Quick thesis chapter revision - applies LaTeX protection, supervisor feedback, and academic polishing WITHOUT humanizer step.
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Overview

Quick revision pipeline (skips humanizer for faster processing):

```
Input: LaTeX Chapter + Supervisor Comments
            │
            ▼
┌─────────────────────────────────┐
│   Step 1: LOAD CONTEXT          │
│   Read terminology & LaTeX rules│
└─────────────────────────────────┘
            │
            ▼
┌─────────────────────────────────┐
│   Step 2: LATEX-GUARD           │
│   Identify protected elements   │
└─────────────────────────────────┘
            │
            ▼
┌─────────────────────────────────┐
│   Step 3: ADDRESS FEEDBACK      │
│   Apply supervisor modifications│
└─────────────────────────────────┘
            │
            ▼
┌─────────────────────────────────┐
│   Step 4: ACADEMIC-POLISHER     │
│   Formal style compliance       │
└─────────────────────────────────┘
            │
            ▼
        Output: target/{chapter}/{chapter}.tex
```

## Required Inputs

Verify the user has provided:

1. **Supervisor's Comments** - Specific feedback on what to modify
2. **Chapter LaTeX Source** - Via `@filename.tex` attachment or pasted content

If either is missing, ask the user to provide them before proceeding.

## Execution Steps

### Step 1: Load Context

Read the following reference files:

1. **Terminology Reference**: `src/rag/terminology.md`
2. **LaTeX Rules**: `src/rag/latex.md`

### Step 2: Apply LaTeX Guard

Identify ALL protected elements before making changes:

| Category | Patterns |
|----------|----------|
| Citations | `\cite{}`, `\citep{}`, `\citet{}`, `\citeauthor{}`, `\citeyear{}` |
| Cross-refs | `\ref{}`, `\label{}`, `\pageref{}`, `\autoref{}`, `\eqref{}` |
| Acronyms | `\acrshort{}`, `\acrlong{}`, `\acrfull{}` |
| Environments | `figure`, `table`, `equation`, `align`, `algorithm` |
| Math | `$...$`, `\(...\)`, `\[...\]` |
| File paths | `\includegraphics{}`, `\input{}`, `\include{}` |

### Step 3: Address Supervisor Feedback

For each supervisor comment:
1. Locate the relevant section
2. Make the requested modification
3. Ensure new content follows academic style
4. Verify protected elements remain unchanged

### Step 4: Apply Academic Polisher

**4.1 First-Person Elimination**

| Avoid | Use Instead |
|-------|-------------|
| I/We conducted | The experiment was conducted |
| I/We observed | It was observed that |
| I/We propose | This study proposes |

**4.2 Paragraph Length Check**

Every paragraph MUST have at least 3 sentences. Expand or merge short paragraphs.

**4.3 Vocabulary Upgrades**

| Avoid | Use Instead |
|-------|-------------|
| shows | demonstrates, indicates |
| get | obtain, achieve |
| big/small | significant/negligible |

**4.4 British English**

Use British spelling: behaviour, analyse, organisation, optimisation, centralised, utilisation.

### Step 5: Generate Output

**Output Location:**
```
target/{chapter_name}/{chapter_name}.tex
```

**Requirements:**
1. Complete, compilable LaTeX code
2. All protected elements unchanged
3. All supervisor comments addressed
4. Academic style compliance verified

### Step 6: Summary Report

```markdown
## Quick Revision Summary

**Chapter**: [chapter name]
**Output**: target/{chapter}/{chapter}.tex

### Changes Made
- Supervisor comments addressed: [count]
- First-person converted: [count]
- Paragraphs expanded/merged: [count]

### Verification
- [ ] Citations preserved
- [ ] Cross-references preserved
- [ ] Figures/tables unchanged

**Note**: Humanizer step skipped. Run `/thesis.revise` for full pipeline with AI pattern reduction.
```

## Important Rules

1. **NEVER modify** LaTeX structural elements
2. **NEVER add/delete** citations
3. **ALWAYS preserve** environments exactly
4. **ALWAYS use** British English
5. **ALWAYS ensure** 3+ sentences per paragraph

## Skill References

- `.cursor/skills/latex-guard/SKILL.md`
- `.cursor/skills/academic-polisher/SKILL.md`
