# Domain

The design's sample numbers are internally consistent, so they double as test fixtures.

## Core concepts

| Term | Meaning |
|---|---|
| **Payday** | A day of the month salary arrives. Default 15th and 30th (end of month when the month is shorter). |
| **Cutoff** | The period from one payday to the day before the next, e.g. **Nov 15 – 29**. Everything (budgets, spent, entries) is scoped to a cutoff, not a calendar month. |
| **Salary per payday** | Net amount received each payday (₱24,000). |
| **Fixed items** | "Taken out before you spend": rent, bills, installments, family support, savings. Summed per cutoff. |
| **Safe to spend** | `salary − fixed items` = 24,000 − 13,000 = **₱11,000** |
| **Spent** | Sum of expense entries in the current cutoff = ₱5,930 |
| **Left to spend** | `safe to spend − spent` = **₱5,070** |
| **Days to payday** | Days from today until the next payday = 8 |
| **Per day** | `left / days to payday`, rounded **down to the nearest ₱10** for display ("about ₱630 a day": 5,070 / 8 = 633.75) |
| **Budgeted** | Sum of category limits for the cutoff (₱9,000). `safe − budgeted` = "₱2,000 not assigned to a category yet". |
| **Category budget** | A per-cutoff limit per category. "Copy last cutoff" clones the previous cutoff's limits. |
| **Wallet** | Where money sits: Cash, GCash, Maya, Bank. Each entry is paid from one wallet. Transfers move money between wallets; "Adjust balance" corrects drift. |
| **QR bank** | Stored QR images: your own receiving QRs per wallet, and other people's QRs (name + relationship label). |
| **Reminder** | Bill due soon, category near limit, category over. Has read/unread and snooze. |

## Budget state rules

| State | Condition | Pill text | Bar color |
|---|---|---|---|
| ok | `spent / limit < NEAR` | "On track" | `--ok` |
| near | `NEAR ≤ spent / limit ≤ 100%` | "Near limit · {pct}%" | `--near` |
| over | `spent > limit` | "Over by ₱{spent − limit}" | `--over`, bar 100% |

**Decision:** the design never states the NEAR threshold. Sample data puts 68% in "ok" and 92% in "near".
Default **NEAR = 85%**, kept as one config constant (backend `config/budget.php`) so it's easy to change.

"Closest to limit" on Home = the top 2 categories by `spent / limit`, descending.

## Known sample-data inconsistency

Home says "Spent ₱5,930", but the Entries screen lists only 5 entries totalling ₱1,261 for the same cutoff.
Category spends (2,100 + 1,350 + 1,380 + 1,100 = 5,930) do match Home. Treat Entries' list as a partial sample.

## Proposed data model (Laravel, migrations to be written, NOT run)

```
users              id, name, email, password, theme (light|dark|system), timestamps
pay_settings       id, user_id, salary_cents, payday_1 (1-31), payday_2 (1-31, nullable)
fixed_items        id, user_id, name, amount_cents, sort
wallets            id, user_id, name, type (cash|ewallet|bank), balance_cents, sort
categories         id, user_id, name, sort, archived_at
cutoffs            id, user_id, starts_on, ends_on   -- derived from paydays; materialised for budgets
category_budgets   id, cutoff_id, category_id, limit_cents
entries            id, user_id, wallet_id, category_id, amount_cents, note, spent_on (date), timestamps
transfers          id, user_id, from_wallet_id, to_wallet_id, amount_cents, transferred_on
balance_adjustments id, wallet_id, delta_cents, reason, created_at
qr_codes           id, user_id, wallet_id (nullable), owner_name, label, image_path
reminders          id, user_id, type (bill_due|near_limit|over), payload json, read_at, snoozed_until
```
Wallet balance changes come from entries (−), transfers (±) and adjustments (±). Pick either a cached `balance_cents`
updated in a transaction or computing on read, and decide it once.

## API sketch (`/api/v1`, Sanctum bearer)

```
POST   auth/register | auth/login | auth/logout
GET    summary?cutoff=YYYY-MM-DD        → left, safe, spent, days_to_payday, per_day, closest[2], recent[5], unread_reminders
GET    cutoffs/{date}/budgets           → budgeted, safe, unassigned, categories[{name, limit, spent, state, pct}]
POST   cutoffs/{date}/budgets/copy-previous
PUT    category-budgets/{id}
GET|POST|PUT|DELETE entries          (filters: q, category_id, wallet_id, cutoff)
GET|POST|PUT wallets ; POST transfers ; POST wallets/{id}/adjust
GET|POST|DELETE qr-codes (multipart upload)
GET    reminders ; POST reminders/{id}/read ; POST reminders/{id}/snooze ; POST reminders/read-all
GET|PUT settings/pay ; CRUD fixed-items ; CRUD categories ; PUT settings/theme
```
All money fields are integer centavos in and out. The client formats with `Intl.NumberFormat('en-PH', {style:'currency', currency:'PHP'})`
and trims `.00` the way the design does ("₱5,070", "₱135").
