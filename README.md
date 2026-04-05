# NexaFinance Dashboard

A premium glassmorphic finance tracking dashboard built with pure HTML, CSS, and JavaScript — no frameworks needed.

---

## ✨ Features

### Core
- **Dashboard Overview** — Summary cards for Balance, Income & Expenses with animated counters
- **Line Chart** — 6-month income vs expense trend (Chart.js)
- **Donut Chart** — Category spending breakdown with interactive hover tooltips
- **Transactions Table** — Full CRUD with search, filter by category/type, and column sorting
- **Insights Panel** — AI-style observations, savings rate progress bar, category breakdown bars
- **Settings Page** — Currency selector, data export, clear data

### Role-Based UI
| Feature | Admin | Viewer |
|---|---|---|
| View all data | ✅ | ✅ |
| Add transaction | ✅ | ❌ |
| Edit transaction | ✅ | ❌ |
| Delete transaction | ✅ | ❌ |
| Export data | ✅ | ✅ |

Role toggle is live in the sidebar — UI updates instantly.

### UX Extras
- 🔍 Real-time search + category/type filters
- ↕️ Sortable columns (click any header)
- 💾 localStorage persistence — data survives page refresh
- 📊 Animated progress bars and number counters
- 📱 Fully responsive (mobile sidebar drawer)
- 📦 Empty state handling
- ↓ CSV and JSON export

---

## 🎨 Design System

| Variable | Value | Usage |
|---|---|---|
| `--accent-1` | `#00e5ff` | Primary cyan — borders, focus, glow |
| `--accent-2` | `#7b61ff` | Purple — secondary actions, gradients |
| `--accent-3` | `#ff6b9d` | Pink/red — expenses |
| `--accent-4` | `#00ffa3` | Green — income, positive |
| `--bg-deep` | `#04050f` | Page background |
| `--glass-bg` | `rgba(255,255,255,0.04)` | Card backgrounds |

All cards use **glassmorphism**: `backdrop-filter: blur()`, translucent backgrounds, and subtle border glow on hover.

Typography: **Syne** (headings, numbers) + **DM Sans** (body text).

---

## 🛠 Tech Stack

- **HTML5 / CSS3 / Vanilla JS** — zero build step required
- **Chart.js 4.4** (CDN) — line + donut charts
- **Google Fonts** — Syne + DM Sans
- **localStorage** — client-side persistence

---

## 🚀 Setup

```bash
# Option 1: Just open the file
open finance-dashboard.html

# Option 2: Serve locally (avoids any CORS edge cases)
npx serve .
# or
python3 -m http.server 8080
```

No npm, no build tools, no dependencies to install.

---

## 🧠 State Management

State lives in a single plain JS object:

```js
let state = {
  transactions: [],   // all transaction records
  role: 'admin',      // 'admin' | 'viewer'
  currency: '₹',      // display currency symbol
  sortKey: 'date',    // active sort column
  sortDir: 'desc',    // 'asc' | 'desc'
  editId: null        // ID of transaction being edited
};
```

`saveState()` serializes to localStorage on every mutation.  
`loadState()` rehydrates on page load and seeds sample data if empty.  
`renderAll()` is a single top-level re-render that updates all components — cards, charts, tables, badges.

---

## 🔐 Role-Based UI

Roles are toggled in the sidebar footer. `setRole(role)` updates:

1. Button active states in the toggle
2. The role indicator badge
3. The Add Transaction button visibility
4. The Actions column in the transactions table (edit/delete buttons hidden for Viewer)

Role is persisted in `state.role` via localStorage so it survives refresh.

---

## 📁 Structure

Single-file architecture — everything in `finance-dashboard.html`:

```
finance-dashboard.html
├── <style>     — all CSS (CSS variables, glassmorphism, animations, responsive)
├── <body>      — sidebar, topbar, 4 sections, modal
└── <script>    — state, render functions, chart config, CRUD, export
```

Component responsibilities:
- `renderCards()` — summary stats with counter animation
- `renderCharts()` — Chart.js line + donut instances
- `renderTransactions()` — filtered/sorted table with inline edit/delete
- `renderInsights()` — AI banner, metric cards, progress bars
- `openModal() / saveTransaction()` — add/edit modal flow
- `exportCSV() / exportJSON()` — data export utilities

---

## 📸 Sections

| Section | Route (nav click) |
|---|---|
| Dashboard | Default view — cards, charts, recent transactions |
| Transactions | Full table with search/filter/sort/CRUD |
| Insights | AI observations, savings rate, category bars |
| Settings | Currency, export, data management |
