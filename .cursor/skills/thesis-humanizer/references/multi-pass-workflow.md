# Multi-Pass Workflow Guide

This reference describes the iterative humanisation process for achieving Turnitin AI detection scores below 10%.

---

## Overview

Single-pass humanisation typically achieves only 60-70% reduction in AI patterns. Multiple targeted passes are required for consistent results.

**Key Insight**: AI patterns interlock. Removing vocabulary issues may reveal structural patterns that were previously masked.

---

## Pass Definitions

### Pass 1: Vocabulary (Highest Impact)

**Target Categories**: vocabulary  
**Expected Reduction**: 40-50% of AI score

**Focus**:
- AI vocabulary words (crucial, delve, foster, enhance)
- Filler phrases (In order to, Due to the fact that)
- Excessive hedging (could potentially possibly)

**Actions**:
1. Scan for words from AI vocabulary list
2. Replace with academic alternatives
3. Remove unnecessary filler phrases
4. Reduce stacked hedging to single qualifiers

**Example**:
```
Before: "Additionally, this research delves into the crucial interplay 
        between privacy and blockchain, highlighting its pivotal role."

After:  "This research examines the relationship between privacy and 
        blockchain."
```

---

### Pass 2: Structure (High Impact)

**Target Categories**: structural  
**Expected Reduction**: 20-30% of remaining patterns

**Focus**:
- Negative parallelisms (Not only...but also)
- Rule of three overuse
- Em dash overuse
- Repetitive sentence patterns

**Actions**:
1. Identify parallel constructions
2. Convert to direct statements
3. Vary list lengths (2, 4, or prose)
4. Replace em dashes with commas/semicolons
5. Vary sentence openings

**Example**:
```
Before: "The framework is not only efficient but also scalable—providing 
        security, privacy, and reliability—while ensuring performance."

After:  "The framework is efficient and scalable. It provides security 
        and privacy while maintaining performance."
```

---

### Pass 3: Transitions (Medium Impact)

**Target Categories**: attribution, promotional (transitions)  
**Expected Reduction**: 10-15% of remaining patterns

**Focus**:
- Formulaic connectors (Furthermore, Additionally, Moreover)
- Vague attributions (Experts argue, Studies show)
- Formulaic challenges sections

**Actions**:
1. Vary or remove formulaic transitions
2. Replace vague attributions with specific citations
3. Rewrite "Despite challenges..." patterns
4. Connect ideas through meaning rather than connectors

**Transition Alternatives**:

| Overused | Alternatives |
|----------|-------------|
| Furthermore | Also, [remove], In addition |
| Additionally | Also, [remove], Moreover |
| Moreover | Also, [remove], Further |
| However | Yet, But, [semicolon instead] |
| Therefore | Thus, So, Consequently |
| Nevertheless | Yet, Still, Even so |

**Example**:
```
Before: "Furthermore, experts argue that blockchain is crucial. 
        Additionally, studies show growing adoption. Moreover, 
        despite challenges, the technology continues to evolve."

After:  "Blockchain adoption has increased significantly since 2020 
        \citep{ieee2024}. Transaction throughput remains a challenge; 
        recent protocols address this through sharding \citep{jones2023}."
```

---

### Pass 4: Organisation (Medium Impact)

**Target Categories**: thesis-specific  
**Expected Reduction**: 5-10% of remaining patterns

**Focus**:
- Repetitive chapter openings
- RQ/RO/RC formula patterns
- Literature review formula
- Methodology formula

**Actions**:
1. Vary chapter introduction verbs
2. Restructure RQ/RO statements
3. Integrate citations more naturally
4. Vary methodology descriptions

**Chapter Opening Variations**:

| Repetitive | Varied |
|------------|--------|
| Chapter 2 presents | Chapter 2 reviews / The literature review examines |
| Chapter 3 presents | The methodology is described in Chapter 3 |
| Chapter 4 presents | Results appear in Chapter 4 / Chapter 4 reports |
| Chapter 5 presents | Chapter 5 analyses / The discussion in Chapter 5 |

**Example**:
```
Before: "Chapter 2 presents the literature review. Chapter 3 presents 
        the methodology. Chapter 4 presents the results."

After:  "Chapter 2 reviews relevant literature on vehicular privacy. 
        The research methodology is described in Chapter 3, while 
        Chapter 4 reports experimental results."
```

---

### Pass 5: Polish (Quality Assurance)

**Target Categories**: all (final check)  
**Expected Reduction**: <5% but catches edge cases

**Focus**:
- Remaining isolated patterns
- Consistency check across document
- Academic formality verification
- Significance stacking

**Actions**:
1. Re-scan for any missed patterns
2. Check paragraph-level consistency
3. Verify academic tone maintained
4. Remove any remaining significance words clustering

**Final Checks**:
- [ ] No more than one significance word per paragraph
- [ ] Consistent terminology throughout
- [ ] All citations preserved
- [ ] No informal expressions remain
- [ ] British spelling throughout

---

## Stop Criteria

Stop iterating when ANY of these conditions are met:

### Condition 1: Target Score Achieved
Turnitin AI Writing detection score below 10%

### Condition 2: No New Patterns
Pass N finds no new patterns to fix

### Condition 3: Stable Density
Pattern density estimate stable for 2 consecutive passes (variation < 0.5 patterns/100 words)

### Condition 4: Diminishing Returns
Pass reduces fewer than 3 patterns

---

## Pattern Density Estimation

Use this metric to estimate AI detection probability without Turnitin access.

### Calculation

```
Density = (Total patterns detected) / (Word count / 100)
```

### Interpretation

| Density | AI Probability | Recommended Action |
|---------|---------------|-------------------|
| >5 patterns/100 words | High | Continue passes |
| 2-5 patterns/100 words | Medium | One more pass recommended |
| <2 patterns/100 words | Low | Likely to pass Turnitin (<10%) |

### Example Calculation

```
Document: 5000 words
Patterns found: 45

Density = 45 / (5000/100) = 45 / 50 = 0.9 patterns/100 words

Result: Low AI probability - likely to pass
```

### Density Tracking

Track density after each pass:

| Pass | Patterns | Words | Density | Change |
|------|----------|-------|---------|--------|
| Initial | 85 | 5000 | 1.7 | - |
| Pass 1 | 45 | 4900 | 0.92 | -0.78 |
| Pass 2 | 28 | 4850 | 0.58 | -0.34 |
| Pass 3 | 20 | 4800 | 0.42 | -0.16 |
| Pass 4 | 18 | 4780 | 0.38 | -0.04 |
| Pass 5 | 17 | 4770 | 0.36 | -0.02 |

**Stop at Pass 5**: Density stable (<0.1 change), below threshold

---

## Quality Checkpoints

### After Each Pass

1. **Verify LaTeX integrity**: All citations, refs, environments intact
2. **Check academic tone**: No informal expressions introduced
3. **Confirm meaning preservation**: Core arguments unchanged
4. **Update change log**: All modifications recorded

### Before Final Submission

1. **Compile LaTeX**: Ensure document compiles without errors
2. **Check references**: All citations still resolve
3. **Review change log**: User approves all modifications
4. **Run Turnitin**: Verify AI score below target

---

## Workflow Summary

```
┌─────────────────────────────────────────────────────────┐
│                    INPUT: LaTeX Chapter                  │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│  Pass 1: VOCABULARY                                      │
│  - AI words, filler phrases, hedging                     │
│  - Expected: 40-50% reduction                            │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│  Pass 2: STRUCTURE                                       │
│  - Parallelisms, rule of three, em dashes               │
│  - Expected: 20-30% reduction                            │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│  Pass 3: TRANSITIONS                                     │
│  - Formulaic connectors, vague attributions             │
│  - Expected: 10-15% reduction                            │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│  Pass 4: ORGANISATION                                    │
│  - Chapter openings, RQ/RO formula, lit review          │
│  - Expected: 5-10% reduction                             │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│  Pass 5: POLISH                                          │
│  - Final check, consistency, remaining patterns         │
│  - Expected: <5% reduction                               │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│  CHECK: Stop criteria met?                               │
│  - Density < 2?                                          │
│  - No new patterns?                                      │
│  - Stable for 2 passes?                                  │
└─────────────────────────────────────────────────────────┘
          │                              │
          │ NO                           │ YES
          ▼                              ▼
    [Continue to                  ┌─────────────────┐
     next pass]                   │ OUTPUT: Clean   │
                                  │ LaTeX + Log     │
                                  └─────────────────┘
```
