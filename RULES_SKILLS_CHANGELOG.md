# Rules and Skills Change Log

This file tracks changes to `.cursor/rules/` and `.cursor/skills/`.

## Format

- Date: YYYY-MM-DD
  - Change: brief description
  - Reason: why the change was made

## Entries

- Date: 2026-01-31
  - Change: Added `.cursor/commands/thesis.revise.md`
  - Reason: Complete thesis revision pipeline command (latex-guard → supervisor feedback → academic-polisher → humanizer)
  
- Date: 2026-01-31
  - Change: Added `.cursor/commands/thesis.revise-quick.md`
  - Reason: Quick revision command without humanizer step for faster processing

- Date: 2026-01-31
  - Change: Added `.cursor/rules/file-hygiene.mdc`
  - Reason: Enforce file hygiene and temp file handling; single log file.

- Date: 2026-02-01
  - Change: Added `.cursor/skills/thesis-refine-with-latex/` skill
  - Reason: Specialized LaTeX thesis revision orchestrator with chunking, self-healing, clarification mode, and change logging. Coordinates latex-guard, academic-polisher, and humanizer for <10% Turnitin AI target.
  - Files:
    - `.cursor/skills/thesis-refine-with-latex/SKILL.md` - Main skill definition
    - `.cursor/skills/thesis-refine-with-latex/references/chunking-strategy.md` - Long document handling
    - `.cursor/skills/thesis-refine-with-latex/references/feedback-matching.md` - Ambiguous feedback clarification
    - `.cursor/skills/thesis-refine-with-latex/references/self-healing.md` - Placeholder recovery
    - `.cursor/skills/thesis-refine-with-latex/references/change-log-format.md` - Output structure

- Date: 2026-02-01
  - Change: Added `.cursor/rules/specify-rules.mdc` (auto-generated)
  - Reason: Development guidelines from speckit plan for thesis-refine-orchestrator feature

- Date: 2026-02-03
  - Change: Added `.cursor/skills/thesis-humanizer/` skill
  - Reason: Academic-specific AI pattern removal for LaTeX thesis content. Merges all 24 humanizer patterns with thesis-specific adaptations. Supports multi-pass iterative processing, LaTeX protection, and change logging. Target: Turnitin AI Writing <10%.
  - Files:
    - `.cursor/skills/thesis-humanizer/SKILL.md` - Main skill definition (~500 lines)
    - `.cursor/skills/thesis-humanizer/references/ai-patterns-academic.md` - All 29 patterns with academic adaptations
    - `.cursor/skills/thesis-humanizer/references/replacement-dictionary.md` - AI vocabulary and formal upgrades
    - `.cursor/skills/thesis-humanizer/references/rhythm-techniques.md` - Sentence variation strategies
    - `.cursor/skills/thesis-humanizer/references/multi-pass-workflow.md` - Iterative processing guide
