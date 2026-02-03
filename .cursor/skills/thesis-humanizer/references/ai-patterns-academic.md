# AI Patterns for Academic Writing

This reference documents all 24 humanizer AI patterns plus 5 thesis-specific patterns, with academic-appropriate detection criteria and replacement strategies.

---

## Part A: Vocabulary Patterns

### Pattern #7: AI Vocabulary Words

**Category**: vocabulary  
**Source**: humanizer-inherit

**Detection Criteria**:
High-frequency AI words that appear far more often in post-2023 text:
- Additionally, align with, crucial, delve, emphasizing, enduring
- enhance, fostering, garner, highlight (verb), interplay
- intricate/intricacies, key (adjective), landscape (abstract noun)
- pivotal, showcase, tapestry (abstract noun), testament
- underscore (verb), valuable, vibrant

**Academic Replacement Strategy**:

| AI Word | Academic Alternative |
|---------|---------------------|
| crucial | important, significant, essential |
| delve into | examine, investigate, analyse |
| enhance | improve, strengthen, increase |
| foster | support, encourage, promote |
| garner | receive, obtain, attract |
| highlight | show, indicate, demonstrate |
| intricate | complex, detailed |
| key (adj) | important, main, central |
| landscape | field, area, domain |
| pivotal | important, central, significant |
| showcase | demonstrate, present, display |
| tapestry | combination, mixture, collection |
| testament | evidence, proof, indication |
| underscore | emphasise, show, demonstrate |
| valuable | useful, important, beneficial |
| vibrant | active, dynamic, thriving |

**Example**:
- Before: "This research delves into the crucial interplay between privacy and blockchain."
- After: "This research examines the relationship between privacy and blockchain."

---

### Pattern #22: Filler Phrases

**Category**: vocabulary  
**Source**: humanizer-inherit

**Detection Criteria**:
Unnecessary words that add length without meaning:
- "In order to" → "To"
- "Due to the fact that" → "Because"
- "At this point in time" → "Now" / "Currently"
- "In the event that" → "If"
- "Has the ability to" → "Can"
- "It is important to note that" → [delete]
- "It should be noted that" → [delete]
- "As a matter of fact" → [delete]

**Academic Replacement Strategy**:
Remove filler entirely or use minimal equivalent.

| Filler Phrase | Academic Alternative |
|---------------|---------------------|
| In order to achieve | To achieve |
| Due to the fact that | Because / Since |
| At this point in time | Currently / Now |
| In the event that | If |
| Has the ability to | Can |
| It is important to note that | [remove - start with main clause] |
| With regard to | Regarding / About |
| In terms of | [often removable] |
| A large number of | Many / Numerous |
| In the context of | In / Within |

**Example**:
- Before: "In order to achieve the research objectives, it is important to note that the methodology was designed..."
- After: "To achieve the research objectives, the methodology was designed..."

---

### Pattern #23: Excessive Hedging

**Category**: vocabulary  
**Source**: humanizer-inherit

**Detection Criteria**:
Over-qualifying statements with stacked uncertainty:
- "could potentially possibly"
- "might perhaps"
- "may potentially"
- "it could be argued that perhaps"

**Academic Replacement Strategy**:
Use single appropriate hedge. Academic writing does use hedging, but one qualifier is sufficient.

| Excessive | Academic |
|-----------|----------|
| could potentially possibly | may / could |
| might perhaps be | may be |
| it could be argued that perhaps | arguably |
| appears to potentially | appears to / may |

**Example**:
- Before: "It could potentially be argued that the results might possibly suggest..."
- After: "The results suggest..." or "The results may indicate..."

---

## Part B: Structural Patterns

### Pattern #9: Negative Parallelisms

**Category**: structural  
**Source**: humanizer-inherit

**Detection Criteria**:
Overused constructions:
- "Not only...but also..."
- "It's not just about X, it's about Y"
- "It's not merely X, it's Y"
- "Not simply...rather..."

**Academic Replacement Strategy**:
Replace with direct statements. State the positive claim directly.

**Example**:
- Before: "This framework is not only efficient but also scalable, providing not just security but comprehensive privacy."
- After: "This framework is efficient and scalable. It provides security and comprehensive privacy."

---

### Pattern #10: Rule of Three Overuse

**Category**: structural  
**Source**: humanizer-inherit

**Detection Criteria**:
Forced groupings of three items:
- "innovation, inspiration, and insights"
- "secure, scalable, and sustainable"
- Three-item lists that feel artificial

**Academic Replacement Strategy**:
Vary list lengths. Use two items, four items, or prose form.

**Example**:
- Before: "The system provides security, scalability, and sustainability while ensuring privacy, performance, and practicality."
- After: "The system provides security and scalability. It also ensures privacy without sacrificing performance."

---

### Pattern #13: Em Dash Overuse

**Category**: structural  
**Source**: humanizer-inherit

**Detection Criteria**:
Multiple em dashes (—) per paragraph, especially:
- Dashes used for emphasis
- Dashes interrupting flow
- More than one dash per sentence

**Academic Replacement Strategy**:
Replace with commas, semicolons, colons, or parentheses. Academic writing typically uses fewer dashes.

| Em Dash Usage | Academic Alternative |
|---------------|---------------------|
| Emphasis interruption | Commas |
| List introduction | Colon |
| Aside/parenthetical | Parentheses |
| Contrast | Semicolon |

**Example**:
- Before: "The protocol—designed for vehicular networks—provides privacy—a crucial requirement—through encryption."
- After: "The protocol, designed for vehicular networks, provides privacy (a key requirement) through encryption."

---

## Part C: Promotional Patterns

### Pattern #1: Undue Emphasis on Significance

**Category**: promotional  
**Source**: humanizer-inherit

**Detection Criteria**:
Words/phrases inflating importance:
- stands/serves as, is a testament/reminder
- vital/significant/crucial/pivotal/key role/moment
- underscores/highlights its importance/significance
- reflects broader, symbolizing its ongoing/enduring/lasting
- key turning point, evolving landscape, focal point
- indelible mark, deeply rooted

**Academic Replacement Strategy**:
State facts without inflation. Let the reader judge significance.

**Example**:
- Before: "This research marks a pivotal moment in the evolution of vehicular privacy, serving as a testament to the crucial role of blockchain in addressing fundamental challenges."
- After: "This research addresses vehicular privacy using blockchain technology."

---

### Pattern #2: Undue Emphasis on Notability

**Category**: promotional  
**Source**: humanizer-inherit

**Detection Criteria**:
- Name-dropping media outlets without context
- "has been featured in..."
- "according to leading experts..."
- Listing multiple sources without specific claims

**Academic Replacement Strategy**:
Cite specific claims from specific sources with proper academic citations.

**Example**:
- Before: "Blockchain technology has been discussed in Nature, IEEE, and ACM publications, highlighting its growing importance."
- After: "Recent studies examine blockchain applications in vehicular networks \citep{smith2024, jones2023}."

---

### Pattern #3: Superficial -ing Analyses

**Category**: promotional  
**Source**: humanizer-inherit

**Detection Criteria**:
Present participle phrases tacked onto sentences:
- highlighting/underscoring/emphasizing...
- ensuring/reflecting/symbolizing...
- contributing to/cultivating/fostering...
- encompassing/showcasing...

**Academic Replacement Strategy**:
Remove or convert to separate sentences with concrete claims.

**Example**:
- Before: "The framework integrates multiple components, showcasing its versatility while highlighting the importance of privacy, ultimately contributing to enhanced security."
- After: "The framework integrates multiple components. Its modular design supports various privacy requirements."

---

### Pattern #4: Promotional Language

**Category**: promotional  
**Source**: humanizer-inherit

**Detection Criteria**:
Marketing-style words:
- boasts, vibrant, rich (figurative), profound
- groundbreaking (figurative), renowned, breathtaking
- stunning, must-visit, nestled, in the heart of
- commitment to, natural beauty, showcasing, exemplifies

**Academic Replacement Strategy**:
Use neutral, factual descriptions. Academic writing avoids promotional tone.

| Promotional | Academic |
|-------------|----------|
| groundbreaking | novel, new |
| cutting-edge | recent, current |
| revolutionary | significant |
| state-of-the-art | current, modern |
| robust | reliable, effective |
| seamless | integrated, smooth |
| comprehensive | complete, thorough |

**Example**:
- Before: "This groundbreaking research presents a robust and seamless solution."
- After: "This research presents a reliable and integrated solution."

---

## Part D: Attribution Patterns

### Pattern #5: Vague Attributions

**Category**: attribution  
**Source**: humanizer-inherit

**Detection Criteria**:
- "Industry reports suggest..."
- "Observers have cited..."
- "Experts argue..."
- "Some critics argue..."
- "Several sources indicate..."
- "According to researchers..."

**Academic Replacement Strategy**:
Replace with specific citations. Every claim needs a traceable source.

**Example**:
- Before: "Experts argue that vehicular privacy is increasingly important. Industry reports suggest growing adoption of V2X technology."
- After: "Vehicular privacy requirements have increased with V2X adoption \citep{ieee2024}. The European Commission projects 30 million connected vehicles by 2030 \citep{ec2023}."

---

### Pattern #6: Formulaic Challenges Sections

**Category**: attribution  
**Source**: humanizer-inherit

**Detection Criteria**:
- "Despite its... faces several challenges..."
- "Despite these challenges..."
- "Challenges and Legacy" section headers
- "Future Outlook" without specific content

**Academic Replacement Strategy**:
Replace with specific challenges and concrete responses.

**Example**:
- Before: "Despite its advantages, blockchain faces several challenges in vehicular networks. Despite these challenges, ongoing research continues to address these issues."
- After: "Blockchain transaction latency (typically 10-60 seconds) exceeds the sub-second requirements for safety messages. Chapter 5 presents a lightweight consensus mechanism that reduces confirmation time to 200ms."

---

## Part E: Style Patterns

### Pattern #8: Copula Avoidance

**Category**: style  
**Source**: humanizer-inherit

**Detection Criteria**:
Avoiding simple "is/are/has" with elaborate substitutes:
- serves as / stands as / marks / represents [a]
- boasts / features / offers [a]
- functions as / acts as

**Academic Replacement Strategy**:
Use simple copulas. "Is" and "are" are perfectly acceptable.

| Elaborate | Simple |
|-----------|--------|
| serves as | is |
| stands as | is |
| functions as | is |
| acts as | is |
| boasts | has |
| features | has / includes |
| offers | provides / has |

**Example**:
- Before: "The framework serves as a comprehensive solution that features multiple privacy mechanisms and boasts high efficiency."
- After: "The framework is a comprehensive solution with multiple privacy mechanisms and high efficiency."

---

### Pattern #11: Synonym Cycling (Elegant Variation)

**Category**: style  
**Source**: humanizer-inherit

**Detection Criteria**:
Excessive synonym substitution to avoid repetition:
- "the protocol... the mechanism... the approach... the scheme"
- "vehicles... automobiles... cars... motorized transport"

**Academic Replacement Strategy**:
Use consistent terminology. Technical writing prefers clarity over variety.

**Example**:
- Before: "The protocol addresses privacy. The mechanism ensures anonymity. The approach prevents tracking. The scheme protects identity."
- After: "The protocol addresses privacy by ensuring anonymity, preventing tracking, and protecting identity."

---

### Pattern #12: False Ranges

**Category**: style  
**Source**: humanizer-inherit

**Detection Criteria**:
"From X to Y" constructions where X and Y are not on a meaningful scale:
- "from theory to practice"
- "from local to global"
- "from simple to complex"

**Academic Replacement Strategy**:
List items directly or describe the actual scope.

**Example**:
- Before: "The research spans from theoretical foundations to practical implementations, from individual privacy to network-wide security."
- After: "The research covers theoretical foundations and practical implementations, addressing both individual privacy and network security."

---

### Pattern #24: Generic Positive Conclusions

**Category**: style  
**Source**: humanizer-inherit

**Detection Criteria**:
- "The future looks bright"
- "Exciting times lie ahead"
- "This represents a major step in the right direction"
- Generic optimism without specifics

**Academic Replacement Strategy**:
Replace with specific future work or concrete implications.

**Example**:
- Before: "The future of vehicular privacy looks bright. Exciting developments lie ahead as blockchain technology continues to evolve."
- After: "Future work should address cross-chain interoperability and formal verification of the consensus mechanism. Real-world deployment testing with automotive manufacturers is planned for 2025."

---

## Part F: Formatting Patterns

### Pattern #14: Boldface Overuse

**Category**: formatting  
**Source**: humanizer-adapt

**Detection Criteria**:
Mechanical bolding of phrases:
- Every acronym bolded
- Key terms bolded repeatedly
- Emphasis through bold instead of sentence structure

**Academic Adaptation**:
In thesis context, bold is acceptable for:
- RQ, RO, RC labels
- First use of defined terms (sparingly)
- Table/figure labels

Remove bold from:
- Repeated terms
- Emphasis within paragraphs
- Acronym expansions after first use

---

### Pattern #15: Inline-Header Vertical Lists

**Category**: formatting  
**Source**: humanizer-adapt

**Detection Criteria**:
Lists where items start with bolded headers followed by colons:
```
- **Item One:** Description...
- **Item Two:** Description...
```

**Academic Adaptation**:
In thesis context, this format is acceptable for:
- Methodology steps
- Research objective lists
- Clearly structured enumerations

Convert to prose when:
- List could be a paragraph
- Items are short
- Flow is disrupted

---

### Pattern #16: Title Case in Headings

**Category**: formatting  
**Source**: humanizer-adapt

**Detection Criteria**:
All main words capitalised:
- "Strategic Negotiations And Global Partnerships"

**Academic Adaptation**:
Follow university style guide. Most thesis guidelines specify either:
- Sentence case: "Strategic negotiations and global partnerships"
- Title case (if required by institution)

Check your university's thesis formatting requirements.

---

### Pattern #17: Emojis

**Category**: formatting  
**Source**: humanizer-adapt

**Detection Criteria**:
Any emoji in academic text:
- 🚀 💡 ✅ ⚠️

**Academic Adaptation**:
Remove all emojis. Emojis are never appropriate in thesis writing.

---

### Pattern #18: Curly Quotation Marks

**Category**: formatting  
**Source**: humanizer-adapt

**Detection Criteria**:
Curly/smart quotes: "..." '...'

**Academic Adaptation**:
In LaTeX, use proper quote syntax:
- Double quotes: \`\`...\'\' or `\enquote{...}`
- Single quotes: \`...\' 

Do not use: "..." or '...'

---

## Part G: Chatbot Artifacts

### Pattern #19: Collaborative Communication Artifacts

**Category**: chatbot  
**Source**: humanizer-adapt

**Detection Criteria**:
- "I hope this helps"
- "Of course!"
- "Certainly!"
- "You're absolutely right!"
- "Would you like..."
- "Let me know"
- "Here is a..."

**Academic Adaptation**:
These should never appear in thesis text. Remove entirely.

---

### Pattern #20: Knowledge-Cutoff Disclaimers

**Category**: chatbot  
**Source**: humanizer-adapt

**Detection Criteria**:
- "as of [date]"
- "Up to my last training update"
- "While specific details are limited..."
- "based on available information..."

**Academic Adaptation**:
Remove entirely. Academic writing should cite specific sources, not acknowledge AI limitations.

---

### Pattern #21: Sycophantic/Servile Tone

**Category**: chatbot  
**Source**: humanizer-adapt

**Detection Criteria**:
- "Great question!"
- "You're absolutely right that..."
- "That's an excellent point about..."
- Excessive agreement/praise

**Academic Adaptation**:
Remove entirely. Academic writing is objective.

---

## Part H: Thesis-Specific Patterns

### Pattern H1: Repetitive Chapter Openings

**Category**: thesis-specific  
**Source**: thesis-specific

**Detection Criteria**:
Same structure for each chapter:
- "Chapter X presents..."
- "This chapter discusses..."
- "Chapter X covers..."

**Academic Replacement Strategy**:
Vary verbs and sentence structure:

| Repetitive | Varied Alternatives |
|------------|---------------------|
| Chapter 2 presents the literature review | The literature review in Chapter 2 examines... |
| Chapter 3 presents the methodology | Chapter 3 describes the research methodology |
| Chapter 4 presents the results | Results are presented in Chapter 4 |
| Chapter 5 presents the discussion | Chapter 5 analyses these findings |

**Example**:
- Before: "Chapter 2 presents the literature review. Chapter 3 presents the methodology. Chapter 4 presents the results."
- After: "Chapter 2 reviews relevant literature on vehicular privacy. The research methodology is described in Chapter 3. Chapter 4 reports experimental results."

---

### Pattern H2: RQ/RO/RC Formula

**Category**: thesis-specific  
**Source**: thesis-specific

**Detection Criteria**:
Identical structure for each research question/objective/contribution:
- "RQ1: How does X affect Y?"
- "RQ2: How does A affect B?"
- "RQ3: How does C affect D?"

**Academic Replacement Strategy**:
Vary sentence construction while maintaining clarity:

**Example**:
- Before: "RQ1: How does anonymisation affect privacy? RQ2: How does encryption affect security? RQ3: How does consensus affect scalability?"
- After: "RQ1: What anonymisation techniques preserve privacy in vehicular networks? RQ2: How can encryption be implemented without compromising V2X latency requirements? RQ3: This research also examines whether lightweight consensus mechanisms can meet vehicular scalability demands."

---

### Pattern H3: Literature Review Formula

**Category**: thesis-specific  
**Source**: thesis-specific

**Detection Criteria**:
Same citation pattern repeated:
- "Author (year) found that..."
- "Author (year) proposed..."
- "Author (year) developed..."

**Academic Replacement Strategy**:
Integrate citations more naturally:

| Formulaic | Natural Integration |
|-----------|---------------------|
| Smith (2024) found that X increases Y | X increases Y \citep{smith2024} |
| Jones (2023) proposed a framework | A recent framework addresses this \citep{jones2023} |
| Brown (2022) developed an algorithm | The algorithm developed by Brown \citeyearpar{brown2022} |

**Example**:
- Before: "Smith (2024) found that blockchain improves privacy. Jones (2023) proposed a consensus mechanism. Brown (2022) developed an encryption scheme."
- After: "Blockchain improves privacy in vehicular contexts \citep{smith2024}. Recent consensus mechanisms \citep{jones2023} and encryption schemes \citep{brown2022} address the specific requirements of V2X communication."

---

### Pattern H4: Significance Stacking

**Category**: thesis-specific  
**Source**: thesis-specific

**Detection Criteria**:
Multiple significance words in same paragraph:
- "crucial", "pivotal", "key", "vital", "essential" appearing together
- "significant", "important", "critical" clustering

**Academic Replacement Strategy**:
Use one significance word per paragraph maximum, or none.

**Example**:
- Before: "Privacy is crucial in vehicular networks. This makes anonymisation a pivotal requirement. Key challenges include the vital need for low latency."
- After: "Privacy in vehicular networks requires anonymisation while maintaining low latency."

---

### Pattern H5: Methodology Formula

**Category**: thesis-specific  
**Source**: thesis-specific

**Detection Criteria**:
Repeated methodology introductions:
- "This study employs..."
- "This research utilises..."
- "This work adopts..."

**Academic Replacement Strategy**:
Vary introductions or state methodology directly.

**Example**:
- Before: "This study employs a mixed-methods approach. This research utilises both quantitative and qualitative data. This work adopts simulation for validation."
- After: "A mixed-methods approach combines quantitative performance measurements with qualitative expert interviews. Validation uses network simulation."

---

## Quick Reference: All 29 Patterns

| # | Pattern | Category | Action |
|---|---------|----------|--------|
| 1 | Undue significance emphasis | promotional | Remove inflation |
| 2 | Undue notability emphasis | promotional | Cite specifically |
| 3 | Superficial -ing analyses | promotional | Remove or separate |
| 4 | Promotional language | promotional | Use neutral terms |
| 5 | Vague attributions | attribution | Add citations |
| 6 | Formulaic challenges | attribution | Be specific |
| 7 | AI vocabulary words | vocabulary | Replace with alternatives |
| 8 | Copula avoidance | style | Use is/are/has |
| 9 | Negative parallelisms | structural | State directly |
| 10 | Rule of three | structural | Vary list lengths |
| 11 | Synonym cycling | style | Use consistent terms |
| 12 | False ranges | style | List directly |
| 13 | Em dash overuse | structural | Use commas/semicolons |
| 14 | Boldface overuse | formatting | Keep for labels only |
| 15 | Inline-header lists | formatting | Keep if appropriate |
| 16 | Title case headings | formatting | Follow style guide |
| 17 | Emojis | formatting | Remove all |
| 18 | Curly quotes | formatting | Use LaTeX quotes |
| 19 | Chatbot artifacts | chatbot | Remove all |
| 20 | Knowledge disclaimers | chatbot | Remove all |
| 21 | Sycophantic tone | chatbot | Remove all |
| 22 | Filler phrases | vocabulary | Remove or simplify |
| 23 | Excessive hedging | vocabulary | Use single hedge |
| 24 | Generic conclusions | style | Be specific |
| H1 | Repetitive chapter openings | thesis-specific | Vary verbs |
| H2 | RQ/RO/RC formula | thesis-specific | Vary structure |
| H3 | Literature review formula | thesis-specific | Integrate citations |
| H4 | Significance stacking | thesis-specific | Use one or none |
| H5 | Methodology formula | thesis-specific | Vary introductions |
