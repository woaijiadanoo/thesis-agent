---
name: latex-guard
description: |
  Protect LaTeX structural elements during thesis text editing and proofreading.
  Use when editing or polishing LaTeX thesis content (.tex files) to ensure all
  citations, cross-references, figures, tables, equations, and file paths remain
  unchanged. Triggers on: (1) LaTeX thesis chapter editing, (2) Academic text
  proofreading with LaTeX, (3) Requests mentioning "protect citations" or
  "preserve references", (4) Thesis chapter polish requests with .tex files.
---

# LaTeX Guard: Structure Protection for Thesis Editing

Protect all LaTeX structural elements while editing thesis text content.

## Your Task

When editing LaTeX thesis content:

1. **Identify protected elements** - Scan for patterns below
2. **Preserve them exactly** - Do not modify protected content
3. **Edit only prose** - Modify text outside protected elements
4. **Escape special characters** - When inserting new text
5. **Output complete LaTeX** - Return compilable code

## Protected Elements (NEVER MODIFY)

### Citation Commands

Preserve entire command including braces and content:

```latex
\cite{key}      \citep{key}     \citet{key}
\citeauthor{key} \citeyear{key}
\autocite{key}  \parencite{key} \textcite{key}
```

### Cross-References

```latex
\ref{label}     \label{name}    \pageref{label}
\autoref{label} \eqref{label}   \nameref{label}
```

### URL Commands

```latex
\url{address}   \href{url}{text}
```

### Environment Blocks

Do not modify anything between `\begin{X}` and `\end{X}`:

- `figure`, `table`, `equation`, `align`
- `algorithm`, `lstlisting`, `verbatim`

### Math Content

```latex
$...$           \(...\)
\[...\]         $$...$$
```

### File Paths

Preserve paths in `\includegraphics`, `\input`, `\include`:

```latex
\includegraphics{chapter_4/figure1.jpg}
\input{sections/methodology}
```

## Editable Content

Text that CAN be modified:
- Paragraph prose outside protected elements
- Section titles (with caution)
- Caption text (style only, preserve internal references)

## Special Character Escaping

When inserting new text, escape:

| Character | Escape As |
|-----------|-----------|
| % | `\%` |
| & | `\&` |
| $ | `\$` |
| # | `\#` |
| _ | `\_` |

## Edge Cases

### Malformed Citations

If a citation appears malformed (unclosed brace, unusual characters):
- Preserve it exactly as-is
- Do not attempt to "fix" it
- User will verify in Overleaf

### Nested Environments

If environments are nested (table inside figure):
- Protect the entire outer environment
- Do not edit any content within

### Minimal Editable Content

If text is mostly within protected environments:
- Return with minimal changes
- Note which areas were editable
- Do not force changes where none needed

### Mixed Content Lines

If a line contains both prose and protected elements:

```latex
The results shown in Figure~\ref{fig:results} demonstrate...
```

- Edit "The results shown in" and "demonstrate..." if needed
- Preserve `Figure~\ref{fig:results}` exactly

## Output Format

Return complete, compilable LaTeX code:

```latex
\section{Results and Discussion}
\label{sec:results}

The experimental results demonstrate significant improvements 
in classification accuracy. As shown in Figure~\ref{fig:results}, 
the proposed method achieved 94.5\% accuracy on the benchmark 
dataset \citep{smith2023}.
```

## Detailed Patterns

For comprehensive pattern lists, see [references/protected-patterns.md](references/protected-patterns.md).

## Process

1. Read the input LaTeX content
2. Identify all protected elements (mark mentally)
3. Make text improvements only in prose sections
4. Verify no protected elements were changed
5. Ensure proper character escaping in new text
6. Return complete LaTeX that can replace original
