# Contract Integration — [Contract Name]

Use when integrating a new smart contract. See SOP:
`references/sops/smart-contract-integration.md`.

## 1. Contract
- **Name:**
- **Network(s):**
- **Address(es):**
- **Key functions (read):**
- **Key functions (write):**
- **Events to listen for:**

## 2. ABI
- Source artifact:
- Stored at: `src/abis/[name].json`
- Functions/events kept:

## 3. Addresses / Config
```js
// config keyed by network
const ADDRESSES = {
  // mainnet: "0x...",
  // testnet: "0x...",
};
```

## 4. Hooks
- [ ] Read hook(s):
- [ ] Write hook(s):
- [ ] Loading / error / pending-tx handling

## 5. UI
- [ ] Components wired to hooks
- [ ] Pending / success / error states shown
- [ ] Actions disabled during in-flight tx

## Pre-Deploy
- [ ] Security review done
- [ ] Happy + failure paths tested on testnet
- [ ] Decision logged in `decisions/log.md`
