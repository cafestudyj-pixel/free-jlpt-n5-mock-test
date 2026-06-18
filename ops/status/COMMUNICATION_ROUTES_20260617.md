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
   - Important: this is a durable record route, not a wake trigger by itself.

## Route Selection Rule

- If Conco is on the same LAN as Subcom: Subcom HTTP mailbox can be used.
- If Conco is outside the LAN: GitHub mailbox must be used.
- If Song must be urgently alerted: use Bluebot / Song-facing route.
- Do not use OneDrive-looking local paths as proof of cross-machine delivery.

## Wake / Bell Rule

GitHub mailbox does not wake Saeko by itself.

A Conco reply in GitHub becomes actionable for Saeko only when one of these is true:

1. Song leaves `!` or a direct wake message in Saeko's active thread.
2. Saeko is already awake and explicitly checks GitHub mailbox.
3. A scheduled/heartbeat wake explicitly includes GitHub mailbox check as its first routine.

Therefore:

- Do not say "Conco replied, so Saeko will see it" unless a wake source exists.
- Do not rely on GitHub INBOX updates as the only continuation mechanism for a live loop.
- If the next step depends on Conco's reply, the task handoff must state both:
  - where the reply should be written, and
  - how Saeko will be woken or when Saeko will check.

Reference post-it:
`ops/status/POSTIT_GITHUB_MAILBOX_IS_NOT_WAKE_TRIGGER_20260618.md`

## Current Public Site

Official current public site:
https://cafestudyj-pixel.github.io/free-jlpt-n5-mock-test/

Current deploy surface:
GitHub Pages from `cafestudyj-pixel/free-jlpt-n5-mock-test`.

Netlify is not the current active deployment route.

## Minimum GitHub Mailbox Write Procedure

1. Create a timestamped message under `ops/mailbox/messages/`.
2. Add or update the recipient inbox index, e.g. `ops/mailbox/conco/INBOX.md`.
3. Add or update the sender outbox index when available.
4. Keep message format human-readable and AI-readable.
5. Do not place secrets, tokens, private account details, or protected settings in public repo files.
6. If the recipient must act soon, provide a separate wake/bell route; mailbox write alone is not enough.

## Decision Lines

GITHUB_EXTERNAL_MAILBOX_ROUTE: active
SUBCOM_HTTP_MAILBOX_ROUTE: lan_only
ONEDRIVE_FILE_BRIDGE: not_trusted
CURRENT_PUBLIC_DEPLOY_ROUTE: github_pages
CONCO_OUTSIDE_LAN_ROUTE: github_mailbox
GITHUB_MAILBOX_IS_WAKE_TRIGGER: no
BELL_ROUTE_REQUIRED_FOR_ASYNC_REPLY: yes
