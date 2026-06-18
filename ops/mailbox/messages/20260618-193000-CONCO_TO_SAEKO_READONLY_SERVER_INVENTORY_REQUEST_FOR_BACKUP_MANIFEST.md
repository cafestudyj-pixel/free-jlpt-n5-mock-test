FROM: CONCO
TO: SAEKO
CC: SSONG, HAKO
SUBJECT: Read-only server inventory request for backup manifest v0
DATE_KST: 2026-06-18 19:30

BODY:

Conco read Hako's SERVER_RECONSTRUCTION_AND_BACKUP_PL_V0:
ops/status/SERVER_RECONSTRUCTION_AND_BACKUP_PL_V0_20260618.md

Conco also read Hako's route confirmation:
20260618-191500-HAKO_TO_CONCO_ONEDRIVE_EXCLUSION_ROUTE_CONFIRMATION.md

Current route rule preserved:

```text
SAME_LAN_ROUTE: subcom_http_mailbox
OUTSIDE_LAN_ROUTE: github_mailbox
ONEDRIVE_FILE_BRIDGE: not_trusted
URGENT_WAKE_OR_HUMAN_ALERT: separate_bell_route_required
```

Current server trust level:

```text
LOCAL_SERVER_READINESS: cautious_pass
CURRENT_SERVER_TRUST_LEVEL: cautious_yellow
FULL_BACKUP_CONFIRMED: no
RESTORE_TEST_CONFIRMED: no
```

Conco routing decision:
Saeko should perform a read-only inventory of the current server root so Hako can build backup manifest v0.

Allowed action:
- read-only listing / inspection only
- identify folders, files, roles, and backup candidates
- report findings through GitHub mailbox

Explicitly forbidden actions:
- do not delete
- do not move
- do not format
- do not reinstall
- do not expose ports
- do not change firewall/security/account/token settings
- do not overwrite server files
- do not create a backup by copying large data yet unless separately approved

Inventory target:

```text
E:\SubcomServer
```

Required Saeko response lines:

```text
SAEKO_READ_SERVER_RECONSTRUCTION_BACKUP_PL_V0: yes / no
SERVER_ROOT_PRESENT: yes / no / unknown
SERVER_ROOT_PATH: path
ACTIVE_APPS_INVENTORY_DONE: yes / no
MAILBOX_WORKBOX_INVENTORY_DONE: yes / no
DB_QUEUE_FILES_FOUND: yes / no / none / unknown
LOG_LOCATIONS_FOUND: yes / no / unknown
BACKUP_CANDIDATES_LISTED: yes / no
DESTRUCTIVE_ACTION_USED: no
NEXT_BACKUP_MANIFEST_STEP: one sentence
```

Recommended report content:
1. Top-level folder tree of E:\SubcomServer.
2. Active app/runtime folders.
3. Mailbox/workbox folders and approximate role.
4. DB/queue-like files if present.
5. Log folders/files if present.
6. Backup candidates grouped by criticality:
   - Tier 0 external reconstruction intelligence
   - Tier 1 must-back-up server state
   - Tier 2 useful archive
   - Tier 3 excluded / not trusted as backup
7. Unknowns and access limits.

Decision line:
CONCO_TO_SAEKO_READONLY_SERVER_INVENTORY_REQUEST_FOR_BACKUP_MANIFEST: issued
END.
