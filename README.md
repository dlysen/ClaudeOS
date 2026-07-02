# ClaudeOS

A Claude Code **operating-system workspace** for solo, full-stack, fast-shipping
development (7–14 day cadence). It holds the operational guide, a set of composable
project templates, custom + external skills, SOPs, and per-project session memory —
so every new build starts from consistent, reusable patterns.

> Full operating manual: [`CLAUDE.md`](CLAUDE.md)

## Layout

```
CLAUDE.md              # Operational guide (read this first)
.claude/               # Claude Code config — rules/ and skills/
context/               # Who/what/goals/priorities (read at session start)
decisions/             # Append-only decision log
templates/             # Reusable, composable templates (see below)
references/sops/        # Standard operating procedures
projects/              # Active projects — each is its OWN git repo (content untracked here)
archives/              # Completed projects (content untracked here)
```

## Composable Templates (`templates/`)

Mix-and-match. **Apply in order: `core-technology` → `design` → add-ons.**
Call all, or only the one you need.

| Template | Purpose | Prereqs |
|----------|---------|---------|
| [core-technology-template.md](templates/core-technology-template.md) | Scaffold — React 19 + Vite + Tailwind v4; public/private page isolation + optional `api/` | none (root) |
| [design-template.md](templates/design-template.md) | Theme + UI foundation with dark/light mode (CSS tokens) | core |
| [content-builder-template.md](templates/content-builder-template.md) | Config-driven page content + generation prompt | core + design |
| [web3-integration-template.md](templates/web3-integration-template.md) | Wallet connect + contracts — wagmi + Reown AppKit | core |
| [mongo-integration-template.md](templates/mongo-integration-template.md) | Database layer — MongoDB via Mongoose (server-side) | core + a server |
| [github-setup-template.md](templates/github-setup-template.md) | Repo + token + GitHub Pages deploy (gh-pages, custom domain, rollback) | — |
| [contract-integration-template.md](templates/contract-integration-template.md) | Wire a smart contract into a frontend | — |
| [session-summary.md](templates/session-summary.md) | Session wrap-up notes | — |

## Skills

Invoked with slash commands (e.g. `/tailwind-ui`, `/project-kickoff`, `/blockchain-developer`).
Local skills live in `.claude/skills/`; 66 external blockchain skills come from
[hairyf/blockchain-skills](https://github.com/hairyf/blockchain-skills) (cloned + symlinked,
not vendored). See `CLAUDE.md` → "Skills & Agents".

## Projects are independent repos

`projects/` and `archives/` keep only their folder shells here — **each project has its
own dedicated GitHub repository and its own token**. Work inside a project folder and push
from there; the workspace repo never tracks project source.

## Getting Started

1. Read [`CLAUDE.md`](CLAUDE.md) and the `context/` files.
2. Start a build with `/project-kickoff`, then layer templates as needed.
3. Follow the session protocol in `references/sops/session-memory.md`.
