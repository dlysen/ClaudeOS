# Decision Log

Append-only. Never delete entries. If a decision is overridden, log the new
decision and reference the old one.

**Format:**
```
[YYYY-MM-DD] DECISION: [What] | REASONING: [Why] | CONTEXT: [Background]
```

---

[2026-06-20] DECISION: Stand up the Claude Code operating-system workspace from CLAUDE.md | REASONING: A consistent, reusable structure (context, skills, SOPs, templates, decision log, session memory) lets every project start clean and ship on the 7–14 day cadence | CONTEXT: Initial environment setup — workspace previously held only CLAUDE.md
