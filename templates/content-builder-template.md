# Content Builder — [Project Name]

Config-driven page content: one typed file holds all copy + an **ordered section list**,
rendered through a registry. Edit one file to rebuild the page. Includes a reusable
**generation prompt** to draft the content config from a brief.

## Prerequisites
- `core-technology-template.md` (base scaffold)
- `design-template.md` (sections render with theme tokens)

## 1. Content Model
```ts
// src/content/site.ts
export type Section =
  | { type: 'hero'; title: string; subtitle: string; cta: { label: string; href: string } }
  | { type: 'features'; heading: string; items: { icon: string; title: string; body: string }[] }
  | { type: 'cta'; title: string; button: { label: string; href: string } }
  // [add section types as needed]

export const site = {
  brand: '[Brand]',
  nav: [{ label: 'Home', href: '#' }],
  sections: [
    { type: 'hero', title: '[Headline]', subtitle: '[Subhead]', cta: { label: '[CTA]', href: '#' } },
    { type: 'features', heading: '[Why us]', items: [/* ... */] },
    { type: 'cta', title: '[Ready?]', button: { label: '[Button]', href: '#' } },
  ] as Section[],
}
```

## 2. Section Registry (renderer)
```tsx
// src/components/SectionRenderer.tsx
import type { Section } from '../content/site'
import { Hero } from '../sections/Hero'
import { Features } from '../sections/Features'
import { CTA } from '../sections/CTA'

const registry = { hero: Hero, features: Features, cta: CTA } as const

export function SectionRenderer({ sections }: { sections: Section[] }) {
  return <>{sections.map((s, i) => {
    const C = registry[s.type] as React.FC<any>
    return C ? <C key={i} {...s} /> : null
  })}</>
}
```
- Each `sections/*.tsx` component is presentational and uses design tokens.
- `App.tsx`: `<SectionRenderer sections={site.sections} />`.

## 3. Generation Prompt (fill the brief, paste to generate `site.ts`)
```
You are generating a `site.ts` content config for a React landing page.
BUSINESS: [what the product/company does]
AUDIENCE: [who it's for]
TONE: [e.g. bold, minimal, technical]
GOAL / PRIMARY CTA: [e.g. "Connect wallet", "Book a demo"]
SECTIONS WANTED: [e.g. hero, features(3), cta]
CONSTRAINTS: match the existing `Section` union types; concise, benefit-led copy;
no placeholder lorem ipsum; return ONLY the `site` object as valid TypeScript.
```

## 4. Structure
```
src/
  content/site.ts              # single source of page content
  components/SectionRenderer.tsx
  sections/Hero.tsx  Features.tsx  CTA.tsx ...
```

## Checklist
- [ ] All copy lives in `content/site.ts` — no hardcoded text in JSX
- [ ] Every `type` in the union has a registry entry + component
- [ ] Sections render in array order; reordering the array reorders the page
- [ ] Components use design tokens (works in light + dark)
- [ ] Generated content reviewed for accuracy before commit

## Next
- Add `web3-integration-template.md` (wallet CTA) or other add-ons as the task needs.
