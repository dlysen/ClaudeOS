# SOP — Session Memory Protocol

How to run a session so context never gets lost.

## Session Start
When Dangal says "Let's work on [project]":
1. Read `context/` files — me.md, work.md, goals.md, current-priorities.md, team.md
2. Read `projects/[project]/CLAUDE.md`
3. Read `projects/[project]/sessions/MILESTONES.md` (current state, decisions, blockers)
4. Read the most recent `projects/[project]/sessions/YYYY-MM-DD.md`
5. **Confirm orientation in 3–5 bullets** before doing any work:
   - "I'm working on X, current state is Y, blocker is Z, next step is W"

## During the Session
- Code-first, docs-second
- Log any non-trivial decision in `decisions/log.md` as you go
- Keep changes scoped to the active project

## Session End
At a natural close or "done for today":

1. **Write** `projects/[project]/sessions/YYYY-MM-DD.md`:
   - Summary (1–2 sentences)
   - What was done (bulleted)
   - Current state (blockers, ready-for-next)
   - Files modified (with line ranges)
   - Next phase (+ estimate)
   - Time spent

2. **Update** `projects/[project]/sessions/MILESTONES.md`:
   - Rewrite "Current State"
   - Append to "Key Accomplishments This Session"
   - Update "Known Limitations", "Deployment Readiness", "Next Session Checklist"

3. **If a major decision:** append to `decisions/log.md`

4. Commit changes with a story-telling message
