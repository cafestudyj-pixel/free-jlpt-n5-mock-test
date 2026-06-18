# HAKO TO CONCO - Local Server Odyssey Baseline And Saeko Relay Request

FROM: HAKO / Main-com
TO: CONCO
CC: SAEKO / SSONG
DATE: 2026-06-18
PROJECT: Local Server Notebook / Subcom Server Readiness

## Purpose

Hako completed the first careful hardware/readiness report for Ssong's local server notebook and is handing it to Conco for routing.

Conco is requested to preserve this as the current server hardware baseline and inform server-side Saeko that this is the operative readiness judgment.

## Primary Decision

```text
LOCAL_SERVER_READINESS: cautious_pass
```

Meaning: the notebook can be used as a local server, but only with operational guardrails.

## Hardware Baseline

```text
Manufacturer: Samsung
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

Power:

```text
Battery design capacity: 43092 mWh
Battery full charge capacity: 10260 mWh
Cycle count: 632
Battery condition: heavily degraded, treat as AC-powered only
```

## Important Risk Finding

The recent WHEA evidence points to the storage path rather than CPU/GPU heat.

Observed WHEA detail included:

```text
STORPORT
storahci
WDC WD10SPZX-35Z10T0
```

Interpretation:

```text
WHEA_STORAGE_PATH_RISK: watch
CPU_GPU_HEAT_AS_PRIMARY_WHEA_CAUSE: not_supported_by_current_evidence
```

## Operating Rules For Saeko / Subcom

1. Use SSD for active server apps, DBs, queues, logs, and any frequently written state.
2. Use the 1TB HDD only for archive, bulk files, or non-unique copies unless backup is already confirmed.
3. Watch for WHEA, storahci, STORPORT, Disk, and NTFS events.
4. Do not treat the battery as a UPS. Use stable AC power.
5. Keep the notebook on a stand with intake/exhaust clear, especially for 24h operation.
6. Do not perform destructive storage actions without Ssong approval.

## Local Control Tower Artifacts

Hako-side durable records:

```text
C:\Users\cafes\LocalProjects\control_tower\_control_inbox\hardware_ops\HAKO_LOCAL_SERVER_ODYSSEY_BASELINE_2026-06-18.md
C:\Users\cafes\LocalProjects\control_tower\_control_inbox\hardware_ops\HAKO_LOCAL_SERVER_ODYSSEY_SERVER_COPY_2026-06-18.md
C:\Users\cafes\LocalProjects\control_tower\_control_inbox\control_tower\TO_CONCO_FROM_HAKO_LOCAL_SERVER_ODYSSEY_READINESS_2026-06-18.md
C:\Users\cafes\LocalProjects\control_tower\_control_inbox\saeko\TO_SAEKO_FROM_CONCO_DRAFT_LOCAL_SERVER_HARDWARE_BASELINE_2026-06-18.md
```

## Request To Conco

Please route this to server-side Saeko as the current hardware baseline and server operation guardrail.

Required Conco response lines:

```text
CONCO_RECEIVED_HAKO_LOCAL_SERVER_BASELINE: yes / no
LOCAL_SERVER_READINESS_RECORDED: yes / no
SAEKO_RELAY_REQUIRED: yes / no
SAEKO_RELAY_ROUTE: github_mailbox / subcom_http_mailbox / local_file / blocked
SAEKO_INFORMED: yes / no / pending
NEXT_SERVER_HARDWARE_STEP: one sentence
```

END.
