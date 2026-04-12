# Security Policy

## Supported Versions

| Version | Supported |
|---------|-----------|
| 1.x     | ✅ Current |

## Architecture Security Summary

The SQL Security Sandbox is a **zero-dependency, client-side-only** application:

- **No server backend** — all code executes in the user's browser
- **No network calls** — no fetch, XHR, or WebSocket connections
- **No third-party scripts** — no CDN dependencies, analytics, or tracking
- **localStorage only** — progress data never leaves the device
- **CSP enforced** — Content Security Policy meta tag restricts script/resource loading
- **XSS-safe editor** — SQL syntax highlighter escapes `<`, `>`, `&` before any innerHTML write

## Reporting a Vulnerability

If you discover a security vulnerability, please report it responsibly:

1. **Email:** cjsmith605@gmail.com
2. **Subject line:** `[SECURITY] SQL Security Sandbox — <brief description>`
3. **Include:** Steps to reproduce, impact assessment, and suggested fix if possible

Please do **not** open a public GitHub issue for security vulnerabilities.

I will acknowledge receipt within 48 hours and provide an estimated timeline for a fix.

## Scope

This policy covers the HTML application and any companion files (manifest.json, sw.js) in this repository. It does not cover third-party forks or derivative works.
