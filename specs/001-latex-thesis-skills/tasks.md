# Tasks: LaTeX Thesis Proofreading Skills

**Input**: Design documents from `/specs/001-latex-thesis-skills/`  
**Prerequisites**: plan.md, spec.md, research.md, data-model.md, quickstart.md

**Tests**: Not applicable - this is a Cursor Skills project. Validation is manual with sample LaTeX content.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each skill.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3, US4)
- Include exact file paths in descriptions

## Path Conventions

- **Skills**: `.cursor/skills/<skill-name>/`
- **References**: `.cursor/skills/<skill-name>/references/`
- **Existing**: `.cursor/skills/humanizer/` (do not modify)

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Prepare skill directory structure

- [x] T001 Create latex-guard skill directory at .cursor/skills/latex-guard/
- [x] T002 [P] Create latex-guard references directory at .cursor/skills/latex-guard/references/
- [x] T003 [P] Create academic-polisher skill directory at .cursor/skills/academic-polisher/
- [x] T004 [P] Create academic-polisher references directory at .cursor/skills/academic-polisher/references/
- [x] T005 [P] Create thesis-pipeline skill directory at .cursor/skills/thesis-pipeline/
- [x] T006 [P] Create thesis-pipeline references directory at .cursor/skills/thesis-pipeline/references/

**Checkpoint**: All skill directories ready for content creation

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Create reference documents that skills will depend on

**⚠️ CRITICAL**: Reference files must exist before SKILL.md files can reference them

- [x] T007 [P] Create protected-patterns.md reference at .cursor/skills/latex-guard/references/protected-patterns.md using protected element categories from data-model.md (lines 10-94) including all command examples and protection rules
- [x] T008 [P] Create vocabulary-upgrades.md reference at .cursor/skills/academic-polisher/references/vocabulary-upgrades.md with informal→formal word mappings from .cursor/rules/thesis-writing-standards.mdc (lines 35-44) and expand with additional academic vocabulary pairs
- [x] T009 [P] Create malaysia-conventions.md reference at .cursor/skills/academic-polisher/references/malaysia-conventions.md with Malaysian university thesis conventions from research.md (lines 47-57) and .cursor/rules/thesis-writing-standards.mdc (lines 8-44)
- [x] T010 [P] Create terminology-template.md reference at .cursor/skills/thesis-pipeline/references/terminology-template.md as user template for cross-chapter consistency using format from quickstart.md (lines 58-80) with sections for abbreviations, key terms, and chapter notes

**Checkpoint**: All reference files ready - skill SKILL.md creation can begin

---

## Phase 3: User Story 1 - LaTeX Structure Protection (Priority: P1) 🎯 MVP

**Goal**: Create latex-guard skill that protects all LaTeX structural elements during text editing

**Independent Test**: Provide a LaTeX chapter with citations, figures, tables, equations. Request text improvements. Verify all LaTeX commands remain exactly unchanged while prose is improved.

### Implementation for User Story 1

- [x] T011 [US1] Create SKILL.md for latex-guard at .cursor/skills/latex-guard/SKILL.md with:
  - YAML frontmatter (name: latex-guard, description with trigger conditions)
  - Protected element categories from data-model.md
  - Clear instructions for identifying and preserving citations, references, environments, math, file paths
  - Reference to protected-patterns.md for detailed patterns
  - Special character escaping rules
  - Output format requirements (complete LaTeX code)
  - Edge case handling guidance: malformed citations, nested environments, minimal editable prose scenarios (spec.md lines 82-88)

- [ ] T012 [US1] Validate latex-guard skill with sample LaTeX content containing:
  - Multiple citation types (\cite, \citep, \citet)
  - Cross-references (\ref, \label)
  - Figure and table environments
  - Inline and display math
  - File paths in \includegraphics

**Checkpoint**: latex-guard skill is functional and can be used independently

---

## Phase 4: User Story 2 - Malaysian Academic Style Compliance (Priority: P2)

**Goal**: Create academic-polisher skill for Malaysian university thesis writing standards

**Independent Test**: Provide text with first-person pronouns and informal vocabulary. Verify output uses passive voice, has minimum 3 sentences per paragraph, and uses formal academic vocabulary.

### Implementation for User Story 2

- [x] T013 [US2] Create SKILL.md for academic-polisher at .cursor/skills/academic-polisher/SKILL.md with:
  - YAML frontmatter (name: academic-polisher, description with trigger conditions)
  - First-person to passive voice conversion rules
  - Paragraph length detection and expansion guidance
  - Reference to vocabulary-upgrades.md for word replacements
  - Reference to malaysia-conventions.md for style rules
  - Integration note: Should be used after latex-guard for structure protection
  - Output format requirements (complete LaTeX code)
  - Edge case handling guidance: exactly 3-sentence paragraphs, mixed-language content (spec.md lines 82-88)

- [ ] T014 [US2] Validate academic-polisher skill with sample text containing:
  - First-person pronouns (I, We, My, Our)
  - Short paragraphs (1-2 sentences)
  - Informal vocabulary (get, thing, very, a lot)

**Checkpoint**: academic-polisher skill is functional and can be used independently

---

## Phase 5: User Story 3 - AI Writing Detection Reduction (Priority: P3)

**Goal**: Verify existing humanizer skill meets requirements for AI pattern reduction

**Independent Test**: Provide AI-polished academic text. Verify output has varied sentence structure, removed formulaic transitions, and preserved technical terminology.

### Implementation for User Story 3

- [x] T015 [US3] Review existing humanizer skill at .cursor/skills/humanizer/SKILL.md against FR-010 through FR-013 requirements
- [x] T016 [US3] Document humanizer integration notes in thesis-pipeline references (no modification to humanizer needed if requirements met)
- [ ] T017 [US3] Validate humanizer with sample AI-polished academic text to confirm:
  - Sentence structure variation
  - Formulaic transition replacement
  - Technical terminology preservation

**Checkpoint**: humanizer skill confirmed suitable for thesis pipeline integration

---

## Phase 6: User Story 4 - Supervisor Feedback Integration (Priority: P4)

**Goal**: Create thesis-pipeline skill that orchestrates all skills for complete chapter processing

**Independent Test**: Provide a LaTeX chapter with supervisor comments. Verify pipeline applies structure protection, academic style, and optional humanization while addressing supervisor feedback.

### Implementation for User Story 4

- [x] T018 [US4] Create SKILL.md for thesis-pipeline at .cursor/skills/thesis-pipeline/SKILL.md with:
  - YAML frontmatter (name: thesis-pipeline, description with trigger conditions)
  - Pipeline execution order: latex-guard → academic-polisher → humanizer (optional)
  - Instructions for processing supervisor feedback
  - Support for optional terminology reference file via @filename
  - Reference to terminology-template.md for users to create their own
  - Cross-chapter consistency guidance
  - Output format requirements (complete LaTeX code)
  - Edge case handling: all edge cases from spec.md lines 82-88 addressed by delegating to appropriate skills

- [ ] T019 [US4] Validate thesis-pipeline skill with:
  - Sample LaTeX chapter
  - Sample supervisor comments document
  - Sample terminology reference file

**Checkpoint**: thesis-pipeline skill orchestrates full workflow successfully

---

## Phase 7: Polish & Cross-Cutting Concerns

**Purpose**: Final validation and documentation updates

- [x] T020 [P] Update quickstart.md with actual skill invocation examples after validation
- [x] T021 [P] Create sample-chapter.tex test file at specs/001-latex-thesis-skills/samples/sample-chapter.tex for future validation
- [x] T022 [P] Create sample-terminology.md test file at specs/001-latex-thesis-skills/samples/sample-terminology.md as user reference
- [x] T023 Review and update existing rules in .cursor/rules/ if any conflicts with new skills
- [ ] T024 Final end-to-end validation: process sample chapter through complete pipeline, verify processing time meets SC-005 (<10 minutes including review), confirm all success criteria SC-001 through SC-006

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion - BLOCKS skill SKILL.md creation
- **User Stories (Phase 3-6)**: All depend on Foundational phase completion
  - US1 (latex-guard): No dependencies on other stories
  - US2 (academic-polisher): No dependencies on other stories (but logically follows US1)
  - US3 (humanizer): No dependencies - review existing skill
  - US4 (thesis-pipeline): Soft dependency on US1-US3 completion for integration
- **Polish (Phase 7)**: Depends on all user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Independent - MVP deliverable
- **User Story 2 (P2)**: Independent - can be developed in parallel with US1
- **User Story 3 (P3)**: Independent - review only, no new development
- **User Story 4 (P4)**: Integration skill - benefits from US1-US3 being ready but can be developed in parallel

### Parallel Opportunities

Within Phase 1:
- T002, T003, T004, T005, T006 can all run in parallel after T001

Within Phase 2:
- T007, T008, T009, T010 can all run in parallel

Within User Stories:
- US1, US2, US3 can be developed in parallel by different developers
- US4 can start development but final validation needs US1-US3

---

## Parallel Example: Phase 2 (Foundational)

```bash
# Launch all reference file creation tasks together:
Task: "Create protected-patterns.md reference at .cursor/skills/latex-guard/references/protected-patterns.md"
Task: "Create vocabulary-upgrades.md reference at .cursor/skills/academic-polisher/references/vocabulary-upgrades.md"
Task: "Create malaysia-conventions.md reference at .cursor/skills/academic-polisher/references/malaysia-conventions.md"
Task: "Create terminology-template.md reference at .cursor/skills/thesis-pipeline/references/terminology-template.md"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup (all directories)
2. Complete Phase 2: Foundational (reference files)
3. Complete Phase 3: User Story 1 (latex-guard skill)
4. **STOP and VALIDATE**: Test latex-guard independently with sample LaTeX
5. Deliver/demo if ready - users can already protect LaTeX structure

### Incremental Delivery

1. Setup + Foundational → Infrastructure ready
2. Add latex-guard (US1) → Test independently → Deploy (MVP!)
3. Add academic-polisher (US2) → Test independently → Deploy
4. Verify humanizer (US3) → Confirm integration → Document
5. Add thesis-pipeline (US4) → Test full workflow → Deploy
6. Polish phase → Samples and documentation

### Single Developer Strategy

Execute in this order:
1. T001-T006 (Setup) - ~10 minutes
2. T007-T010 (Foundational) - ~30 minutes
3. T011-T012 (US1 latex-guard) - ~45 minutes
4. T013-T014 (US2 academic-polisher) - ~45 minutes
5. T015-T017 (US3 humanizer review) - ~15 minutes
6. T018-T019 (US4 thesis-pipeline) - ~30 minutes
7. T020-T024 (Polish) - ~20 minutes

**Estimated Total**: ~3-4 hours

---

## Notes

- [P] tasks = different files, no dependencies
- [Story] label maps task to specific user story for traceability
- Each user story results in an independently usable skill
- Validation is manual with sample LaTeX content (no automated tests for prompt-based skills)
- Existing humanizer skill is not modified - only reviewed and integrated
- All skills follow skill-creator patterns from .cursor/skills/skill-creator/SKILL.md
