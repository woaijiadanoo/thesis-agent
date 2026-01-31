# Thesis Editing Workflow (LaTeX + Supervisor Feedback + Humanizer)

This README explains how to use the skills in this workspace to edit thesis
chapters written in LaTeX. It covers common scenarios such as full revisions
with supervisor feedback, academic polishing, AI writing score reduction, and
targeted humanizer optimization.

## Core Skills and When to Use Them

- `thesis-pipeline`: Full end-to-end workflow. Orchestrates:
  `latex-guard` → `academic-polisher` → `humanizer` (optional).
- `latex-guard`: Protects citations, references, figures, tables, equations,
  math, and file paths. Use whenever touching `.tex` content.
- `academic-polisher`: Academic tone, passive voice, formal wording, paragraph
  structure (minimum 3 sentences).
- `humanizer`: Reduces AI writing signals, improves natural academic flow.

## Global Rules (Always Apply)

- Do not modify `\cite{}` / `\ref{}` / `\label{}` / figure/table/equation blocks.
- Do not add or remove citations unless explicitly requested.
- Preserve all paths in `\includegraphics`, `\input`, `\include`.
- Output must be complete, compilable LaTeX that can replace the original.

---

## Scenario 1: Full Chapter Revision with Supervisor Feedback

### When to use
You have chapter LaTeX plus supervisor comments and want a full revision with
academic polish and optional humanizer.

### Recommended skills
`thesis-pipeline` (includes `latex-guard` + `academic-polisher` + `humanizer`)

### Inputs
- Supervisor feedback (Chinese or English)
- Full LaTeX chapter content (e.g., `sample-chapter.tex`)

### Outputs
- A complete revised LaTeX block, ready to paste back into the file.

### Step-by-step
1. Provide supervisor feedback in text form.
2. Provide the chapter LaTeX content (paste or point to the file).
3. Request the pipeline:
   - "Apply thesis-pipeline with LaTeX protection, academic polish,
     and humanizer. Output full LaTeX."
4. Receive:
   - Modified LaTeX that preserves citations, refs, figures, tables, equations.

---

## Scenario 2: Academic Polishing Only (No Humanizer)

### When to use
You want formal academic tone and structure improvements only.

### Recommended skills
`latex-guard` + `academic-polisher`

### Inputs
- Full LaTeX chapter or section.

### Outputs
- A revised LaTeX block with more formal academic language.

### Step-by-step
1. Provide LaTeX content.
2. Request:
   - "Use latex-guard + academic-polisher. Do not run humanizer."
3. Receive:
   - Academic-polished LaTeX with protected elements unchanged.

---

## Scenario 3: Full Polishing + Humanizer (No Supervisor Feedback)

### When to use
You already have a chapter, want polishing + AI writing reduction, but no
supervisor comments.

### Recommended skills
`thesis-pipeline` with humanizer enabled

### Inputs
- Full LaTeX content.

### Outputs
- Polished and humanized LaTeX.

### Step-by-step
1. Provide LaTeX content.
2. Request:
   - "Apply thesis-pipeline with humanizer. Output full LaTeX."
3. Receive:
   - Revised LaTeX ready to paste.

---

## Scenario 4: AI Writing Score Too High (Targeted Reduction)

### When to use
You ran an AI writing detector and the score is too high.

### Recommended skills
`humanizer` (optionally with `latex-guard` if LaTeX text is provided)

### Inputs
- The high-score paragraphs (LaTeX)
- Optional: AI detector report or flagged sentences

### Outputs
- Revised paragraphs with reduced AI signals.

### Step-by-step
1. Provide the flagged paragraphs in LaTeX form.
2. Indicate:
   - "Reduce AI writing signals only; keep citations/refs unchanged."
3. Receive:
   - Rewritten paragraphs with more natural academic flow.

---

## Scenario 5: Humanizer Result Is Not Good (Second Pass Optimization)

### When to use
Humanizer output still feels unnatural or fails an AI detector.

### Recommended skills
`humanizer` (second pass), optionally with `academic-polisher` afterward

### Inputs
- The humanized LaTeX text that still fails
- Optional: Detector score or feedback

### Outputs
- Further refined text with better naturalness and clarity.

### Step-by-step
1. Provide the humanized output (problematic paragraphs only).
2. Explain:
   - "Humanizer output is still weak; do a second pass, reduce formulaic
     sentence structure."
3. Receive:
   - Improved paragraph(s) with reduced AI patterns.

---

## Scenario 6: Minimal Edit, Preserve Most Text

### When to use
You want only grammar fixes and light academic tone improvements.

### Recommended skills
`latex-guard` + light `academic-polisher`

### Inputs
- LaTeX content to lightly revise.

### Outputs
- Lightly edited LaTeX with minimal changes.

### Step-by-step
1. Provide LaTeX text.
2. Request:
   - "Do minimal edits only, fix grammar and clarity, preserve structure."
3. Receive:
   - Minimal-change LaTeX output.

---

## Scenario 7: Supervisor Wants Specific Paragraph Rewritten

### When to use
Only a single paragraph or section needs rework.

### Recommended skills
`latex-guard` + (`academic-polisher` or `humanizer` depending on need)

### Inputs
- The specific LaTeX paragraph/section
- Supervisor comment for that part

### Outputs
- Updated paragraph only (in LaTeX)

### Step-by-step
1. Provide the paragraph in LaTeX.
2. Provide the supervisor note for this paragraph.
3. Request:
   - "Revise this paragraph only. Keep citations/refs unchanged."
4. Receive:
   - Updated paragraph (LaTeX) to replace in your file.

---

## Scenario 8: Terminology Consistency Pass

### When to use
You want consistent term usage (e.g., "dataset" vs "data set") across a chapter.

### Recommended skills
`latex-guard` + `academic-polisher`

### Inputs
- List of preferred terms
- LaTeX content to normalize

### Outputs
- LaTeX with consistent terminology.

### Step-by-step
1. Provide preferred terminology list.
2. Provide LaTeX content.
3. Request:
   - "Normalize terminology to the list; keep citations/refs unchanged."
4. Receive:
   - Updated LaTeX with consistent terms.

---

## Scenario 9: Output Must Match University Style

### When to use
You need Malaysian university standards (UM/UPM/UTM) style.

### Recommended skills
`academic-polisher` (Malaysian thesis style)

### Inputs
- LaTeX content
- Style requirement (UM/UPM/UTM)

### Outputs
- LaTeX rewritten to match the style.

### Step-by-step
1. Provide LaTeX content.
2. Specify:
   - "Use Malaysian thesis style (UM/UPM/UTM)."
3. Receive:
   - Style-compliant LaTeX output.

---

## Scenario 10: Mixed Content Lines (Prose + References)

### When to use
Lines such as:
"The results in Figure~\ref{fig:results} demonstrate ..."
need polishing but references must remain unchanged.

### Recommended skills
`latex-guard` + `academic-polisher`

### Inputs
- Lines or paragraphs containing mixed prose + refs

### Outputs
- Same refs preserved; only prose updated.

### Step-by-step
1. Provide the mixed lines.
2. Request:
   - "Edit only prose; keep the reference text exactly."
3. Receive:
   - Correctly preserved reference with improved prose.

---

## Scenario 11: Replace the Entire Chapter After Revisions

### When to use
You want a complete replacement block to paste into the `.tex` file.

### Recommended skills
`thesis-pipeline`

### Inputs
- Full chapter LaTeX
- Optional supervisor feedback

### Outputs
- Full revised LaTeX code block

### Step-by-step
1. Provide full LaTeX chapter.
2. Ask:
   - "Return the complete chapter LaTeX only."
3. Receive:
   - Complete, compilable LaTeX block to paste back.

---

## Scenario 12: Section-by-Section Revision

### When to use
Your chapter is large and you want to revise one section at a time.

### Recommended skills
`latex-guard` + `academic-polisher` (+ `humanizer` as needed)

### Inputs
- One section of LaTeX at a time
- Any specific notes for that section

### Outputs
- Revised section in LaTeX

### Step-by-step
1. Provide one section LaTeX.
2. Request:
   - "Revise this section only, return full section LaTeX."
3. Receive:
   - Revised section to paste into the chapter.

---

## Example Request Template (Copy and Fill)

```
[Supervisor feedback]
1) ...
2) ...

[LaTeX content]
\section{...}
...

[Task]
Apply thesis-pipeline with LaTeX protection, academic polish, and humanizer.
Return full revised LaTeX only.
```

