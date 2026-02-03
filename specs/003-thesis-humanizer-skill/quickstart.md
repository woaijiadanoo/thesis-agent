# Quickstart: Thesis Humanizer Skill

**Feature**: 003-thesis-humanizer-skill  
**Date**: 2026-02-03

## Overview

The `thesis-humanizer` skill removes AI-detectable patterns from LaTeX thesis content while maintaining academic formality. It targets Turnitin AI Writing detection scores below 10%.

## Basic Usage

### Invoke the Skill

```
/thesis-humanizer @path/to/chapter.tex
```

Or with output path:

```
/thesis-humanizer @thesis/src/chapter1.tex output to target/chapter1_humanized.tex
```

### Typical Workflow

1. **First Pass**: Run skill on chapter
2. **Review**: Check output and change log
3. **Iterate**: Run additional passes on flagged sections
4. **Validate**: Submit to Turnitin for verification

## Command Patterns

### Full Chapter Processing

```
/thesis-humanizer @thesis/src/chapter1/Chapter1.tex
```
Processes entire chapter with all 5 passes.

### Section-Specific Processing

```
/thesis-humanizer @chapter.tex:50-100
```
Processes only lines 50-100.

### Vocabulary-Only Pass

```
/thesis-humanizer @chapter.tex vocabulary only
```
Targets only AI vocabulary patterns.

### With Change Log Request

```
/thesis-humanizer @chapter.tex with change log
```
Outputs detailed modification record.

## What Gets Changed

### Vocabulary Replacements

| AI Pattern | Academic Alternative |
|------------|---------------------|
| crucial | important |
| delve into | examine, investigate |
| foster | support, encourage |
| leverage | use, employ |
| robust | reliable, effective |
| seamless | smooth, integrated |
| utilize | use |
| groundbreaking | significant, novel |

### Structural Changes

- Varied sentence lengths (mix short declarative with longer explanatory)
- Broken parallel structures (avoid repetitive "Chapter X presents...")
- Replaced formulaic transitions ("Furthermore" → varied connectors)

### What Is NOT Changed

- All `\cite{}`, `\citep{}`, `\citet{}` citations
- All `\ref{}`, `\label{}` cross-references
- Figure, table, and equation environments
- Math content (`$...$`, `\[...\]`)
- LaTeX comments (`%...`)
- File paths (`\input{}`, `\includegraphics{}`)

## Multi-Pass Strategy

### When to Use Multiple Passes

| Situation | Recommended Passes |
|-----------|-------------------|
| First-time processing | All 5 passes |
| Turnitin score 10-20% | 2-3 additional passes |
| Specific section flagged | Targeted pass on section |
| Minor touch-up | Single vocabulary pass |

### Pass Order

1. **Vocabulary**: Replace AI words (highest impact)
2. **Structure**: Vary sentence rhythm
3. **Transitions**: Fix formulaic connectors
4. **Organization**: Vary chapter/section openings
5. **Polish**: Final academic quality check

## Expected Outcomes

### Before Processing

```latex
The rapid proliferation of IoT devices has created crucial challenges
for privacy preservation. This chapter delves into the fundamental
concepts that underpin our proposed framework.
```

### After Processing

```latex
The growth of IoT devices has created important challenges for privacy
preservation. This chapter examines the concepts underlying the
proposed framework.
```

## Troubleshooting

### "No changes needed"

Document may already be sufficiently humanized. Verify with Turnitin.

### Pattern density not decreasing

Try targeting specific pattern categories rather than full passes.

### LaTeX compilation errors after processing

Report issue - protected elements may need adjustment. Restore from original and reprocess with explicit protection.

## Integration with Other Skills

### Recommended Workflow

```
1. academic-polisher  → Ensure formal academic style
2. thesis-humanizer   → Remove AI patterns
3. latex-guard        → Verify structural integrity (automatic)
```

### When to Use thesis-humanizer vs humanizer

| Context | Use |
|---------|-----|
| LaTeX thesis content | thesis-humanizer |
| General writing | humanizer |
| Mixed content | thesis-humanizer (superset) |

## Quick Reference

### Triggers

- `/thesis-humanizer`
- "humanize thesis"
- "reduce AI detection"
- "thesis humanize"

### Key Constraints

- British English (Malaysian university context)
- Third person / passive voice
- Formal academic register
- All LaTeX structures preserved
