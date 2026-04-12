# SQL Security Sandbox — Interactive Cybersecurity SQL Training

> **Cosmic Innovators Collective** — Building Digital Guardians

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![GitHub Pages](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-success)](https://cjsmith605.github.io/sql-security-sandbox/)

---

## Try the Free Demo

**[Launch Demo →](https://cjsmith605.github.io/index/)**

The free demo includes **Module 1: SQL Fundamentals** — 4 fully interactive lessons with a live SQL query engine, XP tracking, and a module challenge. No sign-up required, runs entirely in your browser.

| What You Get (Demo) | What's in the Full Version |
|---|---|
| Module 1: SQL Fundamentals (4 lessons) | All 4 Modules, 17 Lessons |
| Live SQL query engine against training DB | Same — plus advanced multi-table DB |
| XP system + achievements | Full XP system, all 10 achievements |
| NIST & MITRE framework labels | Full framework coverage mapping |
| — | Module 2: Multi-Table Queries & JOINs |
| — | Module 3: Security Analysis & Incident Response |
| — | Module 4: Advanced SQL — Window Functions, CTEs |
| — | Capstone: Build an impossible-travel detector |
| — | Certificate of Completion |

---

## Get the Full Version

The complete SQL Security Sandbox includes **all 4 modules** (17 lessons), challenge labs, the full training database, and a certificate of completion.

**[Purchase on Gumroad →](https://gumroad.com)**

One-time purchase · Instant download · Lifetime updates

---

## What Is This?

The SQL Security Sandbox is an interactive, narrative-driven training program that teaches SQL through a real cybersecurity investigation. You play an analyst investigating suspicious login activity — starting with basic `SELECT` statements and progressing through JOINs, aggregation, window functions, CTEs, and ultimately building a working impossible-travel detector.

### Key Features

- **Zero-install, single-file app** — one HTML file, no server, no dependencies, runs offline
- **Live SQL engine** — sql.js (SQLite compiled to WASM) executes your queries against a realistic training database
- **Narrative-driven** — every lesson advances the investigation, not just isolated exercises
- **XP & achievements** — gamified progression with 10 unlockable achievements
- **NIST & MITRE mapping** — every lesson tagged with real framework controls (NIST CSF, MITRE ATT&CK)
- **Dashboard** — track progress, XP level, framework coverage, and next steps
- **PWA ready** — installable, works offline after first load

### Training Database

The sandbox includes a 4-table training database seeded automatically on first query:

| Table | Purpose | Records |
|---|---|---|
| `auth_log` | Authentication events (logins, failures, privilege changes) | 30 |
| `users` | Employee directory (department, role, status) | 20 |
| `ip_watchlist` | Threat intelligence — flagged IPs with risk tiers | 15 |
| `cloud_auth_log` | Multi-region cloud auth events for travel analysis | 20 |

---

## For Employers

This project demonstrates:

- **Cybersecurity knowledge** — NIST CSF, MITRE ATT&CK, SOC analyst workflows, incident response
- **SQL proficiency** — SELECT, JOINs, aggregation, window functions, CTEs, subqueries
- **Software engineering** — single-file architecture, vanilla JS, WASM integration, CSP configuration, PWA, localStorage persistence
- **Instructional design** — scaffolded curriculum, narrative engagement, gamified progression

---

## For Organizations

Looking to train your team? The SQL Security Sandbox can be deployed as an internal training tool with:

- SCORM/xAPI integration for your LMS
- Custom branding and database scenarios
- Admin dashboards and completion tracking
- Volume licensing

**Contact:** cjsmith605@gmail.com

---

## Technical Architecture

| Property | Detail |
|---|---|
| File | Single HTML file (`index.html` = public demo, full version sold via Gumroad) |
| JS | Vanilla JavaScript — no frameworks, no build step |
| SQL Engine | sql.js 1.12.0 (SQLite WASM) loaded from CDN |
| Persistence | `localStorage` (key: `cic_sql_sandbox_progress_v1`) |
| Theming | CSS custom properties — dark cybersecurity aesthetic |
| CSP | Configured for cdnjs.cloudflare.com (script-src, connect-src, worker-src) |
| PWA | Service worker + manifest for offline use |

---

## File Guide

| File | Description |
|---|---|
| `index.html` | **Free demo** — Module 1 only, with upgrade CTAs (public, GitHub Pages) |
| `sql-security-sandbox-FULL-VERSION.html` | **Full version** — all 4 modules, 17 lessons (sold via Gumroad, not in repo) |
| `AGENT_HANDOFF.md` | Development handoff file for AI agents (Perplexity Computer / Claude) |
| `README.md` | This file |
| `sw.js` | Service worker for PWA offline caching |
| `manifest.json` | PWA manifest |

---

## Roadmap

| Phase | Status | Scope |
|---|---|---|
| Phase 1 | ✅ Complete | GitHub-ready portfolio polish, SEO, PWA |
| Phase 2 | ✅ Complete | Dashboard, XP system, sql.js query engine, NIST/MITRE labels |
| Phase 3 | ⏳ Next | PDF lab reports, certificates, Gumroad payment integration, SCORM |
| Phase 4 | ⏳ Planned | Texas DIR cert, xAPI, Open Badges, admin dashboard, Teachable course |

---

## License

MIT — see [LICENSE](LICENSE)

**© 2026 Cosmic Innovators Collective**
