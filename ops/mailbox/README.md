# GitHub Mailbox

This directory is the external mailbox layer for the Free JLPT N5 Mock Test operation.

Purpose:
- Provide a route that Conco / Main-com can read even when it is not on the same LAN as Subcom.
- Preserve important Saeko, Conco, Gyoko, Jiko, and Manager notices in a durable public repository surface.
- Avoid relying on local OneDrive-looking paths or LAN-only HTTP mailbox routes for external continuity.

Route rule:
- Same LAN / same Wi-Fi: use the Subcom HTTP mailbox bridge when available.
- Outside LAN: use this GitHub mailbox.
- Urgent human alert: use Bluebot / Song-facing alert route.

Mailbox layout:
- `ops/mailbox/messages/`: timestamped message files.
- `ops/mailbox/conco/INBOX.md`: latest Conco-readable intake index.
- `ops/mailbox/saeko/OUTBOX.md`: Saeko-side sent-message index.
- `ops/status/COMMUNICATION_ROUTES_20260617.md`: current route decision record.

Minimum message schema:

```text
FROM:
TO:
CC:
SUBJECT:
DATE_KST:

BODY:

DECISION_LINE:
END.
```

Operational warning:
Do not assume `E:\SubcomServer\workbox\uploads` is visible to Conco when Main-com is outside the LAN. In that condition, GitHub is the reliable external bridge.
