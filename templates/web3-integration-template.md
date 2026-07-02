# Web3 Integration — [Project Name]

Wallet connect + on-chain reads/writes via **wagmi + viem + TanStack Query**, with
**Reown AppKit (Web3Modal)** as the connector UI. Optional add-on — layer on when a
project needs wallets/contracts.

Pairs with the `/wagmi` and `/blockchain-developer` skills; use
`contract-integration-template.md` when wiring a specific contract.

## Prerequisites
- `core-technology-template.md` (base scaffold)
- `design-template.md` recommended (for a themed connect button)
- Reown **Project ID** from `dashboard.reown.com`
```bash
npm install wagmi viem @tanstack/react-query @reown/appkit @reown/appkit-adapter-wagmi
```

## 1. Env
```env
# .env.example
VITE_REOWN_PROJECT_ID=your_reown_project_id_here
```
- Never commit `.env` (see `github-setup-template.md`).

## 2. Config (Reown AppKit + wagmi adapter)
```ts
// src/lib/appkit.ts
import { createAppKit } from '@reown/appkit/react'
import { WagmiAdapter } from '@reown/appkit-adapter-wagmi'
import { mainnet, base } from '@reown/appkit/networks'   // [set target chains]

const projectId = import.meta.env.VITE_REOWN_PROJECT_ID
export const networks = [mainnet, base]
export const wagmiAdapter = new WagmiAdapter({ projectId, networks })

createAppKit({
  adapters: [wagmiAdapter],
  projectId,
  networks,
  metadata: {
    name: '[Project Name]',
    description: '[one-line description]',
    url: 'https://[your-domain]',
    icons: ['https://[your-domain]/icon.png'],
  },
})
export const wagmiConfig = wagmiAdapter.wagmiConfig
```

## 3. Providers + Connect Button
```tsx
// src/main.tsx (wrap App)
import { WagmiProvider } from 'wagmi'
import { QueryClient, QueryClientProvider } from '@tanstack/react-query'
import { wagmiConfig } from './lib/appkit'
const queryClient = new QueryClient()
// <WagmiProvider config={wagmiConfig}>
//   <QueryClientProvider client={queryClient}><App /></QueryClientProvider>
// </WagmiProvider>
```
```tsx
// src/components/ConnectButton.tsx  — Reown web component
export const ConnectButton = () => <appkit-button />
```
- Reads/writes: `useAccount`, `useReadContract`, `useWriteContract`,
  `useWaitForTransactionReceipt` (see `/wagmi`).

## 4. Structure
```
src/
  lib/appkit.ts            # AppKit + wagmi config
  components/ConnectButton.tsx
  hooks/                   # useReadX / useWriteX per contract
  abis/                    # [name].json (see contract-integration-template.md)
```

## Checklist
- [ ] `VITE_REOWN_PROJECT_ID` set; `.env` gitignored; `.env.example` documents it
- [ ] Wallet connects, disconnects, and switches chains
- [ ] Correct `networks` (chains) for the deployment target
- [ ] Loading / pending-tx / error states shown; actions disabled in-flight
- [ ] `npm run build` passes with a placeholder Project ID

## Next
- Wire a specific contract with `contract-integration-template.md`.
- Add `mongo-integration-template.md` if the app needs off-chain persistence.
