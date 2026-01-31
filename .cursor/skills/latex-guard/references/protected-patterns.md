# LaTeX Protected Elements Reference

This reference defines all LaTeX elements that MUST be preserved during text editing.

## 1. Citation Commands (CRITICAL)

Never modify these commands or their contents:

| Command | Example | Package |
|---------|---------|---------|
| `\cite{key}` | `\cite{smith2023}` | Standard |
| `\citep{key}` | `\citep{jones2022}` | natbib |
| `\citet{key}` | `\citet{wang2021}` | natbib |
| `\citeauthor{key}` | `\citeauthor{lee2020}` | natbib |
| `\citeyear{key}` | `\citeyear{chen2019}` | natbib |
| `\autocite{key}` | `\autocite{kim2023}` | biblatex |
| `\parencite{key}` | `\parencite{liu2022}` | biblatex |
| `\textcite{key}` | `\textcite{zhang2021}` | biblatex |

**Rule**: Preserve entire command including braces and key contents.

## 2. Cross-Reference Commands (CRITICAL)

| Command | Example | Purpose |
|---------|---------|---------|
| `\ref{label}` | `\ref{fig:architecture}` | Basic reference |
| `\label{name}` | `\label{sec:methodology}` | Label definition |
| `\pageref{label}` | `\pageref{tab:results}` | Page reference |
| `\autoref{label}` | `\autoref{eq:loss}` | Auto-named |
| `\eqref{label}` | `\eqref{eq:gradient}` | Equation |
| `\nameref{label}` | `\nameref{ch:conclusion}` | Named reference |

**Rule**: Preserve entire command including label names.

## 3. URL and Hyperlink Commands (CRITICAL)

| Command | Example |
|---------|---------|
| `\url{address}` | `\url{https://example.com}` |
| `\href{url}{text}` | `\href{https://x.com}{link}` |

**Rule**: Preserve entire command including URL contents.

## 4. Environment Blocks (CRITICAL)

Do not modify anything between `\begin{X}` and `\end{X}` for:

- `figure` - Images and diagrams
- `table` - Data tables
- `equation` - Display equations
- `align` - Aligned equations
- `algorithm` - Pseudocode
- `lstlisting` - Code listings
- `verbatim` - Literal text

**Rule**: Preserve everything inside, including captions, labels, and content.

## 5. Math Content (CRITICAL)

| Syntax | Example | Type |
|--------|---------|------|
| `$...$` | `$x^2 + y^2$` | Inline |
| `\(...\)` | `\(E = mc^2\)` | Inline |
| `\[...\]` | `\[F = ma\]` | Display |
| `$$...$$` | `$$\sum_{i=1}^n$$` | Display |

**Rule**: Preserve all math content exactly.

## 6. File Paths (HIGH)

Patterns to preserve in `\includegraphics`, `\input`, `\include`:

- Directory patterns: `chapter_X/`, `images/`, `figures/`
- Extensions: `.jpg`, `.png`, `.pdf`, `.eps`, `.csv`
- Relative paths: `./`, `../`

**Rule**: Never modify file paths.

## 7. Custom Commands (MEDIUM)

| Command | Example |
|---------|---------|
| `\newcommand` | `\newcommand{\R}{\mathbb{R}}` |
| `\renewcommand` | `\renewcommand{\vec}[1]{\mathbf{#1}}` |

**Rule**: Preserve definitions; custom command usage depends on context.

## Special Character Escaping

When inserting new text, escape these characters:

| Char | Escape | Context |
|------|--------|---------|
| `%` | `\%` | Percentage |
| `&` | `\&` | Ampersand |
| `$` | `\$` | Dollar sign |
| `#` | `\#` | Hash |
| `_` | `\_` | Underscore |
| `{` | `\{` | Brace |
| `}` | `\}` | Brace |
