# ✦ SQL Security Sandbox

**Interactive SQL training for cybersecurity analysts — from `SELECT` to building a working impossible-travel detector.**

[![Deploy to GitHub Pages](https://github.com/cjsmith605/sql-security-sandbox/actions/workflows/deploy.yml/badge.svg)](https://github.com/cjsmith605/sql-security-sandbox/actions/workflows/deploy.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-00C9A7.svg)](LICENSE)
[![Phase](https://img.shields.io/badge/Phase-2%20Complete-00C9A7.svg)](#roadmap)
[![Live Demo](https://img.shields.io/badge/Live%20Demo-▶%20Launch-F0C040.svg)](https://cjsmith605.github.io/sql-security-sandbox/)

> 🔗 **[Launch the Sandbox →](https://cjsmith605.github.io/sql-security-sandbox/)**

---

## What Is This?

SQL Security Sandbox teaches SQL through a **realistic cybersecurity investigation narrative**. You play as a junior SOC analyst investigating suspicious authentication activity in your company's logs. Each lesson builds on the last, culminating in a working **impossible-travel detector** — a real technique used by security teams to catch compromised accounts.

Built as a **single-file, zero-dependency web application** — no server, no install, no login required. Download one file and open it in any browser.

---

## Key Features (Phase 2 — Current)

| Feature | Details |
|---------|---------|
| 🏠 **Interactive Dashboard** | XP level, streak, skill map per module, achievements grid, activity feed, framework coverage panel |
| ⚡ **XP & Achievement System** | Earn XP on every exercise pass; 10 unlockable badges (First Query, No Hints, Speed Runner, Threat Hunter, and more) |
| ▶ **Live SQL Execution** | Real SQLite engine (sql.js/WASM) runs your queries against a seeded security database — see actual results, not just pass/fail |
| 🛡 **NIST CSF Mapping** | Every lesson tagged to NIST Cybersecurity Framework objectives (DE, RS, ID functions) |
| 🎯 **MITRE ATT&CK Mapping** | Every lesson tagged to real MITRE techniques (T1078, T1110, T1550, and more) |
| 📱 **Responsive / PWA** | Collapsible sidebar on mobile; installable as an offline-capable Progressive Web App |
| ♿ **Accessible** | ARIA roles, keyboard navigation, skip link, `prefers-reduced-motion`, screen reader labels |
| 💾 **Progress Persistence** | Auto-saves to localStorage; separate "visited" vs "mastered" tracking; JSON export |

---

## The Training Database

When you click **▶ Run Query**, your SQL executes against a real in-memory SQLite database pre-seeded with realistic SOC data:

| Table | Rows | Description |
|-------|------|-------------|
| `auth_log` | 25 | Authentication events with login attempts, privilege escalations, failed logins |
| `users` | 8 | Employee accounts with department, role, and active/inactive status |
| `ip_watchlist` | 4 | Threat intelligence — HIGH/MEDIUM/LOW rated IPs with country and ISP data |
| `cloud_auth_log` | 8 | Cloud platform logins for UNION ALL cross-system exercises |

The data is deliberately designed to contain **real attack patterns** — brute force attempts, impossible travel, dormant accounts, and privilege escalation — so every query you write produces meaningful results.

---

## Curriculum

| Module | Topics | Lessons | Difficulty |
|--------|--------|---------|------------|
| **1: SQL Fundamentals** | SELECT, FROM, WHERE, AND/OR, LIKE, ORDER BY, LIMIT | 4 | 🟢 Beginner |
| **2: Multi-Table Queries** | INNER JOIN, LEFT JOIN, Aliases, Multiple JOINs | 4 | 🟡 Intermediate |
| **3: Security Analysis** | COUNT, GROUP BY, HAVING, Subqueries, EXISTS | 4 | 🟠 Advanced |
| **4: Advanced SQL** | DISTINCT, UNION, CASE WHEN, Date/Time Functions, CTEs, Window Functions | 5 | 🔴 Expert |

Each lesson includes:
- Narrative context (you're a SOC analyst on a live investigation)
- Syntax demonstrations with live-highlighted SQL code blocks
- Interactive exercises with instant feedback and hints
- **Live query execution** against the training database
- NIST CSF + MITRE ATT&CK framework alignment chips
- Full answer reveals with explanations

---

## Quick Start

**Option 1 — Use it online (no install):**
[cjsmith605.github.io/sql-security-sandbox](https://cjsmith605.github.io/sql-security-sandbox/)

**Option 2 — Run locally:**
```bash
git clone https://github.com/cjsmith605/sql-security-sandbox.git
cd sql-security-sandbox
open index.html       # macOS
start index.html      # Windows
xdg-open index.html   # Linux
```

**Option 3 — Install as PWA:**
Visit the live site in Chrome/Edge → click the install icon in the address bar → runs fully offline like a native app.

> No server. No login. No build step. Open the file and start hunting threats.

---

## Using the Dashboard

Click the **gold "⌂ Dashboard" button** at the top of the left sidebar to open your personal analytics view:

- **Overview cards** — lessons mastered, total XP, exercises passed, badges earned
- **Skill Map** — progress bars for each module with star ratings
- **Achievements** — 10 unlockable badges with XP bonuses
- **Framework Coverage** — all NIST CSF and MITRE ATT&CK objectives covered in this course
- **All Lessons grid** — jump to any lesson with mastery status visible at a glance

---

## Architecture

```
sql-security-sandbox/
├── index.html          # The entire application (single-file, ~360KB, zero dependencies)
├── manifest.json       # PWA web app manifest
├── sw.js               # Service worker (offline caching, cache-first strategy)
├── assets/             # PWA icons (192px, 512px)
├── AGENT_HANDOFF.md    # Cross-agent development context (Claude ↔ Perplexity)
├── LICENSE             # MIT License
├── SECURITY.md         # Security policy and vulnerability reporting
├── PRIVACY.md          # Privacy notice (100% local, zero data collection)
├── CONTRIBUTING.md     # Contribution guidelines
└── .github/
    └── workflows/
        └── deploy.yml  # CI: validate HTML + auto-deploy to GitHub Pages on push
```

### Design Principles

| Decision | Rationale |
|----------|-----------|
| **Single HTML file** | Maximum portability — one file, any browser, any device |
| **Vanilla JS only** | Zero supply-chain risk, no build step, instant load |
| **sql.js / SQLite WASM** | Real query execution with zero server infrastructure |
| **localStorage persistence** | Progress saves automatically, no account required |
| **Dark theme** | Matches SOC analyst aesthetic; reduces eye strain during training |
| **CSS custom properties** | Consistent theming, easy to white-label for enterprise customers |

---

## Security Framework Alignment

Every lesson is mapped to real cybersecurity frameworks — visible as chips under each lesson title.

### NIST CSF 2.0 Coverage

| Function | Controls Covered |
|----------|-----------------|
| **Identify (ID)** | ID.AM-5 (Asset Management) |
| **Detect (DE)** | DE.AE-1 through DE.AE-5, DE.CM-1, DE.CM-3, DE.CM-4, DE.CM-7, DE.CM-8 |
| **Respond (RS)** | RS.AN-1 through RS.AN-4, RS.MI-1 |

### MITRE ATT&CK Techniques Covered

`T1078` Valid Accounts · `T1110` Brute Force · `T1087` Account Discovery · `T1070.006` Timestomp · `T1550` Use Alternate Auth Material · `T1563` Remote Service Session Hijack · `T1078.004` Cloud Accounts · `T1136` Create Account · `T1098` Account Manipulation · `T1074` Data Staged · and more

---

## Roadmap

### ✅ Phase 1 — Complete
- Mobile responsive layout, hamburger sidebar
- ARIA/accessibility, WCAG labels
- Progress tracking (visited vs mastered)
- Export progress as JSON
- PWA + service worker (offline support)
- GitHub Actions CI/CD → GitHub Pages

### ✅ Phase 2 — Complete
- Interactive Dashboard with XP, skill map, achievements, activity feed
- 10-badge achievement system with XP bonuses
- Real SQL execution via sql.js (SQLite WASM), seeded training database
- NIST CSF 2.0 + MITRE ATT&CK mapping on all 17 lessons
- AGENT_HANDOFF.md for cross-AI-agent development continuity

### 🔲 Phase 3 — Planned
- PDF lab report export per lesson
- Completion certificate (cryptographically hashed, shareable)
- Payment gating (Stripe/Gumroad) for Modules 3–4
- SCORM packaging for enterprise LMS integration
- Marketing landing page

### 🔲 Phase 4 — Future
- Texas DIR certification for government training programs
- Open Badges 3.0 verifiable credentials
- Admin dashboard for enterprise deployments
- xAPI / Tin Can learning record store

---

## For Employers & Evaluators

This project was built to demonstrate:

- **SQL fluency** across all major query patterns used in real SOC work
- **Frontend engineering** — single-file architecture, vanilla JS, WASM integration
- **Security domain knowledge** — NIST CSF, MITRE ATT&CK, realistic threat scenarios
- **Software craftsmanship** — accessibility, PWA, CI/CD, documentation, cross-agent handoff docs
- **Product thinking** — gamification (XP/achievements), UX design, framework market positioning

---

## Author

**Christopher Smith** — [GitHub](https://github.com/cjsmith605)
Part of the **Cosmic Innovators Collective** — Building Digital Guardians.

Dallas-Fort Worth, Texas.

---

## License

[MIT](LICENSE) — free to use, modify, and distribute.
