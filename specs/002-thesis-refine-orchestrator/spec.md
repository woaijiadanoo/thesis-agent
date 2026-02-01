# Feature Specification: thesis-refine-with-latex

**Feature Branch**: `002-thesis-refine-orchestrator`  
**Created**: 2026-02-01  
**Status**: Draft  
**Input**: User description: "Create a new skill `thesis-refine-with-latex` that coordinates latex-guard, academic-polisher, and humanizer for automated LaTeX thesis revision based on supervisor feedback. Keep `thesis-pipeline` generic for future non-LaTeX use."

## Clarifications

### Session 2026-02-01

- Q: How should the system handle malformed LaTeX input? → A: Best-effort processing with Overleaf-validated input assumption; warn on structural anomalies but don't block processing.
- Q: What is the default humanizer intensity? → A: High by default (target <10% Turnitin AI detection). Humanizer skill owns AI detection capability; orchestrator passes through intensity parameter.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Basic Thesis Paragraph Revision (Priority: P1)

A PhD student receives specific feedback from their supervisor about a particular paragraph in their thesis chapter. They want to revise just that paragraph while preserving all LaTeX citations, equations, and cross-references.

**Why this priority**: This is the core use case - targeted paragraph revision with supervisor feedback. Most thesis revisions involve fixing specific sections rather than rewriting entire chapters.

**Independent Test**: Can be fully tested by providing a single LaTeX paragraph with embedded citations and a supervisor comment, then verifying the output maintains all LaTeX syntax while improving academic quality.

**Acceptance Scenarios**:

1. **Given** a LaTeX paragraph containing `\cite{}` commands and a supervisor comment "improve clarity", **When** the user submits both inputs, **Then** the output contains improved academic prose with all original citations intact and unchanged.
2. **Given** a LaTeX paragraph with an inline equation `$...$` and feedback "make more formal", **When** the user processes the content, **Then** the equation remains mathematically identical while surrounding text is formalized.
3. **Given** a paragraph with `\ref{}` cross-references and feedback about passive voice, **When** processed, **Then** cross-references are preserved and passive voice issues are addressed.

---

### User Story 2 - Full Chapter Processing with Chunking (Priority: P2)

A PhD student wants to process an entire thesis chapter (potentially exceeding 8,000 tokens) based on general supervisor feedback about academic tone and AI-like writing patterns.

**Why this priority**: Chapter-level processing is common but more complex than single paragraphs. Requires chunking logic to handle long documents without losing context.

**Independent Test**: Can be tested by providing a long LaTeX chapter file (>8,000 tokens) with global feedback, verifying output maintains document structure and all LaTeX elements across chunk boundaries.

**Acceptance Scenarios**:

1. **Given** a 10,000-token chapter and global feedback "improve academic tone", **When** processed, **Then** the entire chapter is revised with consistent improvements across all chunks.
2. **Given** a multi-section chapter with figures and tables, **When** chunked and processed, **Then** `\begin{figure}` and `\begin{table}` environments remain completely unchanged.
3. **Given** long content requiring 3+ chunks, **When** processed, **Then** no LaTeX structural elements are broken across chunk boundaries.

---

### User Story 3 - AI Writing Pattern Reduction (Priority: P2)

A PhD student's draft has been flagged by AI detection tools. They want to reduce AI-like patterns while maintaining the technical accuracy and academic quality of their writing.

**Why this priority**: AI detection is increasingly important for thesis submissions. This represents a key differentiator of the orchestrator combining humanizer with academic polish.

**Independent Test**: Can be tested by providing AI-generated text with typical patterns (excessive "Furthermore", "In conclusion"), measuring reduction in AI detection scores.

**Acceptance Scenarios**:

1. **Given** text with repeated AI patterns like "Furthermore" and "In conclusion", **When** humanizer is applied, **Then** these patterns are varied or replaced with more natural alternatives.
2. **Given** text with em-dash overuse and rule-of-three patterns, **When** processed, **Then** sentence structures are diversified.
3. **Given** LaTeX text with `et al.` in citations, **When** humanizer runs, **Then** citation formatting including "et al." remains unchanged.

---

### User Story 4 - Ambiguous Feedback Handling (Priority: P3)

A PhD student provides supervisor feedback that doesn't clearly map to any specific paragraph in their LaTeX source. The system should request clarification rather than make incorrect assumptions.

**Why this priority**: Graceful handling of edge cases prevents incorrect modifications. Less frequent than clear feedback scenarios.

**Independent Test**: Can be tested by providing feedback that has <30% semantic match to source content, verifying the system enters clarification mode.

**Acceptance Scenarios**:

1. **Given** feedback about "the methodology section" but source contains multiple methodology-related paragraphs, **When** match confidence is below 30%, **Then** system prompts user to specify which paragraph to modify.
2. **Given** vague feedback like "needs improvement" without specific guidance, **When** processed, **Then** system asks for clarification on what aspect needs improvement.

---

### Edge Cases

- **Malformed LaTeX**: Input is assumed Overleaf-validated; system uses best-effort processing and warns on structural anomalies without blocking.
- How does the system handle nested LaTeX environments (equation inside figure)?
- What happens when humanizer accidentally removes a placeholder token?
- How does the system behave when supervisor feedback is in a different language than the thesis content?
- What happens when the same paragraph is processed multiple times (idempotency)?

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: System MUST accept both LaTeX source content and supervisor feedback as simultaneous inputs
- **FR-002**: System MUST determine whether supervisor feedback targets global document style or specific paragraphs
- **FR-003**: System MUST execute skill chain in strict order: latex-guard (mask) → academic-polisher → humanizer → latex-guard (unmask)
- **FR-004**: System MUST NOT execute any text modification before LaTeX syntax is masked by latex-guard
- **FR-005**: System MUST preserve all `\cite{}`, `\citep{}`, and `\citet{}` citation commands unchanged
- **FR-006**: System MUST preserve all `\ref{}`, `\label{}`, and cross-reference commands unchanged
- **FR-007**: System MUST preserve all `\begin{equation}`, `\begin{figure}`, `\begin{table}` environments unchanged
- **FR-008**: System MUST use British English spelling conventions (Malaysian academic standard)
- **FR-009**: System MUST support chunked processing for content exceeding 8,000 tokens
- **FR-010**: System MUST implement self-healing when placeholder tokens are accidentally modified
- **FR-011**: System MUST enter clarification mode when supervisor feedback matches source content with <30% confidence
- **FR-012**: System MUST produce identical LaTeX structure when the same input is processed multiple times (idempotency)
- **FR-013**: System MUST generate a change log documenting all modifications made
- **FR-014**: System MUST provide an estimated AI writing score for the output
- **FR-015**: System MUST default humanizer intensity to "high" to meet <10% Turnitin AI detection target

### Key Entities

- **LaTeX Source**: The original thesis content containing text, citations, equations, figures, and tables. Key attributes: raw content, detected LaTeX elements, token count.
- **Supervisor Feedback**: Comments from thesis supervisor indicating required changes. Key attributes: feedback text, target scope (global/specific), matched paragraphs.
- **Masked Content**: Intermediate representation with LaTeX syntax replaced by placeholder tokens. Key attributes: plain text, placeholder map.
- **Change Log**: Record of all modifications made during processing. Key attributes: modification type, original text, revised text, status.
- **Processing Result**: Final output containing revised LaTeX and metadata. Key attributes: modified LaTeX, change log, AI score estimate.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: 100% of LaTeX citation commands (`\cite{}`, `\citep{}`, `\citet{}`) remain unchanged after processing
- **SC-002**: 100% of LaTeX environments (equation, figure, table) remain structurally identical after processing
- **SC-003**: Users can process a single paragraph revision in under 30 seconds
- **SC-004**: System successfully processes chapters up to 20,000 tokens without data loss
- **SC-005**: When evaluated externally by the user (e.g., Turnitin AI Writing), output achieves <10% AI detection score (humanizer intensity defaults to "high")
- **SC-006**: 95% of supervisor feedback items are correctly addressed in the output change log
- **SC-007**: Users can complete a full chapter revision workflow in under 5 minutes
- **SC-008**: System correctly identifies ambiguous feedback (requests clarification) in 90% of edge cases

## Assumptions

- Users provide Overleaf-validated LaTeX input (compilable, syntactically correct)
- Supervisor feedback is provided in English or Chinese (matching user's interface language)
- The three underlying skills (latex-guard, academic-polisher, humanizer) are already implemented and functional
- Token counting uses standard GPT tokenization for the 8,000 token threshold
- British English is the default unless explicitly overridden by user preference
