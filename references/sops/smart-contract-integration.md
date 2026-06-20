# SOP — Smart Contract Integration

5-step workflow for adding a smart contract feature to an app.
**Time estimate:** 42–77 minutes per integration.

## 1. Read the Smart Contract
- Understand functions, events, modifiers, access control
- Note state-changing vs. view functions
- Identify the addresses/networks involved

## 2. Extract & Organize ABIs
- Pull the ABI from the compiled artifact
- Keep only the functions/events the app needs
- Store ABIs in a predictable location (e.g. `src/abis/`)

## 3. Wire Up Contract Addresses
- Add addresses to config, keyed by network
- Never hardcode addresses inline
- Document which network each address belongs to

## 4. Update Hooks
- Create/extend hooks for read calls (view) and write calls (tx)
- Handle loading, error, and pending-tx states
- Surface transaction hashes for UX feedback

## 5. Update UI Functions
- Wire buttons/forms to the hooks
- Show pending/success/error states
- Disable actions while a tx is in flight

## Before Deploy
- Run a security review (reentrancy, access control, overflow, oracle risk)
- Test happy + failure paths on a testnet
- Log the integration decision in `decisions/log.md`
