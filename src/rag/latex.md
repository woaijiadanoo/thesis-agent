# LaTeX Rules and Tags

This document centralizes LaTeX usage for the thesis based on `sample-chapter.tex`.

## Citations and Acronyms

- Citations: `\cite{key}` (single or multiple keys separated by commas)
- Acronyms: `\acrshort{IoV}`, `\acrshort{PPF}`, `\acrshort{SBM}` on first use

## Cross-References

- Figures: `\ref{fig:chap1:V2X}`, `\label{fig:chap1:V2X}`
- Tables: `\ref{tab:chap1:ps_rq_ro}`, `\label{tab:chap1:ps_rq_ro}`

## Figures and Tables

- Figures: `\begin{figure}[H]`, `\includegraphics{...}`, `\caption{...}`
- Tables: `\begin{table}[H]`, `\begin{tabular}{...}`

## Technical Formatting

- Math in text: `$O(n^2)$`, `$<200$~ms`
- Units and spacing: `10~Hz`, `100~ms`, `1--3~metres`, `50,000--100,000`
- Acceleration: `m/s\textsuperscript{2}`

## Escaping Special Characters

Use backslash escapes in text:

- Percent: `\%`
- Ampersand: `\&`
- Underscore: `\_`
- Hash: `\#`
- Dollar: `\$`
- Curly braces when literal: `\{` and `\}`

## Ranges and Dashes

- Use `--` for numeric ranges: `2018--2022`, `50,000--100,000`
- Use `-` for hyphenated terms inside words: `multi-chain`, `end-to-end`
