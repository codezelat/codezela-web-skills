---
name: frontend-polish-shadcn-qa
description: Use when building or polishing responsive UI, Figma/design-source implementation, shadcn/ui, dashboards, dialogs, tables, skeletons, empty states, minimal wording, accessibility, i18n/language switching, mobile fixes, animations, or visual QA.
---

# Frontend Polish Shadcn QA

Use this to make UI feel intentionally built, not generated. The default taste is modern, smooth, minimal, readable, and practical.

## Non-Negotiables

- Preserve existing design language unless the user asks for redesign.
- If Figma, screenshots, live references, or brand assets are provided, they are the source of truth. Do not treat them as loose inspiration.
- Use Figma MCP, screenshots, exported assets, or available design metadata when available; if tooling is unavailable, inspect the provided images/assets and state the fallback.
- Use the repo's component system; do not invent parallel primitives.
- Admin UI should be direct, searchable, keyboard-friendly, and low-word.
- Public UI should be clean, real, responsive, and free of fake filler.
- No browser confirm/alert/prompt for production workflows; use dialogs/toasts/inline states.
- Loading skeletons should resemble the final layout and be scoped to the slow section.
- Mobile/tablet/desktop all need explicit review.
- Favor purposeful hierarchy, spacing, and typography over generic cards everywhere.
- Interactive controls need labels, visible focus, keyboard access, and usable mobile tap targets.
- Language switchers and translated UI must not drift, get stuck loading, or claim a language that is not visibly applied.
- Respect reduced motion; use animation to clarify state, not to decorate every element.

## Workflow

1. Inspect existing tokens, `components.json`, UI primitives, layout shells, CSS variables, and available design source.
2. For Figma/design-source work, extract frames, measurements, colors, typography, assets, variants, responsive intent, and interaction states before coding.
3. Build with existing shadcn/ui or project components.
4. Keep copy short: labels, headings, empty states, button text.
5. Add accessible labels, focus states, disabled/pending states, keyboard behavior, and reduced-motion handling.
6. Handle empty/error/loading states.
7. Check responsive behavior, especially nav, tables, dialogs, cards, image crops, language controls, and floating controls.
8. For i18n, check persistence, route changes, cookies/local storage, public/admin exclusions, and visible state sync.
9. Browser-smoke the changed route if possible.

## Checks

- UI has no overflow or clipped controls at mobile/tablet/desktop.
- Design-source implementation matches the supplied reference for layout, spacing, typography, color, imagery, and responsive behavior unless a deliberate deviation is explained.
- Dialogs close/reset correctly after success.
- Pending buttons prevent duplicate submissions.
- Empty and error states are useful.
- No copy bloat or placeholder content remains.
- Interactive controls are reachable by keyboard and have visible focus.
- Language/translation controls work on home and inner routes without permanent spinner states.
