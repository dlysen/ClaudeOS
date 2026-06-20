# SOP — Genealogy / Referral Network Integration

Specialized variant of the smart-contract-integration SOP for dual-tree
genealogy and referral-tracking systems (e.g. MLM/network growth, vesting
referral networks).

## Concepts
- **Dual-tree structure** — typically a sponsor tree + a placement/binary tree
- **Per-user optimization** — each user node tracks upline/downline + volume
- **Referral tracking** — record who referred whom on registration

## Steps (extends the 5-step base SOP)
1. **Read the genealogy contract** — map registration, placement, and reward logic
2. **Extract ABIs** — registration, tree queries, reward/claim functions, events
3. **Wire addresses** — genealogy contract + any reward/token contracts
4. **Update hooks** —
   - read: upline, downline, tree position, accrued rewards
   - write: register (with referrer), claim rewards, place node
5. **Update UI** — referral link generation, tree visualization, reward claim UI

## Edge Cases to Handle
- Self-referral / circular referral prevention
- Re-registration attempts
- Spillover placement rules (binary trees)
- Reward calculation precision (minor units, no float)

## Before Deploy
- Verify tree integrity invariants (no orphan nodes, no cycles)
- Security review of reward math + access control
- Log the decision and tree design in `decisions/log.md`
