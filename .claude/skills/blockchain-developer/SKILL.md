---
name: blockchain-developer
description: >-
  Web3/Solidity expertise — smart contract development, DeFi protocols, gas
  optimization, and security audits. Invoke before any Solidity/Web3 task.
---

# Blockchain Developer

Use for any smart contract, DeFi, or Web3 work.

## When to Use
- Writing or reviewing Solidity contracts
- DeFi protocol design (staking, vesting, DEX, lending)
- Gas optimization
- Contract audits / security review
- Wiring contracts to a frontend (see SOP: smart-contract-integration)

## Core Practices
1. Read the contract fully before changing anything.
2. Prefer audited libraries (OpenZeppelin) over hand-rolled logic.
3. Check for reentrancy, integer issues, access control, and oracle risks.
4. Optimize gas only after correctness is proven.
5. Run a security review before any deploy.

## Toolchain
- Hardhat / Foundry for build + test
- OpenZeppelin for standard contracts
- Alchemy for RPC/indexing
- See `.claude/skills/blockchain-skills-external/` for 69+ specialized skills

## Related
- SOP: `references/sops/smart-contract-integration.md`
- SOP: `references/sops/genealogy-smart-contract-integration.md`
