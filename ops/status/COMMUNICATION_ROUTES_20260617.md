# Communication Routes - 2026-06-17

Project: Free JLPT N5 Mock Test Series

## Current Route Decision

The project now uses two mailbox layers:

1. Subcom HTTP mailbox bridge
   - Base URL pattern: `http://<subcom-lan-ip>:18787`
   - Example when on same LAN: `http://192.168.45.197:18787`
   - Use only when sender/receiver are on the same reachable LAN.
   - Not reliable when Main-com / Conco is outside the local Wi-Fi.

2. GitHub external mailbox
   - Repository: `cafestudyj-pixel/free-jlpt-n5-mock-test`
   - Path: `ops/mailbox/`
   - Use when Conco / Main-com is outside the Subcom LAN.
   - Use for durable external reports, gate results, route status, and PL-relevant notices.

## Route Selection Rule

- If Conco is on the same LAN as Subcom: Subcom HTTP mailbox can be used.
- If Conco is outside the LAN: GitHub mailbox must be used.
- If Song must be urgently alerted: use Bluebot / Song-facing route.
- Do not use OneDrive-looking local paths as proof of cross-machine delivery.

## Current Public Site

Official current public site:
https://cafestudyj-pixel.github.io/free-jlpt-n5-mock-test/

Current deploy surface:
GitHub Pages from `cafestudyj-pixel/free-jlpt-n5-mock-test`.

Netlify is not the current active deployment route.

## Minimum GitHub Mailbox Write Procedure

1. Create a timestamped message under `ops/mailbox/messages/`.
2. Add or update the recipient inbox index, e.g. `ops/mailbox/conco/INBOX.md`.
3. Keep message format human-readable and AI-readable.
4. Do not place secrets, tokens, private account details, or protected settings in public repo files.

## Decision Lines

GITHUB_EXTERNAL_MAILBOX_ROUTE: active
SUBCOM_HTTP_MAILBOX_ROUTE: lan_only
ONEDRIVE_FILE_BRIDGE: not_trusted
CURRENT_PUBLIC_DEPLOY_ROUTE: github_pages
CONCO_OUTSIDE_LAN_ROUTE: github_mailbox
