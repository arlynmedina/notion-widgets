# ☕ Cozy Book Cafe & Reading Tracker — Notion Template

Palette to match your reading widget: cream `#FDFBF7`, sage `#8A9A86`, latte `#A38560`.
In Notion terms that maps to **default/cream page**, **green** accents (sage) and **brown** accents (latte).

---

## 1. Homepage layout

Page name: **☕ The Book Cafe** · Cover: a wide cozy photo (see section 4) · Icon: ☕ or a cropped latte photo · Turn on **Full width** and **Small text**.

```
┌──────────────────────────────────────────────────────────────┐
│ COVER IMAGE (coffee + book, warm light)                      │
├──────────────────────────────────────────────────────────────┤
│ ☕ The Book Cafe                                              │
│ > Quote callout (brown background): "Today's quote" …        │
├──────────────────────────────────────────────────────────────┤
│ ── divider ──                                                │
├───────────────────────────┬──────────────────────────────────┤
│ COLUMN A (≈60%)           │ COLUMN B (≈40%)                  │
│ ### 🕯️ Reading Session    │ ### 🎯 This Week                 │
│ /embed  → reading timer   │ Linked view: Weekly Goals        │
│ (height ≈ 420–480px)      │  (List/Gallery, filter: This     │
│                           │   week, shows ring/bar meters)   │
│ ### 📖 Currently Reading  │ ### 🌿 Quick Links               │
│ Linked view: My Library   │  → My Library                    │
│  Gallery, filter          │  → Reading Log                   │
│  Status = Reading,        │  → Quote Jar                     │
│  card shows Cover +       │  → Wishlist / TBR                │
│  Progress Bar             │                                  │
├───────────────────────────┴──────────────────────────────────┤
│ ### 💬 Favorite Quotes                                        │
│ 3 columns × callout blocks (alternate green_bg / brown_bg)   │
│  > "quote" — Book, Author                                    │
├──────────────────────────────────────────────────────────────┤
│ ### 📚 Up Next (TBR)          │ ### ✨ Recently Finished      │
│ Linked view: Status = TBR,    │ Linked view: Status =         │
│ sort Priority, limit 5        │ Finished, sort Date Finished  │
│                               │ desc, limit 4, show ⭐ rating │
├──────────────────────────────────────────────────────────────┤
│ Toggle: 🗂️ Databases (My Library, Reading Log, Weekly Goals,  │
│ Quote Jar — full pages kept here, out of sight)              │
└──────────────────────────────────────────────────────────────┘
```

Build order:
1. Type `/callout` under the title for the "Today's quote" banner. Set its color to **Brown background** and the icon to 🍂 or ☕.
2. Type `/columns` → 2 columns. Drag the divider to roughly 60/40.
3. **Column A:** add a `### 🕯️ Reading Session` heading, then type `/embed` and paste the published URL of your reading widget (the Pomodoro timer + pages counter). Drag the bottom handle to about 450px so the whole timer shows with no scrollbar.
4. Below it, add `/linked view of database` → **My Library** → Gallery, filter `Status is Reading`, card preview = Cover, visible properties = Author, Progress Bar.
5. **Column B:** add `/linked view` → **Weekly Goals** (schema below) as a List or Gallery, filter `Week Start is This week`, with Pages Meter, Minutes Meter and Books Meter visible. These are the goal meters.
6. **Favorite Quotes:** `/columns` → 3, with one `/callout` per column. Alternate **Green background** (sage) and **Brown background** (latte). You can also make this a linked Gallery of a **Quote Jar** database filtered to `Favorite is checked`.
7. Bottom row: two more columns of linked views (TBR and Recently Finished). Then put a `/toggle` at the very end and keep the full source databases inside it.

---

## 2. Database schemas

### 📚 My Library (main database)

| Property | Type | Options / notes |
|---|---|---|
| **Book Title** | Title | |
| **Author** | Text | (or Relation → an Authors db if you want author pages) |
| **Cover** | Files & media | Upload or paste a cover URL. Set the gallery card preview to this |
| **Genre** | Multi-select | Fantasy, Romance, Literary Fiction, Mystery, Thriller, Sci-Fi, Non-Fiction, Self-Help, Memoir, Classics, Poetry, Cozy Mystery |
| **Format** | Select | Audiobook, Kindle, Physical |
| **Status** | Status | **To-do:** TBR · **In progress:** Reading · **Complete:** Finished, DNF |
| **Star Rating** | Select | ⭐, ⭐⭐, ⭐⭐⭐, ⭐⭐⭐⭐, ⭐⭐⭐⭐⭐ |
| **Current Page** | Number | For audiobooks, put minutes listened here |
| **Total Pages** | Number | For audiobooks, put total runtime in minutes here |
| **Progress Bar** | Formula | See section 3 |
| **Progress %** | Formula | Numeric version, shown as **Bar** or **Ring** |
| **Date Started** | Date | |
| **Date Finished** | Date | |
| **Days to Read** | Formula | `if(empty(prop("Date Finished")), "", format(dateBetween(prop("Date Finished"), prop("Date Started"), "days")) + " days")` |
| **Priority** | Select | 🔥 Next up, 🌿 Soon, ☁️ Someday (handy for TBR sorting) |
| **Owned / Source** | Select | Owned, Library, Kindle Unlimited, Libby, Borrowed |
| **Favorite** | Checkbox | |
| **Reading Log** | Relation | → Reading Log (two-way) |
| **Pages Logged** | Rollup | Reading Log → Pages Read → Sum |
| **Quotes** | Relation | → Quote Jar (two-way) |
| **Review / Notes** | Text | Longer reviews go in the page body |

Suggested views: **📖 Reading** (Gallery), **📚 Shelf** (Gallery of all books, grouped by Status), **🗓️ TBR** (Board by Priority), **✨ Finished** (Table, sorted by Date Finished), **📊 Stats** (Chart view: books finished per month, or Genre breakdown).

### 📝 Reading Log (one row per session; this feeds the weekly meters)

| Property | Type | Notes |
|---|---|---|
| **Session** | Title | e.g. "Evening read" |
| **Date** | Date | Default today |
| **Book** | Relation | → My Library |
| **Pages Read** | Number | Copy it from the widget's pages counter |
| **Minutes** | Number | Pomodoros × your session length |
| **Week** | Relation | → Weekly Goals |
| **Mood** | Select | ☕ Cozy, 🌧️ Rainy day, 🌙 Late night, ☀️ Morning |

### 🎯 Weekly Goals (one row per week)

| Property | Type | Notes |
|---|---|---|
| **Week** | Title | e.g. "Oct 13 – Oct 19" |
| **Week Start** | Date | Monday of that week |
| **Sessions** | Relation | → Reading Log |
| **Pages Goal** | Number | e.g. 300 |
| **Minutes Goal** | Number | e.g. 300 |
| **Books Goal** | Number | e.g. 1 |
| **Books Finished** | Relation | → My Library (link any book finished that week) |
| **Pages Meter** | Formula | `if(prop("Pages Goal") > 0, min(prop("Sessions").map(current.prop("Pages Read")).sum() / prop("Pages Goal"), 1), 0)` → **Number format: Percent, Show as: Ring, Color: Green** |
| **Minutes Meter** | Formula | `if(prop("Minutes Goal") > 0, min(prop("Sessions").map(current.prop("Minutes")).sum() / prop("Minutes Goal"), 1), 0)` → **Percent, Bar, Brown** |
| **Books Meter** | Formula | `if(prop("Books Goal") > 0, min(prop("Books Finished").length() / prop("Books Goal"), 1), 0)` → **Percent, Ring, Green** |

To get the rings and bars, open each formula property's settings, set **Number format** to Percent, then pick **Show as → Ring** (or Bar), set **Divide by** to 1, and choose a color.

### 💬 Quote Jar (optional, powers the quote callouts)

| Property | Type |
|---|---|
| **Quote** | Title |
| **Book** | Relation → My Library |
| **Page** | Number |
| **Favorite** | Checkbox |
| **Vibe** | Select (Comforting, Heartbreaking, Funny, Wise) |

---

## 3. Progress bar formulas (Notion Formulas 2.0)

These need **Current Page** and **Total Pages** as Number properties and **Status** as a Status property.

### A. Text bar — `■■■■■■□□□□ 60%`

Paste this into the **Progress Bar** formula property:

```
lets(
  total, prop("Total Pages"),
  current, if(empty(prop("Current Page")), 0, prop("Current Page")),
  pct, if(prop("Status") == "Finished", 1,
         if(empty(total) or total <= 0, 0, min(max(current / total, 0), 1))),
  filled, round(pct * 10),
  repeat("■", filled) + repeat("□", 10 - filled) + " " + format(round(pct * 100)) + "%"
)
```

What it does:
- It shows 10 blocks, so each block is 10%. For a 5-block bar like `■■■□□`, change both `10`s to `5`.
- It caps at 100% and never goes negative, and it shows `□□□□□□□□□□ 0%` when Total Pages is empty.
- Marking a book **Finished** always fills the bar, even if you never updated the page number.

### B. Aesthetic colored version (sage blocks, latte percentage)

```
lets(
  total, prop("Total Pages"),
  current, if(empty(prop("Current Page")), 0, prop("Current Page")),
  pct, if(prop("Status") == "Finished", 1,
         if(empty(total) or total <= 0, 0, min(max(current / total, 0), 1))),
  filled, round(pct * 10),
  style(repeat("■", filled), "green") +
  style(repeat("□", 10 - filled), "gray") +
  "  " + style(format(round(pct * 100)) + "%", "b", "brown")
)
```

Other block styles you can swap in for `■` / `□`:
- `●` / `○` → ●●●●●●○○○○ 60%
- `▰` / `▱` → ▰▰▰▰▰▰▱▱▱▱ 60%
- `🟫` / `⬜` → a chunky latte-colored bar
- `☕` / `·` → ☕☕☕☕☕☕····

### C. Numeric version (for Notion's built-in bar or ring)

**Progress %** formula:

```
if(prop("Status") == "Finished", 1,
  if(empty(prop("Total Pages")) or prop("Total Pages") <= 0, 0,
    min(prop("Current Page") / prop("Total Pages"), 1)))
```

Then set **Number format: Percent → Show as: Bar → Color: Green**. Use this one on gallery cards, and the text bar (A or B) in tables.

### D. Pages left (bonus)

```
if(prop("Status") == "Finished" or empty(prop("Total Pages")), "",
  format(prop("Total Pages") - prop("Current Page")) + " pages to go 🍂")
```

---

## 4. Unsplash keywords for covers and icons

These are the three searches that best fit a soft, cozy, autumn café mood. Each pairs with your cream, sage and latte palette.

1. **"coffee and book"**: open pages beside a latte on a wooden table or linen, in warm light. Use it on the **homepage cover**. Lean toward the lighter, beige-toned results.
2. **"cozy reading nook"**: a window seat, knit blankets, rainy glass, candlelight. Use it for the **My Library** and **Reading Log** covers.
3. **"dried flowers neutral"** (also try "eucalyptus linen"): soft sage greens and cream textures. These work for **Weekly Goals / Quote Jar** covers, and cropped square, they make good **page icons**.

For icons, square crops work best: search **"latte art top view"** for the homepage, **"stack of books minimal"** for My Library, and **"pressed leaf"** for the Quote Jar. If you'd rather keep it simple, use emoji icons: ☕ 📚 🕯️ 🍂 🌿 📝.

Tip: set every cover's **Reposition** so the main object sits in the lower third. Notion's page title overlaps the bottom edge of the cover, so the center of the image is what people see.
