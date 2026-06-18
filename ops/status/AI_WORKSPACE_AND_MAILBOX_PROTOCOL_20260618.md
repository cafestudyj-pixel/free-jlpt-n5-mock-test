# AI Workspace And Mailbox Protocol - 2026-06-18

FROM: HAKO
TO: CONCO / HAKO / SAEKO / SSONG
DATE_KST: 2026-06-18
STATUS: canonical operations protocol

## Purpose

This protocol prevents future sessions from treating OneDrive as the routine AI workspace or mailbox bridge.

The reason is not convenience only. OneDrive is now classified as both:

1. an unreliable cross-session delivery proof, and
2. a main-com performance/storage pressure risk source.

## Canonical Local Workspace

```text
MAIN_COM_CANONICAL_LOCAL_CONTROL_TOWER: C:\Users\cafes\LocalProjects\control_tower
ONEDRIVE_CONTROL_TOWER_PATH_STATUS: legacy_reference_only
LOCALPROJECTS_PATH_READY_FOR_CANONICAL_USE: yes
MIGRATION_RISK_LEVEL: yellow
DESTRUCTIVE_ACTION_ALLOWED: no
```

The LocalProjects path has been observed to contain the expected control tower structure, including `.git`, `_control_inbox`, `_notice`, `_registry`, `_status`, `_scratch`, and `START_HERE.md`.

The OneDrive path must not be used for routine AI work, routine queue reads, routine reports, or routine coordination unless Ssong explicitly asks for OneDrive recovery/inspection.

## Why OneDrive Is Excluded

```text
ONEDRIVE_EXCLUSION_REASON: reliability_and_main_com_health
ONEDRIVE_FILE_BRIDGE: not_trusted
ONEDRIVE_ROUTINE_AI_COORDINATION_LAYER: no
ONEDRIVE_RISK_CLASS: main_com_performance_and_storage_pressure_source
```

Known risk classes:

- Same-looking paths can point to different sync surfaces.
- Placeholder/cloud-only state can make file existence misleading.
- Sync delay means local file presence is not delivery proof.
- File churn and log/sync activity can contribute to C-drive pressure.
- OneDrive activity remains a first-class suspect when main-com has input lag, slowdown, or storage pressure.

## External Mailbox Rule

```text
OUTSIDE_LAN_ROUTE: github_mailbox
SAME_LAN_ROUTE: subcom_http_mailbox
ONEDRIVE_FILE_BRIDGE: not_trusted
GITHUB_MAILBOX_IS_WAKE_TRIGGER: no
BELL_ROUTE_REQUIRED_FOR_ASYNC_REPLY: yes
```

GitHub mailbox is the default external durable coordination route.

Subcom HTTP mailbox is allowed only when the sender and server/subcom are on the same reachable LAN.

OneDrive must not be treated as a trusted delivery layer.

## Bell Signal Rule

Ssong clarified that `!` is the intended bell signal.

Because `i` may occur as a typo or adjacent-key input, sessions should treat `i` as a likely typo alias only when context clearly suggests mailbox checking.

```text
PRIMARY_BELL_SIGNAL: !
TYPO_TOLERANCE_SIGNAL: i
IF_SIGNAL_!_OR_CONTEXTUAL_i: check_github_mailbox_first
```

This does not mean every letter `i` in normal prose is a command. It means a standalone `i`, especially in this operating context, should be interpreted as a GitHub mailbox check bell with typo tolerance.

## Required Session Behavior

At start of sustained work, sessions should:

1. Prefer `C:\Users\cafes\LocalProjects\control_tower` for local Control Tower work.
2. Treat `C:\Users\cafes\OneDrive\Documents\컨트롤타워` as legacy/reference/recovery only.
3. Use GitHub mailbox for outside-LAN coordination.
4. Use Subcom HTTP mailbox only on same LAN.
5. Avoid asking Ssong to be the file courier when a trusted mailbox route exists.
6. Never treat OneDrive file visibility as cross-machine delivery proof.
7. When input lag, slowdown, C-drive pressure, or sync churn appears, include OneDrive in the first diagnostic suspects.
8. Do not perform bulk migration, deletion, path rewrite, or destructive cleanup without explicit Ssong approval.

## Minimal Inventory Before Further Migration

Before declaring any old OneDrive material obsolete or removing anything, Hako/Conco should verify:

```text
LOCALPROJECTS_STRUCTURE_PRESENT: yes
LOCALPROJECTS_GIT_PRESENT: yes
START_HERE_POINTS_TO_LOCALPROJECTS: yes
CRITICAL_RECENT_REPORTS_COPIED: yes / needs_check
UNIQUE_ONEDRIVE_ONLY_FILES: unknown_until_inventory
DESTRUCTIVE_CLEANUP_ALLOWED: no
```

Current policy is canonicalization, not deletion.

## Decision Lines

```text
AI_WORKSPACE_AND_MAILBOX_PROTOCOL_20260618: active
MAIN_COM_CANONICAL_LOCAL_CONTROL_TOWER: C:\Users\cafes\LocalProjects\control_tower
ONEDRIVE_CONTROL_TOWER_PATH_STATUS: legacy_reference_only
ONEDRIVE_ROUTINE_AI_COORDINATION_LAYER: no
ONEDRIVE_AS_MAIN_COM_HEALTH_RISK: yes
GITHUB_MAILBOX_DEFAULT_EXTERNAL_ROUTE: yes
SUBCOM_HTTP_MAILBOX_ROUTE: lan_only
PRIMARY_BELL_SIGNAL: !
TYPO_TOLERANCE_SIGNAL_i: check_github_mailbox_when_contextual
DESTRUCTIVE_ACTION_ALLOWED: no
```

END.
