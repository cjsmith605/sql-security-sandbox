# Agent Handoff — SQL Security Sandbox
> This file is the single source of truth for both Perplexity Computer and Claude when continuing work on this project.
> **Read this file first. Update the "Current State" section at the end of every session.**

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
- **CSS custom properties** for all theming — defined in `:root`:
  - `--teal #00C9A7` · `--bg #0F1923` · `--gold #F0C040` · `--blue #2E74B5`
  - `--red #FF8080` · `--green #70E8A0` · `--purple #C09FE8`
- **localStorage** for all persistence (key: `cic_sql_sandbox_progress_v1`) — do NOT change this key
- **sql.js** (SQLite WASM) lazy-loaded from CDN (`cdnjs.cloudflare.com/ajax/libs/sql.js/1.12.0/`). Shared DB instance `sqlJsDb` seeded once at first use via `SQL_SEED` const. Tables: `auth_log`, `users`, `ip_watchlist`, `cloud_auth_log`. **Do NOT call `db.run(SQL_SEED)` more than once** — inserts will duplicate.
- **Framework mapping** stored as `lesson.framework = { nist: [...], mitre: [...] }` on every lesson object. All 17 lessons are mapped. Rendered via `.fw-chip.fw-nist` (blue) and `.fw-chip.fw-mitre` (purple) chips.
- All user input MUST be escaped before `innerHTML` — use `escHtml()`. The syntax highlighter also does this.
- Service worker (`sw.js`) + manifest (`manifest.json`) = PWA offline support.
- **CSP note:** The `Content-Security-Policy` meta tag has been expanded to allow sql.js WASM from cdnjs.cloudflare.com. Current directives:
  - `script-src 'self' 'unsafe-inline' 'unsafe-eval' https://cdnjs.cloudflare.com` — allows loading sql-wasm.min.js
  - `connect-src 'self' https://cdnjs.cloudflare.com` — allows fetching sql-wasm.wasm binary
  - `worker-src 'self' blob:` — allows sql.js to spawn its Web Worker via blob URL
  - The SRI `integrity` attribute was removed from the dynamic script tag (conflicts with CSP in some browsers)
  - If adding new external CDN resources, add them to `script-src` AND `connect-src` as needed

---

## Current State (Update This Every Session)

### Last Updated
**April 12, 2026** — Session by Perplexity Computer (Phase 2 COMPLETE + CSP bugfix + demo.html + Gumroad strategy)

### Phase
**Phase 2 FULLY COMPLETE ✅ — deployed to main branch — ready for Phase 3**

> Run Query is now fully working. CSP was blocking cdnjs.cloudflare.com; fixed in commit e3806d9.
> Free demo (demo.html) created with Module 1 only + Gumroad upgrade CTAs.

### Git Log (last 8 commits)
```
68a3c80  feat: add free demo (Module 1 only) with Gumroad upgrade CTA
768bec0  docs(handoff): update CSP fix note and Phase 2 status
e3806d9  fix(csp): allow cdnjs.cloudflare.com for sql.js WASM engine
c412891  docs(handoff): full Phase 2 session update to AGENT_HANDOFF.md
2cb4289  docs: update README to reflect Phase 2 complete
1f0e123  fix(ux): make Dashboard, Run Query, and framework chips unmissable
77b4bf7  feat(phase2): sql.js live query engine + NIST/MITRE framework labels
4c436d2  feat(phase2): complete interactive dashboard + XP/achievement system
```

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

#### Phase 2 (COMPLETE — deployed to main branch)
- [x] `AGENT_HANDOFF.md` (this file)
- [x] **Interactive Dashboard** — home screen with 4 stats cards (Lessons Mastered, Total XP/Level, Exercises Passed, Badges), skill map bars per module, Next Lesson card, Framework Coverage panel, achievements grid, activity feed, all-lessons grid
- [x] **Achievement / Badge system** — 10 unlockable achievements stored in localStorage:
  - `first_query` · `first_pass` · `no_hints` · `module1` · `module2` · `module3` · `module4` · `speed_run` · `all_mastered` · `streak_3`
- [x] **XP / Points system** — +25 XP per exercise passed, +5 XP per first live query run, bonus XP per achievement unlock, header XP chip updates live, level every 200 XP
- [x] **Sidebar "Home" button** — gold gradient pill button at top of sidebar, navigates to dashboard, clears lesson active state
- [x] **`loadProgress()` patched** — restores `totalXP`, `unlockedAchievements` from localStorage on page load
- [x] **`updateXPChip()` called on INIT** — XP display correct immediately after page refresh
- [x] **Duplicate `goPage` patch resolved** — single merged patch handles dashboard state clear + `closeSidebar()`
- [x] **sql.js real query execution** — lazy-loads `sql-wasm.min.js` from CDN on first "Run Query" click; shared SQLite DB seeded via `SQL_SEED`; result table renders below each exercise with column headers, row count, NULL display; SQL errors shown in red; `escHtml()` prevents XSS in rendered results
- [x] **MITRE ATT&CK + NIST CSF mapping** — all 17 lessons have `framework: { nist: [...], mitre: [...] }` property; chips render under each lesson title with shield/target emoji prefix; sidebar shows glowing colored dot indicators; dashboard "Framework Coverage" panel groups NIST by function and lists unique MITRE techniques
- [x] **"Exercises ahead" nudge** — orange banner on intro-only pages (no exercises) warns user that the next page has exercises and explains the Run Query button
- [x] **README fully rewritten** — reflects Phase 2 complete, training database docs, dashboard usage guide, "For Employers" section, correct roadmap

#### UX Fixes Applied This Session (commit `1f0e123`)
- **Dashboard button** redesigned — bold gold gradient pill (`#F0C040 → #E8A030`) with drop shadow; was invisible as plain teal text
- **Run Query button** redesigned — vivid orange gradient (`#FF8C00 → #E06000`) with white text and glow shadow; clearly distinct from Submit Answer (blue)
- **NIST/MITRE chips** redesigned — larger padding (3px→5px), brighter colors, glowing borders, section label "Framework Alignment", emoji prefixes (🛡/🎯)
- **Sidebar fw-dots** — glow effect added to blue (NIST) and purple (MITRE) dots

#### Still Deferred (Phase 3+)
- [ ] PDF lab report export per lesson
- [ ] Completion certificate (cryptographically hashed, shareable)
- [ ] Gumroad product page setup and payment integration
- [ ] SCORM packaging for enterprise LMS
- [ ] Marketing landing page
- [ ] demo.gif / og:image screenshot (needs screen recording software)
- [ ] Color contrast WCAG audit

---

## Demo & Monetization Strategy

### File Structure
| File | Version | Content |
|---|---|---|
| `index.html` | **FULL VERSION** (paid) | All 4 modules, 17 lessons, complete training DB |
| `demo.html` | **FREE DEMO** | Module 1 only (4 lessons), upgrade CTAs throughout |

Both files have clear version headers in the HTML comment block at the top for easy identification.

### Demo Details (`demo.html`)
- **Module 1: SQL Fundamentals** — fully playable (all 4 lessons, all exercises, Run Query works)
- Modules 2–4 are **completely removed** (not locked/hidden — absent from the code)
- `moduleNames`, `lessonNames`, `lessonDifficulty` arrays trimmed to Module 1 only
- **Sidebar CTA** — orange "Unlock All 4 Modules" pill below the subtitle
- **Dashboard CTA** — gold-bordered upgrade banner above the footer
- **Upgrade modal** — `showUpgradeModal()` function, lists all locked content + Gumroad link
- **Welcome overlay** — labeled "(FREE DEMO)" in orange
- **Title/OG tags** — updated to say "FREE DEMO | Module 1"

### Sales Platform
- **Gumroad** (primary) — one-time purchase, instant download, lifetime updates
- Gumroad product page needs to be created (Phase 3)
- Placeholder link `https://gumroad.com` used in demo CTAs — **update to real product URL when created**
- **Teachable** (future/Phase 4) — for full course with video content

### GitHub Pages
- **Demo URL:** `https://cjsmith605.github.io/sql-security-sandbox/demo.html`
- **Full version URL:** `https://cjsmith605.github.io/sql-security-sandbox/` (index.html — keep public for now as portfolio piece; move behind Gumroad in Phase 3)
- README links to demo.html as the primary public link

### Pricing (TBD — Phase 3 Decision)
- Suggested range: $29–$49 for individual
- Enterprise/volume licensing via direct contact

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
  "achievements": ["first_query", "module1"],
  "xp": 250,
  "streak": 3,
  "lastSeenAt": 1713000000000,
  "savedAt": 1713000000000,
  "welcomeSeen": true
}
```

**XP Values:**
- Exercise passed (first time) = +25 XP
- First live query run per exercise = +5 XP
- Achievement `first_query` = +10 XP bonus
- Achievement `first_pass` = +25 XP bonus
- Achievement `no_hints` = +75 XP bonus
- Achievement `module1`–`module4` = +100 / +150 / +200 / +300 XP bonus
- Achievement `speed_run` = +100 XP bonus
- Achievement `all_mastered` = +500 XP bonus
- Achievement `streak_3` = +50 XP bonus
- **Level threshold:** `XP_PER_LEVEL = 200`

---

## Lesson / Exercise Data Structure

```js
lessons[moduleIndex][lessonIndex] = {
  module: "Module N: Name",
  title: "Lesson Title — Subtitle",
  framework: {
    nist: ['DE.AE-1', 'DE.CM-7'],           // NIST CSF 2.0 objective codes
    mitre: ['T1078 • Valid Accounts']        // MITRE ATT&CK technique IDs + names
  },
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
          id: 'ex-0-0-a',           // format: 'ex-{module}-{lesson}-{letter}'
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

## Training Database (sql.js Seed Data)

Seeded via `SQL_SEED` const, runs once on first "Run Query" click.

| Table | Rows | Key Columns |
|-------|------|-------------|
| `auth_log` | 25 | `log_id, username, event_time, source_ip, action, result` |
| `users` | 8 | `user_id, username, full_name, department, role, account_status` |
| `ip_watchlist` | 4 | `id, ip_address, threat_level, country, isp, added_date` |
| `cloud_auth_log` | 8 | `log_id, username, event_time, source_ip, action, result` |

**Notable data patterns** (intentionally designed for exercises):
- `admin_backup` has 5 failed logins followed by a success + PRIV_CHANGE (brute force pattern)
- `jdoe` logs in from `10.0.1.5` then later from `198.51.100.7` within the same day (impossible travel)
- `kpatel` logs in from internal IP then from threat IP `203.0.113.45` within minutes (compromise)
- `tdavis` and `ghost_user` exist in `users` but have no `auth_log` rows (dormant accounts — LEFT JOIN exercises)
- `203.0.113.45` and `203.0.113.99` appear in both `auth_log` and `ip_watchlist` as HIGH threat IPs

---

## Key Functions Reference

| Function | Purpose |
|----------|---------|
| `renderPage(mi, li, pi)` | Renders a lesson page into `#main-content` |
| `renderDashboard()` | Renders the home dashboard into `#main-content` |
| `renderExercise(ex)` | Returns HTML string for a single exercise box |
| `renderSection(s)` | Returns HTML string for a content section |
| `goPage(mi, li, pi)` | Navigates to a lesson page (patched: clears dashboard + closeSidebar) |
| `goHome()` | Navigates to the dashboard |
| `submitAnswer(exId)` | Checks regex answer, awards XP on first pass, updates state |
| `runQuery(exId)` | Executes user SQL via sql.js, renders result table, awards +5 XP first run |
| `initSqlJs(cb)` | Lazy-loads sql.js WASM from CDN, seeds DB, fires callback |
| `escHtml(str)` | XSS-safe HTML escaping for result table rendering |
| `showHint(exId)` | Shows targeted hint for current wrong answer |
| `revealAnswer(exId)` | Reveals full answer, disables submit |
| `saveProgress()` | Serializes full state to localStorage |
| `loadProgress()` | Deserializes state from localStorage (restores XP + achievements) |
| `resetProgress()` | Clears all state and restarts |
| `exportProgress()` | Downloads progress as JSON file |
| `updateMasteredSet()` | Recalculates which lessons have all exercises passed |
| `checkAchievements()` | Evaluates and unlocks achievement badges |
| `awardXP(amount, reason)` | Adds XP, calls updateXPChip(), shows toast, saves |
| `showToast(icon, title, body, isError)` | Shows animated toast notification |
| `getStreak()` | Reads streak from localStorage |
| `updateXPChip()` | Updates header XP display |
| `buildSidebar()` | Renders module/lesson nav + Home button in `#sidebar` |
| `updateSidebar(mi, li)` | Sets active state on sidebar buttons |
| `toggleSidebar()` | Hamburger toggle for mobile |
| `closeSidebar()` | Closes mobile sidebar |
| `highlightSQL(text)` | Token-based SQL syntax highlighter |
| `setupEditor(id)` | Wires up dual textarea/pre editor for a given exercise |
| `updateHeaderProgress()` | Updates the header progress counter and mastered count |

---

## Module / Lesson Names (Exact as in `lessons` array)

```
Module 0 (index 0): "Module 1: SQL Fundamentals"
  0-0: SELECT & FROM — Your First Query
  0-1: WHERE — Filtering Your Results
  0-2: ORDER BY & LIMIT — Sorting & Controlling Output
  0-3: ⚔️ Module Challenge — Incident First Response

Module 1 (index 1): "Module 2: Multi-Table Queries"
  1-0: INNER JOIN — Connecting Related Tables
  1-1: LEFT JOIN — Finding Missing Matches
  1-2: Aliases & Multiple JOINs — Power Queries
  1-3: ⚔️ Module Challenge — Cross-System Correlation

Module 2 (index 2): "Module 3: Security Analysis"
  2-0: COUNT & GROUP BY — Summarizing Data
  2-1: HAVING — Filtering Grouped Results
  2-2: Subqueries — Queries Inside Queries
  2-3: ⚔️ Module Challenge — Threat Intelligence Report

Module 3 (index 3): "Module 4: Advanced SQL"
  3-0: DISTINCT, UNION & CASE WHEN — Shaping Your Data
  3-1: Date/Time & String Functions — Parsing Real Logs
  3-2: CTEs (WITH Clauses) — Multi-Step Queries Made Readable
  3-3: Window Functions — SQL's Crown Jewel
  3-4: ⚔️ Module Challenge — Impossible Travel Detection
```

> **Note:** Array indices are 0-based. `lessons[0][0]` = Module 1 Lesson 1. The `module` property string says "Module 1" etc. but the array index is 0. Don't confuse display name vs array index.

---

## NIST CSF + MITRE ATT&CK Mapping (All 17 Lessons)

| Lesson | NIST CSF | MITRE ATT&CK |
|--------|----------|--------------|
| 0-0 SELECT & FROM | DE.AE-1, DE.CM-7 | T1078, T1133 |
| 0-1 WHERE | DE.AE-3, DE.CM-1 | T1110, T1087 |
| 0-2 ORDER BY & LIMIT | DE.AE-2, RS.AN-1 | T1071, T1499 |
| 0-3 Module 1 Challenge | RS.AN-1, RS.AN-2, DE.AE-3 | T1110, T1078 |
| 1-0 INNER JOIN | DE.CM-3, ID.AM-5 | T1078, T1136 |
| 1-1 LEFT JOIN | ID.AM-5, DE.AE-1 | T1078.001, T1098 |
| 1-2 Multiple JOINs | DE.CM-7, RS.AN-3 | T1518, T1046 |
| 1-3 Module 2 Challenge | DE.AE-4, RS.AN-2, RS.AN-3 | T1071, T1078 |
| 2-0 COUNT & GROUP BY | DE.AE-4, DE.CM-8 | T1110.003, T1589 |
| 2-1 HAVING | DE.AE-4, RS.AN-1 | T1110.001, T1595 |
| 2-2 Subqueries | DE.AE-2, DE.CM-4 | T1190, T1059 |
| 2-3 Module 3 Challenge | RS.AN-2, RS.MI-1, ID.RA-3 | T1595.002, T1588 |
| 3-0 DISTINCT/UNION/CASE | DE.AE-5, RS.AN-4 | T1074, T1020 |
| 3-1 Date/Time Functions | DE.CM-7, DE.AE-3 | T1070.006, T1562 |
| 3-2 CTEs | DE.AE-2, RS.AN-3 | T1078.002, T1021 |
| 3-3 Window Functions | DE.AE-4, RS.AN-2 | T1550, T1563 |
| 3-4 Module 4 Challenge | DE.AE-2, RS.AN-2, RS.AN-4 | T1078.004, T1550.001 |

---

## Phase Roadmap

| Phase | Status | Key Deliverables |
|-------|--------|-----------------|
| 1 | ✅ COMPLETE | Mobile, PWA, WCAG, mastered tracking, export, CI/CD, docs |
| 2 | ✅ COMPLETE | Dashboard, XP/achievements, sql.js real execution, NIST/MITRE labels, UX polish, README rewrite |
| 3 | ⏳ PLANNED | PDF lab reports, completion certificates, payment gating, SCORM, marketing page |
| 4 | ⏳ PLANNED | Texas DIR cert, xAPI/Tin Can, Open Badges 3.0, admin dashboard, Tauri desktop |

---

## Rules for Both Agents

1. **Always read this file first** before making any changes to the project
2. **Never remove Phase 1 or Phase 2 features** — they are live and deployed
3. **Keep single-file architecture** — all app code stays in `index.html`
4. **Test JS syntax** with `node --check` after any script edits
5. **Test mobile layout** at 360px, 768px, 1200px after any CSS changes
6. **No duplicate `const` declarations** — check for existing patches before adding new ones (goPage has already been patched once; don't add a second patch)
7. **Update this file** at the end of every session with git log, current state, and any new architecture notes
8. **Commit message format:** `type(scope): short description\n\n- bullet list`
9. **Always run `git push origin main`** after committing — GitHub Actions auto-deploys to Pages
10. **CSP is restrictive** — new external resources need dynamic `<script>` injection, not `fetch()`
11. **sql.js CDN integrity hash** — the `<script>` tag that loads sql-wasm uses an `integrity` attribute; if upgrading sql.js version, update the hash too
12. **localStorage key** `cic_sql_sandbox_progress_v1` — never change this or all user progress is lost

---

## Files in Repo

| File | Purpose |
|------|---------|
| `index.html` | Entire application (~360KB, 4800+ lines) |
| `manifest.json` | PWA manifest |
| `sw.js` | Service worker (offline cache-first) |
| `assets/icon-192.png` | PWA icon |
| `assets/icon-512.png` | PWA icon |
| `AGENT_HANDOFF.md` | This file |
| `README.md` | Public-facing project documentation |
| `LICENSE` | MIT License |
| `SECURITY.md` | Vulnerability reporting policy |
| `PRIVACY.md` | Privacy notice (local-first, no tracking) |
| `CONTRIBUTING.md` | Contribution guidelines |
| `.github/workflows/deploy.yml` | CI/CD — validates HTML, deploys to GitHub Pages on push to main |
