# Local Server Hardware Baseline - 2026-06-18

Source:
- Hako / Main-com hardware readiness report
- Mailbox message: `20260618-181500-HAKO_TO_CONCO_LOCAL_SERVER_ODYSSEY_BASELINE_AND_SAEKO_RELAY_REQUEST.md`

Primary decision:

```text
LOCAL_SERVER_READINESS: cautious_pass
```

Meaning:
The notebook can be used as a local server only with operational guardrails.

Hardware baseline:

```text
Manufacturer: Samsung
Model/Baseboard: 800G5M/800G5W / NT800G5W-GD72A
CPU: Intel Core i7-7700HQ, 4 cores / 8 threads
RAM: about 8GB visible
GPU: NVIDIA GeForce GTX 1050 4GB
OS: Windows 10 Home 10.0.19045
BIOS: AMI P14RDV.078.181113.XJ, release date 2018-11-13
SSD: SPCC M.2 SSD, about 238GB usable, Healthy/OK
HDD: WDC WD10SPZX-35Z10T0, about 931GB usable, Healthy/OK
Battery: heavily degraded; treat as AC-powered only
```

Risk baseline:

```text
WHEA_STORAGE_PATH_RISK: watch
CPU_GPU_HEAT_AS_PRIMARY_WHEA_CAUSE: not_supported_by_current_evidence
```

Operating guardrails:

1. Use SSD for active server apps, DBs, queues, logs, and frequently written state.
2. Use HDD only for archive, bulk files, or non-unique copies unless backup is confirmed.
3. Watch WHEA, storahci, STORPORT, Disk, and NTFS events.
4. Do not treat battery as UPS. Use stable AC power.
5. Keep intake/exhaust clear for 24h operation.
6. Do not perform destructive storage actions without Ssong approval.

Conco routing decision:

```text
CONCO_RECEIVED_HAKO_LOCAL_SERVER_BASELINE: yes
LOCAL_SERVER_READINESS_RECORDED: yes
SAEKO_RELAY_REQUIRED: yes
SAEKO_RELAY_ROUTE: github_mailbox
SAEKO_INFORMED: pending_until_mailbox_indexed
NEXT_SERVER_HARDWARE_STEP: Saeko should apply SSD/HDD/write-path guardrails before assigning local-server duties.
```

END.
