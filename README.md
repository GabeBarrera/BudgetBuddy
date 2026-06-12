# BudgetBuddy

A single-file, client-side personal budget tracker. No server, no dependencies, no sign-up — everything runs in the browser and persists to `localStorage`.

## Getting Started

Open `index.html` in any modern browser. That's it.

---

## Views

The app has three pages. Swipe left/right, use the arrow keys, or tap the bottom nav dots to switch between them.

### Accounts
Track bank or investment account balances over time.

- **Add account** — name the institution; optionally import a CSV to load historical balance data
- **CSV import** — file must have `Date` and `Total Value` columns; rows are parsed and stored as a time series
- **Cards** — show current balance, total change in dollars and percent, number of data points, and last-updated date
- **Timeline chart** — canvas line chart plotting all accounts on a shared axis; hover to see interpolated values for each account at any date
- **Edit / delete** — re-import CSV to replace an account's history, or delete the account entirely

### Expenses (graph view)
Visualize spending against a configurable budget limit.

**Time filters**
| Filter | Range |
|---|---|
| Today | Current calendar day |
| This week | Sunday – Saturday of the current week |
| This month | First to last day of the current month |
| YTD | Jan 1 to today |
| Custom | Date range, single month, or single year |

**Budget limit**
- Set a monthly limit (dollars); the app automatically pro-rates it to match the active time filter (daily, weekly, YTD, custom range)
- **Modifiers** — named monthly deductions (e.g. rent, savings, 401k contribution) that reduce the effective limit before it is scaled; preset types available or enter a custom name
- The modifiers panel shows total deductions and the net limit per month

**Chart**
- Canvas area chart of cumulative spend over the selected period
- Dashed horizontal line at the scaled limit threshold
- Line and fill turn green when under budget, red when over
- Header shows total spent, scaled limit, remaining/over amount, and percentage used

### Expense Log
Add, edit, and delete individual expense entries.

**Adding an expense** — fill in date (defaults to today), category, vendor (optional), and amount, then submit.

**Categories**
Food · Groceries · Gas · Transit · Rent/Housing · Utilities · Subscriptions · Entertainment · Health · Shopping · Travel · Other

**Table** — entries sorted newest-first; each row has an edit button (opens a modal) and a delete button (confirms before removing).

---

## Settings

Access via the gear icon in the top-right corner.

| Option | What it does |
|---|---|
| **Backup** | Downloads `budgetbuddy.json` containing all expenses, accounts, and settings |
| **Import → Recover Backup** | Restores from a `budgetbuddy.json` backup file, replacing all current data |
| **Import → Expense Log** | Replaces the expense log from a `.json` or `.csv` file |
| **Import → Accounts** | Replaces all accounts from a `.json` or `.csv` file |
| **Export → Expense Log** | Downloads expenses as `budgetbuddy_expenses.json` or `budgetbuddy_expenses.csv` |
| **Export → Accounts** | Downloads accounts as `budgetbuddy_accounts.json` or `budgetbuddy_accounts.csv` |
| **Purge** | Permanently deletes all data; requires checking an acknowledgement box and a second confirmation |

---

## CSV Formats

### Accounts CSV
```
Account,Date,Total Value
Checking,2024-01-01,4200.00
Checking,2024-02-01,4850.00
Savings,2024-01-01,12000.00
```

### Expenses CSV
```
Date,Category,Vendor,Amount
2024-03-15,Food,Chipotle,14.50
2024-03-16,Groceries,Whole Foods,87.23
```

Accepted date formats: `YYYY-MM-DD`, `M/D/YYYY`, `M-D-YYYY`, and most strings parseable by `Date()`.

---

## Theme

Toggle light/dark mode with the moon icon in the top-right corner. The preference is saved automatically.

---

## Data Storage

All data is stored in `localStorage` under three keys:

| Key | Contents |
|---|---|
| `budget_expenses` | Array of expense entries |
| `budget_accounts` | Array of accounts with their time-series data |
| `budget_settings` | Monthly limit, active filter, custom date range, theme, modifiers |

No data is ever sent to a server.
