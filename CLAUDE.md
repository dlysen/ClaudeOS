# Claude Code — Operational System & Developer Guide

**For:** Dangal Macatangay (CEO + Developer)  
**Structure:** Solo operator, full-stack development, fast shipping (7–14 days per project)  
**Last Updated:** 2026-06-12

This document defines how Claude Code operates as your development partner. Use this as a template for all projects.

---

## 🎯 Core Operating Principles

1. **Finish one project at a time** — No context switching, ship fast (7–14 day cadence)
2. **Code-first, docs-second** — Write the work, then document decisions
3. **Persistent memory** — Claude Code learns and adapts across conversations
4. **Reusable patterns** — Build skills for recurring workflows
5. **Clean commits** — Each commit tells a story (no "fix bug" messages)
6. **Session-driven** — Start with context, end with notes, loop seamlessly

---

## 📁 Folder Structure

```
.
├── CLAUDE.md                          # This file (operational guide)
├── CLAUDE.local.md                    # Private config (not in git)
│
├── .claude/                           # Claude Code configuration
│   ├── settings.json                  # Global settings
│   ├── settings.local.json            # Local overrides
│   ├── rules/                         # Behavior rules
│   │   └── communication-style.md     # Tone, format, pet peeves
│   └── skills/                        # Custom & external skills
│       ├── blockchain-developer/      # Web3/Solidity expertise
│       ├── api-test-suite/            # API integration testing
│       ├── payment-gateway/           # Payment flow templates
│       ├── backend-boilerplate/       # Backend scaffolding
│       ├── project-kickoff/           # New project setup
│       ├── tailwind-ui/               # UI component library
│       └── blockchain-skills-external/# 69+ blockchain skills (github.com/hairyf/blockchain-skills)
│
├── .agents/                           # Agent skill library (parallel to .claude)
│   └── skills/                        # Agent-specific skills
│
├── context/                           # Project context (versioned)
│   ├── me.md                          # Your role, timezone, priorities
│   ├── work.md                        # Business structure, revenue, stack focus
│   ├── goals.md                       # Quarterly goals (update Q1/Q2/Q3/Q4)
│   ├── current-priorities.md          # Active priorities (update weekly)
│   └── team.md                        # Team structure (if applicable)
│
├── decisions/                         # Append-only decision log
│   └── log.md                         # [YYYY-MM-DD] DECISION | REASONING | CONTEXT
│
├── projects/                          # Active projects
│   ├── [project-name]/
│   │   ├── CLAUDE.md                  # Project-specific instructions
│   │   ├── CLAUDE.local.md            # Project private config
│   │   ├── README.md                  # Project overview & status
│   │   ├── sessions/                  # Session tracking (date-based)
│   │   │   ├── MILESTONES.md          # Current state + key decisions
│   │   │   ├── 2026-06-12.md          # Daily session notes
│   │   │   ├── 2026-06-11.md
│   │   │   └── ... (one per session)
│   │   ├── [source-code]/             # Project source (src, contracts, app, etc.)
│   │   └── [config]/                  # Project config (package.json, hardhat.config.js, etc.)
│   └── ...
│
├── archives/                          # Completed projects (moved, never deleted)
│   └── [completed-project-name]/      # Same structure as projects/
│
├── references/                        # Shared reference material
│   ├── sops/                          # Standard Operating Procedures
│   │   ├── session-memory.md          # Session workflow protocol
│   │   ├── smart-contract-integration.md # 5-step contract wiring
│   │   └── genealogy-smart-contract-integration.md
│   ├── examples/                      # Code examples & patterns
│   └── [documentation]/
│
└── templates/                         # Reusable templates
    ├── session-summary.md             # Use at session end
    └── contract-integration-template.md
```

---

## 🧠 Context System

Your project context is defined by 5 files in `context/`. Claude Code reads these at session start.

### context/me.md
**Your profile:** Role, timezone, top priority, knowledge areas.

```markdown
# About [You]

- **Name:** [Your name]
- **Role:** [CEO/Developer/Consultant/etc]
- **Timezone:** [Your TZ]
- **What I do:** [Brief description]
- **#1 Priority:** [Your north star]
```

### context/work.md
**Business structure:** How you operate, services, revenue, stack focus.

```markdown
# Work & Business

- **Structure:** [Solo/Team/Agency]
- **Services:** [What you offer]
- **Revenue:** [Current/Target]
- **Stack focus:** [Tech focus areas]
- **Shipping cadence:** [e.g., one project every 7–14 days]
```

### context/goals.md
**Quarterly goals:** Updated at start of Q1/Q2/Q3/Q4.

```markdown
# Goals — Q[X] [YEAR]

*Update this file at the start of each quarter.*

## Category 1
- [ ] Goal 1
- [ ] Goal 2

## Category 2
- [ ] Goal 1
```

### context/current-priorities.md
**Weekly/active priorities:** What matters right now.

```markdown
# Current Priorities

*Last updated: YYYY-MM-DD*

1. **[Priority 1]** — Why this matters
2. **[Priority 2]** — Why this matters
3. **[Priority 3]** — Why this matters
4. **[Principle]** — Always true
```

### context/team.md
**Team structure:** Who does what (if applicable).

---

## 🎓 Skills & Agents

Skills are reusable knowledge packages. Invoke them when tasks match their domain.

### Built-in Skills (Local)
Store in `.claude/skills/[skill-name]/SKILL.md`

| Skill | When to Use |
|-------|-----------|
| **blockchain-developer** | Web3/Solidity contracts, DeFi, audits, gas optimization |
| **api-test-suite** | Generate integration test suites for APIs |
| **payment-gateway** | Payment flow templates & transaction patterns |
| **backend-boilerplate** | Backend server scaffolding (auth, routes, DB, tests) |
| **project-kickoff** | Spin up new full-stack project (7–14 day cadence) |
| **tailwind-ui** | Mobile-first UI components (Tailwind + Lucide + theme system) |

### Blockchain Skills Library
**69 blockchain-focused skills** installed from [hairyf/blockchain-skills](https://github.com/hairyf/blockchain-skills.git):

- Location: `.claude/skills/blockchain-skills-external/`
- Installed: `git clone https://github.com/hairyf/blockchain-skills.git .claude/skills/blockchain-skills-external`
- Update: `cd .claude/skills/blockchain-skills-external && git pull origin main`
- Key skills: hardhat, solidity, openzeppelin, foundry, alchemy, dex, uniswap, aave, etc.

### Using Skills
Invoke with slash command: `/blockchain-developer`, `/api-test-suite`, etc.

---

## 📋 Decision Log

All non-trivial decisions are logged in `decisions/log.md` (append-only).

**Format:**
```
[YYYY-MM-DD] DECISION: [What was decided] | REASONING: [Why] | CONTEXT: [Background]
```

**Examples:**
```
[2026-06-12] DECISION: Use genealogy contract instead of internal referral tracking | 
  REASONING: Dual-tree structure allows complex network growth with per-user optimization | 
  CONTEXT: AEOS vesting system needs scalable referral network
```

**Never delete entries.** If a decision is overridden, log the new decision with reference to the old one.

---

## 🎬 Session Management Protocol

Claude Code sessions are conversation-based and context-aware.

### Session Start (Read These First)
When Dangal says "Let's work on [project]":

1. Read `projects/[project]/CLAUDE.md` — Project-specific instructions
2. Read `projects/[project]/sessions/MILESTONES.md` — Current state, key decisions, blocker status
3. Read the most recent `projects/[project]/sessions/YYYY-MM-DD.md` — What happened last
4. **Confirm orientation** in 3–5 bullets before starting work

### Session End (Write These)
At natural close, wrap-up, or "done for today":

1. **Write** `projects/[project]/sessions/YYYY-MM-DD.md`:
   - Summary (1–2 sentences)
   - What was done (bulleted)
   - Current state (blockers, ready for next)
   - Files modified (with line ranges if relevant)
   - Next phase (what's next, estimate)
   - Time spent

2. **Update** `projects/[project]/sessions/MILESTONES.md`:
   - Rewrite "Current State" section
   - Append to "Key Accomplishments This Session"
   - Update "Known Limitations" if any changed
   - Update "Deployment Readiness" checklist
   - Update "Next Session Checklist"

3. **If a major decision:** Also append to `decisions/log.md`

### Session File Example
```markdown
# Session: YYYY-MM-DD — [Feature/Fix Name]

## Summary
[1–2 sentence overview of what was accomplished]

## What Was Done
- Item 1
- Item 2
- Item 3

## Current State
[Blockers, ready for next phase, testing results]

## Files Modified
- `path/file.js:42-51` — Changed function signature
- `path/config.json:10-15` — Updated token address

## Next Phase
[What's next, estimated time]

## Time Spent
[HH min or total]
```

**Full protocol:** See `references/sops/session-memory.md`

---

## 📜 Standard Operating Procedures (SOPs)

Workflows for recurring tasks. Stored in `references/sops/`.

### sops/session-memory.md
How to run a session: context reading, decision making, note-taking.

### sops/smart-contract-integration.md
5-step workflow for adding smart contract features:
1. Read the smart contract
2. Extract and organize ABIs
3. Wire up contract addresses
4. Update hooks
5. Update UI functions

**Time estimate:** 42–77 minutes per integration

### sops/genealogy-smart-contract-integration.md
Specialized SOP for genealogy/referral network integration (dual-tree, referral tracking).

---

## 🧠 Memory System

Claude Code maintains **persistent memory across conversations** at:
```
/Users/admin/.claude/projects/[PROJECT_PATH]/memory/
```

**Memory types:**

| Type | Purpose | When to Save |
|------|---------|-----------|
| **user** | Your role, goals, preferences, knowledge | Profile changes, new skills |
| **feedback** | How you want Claude to behave | Corrections & confirmations |
| **project** | Active work, milestones, dates, constraints | Project status, deadlines |
| **reference** | Pointers to external systems (Linear, Slack, Grafana) | New integrations, dashboards |

**Example memory:**
```markdown
---
name: blockchain-skill-always-invoke
description: Always invoke blockchain-developer skill before any blockchain task
metadata:
  type: feedback
---

**Rule:** Invoke `/blockchain-developer` skill before any Solidity/Web3 task.

**Why:** Prevents gaps in smart contract knowledge, ensures consistent patterns.

**How to apply:** Every smart contract feature request, contract integration, or DeFi protocol question.
```

---

## 🎨 Rules & Style Guide

Stored in `.claude/rules/`. Define how Claude Code communicates and behaves.

### communication-style.md
```markdown
# Communication Style

## Format
- Use bullet points by default
- No fluff — be concise and direct
- Tables for comparisons
- Code blocks for all code snippets

## Tone
- Internal (working sessions): Professional
- External (public-facing content): Professional and authoritative

## Pet Peeves
- No filler phrases ("Great question!", "Certainly!", "Of course!")
- No unnecessary preamble — lead with the answer
- No emojis unless explicitly requested
- No padding or repetition
```

---

## 🔐 Git Workflow

### Commit Philosophy
Each commit should tell a story:
- **Good:** `feat: add genealogy admin UI with 4-tab interface`
- **Bad:** `fix bug`, `update`, `changes`

### Commit Template
```bash
git commit -m "$(cat <<'EOF'
[type]: [concise description of WHAT was changed]

[Optional: Why this change matters]

Co-Authored-By: Claude Haiku 4.5 <noreply@anthropic.com>
EOF
)"
```

### Types
- `feat:` — New feature
- `fix:` — Bug fix
- `refactor:` — Code reorganization
- `docs:` — Documentation update
- `test:` — Test addition/fix
- `chore:` — Tooling, config, build

### Never Commit
- `.env` files or secrets
- `node_modules/`, `dist/`, build artifacts
- IDE cache (`.DS_Store`, `.idea/`, etc.)

---

## 📁 Archive Rule

**Never delete old work.** Move completed projects to `archives/`:

```bash
git mv projects/[completed-project] archives/[completed-project]
git commit -m "archive: move [project] to completed (shipped 2026-06-12)"
```

Keep the same structure (CLAUDE.md, sessions/, etc.) so you can reference it later.

---

## 🚀 New Project Setup

Use `/project-kickoff` skill or follow this template:

```bash
mkdir -p projects/[project-name]/{sessions,src,docs}

# Create project CLAUDE.md
cat > projects/[project-name]/CLAUDE.md <<'EOF'
# [Project Name] — Development Guide

**Status:** 🟡 In Development  
**Tech Stack:** [List]  
**Ship Target:** [YYYY-MM-DD]

## Overview
[2-3 sentence description]

## Phases
### Phase 1: [Phase Name]
- [ ] Task 1
- [ ] Task 2

## Current State
[What's working, what's blocked]

## Next Phase
[What comes next]
EOF

# Create session MILESTONES.md
cat > projects/[project-name]/sessions/MILESTONES.md <<'EOF'
# [Project Name] — Milestones

**Status:** 🟡 In Development  
**Last Updated:** [YYYY-MM-DD]

## Current State
[What works, what doesn't, blockers]

## Key Accomplishments
- [ ] Item 1
- [ ] Item 2

## Next Session Checklist
- [ ] Item 1
- [ ] Item 2
EOF

# Create initial session file
touch projects/[project-name]/sessions/[YYYY-MM-DD].md
```

---

## 📊 Project Milestones Template

Every project has `sessions/MILESTONES.md` (the source of truth):

```markdown
# [Project Name] — Milestones

**Project Status:** 🟢 Phase X/Y ✅ / 🟡 In Progress / 🔴 Blocked  
**Last Updated:** YYYY-MM-DD  
**Next Session Focus:** [What's next]

---

## Phase Breakdown

### ✅ Phase 1: [Name]
**Status:** COMPLETE
- [x] Task 1
- [x] Task 2

### 🟡 Phase 2: [Name]
**Status:** IN PROGRESS
- [x] Task 1
- [ ] Task 2

### ⏳ Phase 3: [Name]
**Status:** NOT STARTED
- [ ] Task 1

---

## Key Accomplishments This Session

- ✅ Accomplishment 1
- ✅ Accomplishment 2

---

## Current Issues Resolved

| Issue | Status | Solution |
|-------|--------|----------|
| Bug 1 | ✅ FIXED | [How it was fixed] |

---

## Testing Timeline

### ✅ Completed
- Test 1

### 🟡 In Progress
- Test 2

### ⏳ Pending
- Test 3

---

## Known Limitations
1. Limitation 1
2. Limitation 2

---

## Deployment Readiness

### Code Quality
- [x] No compilation errors
- [x] Error handling in place
- [ ] Security review done

### Documentation
- [x] Functions documented
- [x] Setup instructions clear

### Ready for Next Phase
- [x] Core feature working
- [ ] Integration complete

---

## Next Session Checklist

- [ ] Task 1
- [ ] Task 2

---

**Last Session:** YYYY-MM-DD  
**Project Owner:** [Name]  
**Status:** ✅ On Track
```

---

## 🔄 Recommended Workflow Loop

### Every Session (15 min)
```
START
  ↓
[Read context files: me.md, work.md, goals.md, priorities.md]
  ↓
[Read project CLAUDE.md + MILESTONES.md + latest session file]
  ↓
[Confirm orientation: "I'm working on X, current state is Y, blocker is Z"]
  ↓
[DO THE WORK]
  ↓
[Write session notes: what was done, what's next, time spent]
  ↓
[Update MILESTONES.md]
  ↓
[Commit changes]
  ↓
END
```

### Every Week
```
[Review current-priorities.md — still accurate?]
  ↓
[Review active projects — on track?]
  ↓
[Review decisions/log.md — any emerging patterns?]
  ↓
[Archive completed projects]
```

### Every Quarter
```
[Review goals.md — update for new quarter]
  ↓
[Review context files — anything changed?]
  ↓
[Plan next quarter's projects]
```

---

## 🎯 Quick Reference

### Key Commands
```bash
# Start a session
git pull origin main
# [Read CLAUDE.md + MILESTONES.md + latest session]

# End a session
# [Write sessions/YYYY-MM-DD.md]
# [Update sessions/MILESTONES.md]
git add -A
git commit -m "feat: [what was done]"
git push origin main

# Check git status
git status

# View recent commits
git log --oneline -10

# View project structure
tree projects/[project] -L 2
```

### Key Files to Read
- `context/me.md` — Who you are
- `context/current-priorities.md` — What matters now
- `CLAUDE.md` — This operational guide
- `decisions/log.md` — Why things are the way they are
- `projects/[project]/CLAUDE.md` — Project-specific instructions
- `projects/[project]/sessions/MILESTONES.md` — Current state
- `references/sops/session-memory.md` — Session protocol

---

## 📚 Template Files

All templates live in `templates/`:

### session-summary.md
Use at session end to quickly capture what was done.

### contract-integration-template.md
Use when integrating a new smart contract:
- Check contract code
- Extract ABI
- Add to config
- Create hook
- Create UI component

---

## 🛠️ Configuration Files

### .claude/settings.json
Global Claude Code settings (read-only).

### .claude/settings.local.json
Local overrides (not in git). Example:
```json
{
  "defaultModel": "claude-opus-4-8",
  "timeout": 300000,
  "maxTokens": 200000
}
```

### CLAUDE.local.md
Private config for this project. Example:
```markdown
# Local Overrides

Personal preferences and setup-specific config.

## GitHub
- Token: ghp_XXXXX
- User: [username]
```

---

## ✅ Reusability Checklist

When copying this setup to a new project, ensure:

- [ ] Copy `CLAUDE.md` (this file) to project root
- [ ] Copy `.claude/` folder (rules + skills)
- [ ] Create `context/` folder with 5 files (me.md, work.md, goals.md, priorities.md, team.md)
- [ ] Create `projects/[project]/` with CLAUDE.md + sessions/MILESTONES.md
- [ ] Create `references/sops/` with session-memory.md + project-specific SOPs
- [ ] Create `decisions/log.md` (empty, ready to append)
- [ ] Create `archives/` folder (.gitkeep)
- [ ] Create `.gitignore` with standard exclusions
- [ ] Initialize git + first commit
- [ ] Start session with context reading

---

## 🔗 See Also

- `references/sops/session-memory.md` — Session protocol in detail
- `references/sops/smart-contract-integration.md` — Contract wiring SOP
- `context/me.md` — About you
- `context/work.md` — Business structure
- `decisions/log.md` — Project history
- `projects/[active-project]/CLAUDE.md` — Project-specific guide

---

**This document is your operational manual. Share it across projects, update context files per project, and watch Claude Code learn your patterns over time.**

**Last Updated:** 2026-06-12  
**Version:** 2.0 (Comprehensive, Reusable)
