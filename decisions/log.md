# Decision Log

Append-only. Never delete entries. If a decision is overridden, log the new
decision and reference the old one.

**Format:**
```
[YYYY-MM-DD] DECISION: [What] | REASONING: [Why] | CONTEXT: [Background]
```

---

[2026-06-20] DECISION: Stand up the Claude Code operating-system workspace from CLAUDE.md | REASONING: A consistent, reusable structure (context, skills, SOPs, templates, decision log, session memory) lets every project start clean and ship on the 7–14 day cadence | CONTEXT: Initial environment setup — workspace previously held only CLAUDE.md

[2026-06-20] DECISION: Install hairyf/blockchain-skills via shallow clone + per-skill symlinks, kept out of git | REASONING: A plain clone nests skills at blockchain-skills-external/skills/<name>/SKILL.md (two levels deep), too deep for Claude Code's one-level discovery; symlinking each into .claude/skills/<name> makes all 66 valid skills load as real skills while a single clone keeps `git pull` updates trivial. Kept out of git (symlinks ignored, clone ignored) to match the existing do-not-vendor design and keep the repo light. | CONTEXT: Repo has 69 skill dirs; 3 (layerzero, mythril, snarkjs) lack a SKILL.md and were skipped → 66 usable. Corrects the earlier mid-task assumption of 53 skills.
