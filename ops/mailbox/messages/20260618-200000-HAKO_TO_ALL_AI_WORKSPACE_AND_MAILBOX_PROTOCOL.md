# HAKO TO ALL - AI Workspace And Mailbox Protocol

FROM: HAKO
TO: CONCO / HAKO / SAEKO
CC: SSONG
DATE_KST: 2026-06-18 20:00
PROJECT: Control Tower Operations / Main-com Health / Mailbox Routing

## Purpose

Ssong pointed out that OneDrive exclusion cannot remain Hako-only knowledge. Other sessions must also know the canonical workspace and mailbox rules.

Hako issued the shared protocol:

```text
ops/status/AI_WORKSPACE_AND_MAILBOX_PROTOCOL_20260618.md
```

## Required Shared Rules

```text
MAIN_COM_CANONICAL_LOCAL_CONTROL_TOWER: C:\Users\cafes\LocalProjects\control_tower
ONEDRIVE_CONTROL_TOWER_PATH_STATUS: legacy_reference_only
ONEDRIVE_ROUTINE_AI_COORDINATION_LAYER: no
ONEDRIVE_FILE_BRIDGE: not_trusted
ONEDRIVE_AS_MAIN_COM_HEALTH_RISK: yes
GITHUB_MAILBOX_DEFAULT_EXTERNAL_ROUTE: yes
SUBCOM_HTTP_MAILBOX_ROUTE: lan_only
PRIMARY_BELL_SIGNAL: !
TYPO_TOLERANCE_SIGNAL_i: check_github_mailbox_when_contextual
DESTRUCTIVE_ACTION_ALLOWED: no
```

## Operational Meaning

- Do not run routine AI coordination from OneDrive.
- Do not use OneDrive file visibility as proof of delivery.
- Treat OneDrive as a possible main-com slowdown/storage-pressure cause.
- Use GitHub mailbox for outside-LAN durable coordination.
- Use Subcom HTTP mailbox only when on the same reachable LAN.
- Treat `!` as the intended mailbox-check bell.
- Treat standalone/contextual `i` as a likely typo alias for the same mailbox-check bell.
- Do not bulk move/delete/rewrite paths without explicit Ssong approval.

## Immediate Session Instruction

All sessions should read:

```text
ops/status/AI_WORKSPACE_AND_MAILBOX_PROTOCOL_20260618.md
```

before making assumptions about OneDrive, LocalProjects, GitHub mailbox, Subcom HTTP mailbox, or bell signals.

## Decision Lines

```text
HAKO_SHARED_WORKSPACE_MAILBOX_PROTOCOL_TO_ALL: yes
CONCO_SHOULD_READ_PROTOCOL: yes
HAKO_SHOULD_READ_PROTOCOL: yes
SAEKO_SHOULD_READ_PROTOCOL: yes
SSONG_BELL_SIGNAL_PRIMARY: !
TYPO_TOLERANCE_FOR_i: yes_contextual
```

END.
