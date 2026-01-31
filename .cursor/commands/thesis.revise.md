---
description: Process thesis chapter through complete revision pipeline with supervisor feedback, LaTeX protection, academic polishing, and AI pattern reduction.
handoffs:
  - label: Quick Revision (No Humanizer)
    agent: thesis.revise-quick
    prompt: Process chapter without humanizer step
    send: true
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Overview

This command processes a thesis chapter through the complete revision pipeline:

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
┌─────────────────────────────────┐
│   Step 5: HUMANIZER             │
│   Reduce AI writing patterns    │
└─────────────────────────────────┘
            │
            ▼
        Output: target/{chapter}/{chapter}.tex
```

## Required Inputs

Before starting, verify the user has provided:

1. **Supervisor's Comments** - Specific feedback on what to modify (can be in Chinese or English)
2. **Chapter LaTeX Source** - Either via `@filename.tex` attachment or pasted content

If either is missing, ask the user to provide them before proceeding.

## Execution Steps

### Step 1: Load Context and Reference Files

Load the following reference files:

1. **Terminology Reference**: Read `src/rag/terminology.md`
   - Abbreviations and their first-use locations
   - Key terms and capitalisation rules
   - British English spelling conventions
   - Thesis-specific vocabulary mappings

2. **LaTeX Rules**: Read `src/rag/latex.md`
   - Citation and acronym usage
   - Cross-reference patterns
   - Figure and table formats
   - Special character escaping rules

Keep these references active throughout the entire revision process.

### Step 2: Apply LaTeX Guard (Structure Protection)

Before making ANY text changes, identify and mark ALL protected elements:

**Protected Elements (NEVER MODIFY):**

| Category | Patterns |
|----------|----------|
| Citations | `\cite{}`, `\citep{}`, `\citet{}`, `\citeauthor{}`, `\citeyear{}` |
| Cross-refs | `\ref{}`, `\label{}`, `\pageref{}`, `\autoref{}`, `\eqref{}` |
| Acronyms | `\acrshort{}`, `\acrlong{}`, `\acrfull{}` |
| Environments | `figure`, `table`, `equation`, `align`, `algorithm`, `lstlisting` |
| Math | `$...$`, `\(...\)`, `\[...\]` |
| File paths | `\includegraphics{}`, `\input{}`, `\include{}` |
| URLs | `\url{}`, `\href{}` |

**Editable Content:**
- Paragraph prose outside protected elements
- Section/subsection titles (with caution)
- Caption text (style only, preserve internal references)

### Step 3: Address Supervisor Feedback

Parse and categorise the supervisor's comments:

**Comment Types and Actions:**

| Comment Type | Action |
|--------------|--------|
| "Expand discussion on X" | Add relevant supporting information |
| "Add more detail to Section Y" | Elaborate with specific details |
| "Clarify the methodology" | Restructure for clarity |
| "Strengthen the argument for Z" | Add evidence or reasoning |
| "Rewrite this paragraph" | Complete rewrite while preserving meaning |
| "Add transition/connection" | Add transitional sentences |
| "Remove/reduce content" | Condense while keeping essential points |

For each comment:
1. Locate the relevant section in the LaTeX source
2. Make the requested modification
3. Ensure new content follows academic style
4. Verify all protected elements remain unchanged

### Step 4: Apply Academic Polisher

After addressing supervisor feedback, polish the entire chapter:

**4.1 First-Person Elimination**

| Avoid | Use Instead |
|-------|-------------|
| I conducted | The experiment was conducted |
| We observed | It was observed that |
| I analyzed | The data were analyzed |
| We propose | This study proposes |
| My research | This research |
| Our findings | The findings |

**4.2 Paragraph Length Check**

Every paragraph MUST have at least 3 sentences:
1. **Topic sentence** - States the main idea
2. **Supporting content** - Evidence or explanation
3. **Transition/conclusion** - Connects to next idea

If a paragraph has fewer than 3 sentences:
- **Option A**: Expand with supporting details
- **Option B**: Merge with adjacent paragraph on same topic

**4.3 Vocabulary Upgrades**

| Avoid | Use Instead |
|-------|-------------|
| shows | demonstrates, indicates |
| get | obtain, achieve |
| thing | factor, component |
| big/small | significant/negligible |
| a lot of | numerous, substantial |
| use | employ, utilise, apply |
| good | effective, efficient, optimal |

**4.4 British English Spelling**

Ensure British spelling per Malaysian university standards:
- behaviour, analyse, organisation, colour
- optimisation, centralised, decentralised
- randomisation, utilisation, generalisation

### Step 5: Apply Humanizer (AI Pattern Reduction)

Scan and fix AI writing patterns while maintaining academic tone:

**Priority Patterns to Fix:**

1. **Overused AI Vocabulary**
   - Remove: Additionally, Furthermore, Moreover, Notably
   - Remove: crucial, pivotal, landscape, tapestry, testament
   - Remove: fostering, showcasing, underscoring

2. **Rule of Three Overuse**
   - Avoid forcing ideas into groups of three
   - Break artificial patterns

3. **Filler Phrases**
   - "In order to" → "To"
   - "Due to the fact that" → "Because"
   - "At this point in time" → "Now"
   - "It is important to note that" → (remove entirely or rephrase)

4. **Excessive Hedging**
   - "It could potentially possibly be argued" → "The evidence suggests"

5. **Formulaic Transitions**
   - Vary sentence openers
   - Use varied sentence lengths

**Academic Context Override:**
- KEEP passive voice (do not add "I")
- KEEP formal tone
- KEEP third-person perspective
- Focus ONLY on sentence structure variation and AI vocabulary removal

### Step 6: Generate Output

**Output Location:**
```
target/{chapter_name}/{chapter_name}.tex
```

Examples:
- Chapter 1 → `target/chapter 1/chapter 1.tex`
- Chapter 4 → `target/chapter 4/chapter 4.tex`

**Output Requirements:**
1. Complete, compilable LaTeX code
2. All protected elements unchanged from original
3. All supervisor comments addressed
4. Academic style compliance verified
5. Ready for direct use in Overleaf

### Step 7: Generate Summary Report

After completing the revision, provide a brief summary:

```markdown
## Revision Summary

**Chapter**: [chapter name]
**Output**: target/{chapter}/{chapter}.tex

### Supervisor Comments Addressed
- [ ] Comment 1: [summary of change]
- [ ] Comment 2: [summary of change]
...

### Style Improvements
- First-person instances converted: [count]
- Short paragraphs expanded/merged: [count]
- Vocabulary upgrades applied: [count]
- AI patterns removed: [count]

### Verification
- [ ] All citations preserved
- [ ] All cross-references preserved
- [ ] All figures/tables unchanged
- [ ] British spelling applied
- [ ] Minimum 3 sentences per paragraph

**Notes**: [any concerns or suggestions for user review]
```

## Important Rules

1. **NEVER modify** any LaTeX structural elements (`\cite{}`, `\ref{}`, `\label{}`, environments, etc.)
2. **NEVER add** new citations unless supervisor explicitly requests
3. **NEVER delete** existing citations
4. **ALWAYS preserve** figure, table, and equation content exactly
5. **ALWAYS use** British English spelling
6. **ALWAYS ensure** at least 3 sentences per paragraph
7. **ALWAYS verify** terminology consistency with `src/rag/terminology.md`

## Error Handling

**If supervisor comment is unclear:**
- Ask for clarification before proceeding
- Do not guess at the intended change

**If protected element appears malformed:**
- Preserve it exactly as-is
- Note concern in summary report
- User will verify in Overleaf

**If chapter is mostly figures/tables:**
- Return with minimal prose changes
- Note which areas were editable

## Skill References

This command coordinates the following skills:
- `.cursor/skills/latex-guard/SKILL.md`
- `.cursor/skills/academic-polisher/SKILL.md`
- `.cursor/skills/humanizer/SKILL.md`
- `.cursor/skills/thesis-pipeline/SKILL.md`

## Context References

- `src/rag/terminology.md` - Abbreviations and terminology
- `src/rag/latex.md` - LaTeX formatting rules
