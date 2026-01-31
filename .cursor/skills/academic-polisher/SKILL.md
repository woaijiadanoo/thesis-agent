---
name: academic-polisher
description: |
  Apply Malaysian university academic writing standards to thesis content.
  Use when polishing thesis text for: (1) First-person to passive voice
  conversion, (2) Paragraph length enforcement (minimum 3 sentences),
  (3) Informal to formal vocabulary upgrades, (4) Academic tone improvement.
  Triggers on: "academic style", "passive voice", "formal writing",
  "Malaysian thesis standards", or thesis polish requests mentioning UM/UPM/UTM.
---

# Academic Polisher: Malaysian University Thesis Standards

Apply formal academic writing conventions for Malaysian universities.

## Your Task

When polishing thesis text:

1. **Convert first-person** - Change to passive voice or objective descriptions
2. **Check paragraph length** - Ensure minimum 3 sentences per paragraph
3. **Upgrade vocabulary** - Replace informal words with formal alternatives
4. **Maintain logical flow** - Ensure smooth transitions between ideas
5. **Output complete LaTeX** - Return compilable code

## Important Note

**Use after latex-guard**: This skill assumes LaTeX structural elements (citations, figures, etc.) are already protected. Focus only on prose improvements.

## First-Person Elimination

### Conversion Rules

| First-Person | Convert To |
|--------------|------------|
| I conducted | The experiment was conducted |
| We observed | It was observed that |
| I analyzed | The data were analyzed |
| We propose | This study proposes |
| My research | This research |
| Our findings | The findings |
| I/We found | The results indicate |
| I/We believe | It is believed / Evidence suggests |

### Objective Subjects to Use

- This study / This research
- The analysis / The experiment
- The investigation / The present work
- The proposed method / The findings
- The results / The data

## Paragraph Length Rules

### Minimum: 3 Sentences

Every paragraph MUST have:
1. **Topic sentence** - States the main idea
2. **Supporting content** - Evidence or explanation
3. **Transition/conclusion** - Connects to next idea

### Handling Short Paragraphs

If paragraph has 1-2 sentences:
- **Option A**: Expand with supporting details
- **Option B**: Merge with adjacent paragraph on same topic

### Boundary Case: Exactly 3 Sentences

Acceptable, but consider:
- Can supporting evidence strengthen the argument?
- Is more context needed for clarity?

## Vocabulary Upgrades

### Quick Reference

| Avoid | Use Instead |
|-------|-------------|
| shows | demonstrates, indicates |
| get | obtain, achieve |
| thing | factor, component |
| big/small | significant/negligible |
| a lot of | numerous, substantial |
| look into | investigate, examine |

### Detailed Lists

For comprehensive vocabulary mappings, see [references/vocabulary-upgrades.md](references/vocabulary-upgrades.md).

## Formal Tone Requirements

### Always

- Avoid contractions: "do not" not "don't"
- Use third-person perspective
- Avoid colloquialisms and slang
- Avoid rhetorical questions
- Avoid exclamation marks

### British English Preferred

Most Malaysian universities use British spelling:
- behaviour, analyse, organisation, colour

## Edge Cases

### Exactly 3-Sentence Paragraphs

- Leave as-is if content is complete
- Expand only if argument needs strengthening
- Do not artificially pad content

### Mixed-Language Content

When Malay/Chinese terms appear:
- Italicize non-English terms on first use
- Keep existing translations in parentheses
- Do not remove or modify technical terms in other languages

### Direct Quotations

- First-person in direct quotes is acceptable
- Do not modify quoted material
- Only modify the surrounding text

### Acknowledgments Section

- First-person is acceptable here
- Do not convert "I would like to thank..."

## Malaysian Conventions

For detailed Malaysian university style rules, see [references/malaysia-conventions.md](references/malaysia-conventions.md).

## Output Format

Return complete LaTeX code with improvements:

```latex
\section{Methodology}
\label{sec:methodology}

The experimental methodology was designed to evaluate the 
proposed approach systematically. Data were collected from 
three independent sources to ensure reliability. The analysis 
employed both quantitative and qualitative methods to provide 
comprehensive insights into the research questions.
```

## Process

1. Read input text (assumes LaTeX structure already protected)
2. Identify all first-person pronouns
3. Convert to passive voice or objective descriptions
4. Check each paragraph for minimum 3 sentences
5. Expand or merge short paragraphs
6. Upgrade informal vocabulary
7. Verify formal academic tone throughout
8. Return complete LaTeX code
