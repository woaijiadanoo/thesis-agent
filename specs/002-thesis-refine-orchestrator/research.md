# Research: thesis-refine-with-latex

**Branch**: `002-thesis-refine-orchestrator` | **Date**: 2026-02-01
**New Skill**: `thesis-refine-with-latex` (LaTeX-specific orchestrator)

## Research Questions

1. How to chunk long LaTeX documents safely?
2. How to detect ambiguous supervisor feedback?
3. How to estimate AI writing score?
4. How to implement self-healing for lost placeholders?

---

## 1. LaTeX Document Chunking Strategy

### Decision: Section-Based Chunking with Paragraph Fallback

### Rationale

LaTeX documents have natural structural boundaries that must be respected. Chunking at arbitrary positions risks breaking environments.

### Strategy

```
Priority 1: Split at \section{} boundaries
Priority 2: Split at \subsection{} boundaries  
Priority 3: Split at paragraph boundaries (double newline)
Priority 4: Split at sentence boundaries (last resort)
```

### Safe Split Points

| Pattern | Safety | Notes |
|---------|--------|-------|
| Before `\section{}` | ✅ Safe | Natural chapter structure |
| Before `\subsection{}` | ✅ Safe | Natural section structure |
| After `\end{figure}` | ✅ Safe | Environment complete |
| After `\end{table}` | ✅ Safe | Environment complete |
| After `\end{equation}` | ✅ Safe | Math block complete |
| Double newline | ⚠️ Conditional | Only if not inside environment |
| Mid-paragraph | ❌ Avoid | Breaks context |

### Context Overlap

- Overlap: 500 tokens between chunks
- Purpose: Maintain coherence for academic-polisher decisions
- Implementation: Include last paragraph of previous chunk as read-only context

### Alternatives Considered

1. **Fixed token splits**: Rejected - breaks LaTeX environments
2. **Sentence-level splits**: Rejected - loses paragraph context for polisher
3. **No chunking (reject long docs)**: Rejected - chapters commonly exceed 8K tokens

---

## 2. Ambiguous Feedback Detection

### Decision: Keyword Overlap Scoring with 30% Threshold

### Rationale

Supervisor feedback often uses shorthand that requires semantic matching to locate target paragraphs.

### Algorithm

```
1. Extract keywords from feedback (nouns, verbs, technical terms)
2. For each paragraph in source:
   - Count keyword matches
   - Score = matches / total_feedback_keywords
3. If max_score < 0.30:
   - Enter clarification mode
   - Present top 3 candidate paragraphs to user
4. If max_score >= 0.30:
   - Proceed with highest-scoring paragraph
```

### Keyword Extraction Rules

| Include | Exclude |
|---------|---------|
| Technical terms | Common words (the, is, a) |
| Section names | Pronouns |
| Method names | Prepositions |
| Specific numbers | Generic modifiers |

### Clarification Mode Output

```
Cannot confidently match feedback to source content.

Feedback: "improve the CNN accuracy section"

Candidate paragraphs:
1. Section 4.2 (score: 0.28) - "The CNN model achieved..."
2. Section 4.3 (score: 0.22) - "Accuracy improvements were..."
3. Section 3.1 (score: 0.18) - "The proposed architecture..."

Please specify which paragraph to modify: [1/2/3]
```

### Alternatives Considered

1. **Semantic embedding similarity**: More accurate but requires external API - rejected for simplicity
2. **10% threshold**: Too strict - would trigger clarification too often
3. **50% threshold**: Too lenient - would allow poor matches

---

## 3. AI Writing Score Estimation

### Decision: Pattern Density Sampling

### Rationale

Full AI detection requires external tools (Turnitin). Skill can estimate based on known patterns.

### Estimation Method

```
1. Sample 3 random paragraphs from output
2. Count AI pattern occurrences (from humanizer pattern list):
   - High-frequency AI words
   - Em dash usage
   - Rule of three patterns
   - Generic conclusions
3. Pattern density = total_patterns / total_sentences
4. Estimated score = pattern_density * calibration_factor
```

### Calibration

Based on humanizer reference data:

| Pattern Density | Estimated AI Score |
|-----------------|-------------------|
| 0.0 - 0.05 | <5% |
| 0.05 - 0.10 | 5-10% |
| 0.10 - 0.20 | 10-20% |
| >0.20 | >20% |

### Warning Threshold

If estimated score >10%, output warning:

```
⚠️ AI Score Warning: Estimated pattern density suggests 
Turnitin AI score may exceed 10% target. Consider:
- Running humanizer again with manual review
- Checking flagged sections for remaining patterns
```

### Alternatives Considered

1. **External API integration**: More accurate but adds dependency - defer to future
2. **No estimation**: User would need to check manually every time - rejected

---

## 4. Self-Healing Mechanism

### Decision: Placeholder Verification with Recovery

### Rationale

The humanizer occasionally modifies text in ways that corrupt placeholders. Recovery prevents data loss.

### Implementation

```
Stage 2 (Mask):
  original_text -> masked_text + placeholder_map
  
Stage 4 (Humanizer):
  masked_text -> humanized_text
  
Stage 4.5 (Verify - NEW):
  For each placeholder in placeholder_map:
    If placeholder NOT in humanized_text:
      Mark as LOST
      Log warning
  
Stage 5 (Heal - NEW):
  For each LOST placeholder:
    Find approximate position using surrounding context
    Reinsert placeholder from placeholder_map
    Log recovery action
    
Stage 6 (Unmask):
  healed_text -> final_latex
```

### Recovery Strategy

1. **Context matching**: Use 20 characters before/after original placeholder position
2. **Fuzzy match**: If exact context not found, search for similar context (edit distance <5)
3. **Append fallback**: If position cannot be determined, append at paragraph end with warning

### Alternatives Considered

1. **Reject corrupted output**: Too disruptive to user workflow
2. **Manual recovery only**: User burden too high
3. **Prevent modification entirely**: Would reduce humanizer effectiveness

---

## Summary of Decisions

| Question | Decision | Confidence |
|----------|----------|------------|
| Chunking | Section-based with paragraph fallback | High |
| Feedback detection | 30% keyword overlap threshold | Medium |
| AI score | Pattern density sampling | Medium |
| Self-healing | Verify + context-based recovery | High |
