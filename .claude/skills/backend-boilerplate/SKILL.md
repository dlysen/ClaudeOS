---
name: backend-boilerplate
description: >-
  Backend server scaffolding — auth, routes, database layer, config, and a
  baseline test setup ready to extend.
---

# Backend Boilerplate

Use to scaffold a new backend service fast.

## When to Use
- Standing up a new API/service at project kickoff
- Need auth + routes + DB wired with sane defaults

## What It Scaffolds
1. Server entrypoint + config (env-driven)
2. Routing layer with a health check
3. Auth middleware (token/session)
4. Database layer (connection, migrations, models)
5. Error handling + structured logging
6. Baseline test setup

## Checklist
- [ ] `.env.example` documents every required var
- [ ] Health endpoint returns 200
- [ ] Auth middleware protects non-public routes
- [ ] Migrations run cleanly from zero
- [ ] One example test passes
