# Chunking Strategy: Long LaTeX Document Handling

This document defines how `thesis-refine-with-latex` splits long LaTeX documents for processing.

## When to Chunk

Chunk documents when token count exceeds **8,000 tokens** (using GPT tokenization).

## Chunking Priority

Split at these boundaries in priority order:

```
Priority 1: Before \section{} boundaries
Priority 2: Before \subsection{} boundaries
Priority 3: After \end{figure}, \end{table}, \end{equation}
Priority 4: At paragraph boundaries (double newline)
Priority 5: At sentence boundaries (last resort)
```

## Safe Split Points

| Pattern | Safety | Notes |
|---------|--------|-------|
| Before `\section{}` | ✅ Safe | Natural chapter structure |
| Before `\subsection{}` | ✅ Safe | Natural section structure |
| After `\end{figure}` | ✅ Safe | Environment complete |
| After `\end{table}` | ✅ Safe | Environment complete |
| After `\end{equation}` | ✅ Safe | Math block complete |
| Double newline | ⚠️ Conditional | Only if not inside environment |
| Mid-paragraph | ❌ Avoid | Breaks context |

## NEVER Split

- Inside `\begin{...}` and `\end{...}` pairs
- Inside math mode (`$...$`, `\[...\]`)
- Inside citation commands
- Mid-sentence (if avoidable)

## Context Overlap

- **Overlap size**: 500 tokens
- **Purpose**: Maintain coherence for academic-polisher decisions
- **Implementation**: Include last paragraph of previous chunk as read-only context

### Overlap Handling

```
Chunk 1: [content A ... content B ... last_paragraph]
Chunk 2: [last_paragraph (read-only) ... content C ... content D]
Chunk 3: [last_paragraph_of_chunk2 (read-only) ... content E ...]
```

When reassembling:
1. Process each chunk with its context prefix
2. When joining, remove the overlapping portions
3. Keep only the newly processed content from each chunk

## Chunk Processing Flow

```
1. Calculate total token count
2. If <= 8000 tokens: Process as single unit
3. If > 8000 tokens:
   a. Find all safe split points
   b. Create chunks of ~7000 tokens each (leaving room for context)
   c. Add 500-token overlap from previous chunk
   d. Process each chunk through pipeline
   e. Remove overlap duplicates when reassembling
```

## Example Chunking

Given a 15,234 token chapter:

```
Processing chapter (15,234 tokens)...
  Chunk 1/3: Section 4.1-4.2 (5,102 tokens)
    - Split point: Before \section{4.3}
    - Context prefix: None (first chunk)
  
  Chunk 2/3: Section 4.3-4.4 (5,890 tokens)
    - Split point: Before \section{4.5}
    - Context prefix: Last paragraph of Section 4.2 (500 tokens)
  
  Chunk 3/3: Section 4.5 (4,742 tokens)
    - Split point: End of document
    - Context prefix: Last paragraph of Section 4.4 (500 tokens)

Reassembling... ✓
Total: 15,234 tokens processed
All 23 LaTeX elements preserved.
```

## Validation After Chunking

Before processing each chunk, verify:

- [ ] Chunk does not start mid-environment
- [ ] Chunk does not end mid-environment
- [ ] All `\begin{}` have matching `\end{}` within chunk
- [ ] No orphaned math delimiters

## Error Recovery

If a safe split point cannot be found within reasonable bounds:

1. Extend chunk size slightly to reach next safe point
2. Log warning about extended chunk
3. If chunk exceeds 10,000 tokens, force split at paragraph boundary
4. Mark forced splits in warnings for user review
