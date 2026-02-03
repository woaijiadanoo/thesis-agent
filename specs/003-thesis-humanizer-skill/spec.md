# Feature Specification: Thesis Humanizer Skill

**Feature Branch**: `003-thesis-humanizer-skill`  
**Created**: 2026-02-03  
**Status**: Draft  
**Input**: User description: "Create thesis-humanizer skill for academic AI detection reduction, merging humanizer's 24 AI patterns with academic adaptations"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Basic Thesis Chapter Humanization (Priority: P1)

A PhD student has written a thesis chapter using AI assistance and needs to reduce AI-detectable patterns before submission. They invoke the thesis-humanizer skill on their LaTeX file and receive humanized output that passes Turnitin AI Writing detection while maintaining academic formality and preserving all LaTeX structural elements.

**Why this priority**: This is the core use case - transforming AI-assisted academic text to pass plagiarism detection while maintaining quality. Without this, the skill has no value.

**Independent Test**: Can be fully tested by providing a LaTeX chapter file and verifying the output (1) passes Turnitin AI detection <10%, (2) maintains academic tone, (3) preserves all citations and references intact.

**Acceptance Scenarios**:

1. **Given** a LaTeX thesis chapter with AI-detectable patterns, **When** user invokes thesis-humanizer, **Then** the output text contains fewer AI vocabulary patterns (e.g., "crucial", "delve", "foster" replaced with academic alternatives)
2. **Given** a LaTeX file with `\cite{}`, `\ref{}`, figures, and equations, **When** thesis-humanizer processes the file, **Then** all LaTeX structural elements remain unchanged
3. **Given** AI-generated text with promotional language, **When** processed by thesis-humanizer, **Then** promotional terms are replaced with neutral academic language

---

### User Story 2 - Multi-Pass Iterative Refinement (Priority: P2)

A user's first humanization pass still shows some AI patterns. They need to run additional passes targeting specific sections or pattern types until the document achieves acceptable AI detection scores.

**Why this priority**: Single-pass humanization is often insufficient. Iterative refinement is essential for achieving <10% AI detection consistently.

**Independent Test**: Can be tested by running multiple passes on a chapter and measuring AI pattern density reduction after each pass.

**Acceptance Scenarios**:

1. **Given** a partially humanized document, **When** user requests additional passes, **Then** the skill identifies remaining AI patterns and applies targeted fixes
2. **Given** a document with repetitive chapter organization patterns (e.g., "Chapter X presents..."), **When** processed through rhythm variation pass, **Then** sentence structures are varied while maintaining meaning
3. **Given** output from pass N, **When** pass N+1 is applied, **Then** AI pattern count decreases or stabilizes (no regression)

---

### User Story 3 - Pattern-Specific Targeted Humanization (Priority: P3)

A user wants to focus on specific AI pattern types (vocabulary, structure, or promotional language) rather than running a full humanization. They can invoke the skill with pattern-type filters.

**Why this priority**: Advanced users may want fine-grained control to address specific Turnitin feedback or to preserve certain writing styles while fixing others.

**Independent Test**: Can be tested by selecting a single pattern category and verifying only those patterns are modified.

**Acceptance Scenarios**:

1. **Given** a document with mixed AI patterns, **When** user requests vocabulary-only humanization, **Then** only AI vocabulary words are replaced; structural patterns remain
2. **Given** a document flagged for "rule of three" overuse, **When** user requests structural pattern fix, **Then** list patterns are varied without changing vocabulary

---

### User Story 4 - Change Log Generation (Priority: P3)

After humanization, the user needs a detailed record of all modifications made to review and potentially revert specific changes.

**Why this priority**: Academic writing requires accountability. Users need to understand and approve changes made to their work.

**Independent Test**: Can be tested by humanizing a document and verifying the change log contains before/after pairs for each modification.

**Acceptance Scenarios**:

1. **Given** any humanization operation, **When** processing completes, **Then** a change log is generated listing all modifications with line numbers
2. **Given** a change log, **When** user reviews it, **Then** each entry shows original text, replacement text, and pattern category

---

### Edge Cases

- What happens when the input file has no detectable AI patterns? → Skill should report "no changes needed" rather than making unnecessary modifications
- How does the skill handle LaTeX comments? → Comments should be preserved unchanged
- What happens with non-English content in a primarily English document? → Non-English sections should be flagged but not modified
- How does the skill handle custom LaTeX macros? → Custom macros should be treated as protected elements
- What happens if the file exceeds reasonable processing size? → Skill should support chunked processing for large documents

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: Skill MUST detect and replace AI vocabulary patterns (minimum 50 known AI-indicative words/phrases)
- **FR-002**: Skill MUST preserve all LaTeX structural elements including `\cite{}`, `\citep{}`, `\citet{}`, `\ref{}`, `\label{}`, figure environments, table environments, equation environments, and math content
- **FR-003**: Skill MUST maintain academic tone (third person, passive voice, formal register)
- **FR-004**: Skill MUST support iterative multi-pass processing (minimum 3-5 passes)
- **FR-005**: Skill MUST generate a modification change log for each processing run
- **FR-006**: Skill MUST vary sentence rhythm to break AI-detectable structural patterns
- **FR-007**: Skill MUST handle thesis-specific patterns (chapter organization, RQ/RO/RC structures, literature review formulaic phrases)
- **FR-008**: Skill MUST merge and apply all 24 humanizer AI detection patterns with academic-appropriate adaptations
- **FR-009**: Skill MUST use British English conventions for thesis content
- **FR-010**: Skill MUST provide pattern density estimation after processing

### Key Entities

- **AI Pattern**: A linguistic marker indicating AI-generated text; includes pattern category (vocabulary, structural, promotional, attribution, style, formatting, chatbot artifact), detection criteria, and academic-appropriate replacement strategy
- **Protected Element**: A LaTeX structural component that must not be modified; includes citations, cross-references, figures, tables, equations, math content, and file paths
- **Pass**: A single iteration of the humanization workflow targeting specific pattern categories; includes input text, output text, patterns addressed, and changes made
- **Change Log Entry**: A record of a single modification; includes original text, replacement text, pattern category, and location (line number or section)

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Processed thesis chapters achieve Turnitin AI Writing detection score below 10%
- **SC-002**: 100% of LaTeX structural elements (citations, references, figures, equations) remain unchanged after processing
- **SC-003**: Users can complete a full chapter humanization (including all passes) within 30 minutes
- **SC-004**: At least 90% of AI vocabulary patterns in a document are identified and replaced with appropriate academic alternatives
- **SC-005**: Change logs accurately reflect all modifications with zero missed entries
- **SC-006**: Processed text maintains equivalent readability and academic quality as judged by thesis supervisors

## Assumptions

- Users have existing LaTeX thesis content that may contain AI-detectable patterns
- Turnitin AI Writing detection is the primary benchmark for success
- British English is the default language variant (Malaysian university context)
- The skill operates within the Cursor IDE environment
- Input files are well-formed LaTeX documents
- Users may need multiple passes to achieve desired AI detection scores
