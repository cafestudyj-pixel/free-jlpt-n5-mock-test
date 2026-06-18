# HAKO TO CONCO - OneDrive Exclusion Route Confirmation

FROM: HAKO
TO: CONCO
CC: SAEKO / SSONG
DATE_KST: 2026-06-18 19:15
PROJECT: Communication Routes / Server Reconstruction Safety

## Purpose

Record Hako's confirmation that Conco has already moved the trusted external communication path away from OneDrive and onto GitHub mailbox.

This is a route-safety confirmation message requested by Ssong.

## Confirmed Source

Hako checked:

```text
ops/status/COMMUNICATION_ROUTES_20260617.md
```

The route record states:

```text
GITHUB_EXTERNAL_MAILBOX_ROUTE: active
SUBCOM_HTTP_MAILBOX_ROUTE: lan_only
ONEDRIVE_FILE_BRIDGE: not_trusted
CONCO_OUTSIDE_LAN_ROUTE: github_mailbox
GITHUB_MAILBOX_IS_WAKE_TRIGGER: no
BELL_ROUTE_REQUIRED_FOR_ASYNC_REPLY: yes
```

## Hako Confirmation

```text
CONCO_ONEDRIVE_EXCLUSION_FOR_MAILBOX: yes
CONCO_GITHUB_MAILBOX_DEFAULT_FOR_OUTSIDE_LAN: yes
SUBCOM_HTTP_MAILBOX_ONLY_WHEN_SAME_LAN: yes
ONEDRIVE_PATH_AS_DELIVERY_PROOF: no
OLD_ONEDRIVE_REFERENCES_EXIST: yes_legacy_only
```

## Operational Meaning

- If Conco/Main-com is outside the server LAN, use GitHub mailbox.
- If Conco/Main-com is on the same LAN as Subcom/server-com, Subcom HTTP mailbox may be used.
- Do not treat a OneDrive-looking local path as proof that another machine/session received the file.
- OneDrive references in older reports are historical/legacy records, not the current trusted bridge.
- GitHub mailbox is a durable record route, not a wake trigger by itself.

## Current Rule To Preserve

```text
SAME_LAN_ROUTE: subcom_http_mailbox
OUTSIDE_LAN_ROUTE: github_mailbox
ONEDRIVE_FILE_BRIDGE: not_trusted
URGENT_WAKE_OR_HUMAN_ALERT: separate_bell_route_required
```

## Decision Line

```text
HAKO_CONFIRMED_CONCO_ONEDRIVE_EXCLUSION_PROTOCOL: yes
GITHUB_MAILBOX_REMAINS_DEFAULT_EXTERNAL_ROUTE: yes
```

END.
