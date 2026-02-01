# Tasks: thesis-refine-with-latex

**Input**: Design documents from `/specs/002-thesis-refine-orchestrator/`
**Prerequisites**: `plan.md` (required), `spec.md` (required for user stories), `research.md`, `data-model.md`, `quickstart.md`

**Tests**: Not requested in the feature specification. Tasks below focus on implementation + manual validation using `quickstart.md` examples.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## One-shot Implementation Mode (All-in-One)

If you want to implement everything in one pass and then validate end-to-end:

- Execute tasks sequentially from **T001 → T035** without stopping at the MVP checkpoints.
- Defer manual validation until after **T035** (then run the full set of manual checks from `specs/002-thesis-refine-orchestrator/quickstart.md`).
- Keep `thesis-pipeline` unchanged; all new behavior is implemented in `.cursor/skills/thesis-refine-with-latex/`.

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Create the new skill scaffold and required reference files.

- [x] T001 Create new skill directory `.cursor/skills/thesis-refine-with-latex/` (repo root)
- [x] T002 Create new references directory `.cursor/skills/thesis-refine-with-latex/references/` (repo root)
- [x] T003 [P] Draft `.cursor/skills/thesis-refine-with-latex/SKILL.md` with skill metadata + triggers (from `specs/002-thesis-refine-orchestrator/plan.md`)
- [x] T004 [P] Create `.cursor/skills/thesis-refine-with-latex/references/chunking-strategy.md` from `specs/002-thesis-refine-orchestrator/research.md`
- [x] T005 [P] Create `.cursor/skills/thesis-refine-with-latex/references/feedback-matching.md` from `specs/002-thesis-refine-orchestrator/research.md`
- [x] T006 [P] Create `.cursor/skills/thesis-refine-with-latex/references/self-healing.md` from `specs/002-thesis-refine-orchestrator/research.md`
- [x] T007 [P] Create `.cursor/skills/thesis-refine-with-latex/references/change-log-format.md` from `specs/002-thesis-refine-orchestrator/quickstart.md` + `specs/002-thesis-refine-orchestrator/data-model.md`
- [x] T008 [P] Add usage examples to `.cursor/skills/thesis-refine-with-latex/SKILL.md` referencing `specs/002-thesis-refine-orchestrator/quickstart.md`

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Define the orchestrator’s invariant rules (LaTeX protection, ordering, defaults, outputs). This phase MUST be complete before ANY user story work.

- [x] T009 Define the strict pipeline order in `.cursor/skills/thesis-refine-with-latex/SKILL.md`: feedback analysis → (clarify if needed) → (chunk if needed) → latex-guard mask → academic-polisher → humanizer (default high) → verify/self-heal → latex-guard unmask
- [x] T010 Define LaTeX invariants in `.cursor/skills/thesis-refine-with-latex/SKILL.md` aligned with `specs/002-thesis-refine-orchestrator/spec.md` (preserve `\cite*`, `\ref/\label`, figure/table/equation, math, paths)
- [x] T011 Define defaults in `.cursor/skills/thesis-refine-with-latex/SKILL.md`: Overleaf-validated input assumption, British English, humanizer intensity = high (Turnitin AI <10% target)
- [x] T012 Define the required output contract in `.cursor/skills/thesis-refine-with-latex/SKILL.md`: “modified_latex + change_log + ai_score_estimate + warnings”
- [x] T013 Add “do not modify protected elements” guardrails in `.cursor/skills/thesis-refine-with-latex/SKILL.md` and point to `.cursor/skills/latex-guard/references/protected-patterns.md`
- [x] T014 Add a manual validation checklist section in `.cursor/skills/thesis-refine-with-latex/SKILL.md` (verify placeholders restored; verify citations/refs untouched; verify no environment corruption)

**Checkpoint**: Foundation ready — user story implementation can now begin.

---

## Phase 3: User Story 1 - Basic Thesis Paragraph Revision (Priority: P1) 🎯 MVP

**Goal**: Revise a single LaTeX paragraph using supervisor feedback while preserving all LaTeX structural elements and producing a change log.

**Independent Test**: Use the “Single Paragraph Revision” example in `specs/002-thesis-refine-orchestrator/quickstart.md` and confirm: citations unchanged + improved academic tone + change log produced.

- [x] T015 [US1] Implement “target paragraph only” handling instructions in `.cursor/skills/thesis-refine-with-latex/SKILL.md` (when user provides a single paragraph block)
- [x] T016 [US1] Implement “feedback analysis” instructions in `.cursor/skills/thesis-refine-with-latex/SKILL.md` (interpret comments; decide `global` vs `specific`; derive an actionable edit intent list)
- [x] T017 [US1] Implement “change log” rules for single-paragraph edits in `.cursor/skills/thesis-refine-with-latex/references/change-log-format.md`
- [x] T018 [US1] Add output format examples (LaTeX + change log + AI estimate) to `.cursor/skills/thesis-refine-with-latex/SKILL.md` aligned with `specs/002-thesis-refine-orchestrator/quickstart.md`

**Checkpoint**: US1 is independently usable for paragraph-level work.

---

## Phase 4: User Story 2 - Full Chapter Processing with Chunking (Priority: P2)

**Goal**: Process full LaTeX chapters >8K tokens via safe chunking and reassembly without breaking LaTeX structure.

**Independent Test**: Provide a long LaTeX chapter (>8K tokens) and verify: chunk boundaries are safe, processing is consistent across chunks, and output LaTeX remains compilable.

- [x] T019 [US2] Implement chunking decision rules in `.cursor/skills/thesis-refine-with-latex/references/chunking-strategy.md` (section first, paragraph fallback; 500-token overlap)
- [x] T020 [US2] Add chunking workflow instructions to `.cursor/skills/thesis-refine-with-latex/SKILL.md` (how to process chunk-by-chunk and reassemble)
- [x] T021 [US2] Add chunk-level change log guidance to `.cursor/skills/thesis-refine-with-latex/references/change-log-format.md` (record chunk id + section markers)
- [x] T022 [US2] Add a “post-reassembly integrity checks” section to `.cursor/skills/thesis-refine-with-latex/SKILL.md` (no broken environments; all placeholders restored; citations preserved)

**Checkpoint**: US2 is independently usable for chapter-level work.

---

## Phase 5: User Story 3 - AI Writing Pattern Reduction (Priority: P2)

**Goal**: Apply humanizer in academic mode (default high) to reduce AI patterns and report an AI score estimate toward the <10% Turnitin AI target.

**Independent Test**: Provide text with obvious AI patterns and confirm humanizer output reduces those patterns while staying academic and preserves LaTeX structures.

- [x] T023 [US3] Define “academic mode constraints” for humanizer usage in `.cursor/skills/thesis-refine-with-latex/SKILL.md` (no first-person; keep academic tone; avoid chatbot artifacts)
- [x] T024 [US3] Define AI score estimation method in `.cursor/skills/thesis-refine-with-latex/SKILL.md` (pattern density sampling per `specs/002-thesis-refine-orchestrator/research.md`)
- [x] T025 [US3] Add AI score warning thresholds + user guidance in `.cursor/skills/thesis-refine-with-latex/SKILL.md` (warn if likely >10%; suggest re-run / manual review of flagged sections)
- [x] T026 [US3] Update `.cursor/skills/thesis-refine-with-latex/references/change-log-format.md` to tag entries by source step: `academic_polish` vs `humanize`

**Checkpoint**: US3 is independently usable for AI-pattern-heavy drafts.

---

## Phase 6: User Story 4 - Ambiguous Feedback Handling (Priority: P3)

**Goal**: Detect low-confidence matches (<30%) between feedback and source content and enter clarification mode to avoid editing the wrong place.

**Independent Test**: Provide vague feedback and multi-paragraph LaTeX; confirm the skill presents top 3 candidates and asks user to choose.

- [x] T027 [US4] Define keyword extraction + scoring rules in `.cursor/skills/thesis-refine-with-latex/references/feedback-matching.md` (include/exclude rules; 30% threshold)
- [x] T028 [US4] Add clarification-mode prompt template to `.cursor/skills/thesis-refine-with-latex/SKILL.md` (show top 3 candidates with scores; request selection)
- [x] T029 [US4] Add “clarification decision logging” rules to `.cursor/skills/thesis-refine-with-latex/references/change-log-format.md` (record which paragraph/section user selected)

**Checkpoint**: US4 reduces wrong-target edits and is independently usable.

---

## Phase 7: Cross-Cutting - Self-Healing (from FR-010)

**Purpose**: Recover from placeholder loss after humanizer and guarantee successful unmasking.

- [x] T030 Implement placeholder verification rules in `.cursor/skills/thesis-refine-with-latex/references/self-healing.md` (detect missing placeholders)
- [x] T031 Implement recovery strategies in `.cursor/skills/thesis-refine-with-latex/references/self-healing.md` (context match → fuzzy match → append fallback + warning)
- [x] T032 Integrate self-healing instructions into `.cursor/skills/thesis-refine-with-latex/SKILL.md` (when to trigger; what to report in warnings/change log)

---

## Phase 8: Polish & Cross-Cutting Concerns

**Purpose**: Documentation consistency, repo hygiene, and readiness checks.

- [x] T033 [P] Ensure `specs/002-thesis-refine-orchestrator/quickstart.md` matches the finalized behavior/outputs of `.cursor/skills/thesis-refine-with-latex/SKILL.md`
- [x] T034 [P] Ensure `specs/002-thesis-refine-orchestrator/spec.md` remains consistent with the final skill contract (FR list, defaults, SC-005 <10%)
- [x] T036 Add idempotency rules to `.cursor/skills/thesis-refine-with-latex/SKILL.md` (do not double-mask; do not duplicate placeholders; repeated runs keep LaTeX structure identical) and add manual verification steps
- [x] T037 Add “feedback items ↔ change log entries” mapping rules to `.cursor/skills/thesis-refine-with-latex/references/change-log-format.md` (number feedback items; each item must map to >=1 entry or explicit `skipped/partial` with rationale)
- [x] T035 Update `RULES_SKILLS_CHANGELOG.md` to record the new `.cursor/skills/thesis-refine-with-latex/` skill and any `.cursor/rules/` changes made by scripts

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies — can start immediately
- **Foundational (Phase 2)**: Depends on Setup completion — BLOCKS all user stories
- **User Stories (Phase 3–6)**: Depend on Foundational completion; can proceed in parallel by story after Phase 2
- **Self-Healing (Phase 7)**: Depends on Foundational; recommended before finishing US2/US3
- **Polish (Phase 8)**: Depends on completing all desired user stories

### User Story Dependencies

- **US1 (P1)**: Starts after Phase 2; independent MVP
- **US2 (P2)**: Starts after Phase 2; benefits from Phase 7 self-healing
- **US3 (P2)**: Starts after Phase 2; benefits from Phase 7 self-healing
- **US4 (P3)**: Starts after Phase 2; integrates with feedback analysis in US1/US2

### Parallel Opportunities

- Setup reference docs tasks **T004–T007** are parallelizable.
- After Phase 2, **US2/US3/US4** can be developed in parallel by different people (different files under `.cursor/skills/thesis-refine-with-latex/`).

