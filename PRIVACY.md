# Privacy Notice

**Last updated:** April 2026

## Summary

The SQL Security Sandbox is a **local-first, offline-capable** application. It does not collect, transmit, or store your data on any external server.

## What Data Is Stored

The application stores the following data **locally in your browser** using `localStorage`:

| Data | Purpose | Storage Location |
|------|---------|-----------------|
| Current lesson position | Resume where you left off | Browser localStorage |
| Lesson completion status | Track which lessons you've visited | Browser localStorage |
| Exercise attempt state | Remember which exercises you passed or revealed | Browser localStorage |
| Last session timestamp | Display "last played" in the welcome modal | Browser localStorage |

## What Data Is NOT Collected

- ❌ No personal information (name, email, IP address)
- ❌ No analytics or telemetry
- ❌ No cookies
- ❌ No network requests to any server
- ❌ No third-party scripts, trackers, or advertising

## Data Retention

All data is stored exclusively in your browser's localStorage. You can delete it at any time by:

1. Clicking the **"Reset Progress"** button in the application header
2. Clearing your browser's site data for this domain
3. Using your browser's developer tools to remove the `cic_sql_sandbox_progress_v1` key

## Data Export

You can export your progress data as a JSON file at any time using the **"Export"** button in the application header. This file is generated client-side and downloaded directly to your device — no server is involved.

## Service Worker

If you install the application as a PWA (Progressive Web App), a service worker caches the application files for offline use. The service worker does not collect or transmit any data.

## Children's Privacy

This application does not knowingly collect any personal information from anyone, including children under 13. Because no data is collected or transmitted, COPPA obligations are not triggered by the current design.

## Changes to This Notice

If data collection practices change in future versions (e.g., optional analytics or accounts), this notice will be updated and the changes will be clearly communicated.

## Contact

Christopher Smith — cjsmith605@gmail.com
