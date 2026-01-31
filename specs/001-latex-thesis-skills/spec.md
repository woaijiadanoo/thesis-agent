# Feature Specification: LaTeX Thesis Proofreading Skills

**Feature Branch**: `001-latex-thesis-skills`  
**Created**: 2026-01-31  
**Status**: Draft  
**Input**: User description: "Build automated thesis proofreading and LaTeX structure protection workflow using Cursor Skills"

## Clarifications

### Session 2026-01-31

- Q: How should skills be invoked - independently, in sequence, or as a pipeline? → A: Independent skills with optional pipeline mode. Each skill is standalone and domain-focused (can be more than 3 skills if beneficial for modularity). Users can invoke skills individually for targeted optimization, or request a combined workflow that runs all skills in sequence within a single request.
- Q: How should malformed LaTeX input be handled? → A: Assume valid input (pre-validated via Overleaf). Error handling is not required. However, skills MUST maintain LaTeX syntax correctness during modifications (e.g., escape special characters: `%` → `\%`, `&` → `\&`).
- Q: How should cross-chapter consistency (terminology, abbreviations, no duplicates) be handled? → A: Context file optional. Skills work standalone by default, but can use a terminology/abbreviation reference file if provided via `@filename` for thesis-wide consistency.
- Q: Should new skills leverage existing skills in the project? → A: Yes, leverage existing. Use the existing humanizer skill (`.cursor/skills/humanizer/`) as Skill C for AI writing pattern reduction. Create new skills for LaTeX protection and academic polishing.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - LaTeX Structure Protection During Editing (Priority: P1)

A PhD student needs to polish their thesis chapter text while ensuring that all LaTeX citations (`\cite{}`), cross-references (`\ref{}`), figures, tables, equations, and algorithms remain completely untouched. The student wants to improve the prose without risking compilation errors or broken references.

**Why this priority**: This is the foundational capability. Without reliable structure protection, any text modification risks breaking the document. All other features depend on this working correctly.

**Independent Test**: Can be fully tested by providing a LaTeX chapter containing citations and figures, requesting text improvements, and verifying all LaTeX commands remain intact while prose is improved.

**Acceptance Scenarios**:

1. **Given** a LaTeX file containing `\cite{author2023}` references, **When** the user requests text polishing, **Then** all `\cite{}` commands and their contents remain exactly as they were in the original.
2. **Given** a LaTeX file with `\begin{figure}...\end{figure}` environments, **When** text outside these environments is edited, **Then** the figure environment content including file paths like `chapter_4/figure1.jpg` remains unchanged.
3. **Given** a LaTeX file with `\ref{}` and `\label{}` commands, **When** surrounding text is modified, **Then** all reference commands remain functional and unchanged.

---

### User Story 2 - Malaysian Academic Style Compliance (Priority: P2)

A PhD student at a Malaysian university (UM, UPM, UTM, etc.) needs their thesis to conform to local academic writing conventions. This includes converting first-person pronouns to passive voice, ensuring paragraphs have adequate length, and using formal academic vocabulary.

**Why this priority**: Academic style compliance is a common revision requirement from supervisors. Students often struggle with consistent voice and tone throughout their thesis.

**Independent Test**: Can be tested by providing text containing first-person pronouns and short paragraphs, then verifying the output uses passive voice and paragraphs meet minimum sentence requirements.

**Acceptance Scenarios**:

1. **Given** text containing "I conducted the experiment" or "We observed that...", **When** the academic polishing skill is applied, **Then** the text is converted to passive voice like "The experiment was conducted" or "It was observed that...".
2. **Given** a paragraph with only 2 sentences, **When** the polishing skill detects this, **Then** the paragraph is either expanded with contextually appropriate content or merged with an adjacent paragraph.
3. **Given** informal academic phrasing like "look into" or "a lot of", **When** the skill processes the text, **Then** these are replaced with formal alternatives like "investigate" or "substantial".

---

### User Story 3 - AI Writing Detection Reduction (Priority: P3)

After polishing with AI assistance, the student needs to reduce detectable AI writing patterns to pass plagiarism and AI detection tools while maintaining academic integrity and meaning.

**Why this priority**: This is a finishing step that adds value after the core editing is complete. It addresses a practical concern about AI-assisted writing detection.

**Independent Test**: Can be tested by processing AI-polished text and comparing the output against typical AI writing pattern indicators (consistent sentence structure, predictable transitions).

**Acceptance Scenarios**:

1. **Given** text with repetitive sentence structure patterns, **When** the humanizing skill is applied, **Then** the output contains varied sentence lengths and structures (increased "burstiness").
2. **Given** text using formulaic transitions like "Firstly, Secondly, Finally", **When** the skill processes it, **Then** these are replaced with more varied transitional approaches.
3. **Given** academically correct text, **When** humanization is applied, **Then** the technical terminology and academic rigor are preserved while only stylistic patterns change.

---

### User Story 4 - Supervisor Feedback Integration (Priority: P4)

A PhD student receives specific feedback from their supervisor (e.g., "Expand the discussion on data reliability in Section 4.1") and needs to address these comments systematically while following all the above constraints.

**Why this priority**: This integrates the skills into a real-world workflow. Students commonly receive chapter-specific feedback that requires targeted modifications.

**Independent Test**: Can be tested by providing supervisor comments alongside a LaTeX chapter, then verifying that specific feedback items are addressed while maintaining structure protection and style compliance.

**Acceptance Scenarios**:

1. **Given** a supervisor comment "Expand discussion on X", **When** the user references both the comment and the chapter, **Then** the relevant section is expanded with contextually appropriate academic content.
2. **Given** multiple supervisor comments for one chapter, **When** the workflow is executed, **Then** each comment is addressed in the corresponding section without affecting other parts.

---

### Edge Cases

- What happens when a citation key contains special characters or is malformed?
- How does the system handle nested LaTeX environments (e.g., a table inside a figure)?
- What happens when text is entirely within a protected environment with no editable prose?
- How does the system handle mixed-language content (English with occasional Malaysian/Chinese terms)?
- What happens when a paragraph has exactly 3 sentences (boundary condition)?

## Requirements *(mandatory)*

### Functional Requirements

**LaTeX Structure Protection (Skill A)**

- **FR-001**: System MUST identify and preserve all `\cite{}`, `\citep{}`, `\citet{}` citation commands and their contents.
- **FR-002**: System MUST identify and preserve all `\ref{}`, `\label{}`, `\url{}`, `\href{}` reference commands.
- **FR-003**: System MUST identify and preserve complete environment blocks: `figure`, `table`, `equation`, `algorithm`, `lstlisting`.
- **FR-004**: System MUST preserve all file paths appearing in LaTeX (e.g., `chapter_4/figure1.jpg`).
- **FR-005**: System MUST preserve inline math (`$...$`) and display math (`\[...\]`, `$$...$$`) content.

**Academic Style Compliance (Skill B)**

- **FR-006**: System MUST convert first-person pronouns (I, We, Our, My) to passive voice or objective descriptions (This study, The analysis, The research).
- **FR-007**: System MUST identify paragraphs with fewer than 3 sentences and either expand or merge them appropriately.
- **FR-008**: System MUST replace informal academic vocabulary with formal equivalents.
- **FR-009**: System MUST maintain logical flow and coherence when modifying paragraph structure.

**AI Writing Pattern Reduction (Skill C - Existing Humanizer)**

*Note: Leverage existing `.cursor/skills/humanizer/` skill. Requirements below document expected behavior.*

- **FR-010**: System MUST vary sentence structure to avoid repetitive patterns.
- **FR-011**: System MUST replace formulaic transition phrases with varied alternatives.
- **FR-012**: System MUST preserve technical terminology and academic precision during humanization.
- **FR-013**: System MUST NOT sacrifice clarity or accuracy for the sake of variation.

**Workflow Integration**

- **FR-014**: Each skill MUST be standalone and focused on a single domain, enabling independent optimization and testing.
- **FR-015**: The number of skills is NOT limited to three; additional skills MAY be created if beneficial for modularity and independent optimization.
- **FR-016**: Users MUST be able to invoke any single skill independently for targeted processing.
- **FR-017**: Users MUST be able to request a combined pipeline workflow that runs multiple skills in sequence within a single request.
- **FR-018**: System MUST accept chapter-level LaTeX input (not require entire thesis at once).
- **FR-019**: System MUST output complete, compilable LaTeX code that can directly replace the original.
- **FR-020**: When inserting or modifying text, system MUST maintain LaTeX syntax correctness by properly escaping special characters (e.g., `%` → `\%`, `&` → `\&`, `$` → `\$` in prose context).
- **FR-021**: Skills MUST support an optional terminology/abbreviation reference file for cross-chapter consistency when provided via `@filename`.
- **FR-022**: When a reference file is provided, skills MUST ensure consistent terminology usage and proper abbreviation handling (full form on first use only).

### Key Entities

- **LaTeX Chapter**: A `.tex` file containing thesis content with embedded LaTeX commands, citations, figures, tables, equations, and prose text.
- **Protected Element**: Any LaTeX command, environment, or content that must not be modified (citations, references, figures, tables, equations, algorithms, file paths).
- **Editable Prose**: Text content outside protected elements that can be modified for style, grammar, and humanization.
- **Supervisor Comment**: Specific feedback from a thesis supervisor requiring targeted modifications to particular sections.
- **Terminology Reference File**: Optional file containing thesis-wide terminology definitions, abbreviations (with full forms), and consistency rules for cross-chapter coherence.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: 100% of LaTeX citations, references, and environments remain unchanged after processing.
- **SC-002**: Processed chapters compile without LaTeX errors.
- **SC-003**: Zero first-person pronouns remain in processed output (unless within direct quotations).
- **SC-004**: All paragraphs in processed output contain at least 3 sentences.
- **SC-005**: Users can process a single thesis chapter in under 10 minutes (including review).
- **SC-006**: Processed text demonstrates measurable variation in sentence length and structure compared to input.

## Assumptions

- Users have basic familiarity with Cursor IDE and can reference files using `@filename` syntax.
- LaTeX source files are pre-validated via Overleaf and compile successfully before processing.
- Supervisor feedback is provided in a readable format (text file, PDF, or inline comments).
- The thesis follows a standard academic structure (chapters, sections, paragraphs).
- Users will process content chapter-by-chapter rather than the entire thesis at once.
- Users will verify final output in Overleaf and handle any LaTeX compilation issues there.
