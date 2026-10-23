# BBudgeTrakker

**What can you safely spend before the next payday?**

BBudgeTrakker is a budget tracker built around paydays, not calendar months. Tell it your salary, your
paydays (15th and 30th) and what gets taken out first (rent, bills, savings). It shows one honest number,
**left to spend this cutoff**, plus per-category limits that warn you before you go over.

- **Left to spend**: safe-to-spend minus what you've logged, with "about ₱630 a day" until payday
- **Quick add**: type the amount, tap a category, done. Wallet and date remember your last choice
- **Budgets per cutoff**: On track / Near limit / Over, always with an icon and a label, not just color
- **Wallets**: Cash, GCash, Maya, Bank, with transfers and balance adjustments
- **QR bank**: keep your receiving QRs and other people's QRs for one-tap scanning
- **Reminders**: bills due, categories near or over their limit
- Light and dark themes. No bank linking.

## Stack

| | |
|---|---|
| Frontend | [Nuxt](https://nuxt.com) (Vue 3, TypeScript, SPA) in `frontend/` |
| API | [Laravel](https://laravel.com) + Sanctum in `backend/` |
| Database | MySQL |
| Mobile | [Capacitor](https://capacitorjs.com) (phase 1), Expo (phase 2) |
| Hosting | AWS |

## Project layout

```
backend/        Laravel API (/api/v1)
frontend/       Nuxt app (web + Capacitor shell)
design_theme/   Design spec: tokens, components, screens, domain rules, brand
CLAUDE.md       Working notes for AI-assisted development
```

The visual design lives on a Claude design canvas. [`design_theme/`](design_theme/README.md) is its written,
build-ready version.

## Getting started

> The app is not scaffolded yet. These are the target commands.

```bash
# API
cd backend
composer install
cp .env.example .env && php artisan key:generate
# configure DB_* in .env, then run migrations yourself
php artisan serve                 # http://localhost:8000

# Web app
cd frontend
npm install
npm run dev                       # http://localhost:3000

# Mobile (Capacitor)
npm run generate
npx cap sync
npx cap open android              # or: npx cap open ios
```

## Roadmap

1. Scaffold Nuxt + Laravel, design tokens, app shell and navigation
2. Auth and first-run setup (salary, paydays, wallets, budgets)
3. Home, Quick add, Entries
4. Budgets, Wallets, Settings, Personal
5. Reminders, QR bank, offline and empty states
6. Desktop layouts
7. Capacitor builds (Android, then iOS)
8. Phase 2: Expo app on the same API
