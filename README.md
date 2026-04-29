# ✦ SQL Security Sandbox

Interactive SQL training for cybersecurity analysts — from `SELECT` to building a working impossible-travel detector.

[![Deploy to GitHub Pages](https://github.com/cjsmith605/sql-security-sandbox/actions/workflows/deploy.yml/badge.svg)](https://github.com/cjsmith605/sql-security-sandbox/actions/workflows/deploy.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

**[Launch the Sandbox →](https://cjsmith605.github.io/sql-security-sandbox/)**

## The Problem

Cybersecurity analysts need SQL fluency to investigate incidents, hunt threats, and audit access — but most SQL courses teach with generic business data. There's no bridge between "learn SQL" and "use SQL to catch attackers."

## The Solution

SQL Security Sandbox teaches SQL through a **realistic cybersecurity investigation narrative**. You play as a junior SOC analyst investigating suspicious authentication activity in your company's logs. Each lesson builds on the last, culminating in a working **impossible-travel detector** that identifies compromised accounts logging in from distant locations within impossible timeframes.

## The Impact

- **35 lessons** across 7 progressive modules
- **60+ hands-on exercises** with hints, feedback, and full explanations
- **Zero dependencies** — one HTML file, no server, no install, no account
- **Offline-capable PWA** — install it and use it anywhere
- **WCAG-accessible** — keyboard navigation, screen reader support, reduced-motion support

## Quick Start

**Option 1 — Use it online:**
Visit [cjsmith605.github.io/sql-security-sandbox](https://cjsmith605.github.io/sql-security-sandbox/)

**Option 2 — Download and run locally:**
```bash
git clone https://github.com/cjsmith605/sql-security-sandbox.git
cd sql-security-sandbox
open index.html      # macOS
start index.html     # Windows
xdg-open index.html  # Linux
```

**Option 3 — Install as PWA:**
Visit the live site in Chrome/Edge → click the install icon in the address bar → runs offline like a native app.

No server. No login. No build step. Open the file and start hunting threats.

## Curriculum

| Module | Focus | Lessons | Difficulty |
|--------|-------|---------|------------|
| 1: SQL Fundamentals | SELECT, FROM, WHERE, ORDER BY, LIMIT | 3 | 🟢 Beginner |
| 2: Filtering & Aggregation | AND/OR, wildcards, GROUP BY, HAVING, COUNT/SUM/AVG | 5 | 🟡 Intermediate |
| 3: Joins & Subqueries | INNER JOIN, LEFT JOIN, subqueries, multi-table analysis | 5 | 🟠 Advanced |
| 4: Window Functions & CTEs | OVER(), LAG(), LEAD(), WITH, impossible-travel detection | 4 | 🔴 Expert |

Each lesson includes:
- Narrative context (you're investigating a real security incident)
- Syntax demonstrations with live-highlighted code blocks
- Interactive exercises with regex-based validation
- Hints, answer reveals, and detailed explanations

## Architecture

```
sql-security-sandbox/
├── index.html          # The entire application (single-file, zero-dependency)
├── manifest.json       # PWA web app manifest
├── sw.js               # Service worker for offline caching
├── assets/             # Icons and images
├── LICENSE             # MIT License
├── SECURITY.md         # Security policy and vulnerability reporting
├── PRIVACY.md          # Privacy notice (local-first, no data collection)
├── CONTRIBUTING.md     # Contribution guidelines
└── .github/
    └── workflows/
        └── deploy.yml  # CI: validate + auto-deploy to GitHub Pages
```

## Design Decisions

| Decision | Rationale |
|----------|-----------|
| Single HTML file | Maximum portability — download one file, open in any browser |
| Vanilla JS, no frameworks | Zero supply-chain risk, no build step, instant load |
| localStorage persistence | Progress saves automatically, no account required |
| Regex-based answer checker | Dependency-free validation that works offline |
| Dark theme | Matches the "terminal/SOC analyst" aesthetic; reduces eye strain |
| CSS custom properties | Consistent theming, easy to customize or white-label |

## Key Features

- **Live syntax-highlighted SQL editor** — token-based highlighter with keyword, function, string, number, and comment coloring
- **Responsive layout** — collapsible sidebar on mobile, optimized for phones, tablets, and desktops
- **Progress tracking** — separate "visited" vs "mastered" metrics; mastery requires passing all exercises
- **Progress export** — download your completion data as JSON for portfolio evidence
- **Welcome modal with resume** — returning users see their stats and can continue where they left off
- **PWA installable** — works offline with service worker caching
- **Accessibility** — skip link, ARIA roles, keyboard focus management, prefers-reduced-motion support, screen reader labels on all editors

## Security Framework Alignment

| Sandbox Module | NIST CSF 2.0 | SOC 2 Trust Principle |
|---------------|--------------|----------------------|
| Auth Log Analysis | Detect: Continuous Monitoring (DE.CM) | Security (Access Controls) |
| Filtering & Aggregation | Detect: Anomalies & Events (DE.AE) | Security (Threat Detection) |
| Multi-table Joins | Protect: Data Security (PR.DS) | Confidentiality (Data Isolation) |
| Impossible Travel Detection | Respond: Analysis (RS.AN) | Security (Incident Response) |

## Roadmap

- **Phase 2:** Real SQL execution engine (SQLite/WASM) for remaining modules
- **Phase 2:** PDF lab report export and completion certificates
- **Phase 3:** SCORM packaging for enterprise LMS integration
- **Phase 3:** Freemium model with gated content (Modules 3–4)
- **Phase 4:** Texas DIR certification for government training
- **Phase 4:** Open Badges 3.0 verifiable credentials

## Recording a Demo GIF

Haven't captured a demo yet? Here's how:

1. Open `index.html` in a browser, sized comfortably (1200px+ wide)
2. macOS: QuickTime Player → File → New Screen Recording → select the lesson area
3. Record ~10 seconds: type a query, click Submit, see the "Correct!" feedback
4. Export as `.mov`, convert to `.gif` with [ezgif.com](https://ezgif.com/video-to-gif)
5. Save as `assets/demo.gif` and add `![Demo](./assets/demo.gif)` to this README

For a static screenshot: `assets/screenshot.png` (used as the `og:image` meta tag).

## Author

Christopher Smith — [GitHub](https://github.com/cjsmith605)

Part of the [Cosmic Innovators Collective](https://github.com/cjsmith605) training initiative.  
Built in Dallas-Fort Worth, Texas. Designed for the next generation of security professionals.

## License

[MIT](./LICENSE) — free to use, modify, and distribute.
