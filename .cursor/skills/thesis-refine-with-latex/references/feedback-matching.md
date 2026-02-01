# Feedback Matching: Ambiguous Feedback Detection

This document defines how `thesis-refine-with-latex` matches supervisor feedback to source content and when to request clarification.

## Matching Algorithm

### Step 1: Keyword Extraction

Extract keywords from supervisor feedback:

**Include**:
- Technical terms (CNN, accuracy, methodology)
- Section names (Results, Discussion)
- Method names (classification, training)
- Specific numbers or metrics
- Quoted text from the document

**Exclude**:
- Common words (the, is, a, an, to, for)
- Pronouns (it, this, that, they)
- Prepositions (in, on, at, with)
- Generic modifiers (good, better, more)

### Step 2: Scoring

For each paragraph/section in the source:

```
1. Count keyword matches in paragraph
2. Score = matches / total_feedback_keywords
3. Store score with paragraph reference
```

### Step 3: Confidence Decision

```
If max_score >= 0.30:
    → Proceed with highest-scoring paragraph
    → Log selected target in change log

If max_score < 0.30:
    → Enter clarification mode
    → Present top 3 candidates to user
```

## Clarification Mode

### Prompt Template

```
⚠️ Cannot confidently match feedback to source content.

Feedback: "[original feedback text]"

Extracted keywords: [keyword1], [keyword2], [keyword3]...

Candidate paragraphs:
1. Section X.Y (score: NN%) - "[first 50 chars]..."
2. Section X.Z (score: NN%) - "[first 50 chars]..."
3. Section W.V (score: NN%) - "[first 50 chars]..."

Please specify which paragraph to modify: [1/2/3]
```

### User Response Handling

- Accept: `1`, `2`, `3`, or section name
- "all" or "全部": Apply to all candidates
- "skip" or "跳过": Skip this feedback item
- Custom text: Re-run matching with refined feedback

## Scoring Examples

### High Confidence (>=30%)

```
Feedback: "improve the CNN accuracy results in section 4.2"
Keywords: [CNN, accuracy, results, section 4.2]

Section 4.2 paragraph: "The CNN model achieved 94.5% accuracy..."
Matches: CNN ✓, accuracy ✓, results implied, section 4.2 ✓
Score: 3/4 = 75% → Proceed automatically
```

### Low Confidence (<30%)

```
Feedback: "make it more academic"
Keywords: [academic]

Section 3.1: "The methodology was designed..."
Matches: 0/1 = 0%

Section 4.1: "Results demonstrate..."
Matches: 0/1 = 0%

All scores < 30% → Enter clarification mode
```

## Global vs Specific Scope

### Global Scope Detection

Feedback is global if it contains:
- "整章", "全文", "throughout", "overall"
- "the entire chapter", "all sections"
- No specific section/paragraph references

For global scope:
- Skip paragraph matching
- Apply feedback to entire document
- Log as "scope: global" in change log

### Specific Scope Detection

Feedback is specific if it contains:
- Section names ("methodology section")
- Paragraph identifiers ("the third paragraph")
- Quoted text from document
- Line numbers

For specific scope:
- Run matching algorithm
- Apply only to matched content
- Log as "scope: specific" in change log

## Keyword Extraction Rules

### Technical Terms

Identify domain-specific vocabulary:
- Machine learning: CNN, RNN, accuracy, precision, recall, F1
- Statistics: p-value, significance, correlation, regression
- General academic: hypothesis, methodology, findings, analysis

### Section Detection

Match section references:
- "section 4.2" → find `\section{...}` or `\subsection{...}` with "4.2"
- "the methodology section" → find section with "methodology" in title
- "Chapter 3" → find `\chapter{...}` numbered 3

### Quote Matching

If feedback contains quoted text:
1. Search for exact quote in source
2. If found, score = 100% for that location
3. If not found, use fuzzy matching (edit distance < 5)

## Handling Multiple Feedback Items

When supervisor provides multiple feedback points:

```
Feedback: "improve clarity in methodology, fix passive voice issues, 
and make the conclusion more impactful"

Parsed items:
1. [methodology] Improve clarity → specific scope
2. [global] Fix passive voice issues → global scope
3. [conclusion] Make more impactful → specific scope

Process each item:
- Item 1: Match to methodology section
- Item 2: Apply to all content
- Item 3: Match to conclusion section
```

## Logging Clarification Decisions

When user makes a clarification selection:

```
## Clarification Log

Feedback: "improve the CNN section"
Initial confidence: 28% (below threshold)
Candidates presented: 3
User selection: Section 4.2

→ Proceeding with Section 4.2 based on user clarification
```

This entry MUST appear in the change log.
