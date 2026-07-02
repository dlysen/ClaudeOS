# Design System — [Project Name]

Theme + UI foundation with **dark / light mode**. Apply **second, right after
`core-technology-template.md`** — add-on templates render inside this design layer.

Pairs with the `/tailwind-ui` skill (mobile-first, theme tokens, lucide, accessibility).

## Prerequisites
- `core-technology-template.md` (React 19 + Vite + Tailwind v4)
- `npm install lucide-react`

## 1. Theme Tokens (Tailwind v4 `@theme` + CSS variables)
Define light defaults on `:root`, dark overrides on `.dark`, and expose them as
Tailwind color tokens so utilities like `bg-surface text-fg` work.
```css
/* src/index.css */
@import "tailwindcss";
@custom-variant dark (&:where(.dark, .dark *));

:root {
  --color-bg: #ffffff;  --color-surface: #f5f5f7;
  --color-fg: #0a0a0a;  --color-muted: #6b7280;
  --color-primary: #4f46e5;
}
.dark {
  --color-bg: #0a0a0a;  --color-surface: #141416;
  --color-fg: #fafafa;  --color-muted: #9ca3af;
  --color-primary: #818cf8;
}
@theme inline {
  --color-bg: var(--color-bg);
  --color-surface: var(--color-surface);
  --color-fg: var(--color-fg);
  --color-muted: var(--color-muted);
  --color-primary: var(--color-primary);
}
```

## 2. Theme Provider + Toggle
```tsx
// src/components/ThemeToggle.tsx
import { useEffect, useState } from 'react'
import { Moon, Sun } from 'lucide-react'

export function ThemeToggle() {
  const [dark, setDark] = useState(() =>
    localStorage.theme === 'dark' ||
    (!('theme' in localStorage) && matchMedia('(prefers-color-scheme: dark)').matches))
  useEffect(() => {
    document.documentElement.classList.toggle('dark', dark)
    localStorage.theme = dark ? 'dark' : 'light'
  }, [dark])
  return (
    <button aria-label="Toggle theme" onClick={() => setDark(v => !v)}
      className="rounded-md p-2 text-fg hover:bg-surface">
      {dark ? <Sun size={18} /> : <Moon size={18} />}
    </button>
  )
}
```
- Add an FOUC guard in `index.html` `<head>` to set `.dark` before paint:
  ```html
  <script>if(localStorage.theme==='dark'||(!('theme'in localStorage)&&matchMedia('(prefers-color-scheme:dark)').matches))document.documentElement.classList.add('dark')</script>
  ```

## 3. Structure
```
src/
  index.css                 # tokens + dark variant (above)
  components/ThemeToggle.tsx
  components/ui/            # buttons, cards, inputs — theme-token based
```

## Checklist
- [ ] Light + dark both readable; toggle persists across reload
- [ ] No FOUC (dark applied before first paint)
- [ ] Components use tokens (`bg-bg`, `text-fg`, `bg-primary`) — no hardcoded hex
- [ ] Respects `prefers-color-scheme` on first visit
- [ ] Keyboard-focusable toggle with visible focus + `aria-label`

## Next
- Compose add-ons: `content-builder-template.md`, `web3-integration-template.md`,
  `mongo-integration-template.md`, etc. — each renders using these tokens.
