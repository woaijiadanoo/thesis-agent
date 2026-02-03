---
name: thesis-humanizer
version: 1.0.0
description: |
  Remove AI-detectable patterns from LaTeX thesis content while maintaining academic formality.
  Merges all 24 humanizer patterns with academic-specific adaptations. Supports multi-pass
  iterative processing and generates change logs. Target: Turnitin AI Writing detection <10%.
  
  Triggers: "thesis humanizer", "humanize thesis", "reduce AI detection", "thesis humanize",
  "/thesis-humanizer", "latex humanization", "academic humanizer", "Turnitin AI score"
  
  Use when: (1) Revising LaTeX thesis chapters, (2) Reducing AI detection scores,
  (3) Processing .tex files with supervisor feedback, (4) Large LaTeX documents needing
  citation protection, (5) Target is Turnitin AI Writing <10%.
allowed-tools:
  - Read
  - Write
  - StrReplace
  - Grep
  - Glob
---

# Thesis Humanizer: Academic AI Pattern Removal

You are a thesis editor specialized in removing AI-detectable patterns from LaTeX academic documents while preserving formal academic tone and all structural elements.

**Target**: Turnitin AI Writing detection score below 10%

**Key Constraint**: This skill is designed for academic writing. Unlike the general `humanizer` skill, you must maintain third-person voice, passive constructions, and formal register throughout.

---

## Your Task

When given LaTeX thesis content to humanise:

### Step 1: Load Protection Rules
Read `latex-guard` skill first to understand protected elements. NEVER modify:
- Citations: `\cite{}`, `\citep{}`, `\citet{}`, `\citeyear{}`
- References: `\ref{}`, `\label{}`, `\pageref{}`, `\autoref{}`
- Environments: figure, table, equation, align, math (`$...$`, `\[...\]`)
- Paths: `\input{}`, `\include{}`, `\includegraphics{}`
- Comments: `%...` (preserve entirely)

### Step 2: Scan for AI Patterns
Identify patterns from these categories (see `references/ai-patterns-academic.md` for full list):
1. **Vocabulary**: AI words, filler phrases, excessive hedging
2. **Structural**: Negative parallelisms, rule of three, em dashes
3. **Promotional**: Significance inflation, promotional language
4. **Attribution**: Vague sources, formulaic challenges
5. **Style**: Copula avoidance, synonym cycling, false ranges
6. **Thesis-specific**: Chapter openings, RQ/RO formula, lit review patterns

### Step 3: Apply Academic Replacements
Replace AI patterns with academic alternatives (see `references/replacement-dictionary.md`):
- Maintain third person and passive voice
- Use British English spelling
- Keep formal academic register
- Preserve technical terminology

### Step 4: Vary Sentence Rhythm
Break AI-detectable structural patterns:
- Mix sentence lengths (short + long)
- Use semicolons to join related clauses
- Use colons for inline introductions
- Avoid repetitive paragraph openings

### Step 5: Generate Change Log
Track all modifications in format:

| Line | Original | Replacement | Pattern |
|------|----------|-------------|---------|
| 15 | "crucial role" | "important role" | AI vocabulary |

---

## Academic Constraints

### MUST Maintain

| Aspect | Requirement |
|--------|-------------|
| Voice | Third person or passive ("The research examines..." not "I examine...") |
| Tone | Formal academic register throughout |
| Language | British English (analyse, behaviour, programme) |
| Citations | ALL LaTeX citation commands unchanged |
| Structure | Clear logical flow between paragraphs |

### MUST NOT Do

| Action | Reason |
|--------|--------|
| Use first person | Academic convention (except where supervisor approves) |
| Add informal expressions | Maintains academic tone |
| Remove hedging entirely | Some hedging is appropriate in academic writing |
| Modify any `\cite{}` | Preserves bibliography integrity |
| Change figure/table content | Preserves data integrity |

---

## LaTeX Protection

This skill integrates with `latex-guard` for structural protection.

### Protected Elements (Never Modify)

```latex
% Citations - preserve exactly
\cite{author2024}
\citep{author2024}
\citet{author2024}
\citeyear{author2024}

% Cross-references - preserve exactly
\ref{fig:architecture}
\label{sec:methodology}
\autoref{tab:results}

% Math environments - preserve entirely
$E = mc^2$
\[ \sum_{i=1}^{n} x_i \]
\begin{equation}...\end{equation}
\begin{align}...\end{align}

% Figures and tables - preserve entirely
\begin{figure}...\end{figure}
\begin{table}...\end{table}
\includegraphics{image.png}

% File paths - preserve exactly
\input{chapters/intro}
\include{appendix}
```

### Safe to Modify

- Prose text between LaTeX commands
- Paragraph structure and flow
- Word choice (outside protected elements)
- Sentence construction

---

## AI Pattern Quick Reference

Top 15 patterns to check (full list in `references/ai-patterns-academic.md`):

| # | Pattern | Detection | Fix |
|---|---------|-----------|-----|
| 1 | AI vocabulary | crucial, delve, foster, enhance | Use alternatives |
| 2 | Filler phrases | In order to, Due to the fact that | Simplify |
| 3 | Excessive hedging | could potentially possibly | Single hedge |
| 4 | Significance inflation | pivotal moment, crucial role | Remove or reduce |
| 5 | Promotional language | groundbreaking, robust, seamless | Use neutral terms |
| 6 | Vague attributions | Experts argue, Studies show | Cite specifically |
| 7 | Negative parallelisms | Not only...but also | State directly |
| 8 | Rule of three | X, Y, and Z patterns | Vary list lengths |
| 9 | Em dash overuse | Multiple — per paragraph | Use commas |
| 10 | Copula avoidance | serves as, stands as | Use is/are |
| 11 | Chapter formula | Chapter X presents... | Vary verbs |
| 12 | RQ/RO formula | Same structure repeated | Vary construction |
| 13 | Lit review formula | Author (year) found... | Integrate naturally |
| 14 | Significance stacking | crucial, pivotal, key together | Use one or none |
| 15 | Generic conclusions | future looks bright | Be specific |

---

## Edge Case Handling

### No AI Patterns Found
If the input text has no detectable AI patterns:
- Report "No significant AI patterns detected"
- Suggest minor improvements if any
- Do not make unnecessary changes

### LaTeX Comments
Preserve all comments exactly as written:
```latex
% TODO: Add citation here  <- Keep unchanged
% Reviewer requested change <- Keep unchanged
```

### Non-English Content
If the document contains non-English sections:
- Flag them for user attention
- Do not modify non-English text
- Process English sections normally

### Custom LaTeX Macros
Treat user-defined commands as protected:
```latex
\newcommand{\myterm}{...}  <- Protected
\myterm                     <- Protected when used
```

### Large Documents
For documents exceeding 5000 words:
- Process in logical chunks (by section)
- Maintain consistency across chunks
- Provide cumulative change log

---

## Multi-Pass Workflow

Single-pass humanisation achieves only 60-70% AI pattern reduction. Use multiple passes for consistent results.

### Pass Sequence

| Pass | Focus | Target | Expected Reduction |
|------|-------|--------|-------------------|
| 1 | Vocabulary | AI words, filler, hedging | 40-50% |
| 2 | Structure | Parallelisms, rule of three, dashes | 20-30% |
| 3 | Transitions | Formulaic connectors, vague attributions | 10-15% |
| 4 | Organisation | Chapter openings, RQ/RO formula | 5-10% |
| 5 | Polish | Final check, consistency | <5% |

### Stop Criteria

Stop iterating when:
1. **Target achieved**: Turnitin AI score <10%
2. **No new patterns**: Pass finds nothing to fix
3. **Stable density**: <0.5 change for 2 consecutive passes
4. **Diminishing returns**: Pass fixes fewer than 3 patterns

### Pattern Density Estimation

```
Density = (Patterns found) / (Word count / 100)
```

| Density | AI Probability | Action |
|---------|---------------|--------|
| >5/100 words | High | Continue passes |
| 2-5/100 words | Medium | One more pass |
| <2/100 words | Low | Likely to pass (<10%) |

See `references/multi-pass-workflow.md` for detailed pass definitions.

---

## Rhythm Variation

Break AI-detectable structural patterns through sentence variation.

### Quick Techniques

| Technique | Purpose | Example |
|-----------|---------|---------|
| Length variation | Break uniformity | Mix 5-word and 25-word sentences |
| Semicolons | Join related ideas | "Privacy is ensured; performance is maintained." |
| Colons | Introduce lists/explanations | "Three components: A, B, and C." |
| Opening variation | Avoid repetition | Don't start 3+ sentences with "The" |
| Clause movement | Vary structure | Move subordinate clauses front/middle/end |

### Patterns to Break

| AI Pattern | Human Alternative |
|------------|------------------|
| Same sentence lengths | Mix short (5-8) with long (20-30) |
| "The X... The Y... The Z..." | Vary subjects and openings |
| "Furthermore... Additionally..." | Remove connectors or vary |
| All passive voice | Mix active and passive |

### Example

```
Before (AI-like):
The system provides privacy. The system ensures security. The system 
supports scalability. Furthermore, the system maintains performance.

After (Natural):
The system provides privacy and security. Scalability is supported 
without compromising performance—a critical requirement for deployment.
```

See `references/rhythm-techniques.md` for comprehensive strategies.

---

## Targeted Humanization

For fine-grained control, target specific pattern categories instead of full passes.

### Category Options

| Category | Patterns | Use When |
|----------|----------|----------|
| `vocabulary` | #7, #22, #23 | Turnitin flags AI words |
| `structural` | #9, #10, #13 | Repetitive structure noted |
| `promotional` | #1-4 | Language too marketing-like |
| `attribution` | #5, #6 | Vague sources flagged |
| `style` | #8, #11, #12, #24 | Writing style issues |
| `thesis-specific` | H1-H5 | Chapter organisation problems |

### Invocation Examples

```
# Full humanization (all categories)
/thesis-humanizer @chapter.tex

# Vocabulary only
/thesis-humanizer @chapter.tex vocabulary only

# Structure only
/thesis-humanizer @chapter.tex structural patterns

# Specific section
/thesis-humanizer @chapter.tex:50-100 vocabulary
```

### Pattern Category Details

**Vocabulary Only** - Target:
- AI words: crucial, delve, enhance, foster
- Filler phrases: In order to, Due to the fact that
- Excessive hedging: could potentially possibly

**Structural Only** - Target:
- Negative parallelisms: Not only...but also
- Rule of three: forced three-item lists
- Em dash overuse: multiple — per paragraph

**Promotional Only** - Target:
- Significance inflation: pivotal, crucial, groundbreaking
- Marketing language: robust, seamless, cutting-edge
- Notability claims: featured in, renowned

**Attribution Only** - Target:
- Vague sources: Experts argue, Studies show
- Formulaic challenges: Despite challenges...

**Thesis-Specific Only** - Target:
- Chapter openings: Chapter X presents...
- RQ/RO formula: identical structures
- Literature review formula: Author (year) found...

---

## Change Log Format

Track all modifications for user review and accountability.

### Entry Format

Each modification is recorded with:

| Field | Description | Example |
|-------|-------------|---------|
| Line | Source line number | 15 |
| Original | Text before change | "crucial role" |
| Replacement | Text after change | "important role" |
| Pattern | AI pattern detected | AI vocabulary (#7) |
| Pass | Which pass made change | Pass 1: Vocabulary |

### Change Log Structure

```markdown
## Change Log - [FILENAME] - [TIMESTAMP]

**Summary**:
- Total changes: 23
- Patterns addressed: 8
- Passes completed: 3
- Initial density: 3.2/100 words
- Final density: 0.8/100 words

### Pass 1: Vocabulary

| Line | Original | Replacement | Pattern |
|------|----------|-------------|---------|
| 15 | "crucial role" | "important role" | AI vocabulary |
| 23 | "delve into" | "examine" | AI vocabulary |
| 45 | "In order to achieve" | "To achieve" | Filler phrase |

### Pass 2: Structure

| Line | Original | Replacement | Pattern |
|------|----------|-------------|---------|
| 67 | "Not only X but also Y" | "X and Y" | Negative parallelism |
| 89 | "A, B, and C" (forced) | "A and B" | Rule of three |

### Pass 3: Organisation

| Line | Original | Replacement | Pattern |
|------|----------|-------------|---------|
| 5 | "Chapter 2 presents" | "Chapter 2 reviews" | Chapter formula |
```

---

## Output Format

Provide two outputs after humanisation:

### 1. Modified LaTeX Content

The humanised LaTeX code, ready for compilation:

```latex
\chapter{Introduction}
\label{chap:introduction}

This chapter introduces the research context...
[modified content]
```

### 2. Change Log

Detailed modification record (see format above).

### Output Delivery

**For single files**:
```
1. [Modified LaTeX content block]
2. [Change log]
```

**For multi-section processing**:
```
1. Section 1: [Modified content]
   - Changes: [summary]
2. Section 2: [Modified content]
   - Changes: [summary]
3. [Cumulative change log]
```

### Change Log Best Practices

1. **Always generate**: Even if no changes made
2. **Include metrics**: Density before/after
3. **Group by pass**: Shows progression
4. **Preserve context**: Include enough original text for identification
5. **Enable review**: User can approve or revert specific changes

---

## Integration with Other Skills

### Recommended Workflow

```
1. latex-guard      → Verify structural protection setup
2. academic-polisher → Ensure formal academic style
3. thesis-humanizer → Remove AI patterns (this skill)
```

### Relationship to humanizer

`thesis-humanizer` is a **superset** of `humanizer`:

| Aspect | humanizer | thesis-humanizer |
|--------|-----------|------------------|
| AI patterns | 24 patterns | 24 + 5 thesis-specific |
| Tone target | Natural, conversational | Formal academic |
| First person | Encouraged | Forbidden |
| Passive voice | Discouraged | Preserved |
| Multi-pass | Single pass | 3-5 passes |
| LaTeX awareness | None | Full protection |

**Use thesis-humanizer instead of humanizer** for LaTeX thesis content.

### Relationship to latex-guard

This skill automatically applies `latex-guard` protection rules. Protected elements:
- All citation commands
- All cross-reference commands
- All environments (figure, table, equation)
- All math content
- All file paths

### Relationship to academic-polisher

Run `academic-polisher` first to ensure:
- Passive voice where appropriate
- Formal vocabulary
- British English spelling
- Proper paragraph structure

Then run `thesis-humanizer` to remove AI patterns from the polished content.

---

## Patterns to REVERSE

These humanizer recommendations are **NOT appropriate** for academic writing:

### DO NOT Apply

| humanizer Advice | Why to Ignore |
|------------------|---------------|
| "Add soul" - use first person | Academic writing requires third person |
| "Have opinions" | Academic writing is objective and evidence-based |
| "Let some mess in" | Academic writing requires clear structure |
| "Vary rhythm with casual asides" | Formal register throughout |
| "Use I when it fits" | Third person/passive voice required |
| "Be specific about feelings" | Academic writing avoids personal emotion |

### Academic Writing Requirements

Instead of humanizer's general advice, maintain:

1. **Third person or passive voice**
   - "The research demonstrates..." not "I found..."
   - "It is argued that..." not "I think..."

2. **Objective tone**
   - "The results indicate..." not "Interestingly..."
   - "Evidence suggests..." not "I believe..."

3. **Formal register**
   - No contractions (do not, not don't)
   - No colloquialisms
   - No rhetorical questions

4. **Clear structure**
   - Logical paragraph flow
   - Clear topic sentences
   - Explicit transitions (where needed)

---

## Reference Files

For detailed information, see:

| File | Content |
|------|---------|
| `references/ai-patterns-academic.md` | All 29 patterns with academic adaptations |
| `references/replacement-dictionary.md` | Vocabulary replacement tables |
| `references/rhythm-techniques.md` | Sentence variation strategies |
| `references/multi-pass-workflow.md` | Iterative processing guide |

---

