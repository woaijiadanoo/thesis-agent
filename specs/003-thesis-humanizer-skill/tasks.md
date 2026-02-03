# Tasks: Thesis Humanizer Skill

**Input**: Design documents from `/specs/003-thesis-humanizer-skill/`  
**Prerequisites**: plan.md ✓, spec.md ✓, research.md ✓, data-model.md ✓, quickstart.md ✓

**Tests**: Not applicable - this is a documentation-only Cursor skill (no compiled code).

**Organization**: Tasks are grouped by user story to enable independent implementation and testing.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3, US4)
- Include exact file paths in descriptions

## Path Conventions

- **Skill files**: `.cursor/skills/thesis-humanizer/`
- **Reference files**: `.cursor/skills/thesis-humanizer/references/`
- **Changelog**: `RULES_SKILLS_CHANGELOG.md` (repository root)

---

## Phase 1: Setup

**Purpose**: Create skill directory structure and foundational files

- [x] T001 Create skill directory structure at .cursor/skills/thesis-humanizer/references/
- [x] T002 Create SKILL.md frontmatter and basic structure in .cursor/skills/thesis-humanizer/SKILL.md

---

## Phase 2: Foundational (Core Pattern Reference)

**Purpose**: Create the AI pattern reference that ALL user stories depend on

**⚠️ CRITICAL**: This reference file is needed by all user stories - must complete before story implementation

- [x] T003 Create ai-patterns-academic.md with Part A (Vocabulary Patterns #7, #22, #23) in .cursor/skills/thesis-humanizer/references/ai-patterns-academic.md
- [x] T004 Add Part B (Structural Patterns #9, #10, #13) to .cursor/skills/thesis-humanizer/references/ai-patterns-academic.md
- [x] T005 Add Part C (Promotional Patterns #1-4) to .cursor/skills/thesis-humanizer/references/ai-patterns-academic.md
- [x] T006 Add Part D (Attribution Patterns #5, #6) to .cursor/skills/thesis-humanizer/references/ai-patterns-academic.md
- [x] T007 Add Part E (Style Patterns #8, #11, #12, #24) to .cursor/skills/thesis-humanizer/references/ai-patterns-academic.md
- [x] T008 Add Part F (Formatting Patterns #14-18) to .cursor/skills/thesis-humanizer/references/ai-patterns-academic.md
- [x] T009 Add Part G (Chatbot Artifacts #19-21) to .cursor/skills/thesis-humanizer/references/ai-patterns-academic.md
- [x] T010 Add Part H (Thesis-Specific Patterns H1-H5) to .cursor/skills/thesis-humanizer/references/ai-patterns-academic.md

**Checkpoint**: AI pattern reference complete - user story implementation can begin

---

## Phase 3: User Story 1 - Basic Thesis Chapter Humanization (Priority: P1) 🎯 MVP

**Goal**: Enable single-pass humanization of LaTeX thesis content with LaTeX protection and academic tone

**Independent Test**: Invoke `/thesis-humanizer @chapter.tex` and verify (1) AI vocabulary replaced, (2) citations preserved, (3) academic tone maintained

### Implementation for User Story 1

- [x] T011 [P] [US1] Create replacement-dictionary.md with AI vocabulary section (50+ words) in .cursor/skills/thesis-humanizer/references/replacement-dictionary.md
- [x] T012 [P] [US1] Add informal-to-formal vocabulary section to .cursor/skills/thesis-humanizer/references/replacement-dictionary.md
- [x] T013 [US1] Add "Your Task" workflow section (5-step process) to .cursor/skills/thesis-humanizer/SKILL.md
- [x] T014 [US1] Add "Academic Constraints" section (third person, passive voice, British English) to .cursor/skills/thesis-humanizer/SKILL.md
- [x] T015 [US1] Add "LaTeX Protection" section (delegate to latex-guard) to .cursor/skills/thesis-humanizer/SKILL.md
- [x] T016 [US1] Add "AI Pattern Quick Reference" table (top 15 patterns inline) to .cursor/skills/thesis-humanizer/SKILL.md
- [x] T017 [US1] Add edge case handling (no patterns found, comments, non-English) to .cursor/skills/thesis-humanizer/SKILL.md

**Checkpoint**: Basic humanization workflow functional - can process a chapter and replace AI vocabulary

---

## Phase 4: User Story 2 - Multi-Pass Iterative Refinement (Priority: P2)

**Goal**: Enable 3-5 pass iterative processing with pass-specific targeting and density tracking

**Independent Test**: Run multiple passes on a chapter and verify pattern density decreases with each pass

### Implementation for User Story 2

- [x] T018 [P] [US2] Create multi-pass-workflow.md with pass definitions (Pass 1-5) in .cursor/skills/thesis-humanizer/references/multi-pass-workflow.md
- [x] T019 [P] [US2] Create rhythm-techniques.md with sentence variation strategies in .cursor/skills/thesis-humanizer/references/rhythm-techniques.md
- [x] T020 [US2] Add stop criteria section to .cursor/skills/thesis-humanizer/references/multi-pass-workflow.md
- [x] T021 [US2] Add pattern density estimation section to .cursor/skills/thesis-humanizer/references/multi-pass-workflow.md
- [x] T022 [US2] Add "Multi-Pass Workflow" section to .cursor/skills/thesis-humanizer/SKILL.md
- [x] T023 [US2] Add "Rhythm Variation" quick reference to .cursor/skills/thesis-humanizer/SKILL.md

**Checkpoint**: Multi-pass workflow documented - users can run iterative refinement

---

## Phase 5: User Story 3 - Pattern-Specific Targeted Humanization (Priority: P3)

**Goal**: Enable users to target specific pattern categories (vocabulary-only, structure-only, etc.)

**Independent Test**: Request vocabulary-only pass and verify only vocabulary patterns are modified

### Implementation for User Story 3

- [x] T024 [US3] Add pattern category filtering instructions to .cursor/skills/thesis-humanizer/SKILL.md
- [x] T025 [US3] Add "Targeted Humanization" section with category options to .cursor/skills/thesis-humanizer/SKILL.md
- [x] T026 [US3] Add connector variations section to .cursor/skills/thesis-humanizer/references/replacement-dictionary.md
- [x] T027 [US3] Add chapter organization verbs section to .cursor/skills/thesis-humanizer/references/replacement-dictionary.md

**Checkpoint**: Pattern-specific targeting documented - advanced users can filter by category

---

## Phase 6: User Story 4 - Change Log Generation (Priority: P3)

**Goal**: Generate detailed modification records for user review and accountability

**Independent Test**: Run humanization and verify change log contains line/original/replacement/pattern for each change

### Implementation for User Story 4

- [x] T028 [US4] Add "Change Log Format" section to .cursor/skills/thesis-humanizer/SKILL.md
- [x] T029 [US4] Add change log generation instructions to .cursor/skills/thesis-humanizer/SKILL.md
- [x] T030 [US4] Add "Output Format" section (LaTeX output + change log) to .cursor/skills/thesis-humanizer/SKILL.md

**Checkpoint**: Change log generation documented - users can track all modifications

---

## Phase 7: Polish & Cross-Cutting Concerns

**Purpose**: Final integration, triggers, and project documentation

- [x] T031 [P] Add skill triggers and description to SKILL.md frontmatter in .cursor/skills/thesis-humanizer/SKILL.md
- [x] T032 [P] Add integration notes (with latex-guard, academic-polisher) to .cursor/skills/thesis-humanizer/SKILL.md
- [x] T033 [P] Add "Patterns to REVERSE" section (first person, opinions, casual) to .cursor/skills/thesis-humanizer/SKILL.md
- [x] T034 Update RULES_SKILLS_CHANGELOG.md with thesis-humanizer skill addition
- [x] T035 Validate skill against quickstart.md scenarios

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies - can start immediately
- **Foundational (Phase 2)**: Depends on Setup - creates pattern reference needed by all stories
- **User Stories (Phase 3-6)**: All depend on Foundational phase completion
- **Polish (Phase 7)**: Depends on all user stories being complete

### User Story Dependencies

- **User Story 1 (P1)**: Depends on Phase 2 (pattern reference) - No dependencies on other stories
- **User Story 2 (P2)**: Depends on Phase 2 - Can proceed in parallel with US1
- **User Story 3 (P3)**: Depends on US1 (uses same replacement-dictionary.md)
- **User Story 4 (P3)**: Depends on Phase 2 - Can proceed in parallel with US1-US3

### Within Each User Story

- Reference files before SKILL.md sections
- Core functionality before edge cases
- Independent testability at each checkpoint

### Parallel Opportunities

- T011 and T012 can run in parallel (different sections of replacement-dictionary.md)
- T018 and T019 can run in parallel (different reference files)
- T031, T032, T033 can run in parallel (different sections of SKILL.md)
- US1 and US2 can proceed in parallel after Phase 2

---

## Parallel Example: Phase 2

```bash
# All pattern parts are independent sections - can write in parallel:
T003: Part A (Vocabulary)
T004: Part B (Structural)
T005: Part C (Promotional)
T006: Part D (Attribution)
T007: Part E (Style)
T008: Part F (Formatting)
T009: Part G (Chatbot)
T010: Part H (Thesis-Specific)
```

## Parallel Example: User Story 1

```bash
# Reference file tasks can run in parallel:
T011: replacement-dictionary.md AI vocabulary section
T012: replacement-dictionary.md informal-to-formal section
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup (T001-T002)
2. Complete Phase 2: Foundational (T003-T010)
3. Complete Phase 3: User Story 1 (T011-T017)
4. **STOP and VALIDATE**: Test with a sample LaTeX chapter
5. Skill is usable for basic humanization

### Incremental Delivery

1. Setup + Foundational → Pattern reference ready
2. Add User Story 1 → Basic humanization works → **MVP!**
3. Add User Story 2 → Multi-pass workflow available
4. Add User Story 3 → Pattern filtering available
5. Add User Story 4 → Change logs generated
6. Polish → Full integration complete

---

## Notes

- [P] tasks = different files or independent sections
- [Story] label maps task to specific user story for traceability
- Each user story should be independently completable and testable
- This is a documentation-only skill - no compilation or unit tests needed
- Validation is manual via Turnitin AI Writing detection
- Commit after each phase or logical group

---

## Summary

| Metric | Value |
|--------|-------|
| **Total Tasks** | 35 |
| **Setup Tasks** | 2 |
| **Foundational Tasks** | 8 |
| **US1 Tasks** | 7 |
| **US2 Tasks** | 6 |
| **US3 Tasks** | 4 |
| **US4 Tasks** | 3 |
| **Polish Tasks** | 5 |
| **Parallel Opportunities** | 15 tasks marked [P] |
| **MVP Scope** | T001-T017 (17 tasks) |
