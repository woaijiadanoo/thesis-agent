# Self-Healing: Placeholder Recovery

This document defines how `thesis-refine-with-latex` recovers from placeholder loss during processing.

## When Self-Healing is Needed

Placeholders can be lost when:
- Humanizer rewrites sentences containing placeholders
- Sentence restructuring moves or removes placeholder tokens
- Aggressive AI pattern removal accidentally includes placeholder text

## Verification Process

After humanizer and before unmask:

```
For each placeholder in placeholder_map:
    If placeholder NOT in processed_text:
        Mark as LOST
        Add to recovery_queue
        Log warning

If recovery_queue is not empty:
    Trigger self-healing
```

## Recovery Strategies

Try recovery methods in order:

### Strategy 1: Context Matching

Use surrounding context to find insertion point:

```
1. Get 20 characters before original placeholder position
2. Get 20 characters after original placeholder position
3. Search for this context pattern in processed text
4. If found: Insert placeholder at matched position
5. Confidence: HIGH
```

### Strategy 2: Fuzzy Context Matching

If exact context not found:

```
1. Use same context strings as Strategy 1
2. Search with edit distance tolerance < 5
3. If similar context found: Insert placeholder there
4. Confidence: MEDIUM
```

### Strategy 3: Paragraph Append

If context matching fails:

```
1. Identify which paragraph originally contained placeholder
2. Find the corresponding paragraph in processed text
3. Append placeholder at end of paragraph with warning marker
4. Confidence: LOW
```

### Strategy 4: Document Append (Fallback)

If paragraph cannot be identified:

```
1. Append placeholder at end of processed content
2. Mark with special warning: [RECOVERED - POSITION UNCERTAIN]
3. Alert user to manually verify placement
4. Confidence: VERY LOW
```

## Recovery Logging

For each recovered placeholder:

```
⚠️ Self-Healing Applied:
  - Placeholder: __CITE_003__
  - Original: \citep{jones2022}
  - Recovery method: Context matching (HIGH confidence)
  - Inserted at: Line 89, after "findings suggest"
  
  - Placeholder: __REF_007__
  - Original: Figure~\ref{fig:results}
  - Recovery method: Paragraph append (LOW confidence)
  - Inserted at: End of paragraph, line 156
  - ⚠️ Please verify placement manually
```

## Warning Levels

| Recovery Method | Confidence | Warning Level |
|-----------------|------------|---------------|
| Context matching | HIGH | Info |
| Fuzzy matching | MEDIUM | Warning |
| Paragraph append | LOW | Warning + Manual review |
| Document append | VERY LOW | Error + Manual review required |

## Change Log Integration

Self-healing events MUST appear in change log:

```
## Change Log

...other modifications...

Self-healing:
- [RECOVERED] Line 89: \citep{jones2022} (context match)
- [RECOVERED] Line 156: Figure~\ref{fig:results} (paragraph append) ⚠️ VERIFY
```

## Prevention Guidelines

To minimize placeholder loss:

1. **Humanizer constraints**: When applying humanizer, instruct it to preserve tokens matching `__[A-Z]+_[0-9]+__` pattern
2. **Sentence boundaries**: Prefer rewrites that keep placeholders at sentence boundaries
3. **Atomic units**: Treat `text + placeholder` as atomic unit when possible

## Verification After Recovery

After self-healing completes:

```
For each recovered placeholder:
    Verify placeholder now exists in processed_text
    If still missing: Mark as UNRECOVERABLE
    
If any UNRECOVERABLE:
    STOP processing
    Return error with list of lost elements
    Suggest user manually re-add LaTeX elements
```

## Error Response

If recovery fails completely:

```
❌ Self-Healing Failed

Unable to recover the following LaTeX elements:
1. \citep{smith2023} - Original line 45
2. \ref{fig:architecture} - Original line 78

Please manually re-add these elements to the output or 
retry processing with a smaller text segment.
```
