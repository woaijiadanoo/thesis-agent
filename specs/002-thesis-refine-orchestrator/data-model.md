# Data Model: thesis-refine-with-latex

**Branch**: `002-thesis-refine-orchestrator` | **Date**: 2026-02-01
**New Skill**: `thesis-refine-with-latex` (LaTeX-specific orchestrator)

## Overview

This document defines the conceptual entities used by the `thesis-refine-with-latex` skill. Since this is a Cursor Agent Skill (not a database-backed system), these entities exist as in-memory structures during processing.

---

## Entity Definitions

### 1. ProcessingRequest

The input bundle provided by the user.

| Attribute | Type | Description |
|-----------|------|-------------|
| source_latex | string | Original LaTeX content (Overleaf-validated) |
| supervisor_feedback | string | Supervisor's comments/requirements |
| target_scope | enum | `global` or `specific` |
| options | Options | Processing configuration |

**Options**:
| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| humanizer_intensity | enum | `high` | `low`, `medium`, `high` |
| enable_clarification | boolean | true | Allow clarification prompts |
| language | enum | `en-GB` | British English default |

---

### 2. LaTeXSource

Parsed representation of the input LaTeX.

| Attribute | Type | Description |
|-----------|------|-------------|
| raw_content | string | Unmodified LaTeX source |
| token_count | integer | GPT tokenization count |
| sections | Section[] | Parsed section structure |
| protected_elements | ProtectedElement[] | Detected LaTeX structures |

**Section**:
| Attribute | Type | Description |
|-----------|------|-------------|
| id | string | Section label (e.g., `sec:methodology`) |
| title | string | Section heading text |
| level | integer | 1=section, 2=subsection, 3=subsubsection |
| content | string | Section body content |
| start_line | integer | Line number in source |
| token_count | integer | Section token count |

**ProtectedElement**:
| Attribute | Type | Description |
|-----------|------|-------------|
| type | enum | `citation`, `reference`, `equation`, `figure`, `table`, `url` |
| pattern | string | Original LaTeX pattern |
| placeholder | string | Replacement token (e.g., `__CITE_001__`) |
| start_pos | integer | Character position in source |
| end_pos | integer | Character position in source |

---

### 3. SupervisorFeedback

Parsed and analyzed supervisor comments.

| Attribute | Type | Description |
|-----------|------|-------------|
| raw_text | string | Original feedback text |
| target_scope | enum | `global` or `specific` |
| keywords | string[] | Extracted keywords for matching |
| matched_sections | MatchResult[] | Candidate section matches |
| confidence | float | Overall match confidence (0-1) |
| requires_clarification | boolean | True if confidence <0.30 |

**MatchResult**:
| Attribute | Type | Description |
|-----------|------|-------------|
| section_id | string | Matched section identifier |
| score | float | Keyword overlap score (0-1) |
| matched_keywords | string[] | Keywords found in section |

---

### 4. MaskedContent

Intermediate representation after latex-guard masking.

| Attribute | Type | Description |
|-----------|------|-------------|
| plain_text | string | Content with placeholders |
| placeholder_map | Map<string, string> | placeholder → original LaTeX |
| chunk_boundaries | integer[] | Safe split positions |

---

### 5. ProcessingChunk

Unit of processing for long documents.

| Attribute | Type | Description |
|-----------|------|-------------|
| chunk_id | integer | Sequential chunk number |
| content | string | Chunk text content |
| context_prefix | string | Overlap from previous chunk (read-only) |
| section_ids | string[] | Sections included in chunk |
| token_count | integer | Chunk token count |

---

### 6. ChangeLogEntry

Single modification record.

| Attribute | Type | Description |
|-----------|------|-------------|
| id | string | Unique entry ID |
| modification_type | enum | `academic_polish`, `humanize`, `expand`, `clarify` |
| source_skill | string | Which skill made the change |
| original_text | string | Text before modification |
| revised_text | string | Text after modification |
| feedback_reference | string | Related supervisor feedback (if any) |
| status | enum | `done`, `partial`, `skipped` |

---

### 7. ProcessingResult

Final output of the orchestrator.

| Attribute | Type | Description |
|-----------|------|-------------|
| modified_latex | string | Final processed LaTeX |
| change_log | ChangeLogEntry[] | All modifications made |
| ai_score_estimate | float | Estimated AI pattern density |
| warnings | string[] | Any issues encountered |
| processing_time | integer | Total processing time (seconds) |

---

## Entity Relationships

```
ProcessingRequest
    │
    ├── LaTeXSource (parsed from source_latex)
    │       │
    │       └── Section[] ──────────────┐
    │               │                    │
    │               └── ProtectedElement[]
    │
    ├── SupervisorFeedback (parsed from supervisor_feedback)
    │       │
    │       └── MatchResult[] ←─────────┘ (references Section)
    │
    └── Options

LaTeXSource
    │
    └── MaskedContent (after latex-guard mask)
            │
            └── ProcessingChunk[] (if chunking needed)

ProcessingChunk[]
    │
    └── (processed through academic-polisher → humanizer)
            │
            └── ProcessingResult
                    │
                    ├── modified_latex
                    ├── ChangeLogEntry[]
                    └── ai_score_estimate
```

---

## State Transitions

### Document Processing States

```
┌─────────────┐
│   RECEIVED  │ ← Initial input
└──────┬──────┘
       │
       ▼
┌─────────────┐
│   PARSED    │ ← LaTeXSource + SupervisorFeedback created
└──────┬──────┘
       │
       ▼ (if confidence < 0.30)
┌─────────────┐
│  CLARIFYING │ ← Awaiting user paragraph selection
└──────┬──────┘
       │
       ▼
┌─────────────┐
│   MASKED    │ ← latex-guard applied
└──────┬──────┘
       │
       ▼ (if token_count > 8000)
┌─────────────┐
│  CHUNKING   │ ← Document split into chunks
└──────┬──────┘
       │
       ▼
┌─────────────┐
│ PROCESSING  │ ← academic-polisher + humanizer running
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  VERIFYING  │ ← Placeholder integrity check
└──────┬──────┘
       │
       ▼ (if placeholders lost)
┌─────────────┐
│   HEALING   │ ← Self-healing recovery
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  UNMASKING  │ ← latex-guard unmask
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  COMPLETE   │ ← ProcessingResult returned
└─────────────┘
```

---

## Validation Rules

### LaTeXSource

- `token_count` must be calculable (valid UTF-8)
- At least one parseable section OR content outside sections

### SupervisorFeedback

- Cannot be empty string
- Must have at least 2 extractable keywords

### MaskedContent

- `placeholder_map` must be non-empty if `protected_elements` exist
- Each placeholder must be unique

### ProcessingResult

- `modified_latex` must pass basic LaTeX syntax validation
- All placeholders from `placeholder_map` must be restored
- `ai_score_estimate` must be in range [0, 1]
