# Data Model: Thesis Humanizer Skill

**Feature**: 003-thesis-humanizer-skill  
**Date**: 2026-02-03

## Entities

### 1. AI Pattern

A linguistic marker indicating AI-generated text.

| Attribute | Type | Description |
|-----------|------|-------------|
| id | String | Unique identifier (e.g., "vocab-7", "struct-9", "thesis-H1") |
| name | String | Human-readable name (e.g., "AI vocabulary words") |
| category | Enum | One of: vocabulary, structural, promotional, attribution, style, formatting, chatbot, thesis-specific |
| detection_criteria | String | How to identify this pattern in text |
| replacement_strategy | String | Academic-appropriate fix approach |
| examples | List | Before/after example pairs |
| source | Enum | One of: humanizer-inherit, humanizer-adapt, thesis-specific |

**Categories**:
- `vocabulary`: Word/phrase level patterns (#7, #22, #23)
- `structural`: Sentence/paragraph structure (#9, #10, #13)
- `promotional`: Overstated significance (#1-4)
- `attribution`: Vague or formulaic references (#5, #6)
- `style`: Writing style markers (#8, #11, #12, #24)
- `formatting`: Visual presentation (#14-18)
- `chatbot`: AI assistant artifacts (#19-21)
- `thesis-specific`: Academic document patterns (H1-H5)

---

### 2. Protected Element

A LaTeX structural component that must not be modified.

| Attribute | Type | Description |
|-----------|------|-------------|
| type | Enum | One of: citation, cross-reference, figure, table, equation, math, path, comment, custom-macro |
| pattern | Regex | Recognition pattern (e.g., `\\cite\{[^}]+\}`) |
| preserve_content | Boolean | Whether inner content is also protected |

**Protected Element Types**:

| Type | LaTeX Commands | Preserve Content |
|------|----------------|------------------|
| citation | `\cite{}`, `\citep{}`, `\citet{}`, `\citeyear{}` | Yes |
| cross-reference | `\ref{}`, `\label{}`, `\pageref{}`, `\autoref{}` | Yes |
| figure | `\begin{figure}...\end{figure}` | Yes |
| table | `\begin{table}...\end{table}`, `\begin{tabular}` | Yes |
| equation | `\begin{equation}`, `\begin{align}`, `$$...$$`, `\[...\]` | Yes |
| math | `$...$`, `\(...\)` | Yes |
| path | `\input{}`, `\include{}`, `\includegraphics{}` | Yes |
| comment | `%...` (to end of line) | Yes |
| custom-macro | User-defined commands | Yes |

---

### 3. Pass

A single iteration of the humanization workflow.

| Attribute | Type | Description |
|-----------|------|-------------|
| number | Integer | Pass sequence (1-5) |
| name | String | Descriptive name (e.g., "Vocabulary Pass") |
| target_categories | List | Pattern categories addressed in this pass |
| input_text | String | Text at start of pass |
| output_text | String | Text after pass processing |
| changes_made | List | Change Log Entries generated |
| pattern_density_before | Float | Patterns per 100 words before |
| pattern_density_after | Float | Patterns per 100 words after |

**Standard Pass Sequence**:

| Pass | Name | Target Categories |
|------|------|-------------------|
| 1 | Vocabulary | vocabulary |
| 2 | Structure | structural |
| 3 | Transitions | attribution (connectors) |
| 4 | Organization | thesis-specific |
| 5 | Polish | all (final check) |

---

### 4. Change Log Entry

A record of a single modification.

| Attribute | Type | Description |
|-----------|------|-------------|
| line_number | Integer | Location in source file |
| original_text | String | Text before modification |
| replacement_text | String | Text after modification |
| pattern_id | String | Which AI pattern triggered this change |
| pattern_category | Enum | Category of the pattern |
| pass_number | Integer | Which pass made this change |

---

### 5. Processing Session

A complete humanization operation on a document.

| Attribute | Type | Description |
|-----------|------|-------------|
| input_file | Path | Source LaTeX file |
| output_file | Path | Destination file |
| passes_executed | List | List of Pass objects |
| total_changes | Integer | Sum of all changes across passes |
| initial_density | Float | Pattern density before processing |
| final_density | Float | Pattern density after all passes |
| estimated_ai_score | String | Low/Medium/High probability |

---

## Relationships

```
Processing Session
    │
    ├── contains 1..5 → Pass
    │                     │
    │                     └── generates 0..* → Change Log Entry
    │                                            │
    │                                            └── references 1 → AI Pattern
    │
    └── protects 0..* → Protected Element
```

## State Transitions

### Pass State Machine

```
[Not Started] → [In Progress] → [Completed]
                     │
                     └── [Skipped] (if no patterns found)
```

### Session State Machine

```
[Initialized] → [Pass 1] → [Pass 2] → [Pass 3] → [Pass 4] → [Pass 5] → [Completed]
                   │          │          │          │          │
                   └──────────┴──────────┴──────────┴──────────┴── [Early Stop]
                                                                   (density stable or <2)
```

## Validation Rules

### AI Pattern
- `id` must be unique across all patterns
- `category` must be one of the defined enum values
- `examples` must have at least one before/after pair

### Protected Element
- `pattern` must be valid regex
- All LaTeX structural commands must be covered

### Change Log Entry
- `line_number` must be positive integer
- `original_text` must differ from `replacement_text`
- `pattern_id` must reference existing AI Pattern

### Pass
- `number` must be between 1 and 5
- `pattern_density_after` should be ≤ `pattern_density_before`
