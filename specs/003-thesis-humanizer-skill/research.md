# Research: Thesis Humanizer Skill

**Feature**: 003-thesis-humanizer-skill  
**Date**: 2026-02-03

## Research Questions

### RQ1: What are the 24 humanizer AI patterns?

**Decision**: Categorize patterns into 8 groups for systematic coverage.

**Findings** (from existing `humanizer` skill):

| # | Pattern | Category |
|---|---------|----------|
| 1 | Undue emphasis on significance | Promotional |
| 2 | Undue emphasis on notability | Promotional |
| 3 | Superficial -ing analyses | Promotional |
| 4 | Promotional language | Promotional |
| 5 | Vague attributions | Attribution |
| 6 | Formulaic challenges sections | Attribution |
| 7 | AI vocabulary words | Vocabulary |
| 8 | Copula avoidance | Style |
| 9 | Negative parallelisms | Structural |
| 10 | Rule of three overuse | Structural |
| 11 | Synonym cycling (elegant variation) | Style |
| 12 | False ranges | Style |
| 13 | Em dash overuse | Structural |
| 14 | Boldface overuse | Formatting |
| 15 | Inline-header vertical lists | Formatting |
| 16 | Title case in headings | Formatting |
| 17 | Emojis | Formatting |
| 18 | Curly quotation marks | Formatting |
| 19 | Collaborative communication artifacts | Chatbot |
| 20 | Knowledge-cutoff disclaimers | Chatbot |
| 21 | Sycophantic/servile tone | Chatbot |
| 22 | Filler phrases | Vocabulary |
| 23 | Excessive hedging | Vocabulary |
| 24 | Generic positive conclusions | Style |

**Rationale**: Complete pattern coverage ensures thesis-humanizer matches humanizer's detection capability.

---

### RQ2: Which patterns need academic adaptation?

**Decision**: 15 patterns apply as-is; 9 require academic-specific fixes.

**Findings**:

#### Patterns to INHERIT (15)
Apply standard humanizer fix:
- #1-10: Promotional, attribution, vocabulary, structural patterns
- #12-13: False ranges, em dashes
- #22-23: Filler phrases, hedging

#### Patterns to ADAPT (9)

| # | Pattern | humanizer Fix | Academic Fix |
|---|---------|---------------|--------------|
| 14 | Boldface | Remove all | Keep for RQ/RO/RC labels |
| 15 | Inline lists | Convert to prose | Keep for methodology if appropriate |
| 16 | Title case | Sentence case | Follow university style guide |
| 17 | Emojis | Remove | Remove (already absent in thesis) |
| 18 | Curly quotes | Straight quotes | LaTeX quotes (``...'' or \enquote{}) |
| 19-21 | Chatbot artifacts | Remove | Remove (already absent) |
| 24 | Generic conclusions | Remove | Replace with specific future work |

#### Patterns to REVERSE (4 advice items)

| humanizer Advice | Academic Requirement |
|------------------|---------------------|
| "Add soul" - use first person | Third person/passive voice required |
| "Have opinions" | Objective, evidence-based only |
| "Let mess in" | Clear structure required |
| "Vary with casual asides" | Formal register throughout |

**Rationale**: Academic writing has strict conventions that conflict with general humanization advice.

---

### RQ3: What thesis-specific patterns exist beyond humanizer's 24?

**Decision**: Add 5 thesis-specific patterns (Part H).

**Findings** (from successful Chapter 1 humanization session):

| # | Pattern | Detection | Fix |
|---|---------|-----------|-----|
| H1 | Repetitive chapter openings | "Chapter X presents..." pattern | Vary verbs: covers, addresses, details, reviews |
| H2 | RQ/RO/RC formula | Same structure for each | Vary sentence construction |
| H3 | Literature review formula | "Author (year) found that..." | Integrate citations more naturally |
| H4 | Significance stacking | "crucial", "pivotal", "key" in same paragraph | Use one or none |
| H5 | Methodology formula | "This study employs..." repeated | Use varied introductions |

**Rationale**: These patterns emerged during actual thesis revision and caused Turnitin flags.

---

### RQ4: What is the optimal multi-pass workflow?

**Decision**: 5-pass workflow with diminishing returns check.

**Findings** (from successful humanization session):

```
Pass 1: Vocabulary (highest impact)
        Target: AI words, filler phrases, hedging
        Expected reduction: 40-50% of AI score

Pass 2: Structural (high impact)
        Target: Sentence rhythm, parallel structures
        Expected reduction: 20-30% of remaining

Pass 3: Transitions (medium impact)
        Target: Formulaic connectors
        Expected reduction: 10-15% of remaining

Pass 4: Organization (medium impact)
        Target: Chapter/section patterns
        Expected reduction: 5-10% of remaining

Pass 5: Polish (low impact, quality assurance)
        Target: Final academic formality check
        Expected reduction: <5% but catches edge cases
```

**Stop Criteria**:
- Turnitin AI score <10%
- No new patterns detected in pass
- Pattern density estimate stable for 2 consecutive passes

**Rationale**: Iterative approach proved necessary in actual session; single pass achieved only 60-70% reduction.

---

### RQ5: How to estimate AI pattern density?

**Decision**: Use pattern count per 100 words as density metric.

**Findings**:

| Density | Score | Action |
|---------|-------|--------|
| >5 patterns/100 words | High AI probability | Continue passes |
| 2-5 patterns/100 words | Medium | One more pass recommended |
| <2 patterns/100 words | Low | Likely to pass Turnitin |

**Calculation**:
```
Density = (Total patterns detected) / (Word count / 100)
```

**Rationale**: Provides actionable guidance without requiring Turnitin access during processing.

---

## Alternatives Considered

### Alternative 1: Single comprehensive pass
**Rejected**: Session experience showed single pass insufficient; AI patterns interlock and require layered treatment.

### Alternative 2: Automated pattern detection via regex
**Rejected**: Cursor skills are instruction-based, not programmatic. Detection relies on Claude's language understanding.

### Alternative 3: Separate skill per pattern category
**Rejected**: User experience would suffer; single skill with multi-pass workflow is more cohesive.

### Alternative 4: Extend existing humanizer skill
**Rejected**: Academic constraints are fundamentally incompatible with general humanizer's "add personality" approach. Clean separation is better.
