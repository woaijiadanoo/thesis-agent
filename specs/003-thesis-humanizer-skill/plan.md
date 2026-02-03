# Implementation Plan: Thesis Humanizer Skill

**Branch**: `003-thesis-humanizer-skill` | **Date**: 2026-02-03 | **Spec**: [spec.md](./spec.md)  
**Input**: Feature specification from `/specs/003-thesis-humanizer-skill/spec.md`

## Summary

Create a Cursor skill (`thesis-humanizer`) that removes AI-detectable patterns from LaTeX thesis content while preserving academic formality and all structural elements. The skill merges all 24 patterns from the existing `humanizer` skill with academic-specific adaptations, supports multi-pass iterative processing, and generates change logs. Target: Turnitin AI Writing detection <10%.

## Technical Context

**Language/Version**: Markdown (SKILL.md format) + reference files  
**Primary Dependencies**: Existing skills (`latex-guard`, `academic-polisher`, `humanizer` patterns)  
**Storage**: File-based (`.cursor/skills/thesis-humanizer/`)  
**Testing**: Manual validation via Turnitin AI Writing detection  
**Target Platform**: Cursor IDE (Windows, macOS, Linux)  
**Project Type**: Cursor Skill (documentation-based, no compiled code)  
**Performance Goals**: Process a 5000-word chapter in <30 minutes (including all passes)  
**Constraints**: Must work within Cursor's skill loading mechanism; progressive disclosure for context efficiency  
**Scale/Scope**: Single skill with 4 reference files; ~500 lines SKILL.md + ~800 lines references

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Status | Notes |
|-----------|--------|-------|
| Constitution not defined | N/A | Project constitution is template-only; no specific gates to enforce |

**Result**: PASS (no constitution violations)

## Project Structure

### Documentation (this feature)

```text
specs/003-thesis-humanizer-skill/
├── spec.md              # Feature specification
├── plan.md              # This file
├── research.md          # Phase 0 output - pattern research
├── data-model.md        # Phase 1 output - entity definitions
├── quickstart.md        # Phase 1 output - usage guide
└── tasks.md             # Phase 2 output (created by /speckit.tasks)
```

### Source Code (skill files)

```text
.cursor/skills/thesis-humanizer/
├── SKILL.md                          # Main skill instructions (~500 lines)
└── references/
    ├── ai-patterns-academic.md       # All 24+ AI patterns with academic adaptations
    ├── replacement-dictionary.md     # Word/phrase replacement lookup table
    ├── rhythm-techniques.md          # Sentence variation strategies
    └── multi-pass-workflow.md        # Iterative processing guide
```

**Structure Decision**: Cursor skill structure follows established pattern from existing skills (`humanizer`, `latex-guard`, `academic-polisher`). Main SKILL.md contains workflow and quick references; detailed content in `references/` subdirectory for progressive disclosure.

## Design Decisions

### D1: Pattern Merge Strategy

Merge all 24 humanizer patterns into thesis-humanizer with three treatment categories:

| Category | Count | Treatment |
|----------|-------|-----------|
| INHERIT as-is | 15 | Apply directly (#1-10, #12-13, #22-23) |
| ADAPT for academic | 9 | Modify fix strategy (#14-21, #24) |
| REVERSE | 4 | Ignore/invert advice (first person, opinions, casual) |

### D2: Multi-Pass Architecture

```
Pass 1: Vocabulary → Remove AI words (crucial, delve, foster)
Pass 2: Structure → Vary sentence rhythm, break patterns
Pass 3: Transitions → Replace formulaic connectors
Pass 4: Organization → Vary chapter/section openings
Pass 5: Polish → Final academic formality check
```

### D3: LaTeX Protection Mechanism

Delegate to existing `latex-guard` skill for protection. Protected elements:
- Citations: `\cite{}`, `\citep{}`, `\citet{}`
- References: `\ref{}`, `\label{}`
- Environments: figure, table, equation, align, math
- Paths: `\input{}`, `\include{}`, `\includegraphics{}`

### D4: Change Log Format

```markdown
## Change Log - [TIMESTAMP]

| Line | Original | Replacement | Pattern |
|------|----------|-------------|---------|
| 15 | "crucial role" | "important role" | AI vocabulary |
| 23 | "delve into" | "examine" | AI vocabulary |
```

## Phases

### Phase 0: Research (Complete)
- [x] Identify all 24 humanizer patterns
- [x] Classify patterns by academic applicability
- [x] Document successful humanization session patterns

### Phase 1: Design (Complete)
- [x] Define skill file structure
- [x] Define entity model (AI Pattern, Protected Element, Pass, Change Log Entry)
- [x] Document merge strategy
- [x] Create quickstart usage guide

### Phase 2: Implementation (via /speckit.tasks)
- [ ] Create SKILL.md with frontmatter and workflow
- [ ] Create ai-patterns-academic.md reference
- [ ] Create replacement-dictionary.md reference
- [ ] Create rhythm-techniques.md reference
- [ ] Create multi-pass-workflow.md reference
- [ ] Update RULES_SKILLS_CHANGELOG.md

## Complexity Tracking

> No complexity violations - this is a documentation-only skill with no compiled code.

| Aspect | Justification |
|--------|---------------|
| 4 reference files | Progressive disclosure pattern; keeps SKILL.md focused while providing detailed references when needed |
| Merging 24 patterns | Required to match humanizer capability; academic adaptations add thesis-specific value |
