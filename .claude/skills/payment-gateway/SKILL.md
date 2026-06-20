---
name: payment-gateway
description: >-
  Payment flow templates and transaction patterns — checkout, webhooks,
  idempotency, refunds, and reconciliation.
---

# Payment Gateway

Use when integrating payments or building transaction flows.

## When to Use
- Adding checkout / payment capture
- Handling provider webhooks
- Refunds, disputes, reconciliation
- On-chain payment / token transfer flows

## Core Patterns
1. **Idempotency** — every charge/refund carries an idempotency key.
2. **Webhook verification** — verify signatures before trusting events.
3. **State machine** — pending → authorized → captured → settled/refunded.
4. **Reconciliation** — never trust client state; reconcile against provider.
5. **Audit trail** — log every transition with amounts and IDs.

## Checklist
- [ ] No secrets in client code
- [ ] Webhook signatures verified
- [ ] Idempotent retries
- [ ] Amounts handled in minor units (avoid float)
- [ ] Failure + refund paths tested
