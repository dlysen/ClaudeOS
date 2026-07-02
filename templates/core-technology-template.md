# Core Technology — [Project Name]

**The base scaffold. Always apply this first** — every other template
(`design-template.md`, `content-builder-template.md`, `web3-integration-template.md`,
`mongo-integration-template.md`, …) builds on top of it.

Stack: **React 19 + Vite + TypeScript + TailwindCSS v4**.

## Prerequisites
- None. This is the root template.

## 1. Scaffold
```bash
npm create vite@latest [project-name] -- --template react-ts   # React 19 + Vite + TS
cd [project-name]
npm install
npm install react-router-dom                                    # routing (public/private pages)
npm install -D tailwindcss @tailwindcss/vite                    # Tailwind v4 (Vite plugin)
```

## 2. Wire Tailwind (v4)
```ts
// vite.config.ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({ plugins: [react(), tailwindcss()] })
```
```css
/* src/index.css */
@import "tailwindcss";
```

## 3. Baseline Folder Structure
Pages are **isolated by access level**: `pages/public/` (open to everyone) and
`pages/private/` (behind an auth guard). A root-level `api/` folder is **optional** —
add it only when the project needs simple serverless webhooks (Telegram, Stripe, etc.).
```
[project-name]/
  api/                       # OPTIONAL — serverless webhook handlers (Vercel/Netlify style)
    telegram.ts              #   e.g. POST /api/telegram — parse update payload
    webhook.ts               #   e.g. generic inbound webhook (verify signature first)
  src/
    main.tsx                 # entry — mounts <RouterProvider/>, imports index.css
    App.tsx                  # root layout (nav, <Outlet/>, theme)
    index.css                # @import "tailwindcss";
    routes/
      index.tsx              # route tree: public routes + guarded private routes
      ProtectedRoute.tsx     # gate — redirects to /login if not authed
    pages/
      public/                # NO auth — landing, login, pricing, 404, ...
        Landing.tsx
        Login.tsx
      private/               # REQUIRES auth — dashboard, settings, ...
        Dashboard.tsx
    auth/
      AuthProvider.tsx       # session/user context + useAuth()
    components/              # shared UI (composed by design-template.md)
    lib/                     # helpers, clients (db/web3/api added by add-on templates)
```

## 4. Routing + Auth Gate
- Wrap private routes in `ProtectedRoute`; public routes render freely.
```tsx
// src/routes/ProtectedRoute.tsx
import { Navigate, Outlet } from 'react-router-dom'
import { useAuth } from '../auth/AuthProvider'

export function ProtectedRoute() {
  const { user, loading } = useAuth()
  if (loading) return null                          // or a spinner
  return user ? <Outlet /> : <Navigate to="/login" replace />
}
```
```tsx
// src/routes/index.tsx
import { createBrowserRouter } from 'react-router-dom'
import App from '../App'
import { ProtectedRoute } from './ProtectedRoute'
import { Landing } from '../pages/public/Landing'
import { Login } from '../pages/public/Login'
import { Dashboard } from '../pages/private/Dashboard'

export const router = createBrowserRouter([
  { element: <App />, children: [
    { path: '/', element: <Landing /> },            // public
    { path: '/login', element: <Login /> },         // public
    { element: <ProtectedRoute />, children: [       // everything below needs auth
      { path: '/dashboard', element: <Dashboard /> },
    ]},
  ]},
])
```
- `api/` handlers are **server-side**: verify the source (Telegram secret token / Stripe
  signature) before trusting the payload; keep secrets in `.env` (never `VITE_`-prefixed).

## 5. Scripts / Env
- `npm run dev` (Vite dev server), `npm run build` (typecheck + build), `npm run preview`.
- Create `.env.example` now; all client vars are prefixed `VITE_`. `.env` is gitignored
  (see `github-setup-template.md`).

## Checklist
- [ ] `npm run dev` serves the app
- [ ] Tailwind classes apply (test one utility on `App.tsx`)
- [ ] Public pages load without auth; private pages redirect to `/login` when signed out
- [ ] `pages/public/` vs `pages/private/` separation kept (no auth-gated view in public/)
- [ ] `api/` handlers verify sender signature/secret before acting (only if `api/` used)
- [ ] `npm run build` passes (no TS errors)
- [ ] `.env.example` created; `.env` in `.gitignore`; no secrets `VITE_`-prefixed
- [ ] Repo initialized per `github-setup-template.md`

## Next
- Apply `design-template.md` (theme + dark/light) — the second prerequisite.
- Then compose any add-on template as the task needs.
