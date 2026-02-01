---
name: thesis-refine-with-latex
description: |
  Orchestrate LaTeX thesis revision with full structural protection, chunking, and AI pattern reduction.
  Coordinates latex-guard, academic-polisher, and humanizer for supervisor feedback-based revision.
  Use when: (1) Revising LaTeX thesis chapters with supervisor feedback, (2) Processing .tex files 
  that need citation/reference protection, (3) Long LaTeX documents (>8K tokens) requiring chunking,
  (4) Requests mentioning "thesis refine", "latex revision", "protect citations", (5) User provides
  both LaTeX content and supervisor comments, (6) Target is <10% Turnitin AI detection score.
  Triggers: "thesis refine with latex", "latex thesis revision", "revise latex chapter",
  "process latex with supervisor feedback", "使用 thesis-refine-with-latex".
---

# thesis-refine-with-latex

Coordinate LaTeX thesis revision: feedback analysis → chunking → latex-guard → academic-polisher → humanizer → verify → output.

## Your Task

Process LaTeX thesis content with supervisor feedback through this pipeline:

```
1. FEEDBACK ANALYSIS   → Parse feedback; determine scope (global/specific)
2. CLARIFICATION       → If match confidence <30%, ask user to specify target
3. CHUNKING            → If >8K tokens, split at safe LaTeX boundaries
4. LATEX-GUARD (MASK)  → Protect citations, refs, equations, figures, tables
5. ACADEMIC-POLISHER   → Formal style, passive voice, British English
6. HUMANIZER (high)    → Reduce AI patterns toward <10% target
7. VERIFY & SELF-HEAL  → Check placeholders; recover if lost
8. LATEX-GUARD (UNMASK)→ Restore LaTeX elements
9. OUTPUT              → Return modified_latex + change_log + ai_score_estimate + warnings
```

## Defaults

| Setting | Value | Rationale |
|---------|-------|-----------|
| Input assumption | Overleaf-validated | User confirms LaTeX compiles |
| Language | British English (en-GB) | Malaysian academic standard |
| Humanizer intensity | `high` | Target <10% Turnitin AI |
| Clarification threshold | 30% | Below this, ask user |
| Chunk size | 8,000 tokens | Safe processing limit |
| Context overlap | 500 tokens | Maintain coherence |

## LaTeX Invariants

NEVER modify these elements—they are masked and restored exactly:

- **Citations**: `\cite{}`, `\citep{}`, `\citet{}`, `\autocite{}`, `\parencite{}`
- **References**: `\ref{}`, `\label{}`, `\pageref{}`, `\autoref{}`, `\eqref{}`
- **Environments**: `figure`, `table`, `equation`, `align`, `algorithm`, `lstlisting`
- **Math**: `$...$`, `\(...\)`, `\[...\]`, `$$...$$`
- **Paths**: `\includegraphics{}`, `\input{}`, `\include{}`

See [latex-guard protected patterns](../latex-guard/references/protected-patterns.md) for complete list.

## Feedback Analysis

### Scope Detection

**Global scope** (apply to entire document):
- Keywords: "整章", "全文", "throughout", "overall tone"
- No specific section references

**Specific scope** (apply to matched location):
- Section names: "methodology section"
- Paragraph references: "the CNN accuracy part"
- Quoted text from document

### Edit Intent List

Number each feedback item for tracking:

```
Feedback: "improve clarity in methodology, fix passive voice, make conclusion impactful"

1. [F1] [methodology] Improve clarity
2. [F2] [global] Fix passive voice
3. [F3] [conclusion] Make impactful
```

Each item MUST map to change log entries or explicit skip reason.

## Clarification Mode

When feedback-to-content match < 30%:

```
⚠️ Cannot confidently match feedback to source content.

Feedback: "[text]"
Extracted keywords: [k1], [k2], [k3]

Candidates:
1. Section X.Y (NN%) - "[first 50 chars]..."
2. Section X.Z (NN%) - "[first 50 chars]..."
3. Section W.V (NN%) - "[first 50 chars]..."

Please specify: [1/2/3/all/skip]
```

See [feedback-matching.md](references/feedback-matching.md) for scoring algorithm.

## Chunking

For documents >8K tokens:

1. Split at `\section{}` or `\subsection{}` boundaries
2. Add 500-token overlap from previous chunk
3. Process each chunk through full pipeline
4. Reassemble; remove overlap duplicates
5. Verify: no broken environments, all placeholders restored

See [chunking-strategy.md](references/chunking-strategy.md) for safe split points and edge cases.

## Humanizer Academic Constraints

Override default humanizer behavior for thesis content:

- ✅ Maintain passive voice (academic standard)
- ✅ Keep formal academic tone
- ❌ No first-person ("I", "we")
- ❌ No chatbot artifacts

Focus on: sentence variation, removing formulaic transitions ("Furthermore"), eliminating AI vocabulary, breaking rule-of-three patterns.

## AI Score Estimation

After processing:

1. Sample 3 paragraphs
2. Count AI patterns (AI words, em dashes, rule-of-three, generic conclusions)
3. Calculate: `pattern_density = patterns / sentences`

| Density | Estimate | Status |
|---------|----------|--------|
| 0.0-0.05 | <5% | ✓ |
| 0.05-0.10 | 5-10% | ✓ |
| 0.10-0.20 | 10-20% | ⚠️ Warn |
| >0.20 | >20% | ❌ Re-run |

## Self-Healing

If placeholders lost during humanizer:

1. Context match (20 chars before/after) → HIGH confidence
2. Fuzzy match (edit distance <5) → MEDIUM confidence
3. Paragraph append → LOW confidence (warn user)
4. Document append → VERY LOW (error, manual review)

See [self-healing.md](references/self-healing.md) for recovery strategies.

## Required Output

Every run produces:

### 1. Modified LaTeX

```latex
\section{Results}
\label{sec:results}

The experimental results demonstrate the effectiveness...
\citep{smith2023}. These findings align with \citet{wang2021}.
```

### 2. Change Log

```
## Change Log

Feedback: 3 items
- [F1] improve clarity → 2 changes (done)
- [F2] formal tone → 3 changes (done)
- [F3] fix section → skipped (already meets requirement)

Modifications:
1. [academic_polish] [F1] L15: "We observed" → "It was observed that"
2. [academic_polish] [F2] L23: "shows" → "demonstrates"
3. [humanize] L31: Removed "Furthermore"
4. [humanize] L45: Restructured rule-of-three

Self-healing: None

Summary: 4 modifications | Feedback: 3/3 ✓ | AI: ~7% ✓
```

See [change-log-format.md](references/change-log-format.md) for full format specification.

### 3. AI Score Estimate

```
AI Pattern Analysis: ~7%
Target: <10% | Status: PASS
```

### 4. Warnings (if any)

```
⚠️ Self-Healing: 1 placeholder recovered (context match)
⚠️ AI Score: Section 4.3 has elevated pattern density
```

## Idempotency

- Do NOT double-mask (check for existing `__CITE_NNN__` patterns)
- Do NOT duplicate placeholders
- Repeated runs MUST keep LaTeX structure identical

## Validation Checklist

After processing, verify:

- [ ] All `\cite{}`, `\ref{}`, `\label{}` unchanged
- [ ] All figure/table/equation environments unchanged
- [ ] All math content unchanged
- [ ] No broken LaTeX environments
- [ ] Change log accounts for all modifications
- [ ] AI score estimate provided

## Reference Documents

- [chunking-strategy.md](references/chunking-strategy.md) - Long document handling
- [feedback-matching.md](references/feedback-matching.md) - Clarification logic
- [change-log-format.md](references/change-log-format.md) - Output structure
- [self-healing.md](references/self-healing.md) - Placeholder recovery

## Related Skills

- [latex-guard](../latex-guard/SKILL.md) - LaTeX element protection
- [academic-polisher](../academic-polisher/SKILL.md) - Academic style
- [humanizer](../humanizer/SKILL.md) - AI pattern reduction
- [thesis-pipeline](../thesis-pipeline/SKILL.md) - Generic thesis processing (non-LaTeX)
