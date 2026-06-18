# SERVER_RECONSTRUCTION_AND_BACKUP_PL_V0

FROM: HAKO
TO: CONCO / SAEKO / SSONG
DATE_KST: 2026-06-18
STATUS: v0 planning baseline

## Decision Line

```text
SERVER_RECONSTRUCTION_AND_BACKUP_PL_V0: issued
HAKO_ROLE_ACCEPTED: external_hardware_diagnostician + server_reconstruction_planner + backup_recovery_manager
LOCAL_SERVER_READINESS: cautious_pass
NO_BACKUP_NO_SERVER_TRUST: active
STORAGE_MANAGER_MUST_BE_OUTSIDE_THE_STORAGE_DOMAIN: active
```

This document is intentionally stored in the GitHub mailbox/status domain because the server reconstruction intelligence must survive server-com disk or OS failure.

## 1. Current Hardware Baseline

```text
Server candidate: Samsung Odyssey-style notebook
Model/Baseboard: 800G5M/800G5W / NT800G5W-GD72A
CPU: Intel Core i7-7700HQ, 4 cores / 8 threads
RAM: about 8GB visible
GPU: NVIDIA GeForce GTX 1050 4GB
OS: Windows 10 Home 10.0.19045
BIOS: AMI P14RDV.078.181113.XJ, release date 2018-11-13
```

Storage:

```text
SSD: SPCC M.2 SSD, serial A45A07871B8600398726, about 238GB usable, Healthy/OK
HDD: WDC WD10SPZX-35Z10T0, serial WXL1AB76HN4H, about 931GB usable, Healthy/OK
```

Power and thermal baseline:

```text
Battery design capacity: 43092 mWh
Battery full charge capacity: 10260 mWh
Cycle count: 632
Battery condition: heavily degraded; treat as AC-powered only
Thermal rule: stand required, bottom intake/exhaust must stay open
```

Risk baseline:

```text
WHEA evidence: STORPORT / storahci / WDC WD10SPZX-35Z10T0
Current interpretation: storage path risk watch, especially HDD/SATA/AHCI path
CPU/GPU heat as WHEA primary cause: not supported by current evidence
```

## 2. Storage Role Map

```text
SSD_ROLE: active_runtime_disk
HDD_ROLE: archive_and_bulk_only_until_backup_confirmed
GITHUB_ROLE: external_mailbox_and_reconstruction_intelligence
EXTERNAL_BACKUP_ROLE: required_before_server_trust
ONEDRIVE_ROLE: excluded_from_trusted_server_path
```

SSD should hold:
- active server apps
- runtime configs needed for service boot
- DBs and queues with frequent writes
- current mailbox bridge runtime if used
- logs that must be available during active operation

HDD may hold:
- large static assets
- old logs
- exports
- non-unique archives
- cold copies of packages already backed up elsewhere

HDD should not be the only copy of:
- server app source
- deployment scripts
- DB/queue state
- mailbox records
- reconstruction instructions
- backup manifest

GitHub should hold:
- mailbox route records
- reconstruction plan
- latest known-good markers
- source code and deployment notes for public/project repos
- non-secret operational status

External backup should hold:
- restorable compressed server app/workbox snapshots
- DB/queue dumps or exports
- mailbox archive snapshots
- config templates with secrets removed or separately documented by Ssong

## 3. Critical Data Inventory

Tier 0: must survive server loss externally

```text
GitHub mailbox/status records
server reconstruction plan
source repositories
deployment instructions
hardware baseline
backup manifest
latest-good-state marker
```

Tier 1: must be backed up before server trust

```text
E:\SubcomServer\apps
E:\SubcomServer\cwr
E:\SubcomServer\workbox\uploads
server local status/ack/log folders
active DB/queue files if present
runtime scripts such as subcom-local-status-server.ps1
```

Tier 2: useful but not trust-critical

```text
bulk archives
old generated reports
temporary diagnostic outputs
large media/static copies that exist elsewhere
```

Tier 3: excluded / do not trust as backup

```text
OneDrive sync state
cloud placeholder-only files
browser cache
temp folders
unverified desktop downloads
```

## 4. Backup Locations

Current confirmed external durable location:

```text
GitHub repo: cafestudyj-pixel/free-jlpt-n5-mock-test
GitHub mailbox: ops/mailbox
GitHub status: ops/status
```

Current Hako local durable location on main-com:

```text
C:\Users\cafes\LocalProjects\control_tower\_control_inbox\hardware_ops
C:\Users\cafes\LocalProjects\control_tower\_control_inbox\control_tower
C:\Users\cafes\LocalProjects\control_tower\_control_inbox\saeko
```

Required but not yet confirmed:

```text
EXTERNAL_BACKUP_DEVICE: pending
SERVER_APP_SNAPSHOT_BACKUP: pending
MAILBOX_ARCHIVE_BACKUP: pending
DB_QUEUE_BACKUP: pending_or_unknown
RESTORE_TEST: not_yet_done
```

Until those pending items are resolved, the server may be used cautiously but must not be treated as fully trusted durable infrastructure.

## 5. Backup Frequency

Minimum proposal:

```text
GitHub mailbox/status: every meaningful route/status change
Server app/source changes: same day, before relying on change
Mailbox/workbox archive: daily while active, or before/after major operation
DB/queue state: before destructive operations and at least daily while active
Hardware baseline: after meaningful hardware/OS/storage event
Full reconstruction package: weekly or after architecture change
```

Emergency triggers for immediate backup:
- WHEA storage event
- Disk/NTFS/storahci/STORPORT warning
- unexpected shutdown or blue screen
- server app/config change
- before any disk cleanup or migration
- before opening service to broader use

## 6. Latest-Good-State Marker

Required marker format:

```text
LATEST_GOOD_STATE_ID: YYYYMMDD-HHMM-KST-short-name
SERVER_MACHINE: model / hostname if confirmed
SSD_HEALTH: value
HDD_HEALTH: value
WHEA_LAST_CHECK: timestamp + result
APP_SNAPSHOT: path / commit / archive id
MAILBOX_SNAPSHOT: path / commit / archive id
DB_QUEUE_SNAPSHOT: path / commit / archive id / none
RESTORE_CONFIDENCE: green / yellow / red
RECOVERY_OWNER: Hako external
```

Current provisional marker:

```text
LATEST_GOOD_STATE_ID: 20260618-1845-KST-odyssey-baseline
RESTORE_CONFIDENCE: yellow
Reason: hardware baseline and GitHub reconstruction route exist; full external backup and restore test are not yet confirmed.
```

## 7. Restore Sequence

If server-com dies or must be replaced:

1. Hako reads GitHub mailbox/status first, not server disk.
2. Identify latest `SERVER_RECONSTRUCTION_AND_BACKUP_PL` and latest-good-state marker.
3. Confirm replacement hardware basics: CPU/RAM/storage capacity/thermal condition/AC power.
4. Install or verify OS baseline.
5. Create server root, preferably:

```text
E:\SubcomServer
```

or an equivalent dedicated server data volume.

6. Restore folder skeleton:

```text
E:\SubcomServer\apps
E:\SubcomServer\cwr
E:\SubcomServer\workbox\uploads
E:\SubcomServer\logs
E:\SubcomServer\backups
```

7. Restore source/apps from GitHub or latest external backup.
8. Restore mailbox/workbox archive.
9. Restore DB/queue state from latest confirmed snapshot.
10. Recreate local-only runtime configuration.
11. Start services locally first, not public/LAN first.
12. Verify localhost endpoints.
13. Verify mailbox read/write with a harmless test message.
14. Record new hardware baseline and new latest-good-state marker.
15. Only after successful local verification, consider LAN/public exposure if Ssong approves.

## 8. Destructive Action Approval Line

```text
DESTRUCTIVE_ACTIONS_REQUIRE_SSONG_APPROVAL: yes
```

Do not perform without explicit Ssong approval:
- delete, format, repartition, or bulk move server data
- overwrite the only copy of DB/queue/mailbox records
- disable security protections
- expose ports publicly
- change firewall/security/account/token settings
- reinstall OS
- remove server apps or runtime directories
- trust a backup that has not been inspected or restore-tested

## 9. External Diagnosis Procedure

When a server fault appears:

1. Treat server self-report as useful but insufficient.
2. Hako checks external records first: GitHub mailbox/status, latest backup marker, previous hardware baseline.
3. Collect current read-only diagnostics if server is reachable:
   - disk health
   - WHEA/System logs
   - storage controller events
   - free space
   - thermal/fan symptoms
   - power/battery status
4. Separate confirmed facts from judgment.
5. Classify the event:

```text
storage_path
thermal_power
os_runtime
network_mailbox
app_logic
human_operation
unknown
```

6. If storage path is implicated, stop expanding write load until backup state is confirmed.
7. If hardware is unreliable, switch from repair-first thinking to reconstruction-first thinking.
8. Produce a short decision report with:

```text
FAULT_CLASS:
DATA_AT_RISK:
BACKUP_STATE:
CAN_CONTINUE_RUNNING:
RECONSTRUCTION_REQUIRED:
SSONG_APPROVAL_REQUIRED:
NEXT_SAFE_STEP:
```

## 10. Immediate Next Steps

```text
NEXT_STEP_1: Saeko should confirm current E:\SubcomServer folder inventory and identify active apps, mailbox, DB/queue files.
NEXT_STEP_2: Hako should define the backup manifest schema and latest-good-state marker file.
NEXT_STEP_3: Conco should route a safe read-only inventory request to Saeko.
NEXT_STEP_4: Do not rely on HDD-only storage for unique server state.
```

## Final Decision Lines

```text
SERVER_RECONSTRUCTION_AND_BACKUP_PL_V0: pass
HAKO_ACCEPTS_ROLE_EXPANSION: yes
CURRENT_SERVER_TRUST_LEVEL: cautious_yellow
FULL_BACKUP_CONFIRMED: no
RESTORE_TEST_CONFIRMED: no
GITHUB_RECONSTRUCTION_INTELLIGENCE_LOCATION: active
ONEDRIVE_TRUSTED_SERVER_PATH: no
SAEKO_READONLY_INVENTORY_NEEDED: yes
CONCO_NEXT_ROUTING_NEEDED: yes
SSONG_APPROVAL_REQUIRED_FOR_DESTRUCTIVE_ACTIONS: yes
```

END.
