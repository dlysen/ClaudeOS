---
name: api-test-suite
description: >-
  Generate integration test suites for APIs — happy paths, edge cases, auth,
  error handling, and contract validation.
---

# API Test Suite

Use to build comprehensive integration tests for an API.

## When to Use
- A new or changed API endpoint needs coverage
- Validating request/response contracts
- Regression-proofing before a ship

## What It Produces
1. Happy-path tests for each endpoint
2. Edge cases (empty, oversized, malformed input)
3. Auth tests (missing/invalid/expired tokens, role checks)
4. Error-path tests (4xx/5xx with correct bodies)
5. Contract assertions (status, schema, headers)

## Checklist
- [ ] Every endpoint has at least one happy + one failure test
- [ ] Auth boundaries tested
- [ ] Tests are isolated and repeatable (no shared mutable state)
- [ ] CI-runnable with a single command
