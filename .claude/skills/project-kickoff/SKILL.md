---
name: project-kickoff
description: >-
  Spin up a new full-stack project on the 7–14 day cadence — folder structure,
  project CLAUDE.md, sessions/MILESTONES.md, and first session file.
---

# Project Kickoff

Use to create a new project under `projects/`.

## When to Use
- Starting any new build (the "one project at a time" rule)

## Steps
1. `mkdir -p projects/[name]/{sessions,src,docs}`
2. Create `projects/[name]/CLAUDE.md` (status, stack, ship target, phases)
3. Create `projects/[name]/sessions/MILESTONES.md` (source of truth)
4. Create the first session file `sessions/YYYY-MM-DD.md`
5. Log the kickoff decision in `decisions/log.md`
6. Confirm orientation in 3–5 bullets before writing code

## Outputs
- A ready project folder matching the workspace structure
- MILESTONES.md seeded with Phase 1 tasks
- A clean first commit: `feat: kick off [project]`

## Reference
- Templates: `templates/`
- Structure: root `CLAUDE.md` → "New Project Setup"
