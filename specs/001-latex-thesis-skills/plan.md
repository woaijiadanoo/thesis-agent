# Implementation Plan: LaTeX Thesis Proofreading Skills

**Branch**: `001-latex-thesis-skills` | **Date**: 2026-01-31 | **Spec**: [spec.md](spec.md)
**Input**: Feature specification from `/specs/001-latex-thesis-skills/spec.md`

## Summary

Build a modular set of Cursor Skills for PhD thesis proofreading that protects LaTeX structure while enabling academic style compliance and AI writing pattern reduction. Leverage the existing humanizer skill and create two new skills (LaTeX Guard, Academic Polisher) following the established skill-creator patterns.

## Technical Context

**Language/Version**: Markdown (SKILL.md files), Python 3.x (optional helper scripts)  
**Primary Dependencies**: Cursor IDE Skills system, existing humanizer skill  
**Storage**: N/A (Skills are prompt-based, no persistent storage)  
**Testing**: Manual validation with sample LaTeX chapters  
**Target Platform**: Cursor IDE on Windows/macOS/Linux  
**Project Type**: Cursor Skills (prompt engineering + reference files)  
**Performance Goals**: Process single chapter in <10 minutes (including user review)  
**Constraints**: Skills must work independently and in pipeline mode  
**Scale/Scope**: Chapter-level processing, optional thesis-wide terminology file

## Constitution Check

*GATE: Constitution template not customized for this project - N/A*

This project creates Cursor Skills (prompt-based AI guidance), not traditional software. Standard constitution gates for testing, CI/CD, and code architecture do not apply. Quality is ensured through:
- Following established skill-creator patterns
- Leveraging existing humanizer skill structure
- Manual validation with sample LaTeX content

## Project Structure

### Documentation (this feature)

```text
specs/001-latex-thesis-skills/
├── plan.md              # This file
├── research.md          # Phase 0 output (skill patterns research)
├── data-model.md        # Phase 1 output (protected elements taxonomy)
├── quickstart.md        # Phase 1 output (usage guide)
└── tasks.md             # Phase 2 output (/speckit.tasks command)
```

### Source Code (repository root)

```text
.cursor/
├── rules/                          # Existing rules (already populated)
│   ├── thesis-writing-standards.mdc
│   ├── academic-proofreading.mdc
│   ├── latex-thesis-format.mdc
│   └── ...
└── skills/
    ├── humanizer/                  # EXISTING - Skill C (leverage as-is)
    │   ├── SKILL.md
    │   ├── README.md
    │   └── WARP.md
    ├── latex-guard/                # NEW - Skill A
    │   ├── SKILL.md
    │   └── references/
    │       └── protected-patterns.md
    ├── academic-polisher/          # NEW - Skill B
    │   ├── SKILL.md
    │   └── references/
    │       ├── vocabulary-upgrades.md
    │       └── malaysia-conventions.md
    └── thesis-pipeline/            # NEW - Combined workflow
        ├── SKILL.md
        └── references/
            └── terminology-template.md
```

**Structure Decision**: Cursor Skills structure with each skill as a self-contained directory under `.cursor/skills/`. This follows the existing humanizer skill pattern and skill-creator guidelines.

## Design Decisions

### Skill Architecture

Each skill follows the skill-creator pattern:
1. **SKILL.md** - YAML frontmatter (name, description) + Markdown instructions
2. **references/** - Domain-specific reference files (loaded on demand)
3. No scripts needed (skills are prompt-based, not code-execution)

### Protected Elements Strategy (Skill A)

The LaTeX Guard skill will use pattern recognition via clear instructions:
- Citation commands: `\cite{}`, `\citep{}`, `\citet{}`
- Reference commands: `\ref{}`, `\label{}`, `\url{}`, `\href{}`
- Environment blocks: `figure`, `table`, `equation`, `algorithm`, `lstlisting`
- Math content: `$...$`, `\[...\]`, `$$...$$`
- File paths: Patterns like `chapter_X/filename.ext`

### Academic Style Approach (Skill B)

The Academic Polisher skill will provide:
- First-person to passive voice conversion rules
- Paragraph length detection and expansion guidance
- Vocabulary upgrade reference (informal → formal)
- Malaysian university convention notes

### Pipeline Integration (Combined Skill)

A thesis-pipeline skill will:
- Orchestrate skills in sequence: Guard → Polisher → Humanizer
- Accept optional terminology reference file via `@filename`
- Provide clear invocation instructions

## Skill Dependencies

```
thesis-pipeline (optional combined workflow)
    ├── latex-guard (Skill A) - REQUIRED first
    ├── academic-polisher (Skill B) - REQUIRED second
    └── humanizer (Skill C) - OPTIONAL final step
```

## Implementation Phases

### Phase 0: Research (Complete)
- Skill-creator patterns: Documented in research.md
- Humanizer skill structure: Analyzed and understood
- LaTeX protected elements: Taxonomy defined

### Phase 1: Design & Contracts
- Protected elements taxonomy: data-model.md
- Skill interface contracts: How each skill accepts input and produces output
- Usage quickstart: quickstart.md

### Phase 2: Implementation (via /speckit.tasks)
- Create latex-guard skill
- Create academic-polisher skill  
- Create thesis-pipeline skill
- Test with sample LaTeX content
- Update existing rules if needed

## Complexity Tracking

No constitution violations - this is a straightforward Cursor Skills implementation following established patterns.
