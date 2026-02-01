# Change Log Format

This document defines the structured output format for change logs in `thesis-refine-with-latex`.

## Change Log Structure

Every processing run produces a change log with these sections:

```markdown
## Change Log

**Processing Info**
- Input tokens: NNNN
- Chunks processed: N
- Total modifications: NN

**Feedback Items**
[List of parsed supervisor feedback items with tracking status]

**Modifications**
[Numbered list of all changes made]

**Self-healing** (if any)
[List of recovered placeholders]

**Summary**
- Modifications: NN total
- Feedback addressed: N/N items
- AI score estimate: ~N%
```

## Feedback Item Tracking

Parse supervisor feedback into numbered items:

```
**Feedback Items**

Original feedback: "improve clarity in methodology, fix passive voice, 
make conclusion impactful"

Parsed items:
1. [F1] [methodology] Improve clarity → 2 changes (done)
2. [F2] [global] Fix passive voice → 3 changes (done)
3. [F3] [conclusion] Make impactful → 0 changes (skipped: already impactful)
```

### Item Status Values

- `done` - Feedback fully addressed
- `partial` - Some aspects addressed, others not applicable
- `skipped` - Not applicable (with rationale)
- `clarified` - User clarification was requested and received

## Modification Entry Format

Each modification follows this format:

```
N. [source_step] [feedback_ref?] Location: "original" → "revised"
```

### Source Steps

- `[academic_polish]` - Changed by academic-polisher
- `[humanize]` - Changed by humanizer
- `[expand]` - Content added based on feedback
- `[clarify]` - Restructured for clarity
- `[self_heal]` - Recovered by self-healing

### Examples

```
**Modifications**

1. [academic_polish] [F1] Line 15: "We observed" → "It was observed that"
2. [academic_polish] [F2] Line 23: "shows" → "demonstrates"
3. [academic_polish] [F2] Line 31: "get" → "obtain"
4. [humanize] Line 45: Removed "Furthermore" sentence opener
5. [humanize] Line 52: Restructured rule-of-three pattern
6. [expand] [F1] Line 67: Added supporting sentence: "This approach..."
7. [humanize] Line 78: "In conclusion" → "The findings indicate"
```

## Chunk-Level Logging

For chunked documents, include chunk markers:

```
**Modifications**

--- Chunk 1/3 (Section 4.1-4.2) ---
1. [academic_polish] Line 15: "We observed" → "It was observed that"
2. [humanize] Line 31: Removed "Furthermore"

--- Chunk 2/3 (Section 4.3-4.4) ---
3. [academic_polish] Line 89: "big" → "significant"
4. [expand] [F1] Line 102: Added clarifying sentence

--- Chunk 3/3 (Section 4.5) ---
5. [humanize] Line 156: Restructured conclusion
```

## Clarification Logging

When user clarification was requested:

```
**Clarification Log**

Feedback: "improve the CNN section"
- Initial confidence: 28% (below 30% threshold)
- Candidates presented: 3
  1. Section 4.2 (28%) - "The CNN model achieved..."
  2. Section 4.3 (22%) - "Accuracy improvements..."
  3. Section 3.1 (18%) - "The proposed architecture..."
- User selection: 1 (Section 4.2)
- Outcome: Applied changes to Section 4.2
```

## Self-Healing Section

If any placeholders were recovered:

```
**Self-healing**

- [RECOVERED] Line 89: \citep{jones2022}
  Method: Context matching (HIGH confidence)
  
- [RECOVERED] Line 156: Figure~\ref{fig:results}
  Method: Paragraph append (LOW confidence)
  ⚠️ Please verify placement manually
```

## Summary Section

```
**Summary**

| Metric | Value |
|--------|-------|
| Total modifications | 12 |
| Academic polish changes | 5 |
| Humanizer changes | 6 |
| Expansions | 1 |
| Feedback items addressed | 3/3 (100%) |
| Self-healing recoveries | 2 |
| AI score estimate | ~7% ✓ |
| Processing time | 45 seconds |

Status: ✓ All feedback addressed | ✓ AI target met
```

## Feedback Mapping Rules

Every feedback item MUST be accounted for:

### Mapping Requirements

1. **Number each feedback item** at the start of processing
2. **Tag modifications** with feedback reference (e.g., `[F1]`)
3. **Track coverage**: Each item must have ≥1 modification OR explicit skip reason

### Skip Reasons (valid)

- "Already meets requirement" - e.g., passive voice already used
- "Not applicable to content" - e.g., no equations to improve
- "Conflicting with other feedback" - e.g., user wanted both formal and casual
- "User declined during clarification" - e.g., user said "skip" to a suggestion

### Skip Entry Format

```
[F3] [conclusion] Make impactful → skipped
    Reason: Conclusion already uses strong action verbs and specific metrics.
    No changes needed to meet this feedback item.
```

## Compact Format (Optional)

For simple single-paragraph edits:

```
## Change Log (Compact)

Input: 1 paragraph | Output: 1 paragraph | Changes: 3

1. "We used" → "The study employed" [academic_polish]
2. "Furthermore" removed [humanize]
3. "shows" → "demonstrates" [academic_polish]

Feedback: ✓ All addressed | AI Score: ~6%
```

## Machine-Readable Format (Optional)

For programmatic consumption:

```json
{
  "processing_info": {
    "input_tokens": 1234,
    "chunks": 1,
    "total_modifications": 5
  },
  "feedback_items": [
    {"id": "F1", "text": "improve clarity", "status": "done", "changes": 2}
  ],
  "modifications": [
    {
      "id": 1,
      "source": "academic_polish",
      "feedback_ref": "F1",
      "line": 15,
      "original": "We observed",
      "revised": "It was observed that"
    }
  ],
  "summary": {
    "total_modifications": 5,
    "feedback_addressed": "3/3",
    "ai_score_estimate": 0.07
  }
}
```
