---
name: Create thesis-humanizer skill
overview: 基于本次对话成功通过 Turnitin AI Writing 检测的经验，创建一个专门用于学术论文（特别是 LaTeX 博士论文）的 AI 痕迹去除 skill。融合现有 humanizer 的 24 种 AI 模式规则，并针对学术场景进行调整。
todos:
  - id: create-skill-structure
    content: Create thesis-humanizer/ folder with SKILL.md and references/ subdirectory
    status: pending
  - id: write-skill-md
    content: Write SKILL.md with frontmatter, workflow, academic constraints, merged AI patterns (24 from humanizer + thesis-specific), and quick reference
    status: pending
  - id: write-ai-patterns-academic
    content: Create references/ai-patterns-academic.md - Merge all 24 humanizer patterns with academic adaptations
    status: pending
  - id: write-replacement-dictionary
    content: Create references/replacement-dictionary.md with comprehensive word/phrase mappings
    status: pending
  - id: write-rhythm-techniques
    content: Create references/rhythm-techniques.md with sentence variation strategies
    status: pending
  - id: write-multi-pass-workflow
    content: Create references/multi-pass-workflow.md with iterative processing guide
    status: pending
  - id: update-changelog
    content: Update RULES_SKILLS_CHANGELOG.md to record the new skill
    status: pending
isProject: false
---

# Create thesis-humanizer Skill

## Background: Why a New Skill

本次对话从原始 Chapter 1 到通过 Turnitin AI Writing 检测，经历了 **8+ 轮迭代**。现有 `humanizer` skill 针对通用写作，包含"add personality"、"use I when it fits" 等指导，但这些对学术论文是**反效果的**。

需要一个专门针对 **LaTeX 学术论文** 的 humanizer，**融合 humanizer 的 24 种 AI 模式检测规则**，保持正式学术语气的同时去除 AI 痕迹。

---

## Merging humanizer Rules (24 Patterns)

### Patterns to FULLY INHERIT (apply as-is)


| #   | Pattern                        | Academic Adaptation                                 |
| --- | ------------------------------ | --------------------------------------------------- |
| 1   | Undue emphasis on significance | Remove "pivotal moment", "key turning point"        |
| 2   | Undue emphasis on notability   | Remove media name-dropping                          |
| 3   | Superficial -ing analyses      | Remove "highlighting", "underscoring", "showcasing" |
| 4   | Promotional language           | Remove "groundbreaking", "vibrant", "renowned"      |
| 5   | Vague attributions             | Replace with specific citations                     |
| 6   | Formulaic challenges sections  | Rewrite "Despite challenges..." patterns            |
| 7   | AI vocabulary words            | Replace "crucial", "delve", "enhance", "foster"     |
| 8   | Copula avoidance               | Use "is/are" instead of "serves as/stands as"       |
| 9   | Negative parallelisms          | Remove "Not only...but also", "It's not just..."    |
| 10  | Rule of three overuse          | Vary list lengths                                   |
| 11  | Synonym cycling                | Consistent terminology                              |
| 12  | False ranges                   | Remove "from X to Y" when meaningless               |
| 13  | Em dash overuse                | Use commas or semicolons                            |
| 22  | Filler phrases                 | Remove "In order to", "Due to the fact that"        |
| 23  | Excessive hedging              | Reduce "could potentially possibly"                 |


### Patterns to ADAPT for Academic Context


| #   | Pattern                      | humanizer says               | thesis-humanizer adaptation               |
| --- | ---------------------------- | ---------------------------- | ----------------------------------------- |
| 14  | Boldface overuse             | Remove all bold              | Keep bold for RQ/RO/RC labels only        |
| 15  | Inline-header lists          | Convert to prose             | Keep for methodology steps if appropriate |
| 16  | Title case in headings       | Use sentence case            | Follow university style guide             |
| 17  | Emojis                       | Remove all                   | Remove all (already not used in thesis)   |
| 18  | Curly quotes                 | Use straight quotes          | Use LaTeX quotes (``...'' or \enquote{})  |
| 19  | Chatbot artifacts            | Remove "I hope this helps"   | Remove (already not in thesis)            |
| 20  | Knowledge-cutoff disclaimers | Remove                       | Remove                                    |
| 21  | Sycophantic tone             | Remove "Great question!"     | Remove                                    |
| 24  | Generic conclusions          | Remove "future looks bright" | Replace with specific future work         |


### Patterns to IGNORE/REVERSE for Academic


| humanizer Pattern                | Why to Ignore/Reverse                          |
| -------------------------------- | ---------------------------------------------- |
| "Add soul" - use first person    | Academic writing requires third person/passive |
| "Have opinions"                  | Academic writing is objective                  |
| "Let mess in"                    | Academic writing requires clear structure      |
| "Vary rhythm with casual asides" | Keep formal throughout                         |


---

## Key Learnings from This Session

### 1. Academic-Specific Anti-Patterns (vs General Humanizer)


| Pattern       | General Humanizer       | Thesis Humanizer       |
| ------------- | ----------------------- | ---------------------- |
| First person  | Add "I" for personality | NEVER use first person |
| Passive voice | Convert to active       | KEEP passive voice     |
| Informal tone | Acceptable              | Must remain formal     |
| Opinions      | Encouraged              | Not appropriate        |
| Em dashes     | Reduce                  | Reduce                 |


### 2. Multi-Pass Iterative Approach (Critical Finding)

Single pass is insufficient. The successful workflow was:

```
Pass 1: Remove obvious AI vocabulary
        (surged → increased, crucial → important)

Pass 2: Vary sentence rhythm
        (add short sentences, use semicolons/colons)

Pass 3: Remove formulaic transitions
        (Furthermore → [delete], Additionally → Also)

Pass 4: Break structural patterns
        ("Chapter X presents" → varied verbs)

Pass 5: Fine-tune academic formality
        (like → such as, via → through)
```

### 3. Thesis-Specific Replacement Patterns (New Content)


| AI Pattern          | Thesis Replacement        | Example                                                                          |
| ------------------- | ------------------------- | -------------------------------------------------------------------------------- |
| surged              | increased substantially   | "IoT device deployment has surged" → "deployment has increased substantially"    |
| massive             | substantial               | "massive data volumes" → "substantial data volumes"                              |
| via                 | through / using           | "via peer-to-peer" → "through peer-to-peer"                                      |
| like (informal)     | such as                   | "functions, like collision avoidance" → "functions, such as collision avoidance" |
| crucial/pivotal/key | important / specific term | Context-dependent                                                                |
| Chapter X presents  | varied verbs              | presents/covers/addresses/details/reviews                                        |


### 4. Rhythm Variation Techniques (New Content)

- Use semicolons to join related short clauses
- Use colons to introduce inline lists
- Mix long explanatory sentences with short declarative ones
- Break up parallel structures with varied connectors

---

## Skill Structure

```
thesis-humanizer/
├── SKILL.md                          # Main instructions (~500 lines, includes merged patterns)
└── references/
    ├── ai-patterns-academic.md       # ALL 24 humanizer patterns + academic adaptations
    ├── replacement-dictionary.md     # Word/phrase replacement lookup table
    ├── rhythm-techniques.md          # Sentence variation strategies
    └── multi-pass-workflow.md        # Iterative processing guide
```

### SKILL.md Core Sections

1. **Frontmatter** - name, description with triggers
2. **Your Task** - 5-step process
3. **AI Pattern Checklist** - Quick reference for all 24+ patterns (merged from humanizer)
4. **Academic Constraints** - What to preserve vs modify
5. **Pass-by-Pass Workflow** - Iterative approach
6. **Quick Reference Table** - Most common replacements
7. **Output Format** - LaTeX + change log

---

## Key Differentiators from Existing Skills


| Aspect          | humanizer               | thesis-humanizer              |
| --------------- | ----------------------- | ----------------------------- |
| AI patterns     | 24 patterns             | 24 patterns + thesis-specific |
| Tone target     | Natural, conversational | Formal academic               |
| First person    | Encouraged              | Forbidden                     |
| Passive voice   | Discourage              | Preserve                      |
| Multi-pass      | Single pass             | 3-5 passes                    |
| LaTeX awareness | None                    | Full protection               |
| British English | Not specified           | Required                      |
| Target metric   | General readability     | Turnitin AI &lt;10%           |


### Relationship to humanizer

`thesis-humanizer` is a **superset** of `humanizer`:

- Inherits ALL 24 AI detection patterns
- ADAPTS general fixes to academic constraints
- ADDS thesis-specific patterns (chapter organization, RQ/RO/RC, lit review)
- REVERSES non-academic advice (first person, informal asides)

---

## Files to Create

### 1. `SKILL.md` (~500 lines)

Core workflow and essential patterns, following progressive disclosure.

**Includes inline:**

- Quick AI pattern checklist (top 15 most common)
- Essential replacement table
- Multi-pass workflow summary

### 2. `references/ai-patterns-academic.md` (NEW - Merged from humanizer)

**Complete reference with all 24 humanizer patterns + thesis-specific additions:**


| Section                      | Content                                                               |
| ---------------------------- | --------------------------------------------------------------------- |
| Part A: Vocabulary Patterns  | #7 AI words, #22 filler phrases, #23 hedging                          |
| Part B: Structural Patterns  | #9 negative parallelisms, #10 rule of three, #13 em dashes            |
| Part C: Promotional Patterns | #1-4 significance/notability/promotional/superficial                  |
| Part D: Attribution Patterns | #5 vague attributions, #6 formulaic challenges                        |
| Part E: Style Patterns       | #8 copula avoidance, #11 synonym cycling, #12 false ranges            |
| Part F: Formatting Patterns  | #14-18 bold/lists/title case/emojis/quotes                            |
| Part G: Chatbot Artifacts    | #19-21 collaborative artifacts/disclaimers/sycophancy                 |
| Part H: Academic-Specific    | Thesis chapter organization, RQ/RO/RC repetition, lit review patterns |


Each pattern includes:

- Detection criteria
- Academic-appropriate fix
- Example before/after

### 3. `references/replacement-dictionary.md`

Comprehensive lookup table from this session:

- AI vocabulary → Academic alternatives
- Informal → Formal upgrades
- Connector variations
- Chapter organization verbs

### 4. `references/rhythm-techniques.md`

Sentence variation strategies:

- Semicolon usage
- Colon introduction
- Length variation
- Structure mixing
- Avoiding parallel patterns

### 5. `references/multi-pass-workflow.md`

Detailed iteration guide:

- When to stop iterating
- Quality checkpoints
- AI score estimation
- Pattern density measurement

---

## Implementation Notes

- **Supersedes humanizer for thesis work**: When working on LaTeX thesis files, use thesis-humanizer instead of humanizer (not both)
- **Integrate with latex-guard**: thesis-humanizer should call latex-guard for protection
- **Coordinate with academic-polisher**: Run academic-polisher first, then thesis-humanizer
- **Output change log**: Track all modifications for user review
- **Estimate AI score**: Provide pattern density estimate after processing

## Pattern Merge Strategy

```
humanizer (24 patterns)
    │
    ├── INHERIT as-is (15 patterns)
    │   └── #1-10, #22-24, #12-13
    │
    ├── ADAPT for academic (9 patterns)
    │   └── #14-21 (formatting/chatbot artifacts)
    │
    └── REVERSE (advice that conflicts with academic writing)
        └── First person, opinions, casual asides

thesis-humanizer = humanizer patterns (adapted) + thesis-specific patterns
```

