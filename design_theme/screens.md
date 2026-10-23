# Screens

Routes are suggested Nuxt pages. "Sample" values are the design's placeholder data. Use them for
seeders and mock API responses, never hard-coded in components.

Mobile and desktop are **one responsive app**. Below ~900px, use the mobile shell (BottomTabBar).
Above that, use the DesktopShell (sidebar). Only Home, Entries and Budgets have desktop-specific layouts in the
design. Other screens render inside the desktop main column using their mobile layout.

## Auth and onboarding

### Sign in: `/login`
Full-height column, padding 0 24, content vertically centred. BB logo 72, then "BBudgeTrakker" (Fraunces 40)
and the tagline "What can you safely spend before the next payday?" (18/500 `--ink2`, max-width 300).
Email and Password TextFields (gap 16), primary "Sign in" (54), then text button "Create an account" → `/setup`.
Footer: "Your data is encrypted and stays yours. No bank linking." (13 `--ink2`, centred, 28 from bottom).

### First run: `/setup` (5 steps, one page with step state)
Header: back button (steps 2–4 only) and "BBudgeTrakker" Fraunces 18. StepIndicator below (steps 1–4).
Footer: primary CTA plus "Skip for now" (steps 1–4). Step 5 shows only "Go to Home".

| Step | Title / lead | Body | CTA |
|---|---|---|---|
| 1 Account | "Create your account" / "So your budget is saved and stays yours." | Email, Password ("At least 8 characters") | Create account |
| 2 Salary | "Your salary and payday" / "This is what makes the left-to-spend number work." | Salary per payday (₱24,000); Paydays chips 15th ✓ 30th ✓; "What is in each wallet" FormRows Cash 1,250 · GCash 3,480 · Maya 620 · Bank 9,800 | Save and continue |
| 3 Budgets | "Set your first budgets" / "A limit for each category, per cutoff. Change them any time." | FormRows Food 4,500 · Transport 2,000 · Fun 1,500 · Shopping 1,000 | Save and continue |
| 4 QR codes | "Add your QR codes" / "Upload the QRs you use so scanning next time is one tap." | "My wallets" list (GCash, Maya, Bank, each with Upload); "Other people" dashed "Add someone's QR" | Finish |
| 5 Done | SuccessMark, "You are set" / "Anything you skipped is waiting in Settings. Home shows what you can safely spend before payday." | n/a | Go to Home |

## Main tabs

### Home: `/`
Header: CutoffSwitcher (left) and ReminderBell with badge (right), height 56.
1. **LeftToSpendCard**: ₱5,070 · "8 days to payday · about ₱630 a day" · Spent ₱5,930 of ₱11,000 · 54%.
2. **Closest to limit**: the 2 categories with the highest % used (BudgetRow, Home variant). Sample: Shopping (Over by ₱100, ₱1,100 of ₱1,000), Fun (Near limit · 92%, ₱1,380 of ₱1,500). Each links to Budgets.
3. **Recent**: header with "See all" link → Entries. The 5 latest EntryRows with meta "Category · Wallet · Relative day".

Desktop (`DesktopHome`): page header "Home" plus "Cutoff Nov 15 – 29" and a "3 reminders" pill link on the right.
Two-column auto-fit grid: left has the hero card (amount 84px, padding 28) and Closest to limit; right has Recent.

### Quick add: `/add` (full screen, no tab bar)
Header: close × (→ back) · "Add expense" 17/700 · spacer.
- Amount display: ₱ + Fraunces 64, centred. Empty state "0.00" in `--ink2`. Typed value in `--ink`.
- **Category** label 13/600 and wrapping Chips: Food, Transport, Bills, Load, Fun, Family, Shopping.
- Row of chips: wallet (default = last used, e.g. Cash/GCash with its icon), date ("Today" with calendar icon),
  note (dashed "Add note" until filled, then shows the note text, e.g. "Milk tea", flex 1, ellipsis).
- Spacer, then the save button above the Keypad.
  - No category yet: disabled "Choose a category to save".
  - Ready: primary "Save ₱135".
- **States:** Keypad (nothing chosen) → Chosen (category `.on`, amount typed) → **Saved** screen:
  SuccessMark, "Saved", summary "₱135 · Milk tea · Fun · GCash · Today", a mini Left-to-spend card
  (₱5,070, 28/700, with the per-day line), then "Add another" (primary) and "Done" (secondary → Home).
- Wallet and date remember the last choice (from the showcase copy).

### Entries: `/entries`
ScreenHeader "Entries" + "Nov 15 – 29 · 5 entries · ₱1,261". SearchField "Search notes and amounts".
Horizontally scrolling FilterChips "All categories ▾", "All wallets ▾".
Day groups, newest first: "Today · Nov 22" (₱166), "Yesterday · Nov 21" (₱995), "Nov 20" (₱100). Rows have meta
"Category · Wallet". Tapping a row opens it in Quick add for editing (`/add?entry=ID`).

Desktop (`DesktopEntries`): the same header, search and filters, then a **table** with columns Note | Category | Wallet | Date | Amount (amount right-aligned).

### Budgets: `/budgets`
ScreenHeader "Budgets" + "Cutoff Nov 15 – 29".
1. Summary card (radius 20): "Budgeted ₱9,000" left, "Safe to spend ₱11,000" right (26/700), a 10px accent bar at 82%,
   and "₱2,000 not assigned to a category yet".
2. Secondary button "Copy last cutoff" (copy icon, 48 high, radius 14).
3. **By category**: BudgetRows for Food (ok 47%), Transport (ok 68%), Fun (near 92%), Shopping (over). Tapping a row opens limit editing.

Desktop (`DesktopBudgets`): header with "Copy last cutoff" beside the title, summary card, and category cards in a grid.

### Wallets: `/wallets`
ScreenHeader "Wallets" + "Total across wallets **₱15,150**".
Buttons: primary "Transfer" (transfer icon) and secondary "Adjust balance" (flex 1 each, 48 high, radius 14).
QR bank banner link (52 high, radius 14, `--ok-bg`/`--ok-ink`): QR icon, "QR bank", then "Saved QRs for scanning" on the right → `/wallets/qr`.
WalletCards: Cash "On hand" ₱1,250 · GCash "E-wallet" ₱3,480 · Maya "E-wallet" ₱620 · Bank "Savings account" ₱9,800.

### More / Settings: `/settings`
ScreenHeader "Settings". Groups (13/700 labels, list cards):
- **Paydays**: First payday 15th, Second payday 30th.
- **Categories**: Food, Transport, Bills, Load, Fun, Family, each with a "Rename" button, and "+ Add category".
- **Theme**: SegmentedControl Light / Dark / Match phone.
- **Account**: "Personal: salary and payday" → `/settings/personal`, "QR bank" → `/wallets/qr`, "Reminders" → `/reminders`.
- "Sign out".

## Sub-pages (no tab bar, SubPageHeader with back)

### Reminders: `/reminders`
Title "Reminders", "3 unread", and a "Mark all read" action. ReminderCards:
- "Internet bill due in 2 days" · "₱800 · due Nov 24"
- "Fun is at 92% of its limit" · "₱1,380 of ₱1,500 · ₱120 left" (near)
- "Shopping is over budget by ₱100" · "₱1,100 of ₱1,000" (over)
Each has "Mark read" and "Snooze".

### QR bank: `/wallets/qr`
Intro: "Keep the QR codes you pay with or send to, so scanning next time is one tap."
"My wallets": GCash, Maya, Bank (each "My receiving QR", Show). "Other people": Mama ("Family · saved QR"),
Rent share ("Housemate · saved QR"). Primary "Upload a QR" (upload icon) at the bottom.

### Personal: `/settings/personal`
- **Salary and paydays**: Salary per payday ₱24,000; First payday 15th; Second payday 30th ("Day of the month").
- **Taken out before you spend** (fixed deductions): Rent share ₱5,000 · Internet ₱800 · Pay-later installment ₱1,200 ·
  Family support ₱3,000 · Savings ₱3,000 · "+ Add item" (accent).
- Result card (`--ok-bg`/`--ok-ink`, radius 20): "Safe to spend each cutoff" **₱11,000** · "₱24,000 minus ₱13,000 of fixed items".

## System states (see States artboard)
- **Offline**: OfflineAlert at the top of the screen, with the hero number dimmed plus the stale-data note.
- **Empty entries**: EmptyState "No entries yet" / "Type an amount, tap a category, and it is logged." / "Add expense".
