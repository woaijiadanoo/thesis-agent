# Research: LaTeX Thesis Proofreading Skills

**Feature**: 001-latex-thesis-skills  
**Date**: 2026-01-31

## Skill-Creator Patterns Research

### Decision: Follow existing skill-creator guidelines
**Rationale**: The project already has a skill-creator skill with comprehensive documentation. Following these patterns ensures consistency and leverages proven approaches.

**Key patterns to apply**:
1. YAML frontmatter with `name` and `description` only
2. Description should include triggering conditions
3. Body contains procedural instructions
4. References folder for domain-specific details (loaded on demand)
5. Keep SKILL.md under 500 lines for context efficiency

### Decision: Leverage existing humanizer skill as Skill C
**Rationale**: The humanizer skill (v2.1.1) is comprehensive and well-documented with 467 lines covering AI writing patterns. No need to recreate this functionality.

**Alternatives considered**:
- Create new humanizer: Rejected (duplication of effort)
- Modify humanizer: Rejected (works well as-is, modifications could break existing use cases)

## LaTeX Protection Patterns Research

### Decision: Instruction-based pattern recognition
**Rationale**: Cursor Skills are prompt-based. Rather than regex code, clear instructions guide Claude to recognize and preserve LaTeX patterns.

**Protected element categories**:

| Category | Patterns | Priority |
|----------|----------|----------|
| Citations | `\cite{}`, `\citep{}`, `\citet{}`, `\autocite{}` | Critical |
| References | `\ref{}`, `\label{}`, `\pageref{}`, `\autoref{}` | Critical |
| URLs | `\url{}`, `\href{}` | Critical |
| Environments | `\begin{X}...\end{X}` for figure, table, equation, algorithm, lstlisting | Critical |
| Math | `$...$`, `\(...\)`, `\[...\]`, `$$...$$` | Critical |
| File paths | `chapter_X/`, `.jpg`, `.png`, `.pdf`, `.eps` | High |
| Custom commands | `\newcommand`, `\renewcommand` definitions | Medium |

**Alternatives considered**:
- Regex-based scripts: Rejected (skills are prompt-based, scripts add complexity)
- External LaTeX parser: Rejected (overkill for this use case, requires Python dependencies)

## Malaysian Academic Style Research

### Decision: Passive voice + formal vocabulary focus
**Rationale**: Malaysian university thesis guidelines (UM, UPM, UTM) emphasize formal academic English with passive voice and third-person perspective.

**Key style rules**:
1. No first-person pronouns (I, We, My, Our)
2. Passive voice for methodology/results
3. Objective descriptions using "This study", "The analysis"
4. Minimum 3 sentences per paragraph
5. Formal vocabulary (avoid colloquialisms)

**Reference**: Existing rules in `.cursor/rules/thesis-writing-standards.mdc` already capture these conventions.

## Pipeline Integration Research

### Decision: Optional combined workflow skill
**Rationale**: Users want both independent skill invocation and combined pipeline mode. A separate pipeline skill provides the combined workflow without coupling the individual skills.

**Execution order**:
1. LaTeX Guard (structure protection context)
2. Academic Polisher (style improvements)
3. Humanizer (optional, for AI pattern reduction)

**Alternatives considered**:
- Single monolithic skill: Rejected (violates modularity requirement)
- Automatic chaining: Rejected (users need control over which skills to apply)

## Terminology Reference Research

### Decision: Optional file-based context
**Rationale**: Users process chapters independently but need thesis-wide consistency. An optional terminology file provides this context without requiring it.

**File format**: Markdown with sections for:
- Abbreviations (full form → abbreviation)
- Key terms (canonical spelling/usage)
- Chapter-specific notes

**Alternatives considered**:
- Database/JSON format: Rejected (Markdown is human-readable and editable)
- Required file: Rejected (should work without it for quick edits)
