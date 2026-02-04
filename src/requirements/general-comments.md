# PhD Thesis Revision Standards

## 1. Language Clarity and Precision
- Several terms used are ambiguous and lack sufficient clarity, which affects the overall quality of the thesis
- A major revision is required to improve precision
- Direct translation has led to wording that does not fully convey the intended meaning
- Many grammatical errors require correction

## 2. Sentence Structure
- Remove short, fragmented, informal sentences (e.g., "Significantly actually.", "At source specifically.", "Frequent sudden breaking.")
- Combine fragments into complete, formal academic sentences
- Remove filler words such as "actually", "indeed", "though" (at sentence end)

## 3. Parenthetical Content
- Remove all parenthetical supplementary information that does not add essential academic value
- Reserve parentheses for in-text citations only
- Examples of content to remove:
  - Technical specifications: "(LIDAR units generating 100MB per minute, camera arrays capturing 50MP images...)"
  - Numerical clarifications: "(10 gigabits per second, roughly 1,250 megabytes per second)"
  - Location lists: "(MIT testing facilities, Fraunhofer Institute Germany, NTT DOCOMO labs Japan)"
  - Range expansions: "(rising from approximately 15 billion to over 50 billion active units)"

## 4. Fabricated Data and AI-Generated Content

### 4.1 Identifying and Eliminating Fabricated Content

Unsupported statistics and specific numerical claims are often AI-fabricated content designed to appear authoritative. These fabricated elements undermine academic credibility and must be eliminated entirely—not merely rephrased.

**Recognition Pattern:**
AI-generated text often includes:
- Specific percentages without citations (e.g., "73% of users", "40-60% failure rate")
- Precise numerical ranges without sources (e.g., "300-500 metres", "10-100ms latency")
- Market projections and financial figures (e.g., "\$556 billion by 2028")
- Survey counts and sample sizes (e.g., "847 peer-reviewed articles", "2,800 vehicles")
- Fabricated institutional references (e.g., "University of Michigan trials", "European field trials 2022-2023")

**Elimination Principle:**
These fabricated elements and their surrounding context should be completely rewritten based on:
1. The actual logical purpose of the paragraph within the thesis structure
2. What the paragraph needs to convey to connect the preceding and following content
3. Genuine academic arguments supported by existing citations in the document

**Rewriting Approach:**

1. **Identify the paragraph's role**: What is its function in the thesis structure? (introducing a problem, reviewing literature, establishing a gap, etc.)

2. **Extract the core argument**: What genuine academic point is being made, stripped of fabricated details?

3. **Rewrite for clarity and flow**: Reconstruct the content to:
   - Maintain logical connection with preceding paragraphs
   - Establish clear transition to following content
   - Support claims only with properly cited sources already in the document
   - Improve readability and comprehension

4. **Remove entirely if unnecessary**: If a sentence or paragraph exists only to present fabricated data and serves no structural purpose, delete it completely.

**Quality Standard:**
The rewritten content should make the thesis easier to read and understand, not merely "acceptable." Each paragraph should clearly advance the argument and connect smoothly with surrounding text.

### 4.2 Supported Statistics May Be Retained
Statistics with proper citations within the same logical context may be retained:
- Year ranges describing literature scope when cited works actually span those years
- Technical specifications from cited standards (e.g., IEEE 802.11p frequency band from the standard document)
- Findings directly attributed to cited research (e.g., "De Montjoye et al. reported that four spatiotemporal points...")

### 4.3 Verification Process
Before including any specific number:
1. Identify the source: Is there a `\cite{}` or `\citep{}` directly supporting this claim?
2. Verify accuracy: Does the cited work actually contain this exact data?
3. If unsupported: Rewrite the passage to convey the concept without the specific number
4. Quality check: Does the rewritten text maintain academic rigour and logical coherence?

## 5. Redundant Content
- Delete content not used elsewhere in the thesis (e.g., "Paid Information Collection")
- Remove ineffective, redundant descriptive information while maintaining logical flow
- Maintain coherent logical connections throughout the document

## 6. Academic Tone
- Use passive voice for formal academic writing
- Avoid colloquial expressions (e.g., "got designed for" → "was designed for")
- Ensure each paragraph contains at least 3 sentences
- Upgrade vocabulary to formal academic register

## 7. Citation Consistency
- Do not modify any `\cite{}`, `\citep{}`, `\citet{}`, `\citeA{}` commands
- Do not add new citations unless explicitly required
- Do not remove existing citations
- Preserve all cross-references (`\ref{}`, `\label{}`)

## 8. LaTeX Structure Protection
Preserve unchanged:
- All citation commands
- All cross-reference commands
- Table and figure environments
- Mathematical formulas and equations
- Acronym commands (`\acrshort{}`, `\acrlong{}`)
- File paths and includes
