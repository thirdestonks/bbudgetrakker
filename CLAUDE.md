# BBudgeTrakker

A budget tracker built around **paydays, not calendar months**. The one question it answers:
*"What can I safely spend before the next payday?"* Filipino context: ₱ amounts, 15th/30th
paydays ("cutoffs"), Cash / GCash / Maya / Bank wallets.

## Stack

| Layer | Choice | Folder |
|---|---|---|
| Web + app UI | **Nuxt** (Vue 3, TypeScript, SPA mode) | `frontend/` |
| API | **Laravel** (REST JSON, Sanctum token auth) | `backend/` |
| Database | MySQL | n/a |
| Mobile, phase 1 | **Capacitor**, wrapping the Nuxt static build | `frontend/` (`android/`, `ios/`) |
| Mobile, phase 2 | Expo (React Native), a separate app on the same Laravel API | later |
| Hosting | AWS | n/a |

### Rules that follow from this stack

- **Nuxt runs with `ssr: false`** and ships with `nuxt generate`. Capacitor needs a static SPA,
  so don't add anything that requires a Node server at runtime (server routes, SSR-only data fetching).
- **All business logic lives in Laravel.** Money math (safe to spend, left to spend, budget states)
  is computed server-side and returned by the API. The Expo app in phase 2 reuses the API, and
  logic kept in Vue would have to be rewritten.
- **Auth = Sanctum personal access tokens** (Bearer), not cookie SPA auth. Capacitor's origin
  (`https://localhost` / `capacitor://localhost`) makes cookie auth painful.
- **Money is stored as integer centavos** (`amount_cents`, BIGINT). Never floats. Format on the client.
- **No 3D libraries** (Three.js, Babylon). The design has no 3D, so don't add them without a concrete feature.

## Design source of truth

- Live design canvas: https://claude.ai/code/artifact/8cc7f248-7ae3-4688-b015-75729ae41795
- Written spec: [`design_theme/`](design_theme/README.md). **Read it before building any screen.**
  - [tokens.md](design_theme/tokens.md): colors (light and dark), type, spacing, radii. Ready-to-paste CSS.
  - [components.md](design_theme/components.md): every reusable piece and its exact styling.
  - [screens.md](design_theme/screens.md): every screen, its route, and its contents.
  - [domain.md](design_theme/domain.md): cutoffs, safe-to-spend math, budget states, data model.
  - [brand.md](design_theme/brand.md): logo, voice, copy rules, marketing pieces.

Design rules that must hold in code:
- Colors only through CSS custom properties (`var(--accent)` and so on). No raw hex in components.
- Budget states always show **icon + label**, never color alone.
- Touch targets are at least 44px. Amounts use tabular numerals (`.num`).
- Every screen works in light and dark. Theme options are Light / Dark / Match phone.

## Conventions

- Frontend: Vue SFCs with `<script setup lang="ts">`. Components in `frontend/app/components/`,
  pages in `frontend/app/pages/` (Nuxt 4 `app/` dir). One component per design element in components.md.
- Styling: plain scoped CSS plus the global token sheet. No Tailwind or UI kit unless agreed, because the
  design's exact values are easier to hit by hand.
- Icons: inline stroke SVG, as in the design (24×24 viewBox, `stroke="currentColor"`). No emoji.
- Backend: Laravel API resources under `routes/api.php`, versioned `/api/v1/...`.
  Form Requests for validation, API Resources for responses.

## Hard rules (also in the global CLAUDE.md)

- Never `git commit` / `git push` / create PRs. The user commits.
- Never run migrations (`php artisan migrate*`, `db:wipe`, etc.). Write migration files; the user runs them.

## Commands (once scaffolded)

```bash
# frontend
cd frontend && npm install && npm run dev          # http://localhost:3000
npm run generate && npx cap sync                    # build for Capacitor

# backend
cd backend && composer install && php artisan serve # http://localhost:8000
```
