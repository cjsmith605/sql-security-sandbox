# Agent Handoff — SQL Security Sandbox
> This file is the single source of truth for both Perplexity Computer and Claude when continuing work on this project.
> Update the "Current State" and "Last Session" sections after every work session.

---

## Project Identity
- **Name:** SQL Security Sandbox
- **Brand:** Cosmic Innovators Collective
- **Author:** Christopher Smith (`cjsmith605@gmail.com`, GitHub: `cjsmith605`)
- **Repo:** https://github.com/cjsmith605/sql-security-sandbox
- **Live Demo:** https://cjsmith605.github.io/sql-security-sandbox/
- **License:** MIT

---

## Architecture (Do Not Break These Principles)
- **Single HTML file** (`index.html`) — zero dependencies, zero build step, opens in any browser
- **Vanilla JS only** — no frameworks, no npm, no bundler. Keep it this way unless explicitly decided otherwise.
- **CSS custom properties** for all theming — defined in `:root`, colors: `--teal #00C9A7`, `--bg #0F1923`, `--gold #F0C040`, `--blue #2E74B5`
- **localStorage** for all persistence (key: `cic_sql_sandbox_progress_v1`)
- **sql.js** (SQLite WASM) lazy-loaded from CDN (`cdnjs.cloudflare.com/ajax/libs/sql.js/1.12.0/`). The shared DB (`sqlJsDb`) is seeded once at first use via `SQL_SEED` const. Tables: `auth_log`, `users`, `ip_watchlist`, `cloud_auth_log`. Do NOT call `db.run(SQL_SEED)` more than once — it uses `CREATE TABLE IF NOT EXISTS` but data inserts will duplicate if re-run.
- **Framework mapping** stored as `lesson.framework = { nist: [...], mitre: [...] }` on every lesson object. All 17 lessons are mapped. Render via `.fw-chip.fw-nist` (blue) and `.fw-chip.fw-mitre` (purple) chips.
- All user input MUST be escaped before `innerHTML` — the syntax highlighter already does this
- Service worker (`sw.js`) + manifest (`manifest.json`) = PWA offline support

---

## Current State (Update This Every Session)

### Last Updated
**April 12, 2026** — Session by Perplexity Computer (Phase 2 COMPLETE)

### Phase
**Phase 2 COMPLETE — fully deployed to main branch — ready for Phase 3**

### What's Implemented

#### Phase 1 (COMPLETE — deployed to main branch)
- [x] Mobile responsive layout (`@media 900px` collapsible sidebar, `@media 600px` compact)
- [x] Hamburger toggle button (`#sidebar-toggle`) + backdrop overlay (`#sidebar-backdrop`)
- [x] `prefers-reduced-motion` CSS block
- [x] `sr-only` class + `<label>` and `aria-describedby` on all SQL editors (WCAG fix)
- [x] `Content-Security-Policy` meta tag
- [x] `theme-color` meta tag (`#0F1923`)
- [x] PWA: `manifest.json` + `sw.js` (cache-first, offline)
- [x] PWA icons: `assets/icon-192.png`, `assets/icon-512.png`
- [x] **Mastered vs Visited tracking** — `mastered` Set (all exercises passed) vs `completed` Set (page visited)
- [x] `updateMasteredSet()` — recalculates mastered on every header update
- [x] **Export Progress button** — downloads `sql-security-sandbox-progress.json`
- [x] Dynamic copyright year (`new Date().getFullYear()`)
- [x] GitHub Actions CI/CD (`.github/workflows/deploy.yml`) — validate + auto-deploy to GitHub Pages
- [x] `LICENSE` (MIT), `SECURITY.md`, `PRIVACY.md`, `CONTRIBUTING.md`
- [x] Professional `README.md` with curriculum table, architecture, framework alignment, badges

#### Phase 2 (DASHBOARD COMPLETE — deployed to main)
- [x] `AGENT_HANDOFF.md` (this file)
- [x] **Interactive Dashboard** — home screen with 4 stats cards (Lessons Done, Mastered, Total XP, Badges), skill map bars per module, Next Lesson card, all-lessons grid, achievements grid, activity feed
- [x] **Achievement / Badge system** — 10 unlockable achievements (`first_query`, `first_pass`, `no_hints`, `module1`–`module4` completion, `speed_run`, `all_mastered`, `streak_3`)
- [x] **XP / Points system** — +25 XP per exercise passed, bonus XP per achievement, header XP chip, level display
- [x] **Sidebar "Home" button** — navigates to dashboard, clears lesson state
- [x] **`loadProgress()` patched** — restores `totalXP`, `unlockedAchievements` from localStorage on init
- [x] **`updateXPChip()` called on init** — XP display correct on page refresh
- [x] **Duplicate `goPage` patch resolved** — single merged patch handles both dashboard clear + closeSidebar
- [x] **sql.js real query execution** — lazy-loads sql-wasm from CDN on first "Run Query" click; shared SQLite DB seeded with 25-row `auth_log`, `users`, `ip_watchlist`, `cloud_auth_log`; result table renders below each exercise; errors shown cleanly; +5 XP per first run per exercise; `escHtml()` prevents XSS in rendered results
- [x] **MITRE ATT&CK + NIST CSF mapping labels** — all 17 lessons have `framework: { nist: [...], mitre: [...] }` property; blue chips render under each lesson title; purple MITRE chips render; sidebar shows color-coded dot indicators (blue=NIST, purple=MITRE); dashboard has "Framework Coverage" panel with grouped NIST functions and deduplicated MITRE technique chips
- [ ] PDF lab report export (Phase 3 candidate)
- [ ] Completion certificate (Phase 3 candidate)

---

## Data Model (localStorage)

Key: `cic_sql_sandbox_progress_v1`

```json
{
  "v": 1,
  "currentModule": 0,
  "currentLesson": 0,
  "currentPage": 0,
  "completed": ["0-0", "0-1"],
  "visitedPages": ["0-0-0", "0-0-1"],
  "exerciseState": {
    "ex-id-here": { "attempts": 2, "revealed": false, "passed": true }
  },
  "achievements": ["first_query", "module1_complete"],
  "xp": 250,
  "streak": 3,
  "lastSeenAt": 1713000000000,
  "welcomeSeen": true
}
```

---

## Lesson / Exercise Data Structure

```js
lessons[moduleIndex][lessonIndex] = {
  module: "Module N: Name",
  title: "Lesson Title — Subtitle",
  pages: [
    {
      sections: [
        { type: 'badge', cls: 'badge-intro', label: 'Introduction' },
        { type: 'html', content: `<h3>...</h3><p>...</p>` },
        { type: 'code', content: `<span class="kw">SELECT</span> ...` },
        { type: 'scenario', content: `<p>...</p>` },
        { type: 'protip', content: `<p>...</p>` },
        { type: 'ref', content: `<p>...</p>` },
        { type: 'table', headers: [...], rows: [[...], ...] },
        { type: 'divider' }
      ],
      exercises: [
        {
          id: 'unique-id',           // format: 'mNlNex1' e.g. 'm0l0ex1'
          label: 'Exercise 1',
          context: '<strong>Table:</strong> auth_log<br>...',
          question: 'Write a query that...',
          checks: [
            { regex: 'SELECT', hint: 'You need a SELECT statement' },
            { regex: 'FROM\\s+auth_log', hint: 'Query the auth_log table' }
          ],
          generalHint: 'Start with SELECT * FROM ...',
          correctMsg: 'Well done! ...',
          answer: '<div class="code-block">...</div><p>Explanation...</p>'
        }
      ]
    }
  ]
}
```

---

## Key Functions Reference

| Function | Purpose |
|----------|---------|
| `renderPage(mi, li, pi)` | Renders a lesson page into `#main-content` |
| `renderDashboard()` | Renders the home dashboard into `#main-content` |
| `goPage(mi, li, pi)` | Navigates to a lesson page |
| `goHome()` | Navigates to the dashboard |
| `submitAnswer(exId)` | Checks a regex-based answer, updates state |
| `showHint(exId)` | Shows targeted hint for current wrong answer |
| `revealAnswer(exId)` | Reveals full answer, disables submit |
| `saveProgress()` | Serializes state to localStorage |
| `loadProgress()` | Deserializes state from localStorage |
| `resetProgress()` | Clears all state and restarts |
| `exportProgress()` | Downloads progress as JSON |
| `updateMasteredSet()` | Recalculates which lessons have all exercises passed |
| `checkAchievements()` | Evaluates and unlocks achievement badges |
| `awardXP(amount)` | Adds XP to total and saves |
| `buildSidebar()` | Renders module/lesson nav in `#sidebar` |
| `toggleSidebar()` | Hamburger toggle for mobile |
| `closeSidebar()` | Closes mobile sidebar |
| `highlightSQL(text)` | Token-based SQL syntax highlighter |
| `setupEditor(id)` | Wires up dual textarea/pre editor |

---

## Module / Lesson Names Reference

```
Module 0 (index): SQL Fundamentals
  0-0: SELECT & FROM — Your First Query
  0-1: WHERE — Filtering the Noise
  0-2: ORDER BY & LIMIT — Sorting and Slicing
  0-3: Module 1 Challenge

Module 1: Multi-Table Queries
  1-0: INNER JOIN — Connecting Tables
  1-1: Filtering JOINed Data
  1-2: LEFT JOIN — Including Unmatched Rows
  1-3: Multi-Table Investigation

Module 2: Security Analysis
  2-0: GROUP BY & Aggregation — The Bird's-Eye View
  2-1: HAVING — Filtering Aggregates
  2-2: CASE WHEN — Conditional Logic
  2-3: Date & Time Functions

Module 3: Advanced SQL
  3-0: Subqueries — Queries Within Queries
  3-1: Window Functions — OVER()
  3-2: LAG() & LEAD() — Comparing Rows
  3-3: CTEs — WITH Clause
  3-4: Impossible Travel Detector (Capstone)
```

---

## NIST CSF / MITRE ATT&CK Mapping (To Be Labeled in Lessons)

| Lesson | NIST CSF 2.0 | MITRE ATT&CK |
|--------|-------------|--------------|
| 0-0: SELECT/FROM | GV.RR (Roles & Responsibilities) | T1078 Valid Accounts (detection) |
| 0-1: WHERE | DE.CM (Continuous Monitoring) | T1110 Brute Force (detection) |
| 0-2: ORDER BY/LIMIT | DE.AE (Anomalies & Events) | T1133 External Remote Services |
| 1-0: INNER JOIN | PR.DS (Data Security) | T1078 Valid Accounts |
| 1-1: Filtering JOINed | DE.CM | T1098 Account Manipulation |
| 2-0: GROUP BY | DE.AE | T1110.003 Password Spraying |
| 2-2: CASE WHEN | RS.AN (Analysis) | T1059 Command & Scripting |
| 3-4: Impossible Travel | DE.AE + RS.AN | T1078 Valid Accounts (impossible travel) |

---

## Phase Roadmap Summary

| Phase | Status | Key Deliverables |
|-------|--------|-----------------|
| 1 | ✅ DONE | Mobile, PWA, WCAG, mastered tracking, export, CI/CD, docs |
| 2 | 🟡 IN PROGRESS | Dashboard, achievements, XP, sql.js real execution, MITRE labels, PDF lab report |
| 3 | ⏳ PLANNED | Payment gating, SCORM, marketing page, white-label |
| 4 | ⏳ PLANNED | Texas DIR cert, xAPI, Open Badges, admin dashboard, Tauri desktop |

---

## Rules for Both Agents
1. **Always read this file first** before making changes
2. **Never remove Phase 1 features** — they are foundational
3. **Test mobile layout** at 360px, 768px, 1200px after any CSS changes
4. **Keep single-file architecture** — all app code stays in `index.html`
5. **Update this file** at the end of every session with current state
6. **Commit messages** format: `Phase N: Short description\n\n- bullet list of changes`
7. **XP values**: First query = 10 XP, each passed exercise = 25 XP, module complete = 100 XP bonus
8. **Achievement IDs** use snake_case, stored in `achievements[]` array in localStorage
