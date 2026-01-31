# Data Model: Protected Elements Taxonomy

**Feature**: 001-latex-thesis-skills  
**Date**: 2026-01-31

## Overview

This document defines the taxonomy of LaTeX elements that must be protected during thesis proofreading. These elements form the "Protected Element" entity from the specification.

## Protected Element Categories

### 1. Citation Commands (CRITICAL - Never Modify)

| Command | Example | Notes |
|---------|---------|-------|
| `\cite{key}` | `\cite{smith2023}` | Basic citation |
| `\citep{key}` | `\citep{jones2022}` | Parenthetical citation (natbib) |
| `\citet{key}` | `\citet{wang2021}` | Textual citation (natbib) |
| `\citeauthor{key}` | `\citeauthor{lee2020}` | Author only |
| `\citeyear{key}` | `\citeyear{chen2019}` | Year only |
| `\autocite{key}` | `\autocite{kim2023}` | BibLaTeX citation |
| `\parencite{key}` | `\parencite{liu2022}` | BibLaTeX parenthetical |
| `\textcite{key}` | `\textcite{zhang2021}` | BibLaTeX textual |

**Protection rule**: Preserve entire command including braces and key contents.

### 2. Cross-Reference Commands (CRITICAL - Never Modify)

| Command | Example | Notes |
|---------|---------|-------|
| `\ref{label}` | `\ref{fig:architecture}` | Basic reference |
| `\label{name}` | `\label{sec:methodology}` | Label definition |
| `\pageref{label}` | `\pageref{tab:results}` | Page reference |
| `\autoref{label}` | `\autoref{eq:loss}` | Auto-named reference |
| `\eqref{label}` | `\eqref{eq:gradient}` | Equation reference |
| `\nameref{label}` | `\nameref{ch:conclusion}` | Named reference |

**Protection rule**: Preserve entire command including label names.

### 3. URL and Hyperlink Commands (CRITICAL - Never Modify)

| Command | Example | Notes |
|---------|---------|-------|
| `\url{address}` | `\url{https://example.com}` | Plain URL |
| `\href{url}{text}` | `\href{https://x.com}{link}` | Hyperlink with text |

**Protection rule**: Preserve entire command including URL contents.

### 4. Environment Blocks (CRITICAL - Never Modify Contents)

| Environment | Purpose | Content to Protect |
|-------------|---------|-------------------|
| `figure` | Images/diagrams | Everything between `\begin{figure}` and `\end{figure}` |
| `table` | Data tables | Everything between `\begin{table}` and `\end{table}` |
| `equation` | Display equations | Everything between `\begin{equation}` and `\end{equation}` |
| `align` | Aligned equations | Everything between `\begin{align}` and `\end{align}` |
| `algorithm` | Pseudocode | Everything between `\begin{algorithm}` and `\end{algorithm}` |
| `lstlisting` | Code listings | Everything between `\begin{lstlisting}` and `\end{lstlisting}` |
| `verbatim` | Literal text | Everything between `\begin{verbatim}` and `\end{verbatim}` |

**Protection rule**: Do not modify anything inside these environments, including captions, labels, and content.

### 5. Math Content (CRITICAL - Never Modify)

| Syntax | Example | Notes |
|--------|---------|-------|
| `$...$` | `$x^2 + y^2$` | Inline math |
| `\(...\)` | `\(E = mc^2\)` | LaTeX inline math |
| `\[...\]` | `\[F = ma\]` | Display math |
| `$$...$$` | `$$\sum_{i=1}^n$$` | TeX display math |

**Protection rule**: Preserve all math content exactly as written.

### 6. File Paths (HIGH - Preserve Exactly)

| Pattern | Example | Context |
|---------|---------|---------|
| `chapter_X/` | `chapter_4/figure1.jpg` | Figure paths |
| `.jpg`, `.png` | `images/diagram.png` | Image files |
| `.pdf`, `.eps` | `figures/plot.pdf` | Vector graphics |
| `./`, `../` | `./data/results.csv` | Relative paths |

**Protection rule**: Never modify file paths in `\includegraphics`, `\input`, `\include` commands.

### 7. Custom Commands (MEDIUM - Context Dependent)

| Command | Example | Notes |
|---------|---------|-------|
| `\newcommand` | `\newcommand{\R}{\mathbb{R}}` | Definition - preserve |
| `\renewcommand` | `\renewcommand{\vec}[1]{\mathbf{#1}}` | Redefinition - preserve |
| Custom usage | `\R`, `\vec{x}` | Usage - preserve |

**Protection rule**: Preserve definitions; usage depends on context.

## Editable Prose Definition

Text that CAN be modified includes:
- Paragraph text outside protected environments
- Section/subsection titles (with supervisor approval)
- Caption text (style only, not references within)
- Comments in LaTeX (`% comment`)

## Special Character Escaping

When inserting or modifying text, escape these characters:

| Character | Escape | Context |
|-----------|--------|---------|
| `%` | `\%` | Percentage in text |
| `&` | `\&` | Ampersand in text |
| `$` | `\$` | Dollar sign in text |
| `#` | `\#` | Hash in text |
| `_` | `\_` | Underscore in text |
| `{` | `\{` | Brace in text |
| `}` | `\}` | Brace in text |

## Validation Checklist

After processing, verify:
- [ ] All `\cite` commands unchanged
- [ ] All `\ref` and `\label` commands unchanged
- [ ] All environment blocks intact
- [ ] All math expressions unchanged
- [ ] All file paths unchanged
- [ ] No LaTeX syntax errors introduced
