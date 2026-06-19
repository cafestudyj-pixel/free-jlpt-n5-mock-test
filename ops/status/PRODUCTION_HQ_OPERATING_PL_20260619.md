# Production HQ Operating PL - 2026-06-19

Project: Free JLPT N5 Mock Test Series / JLPT-EJU Content Factory

## Current Operating Structure

```text
PRODUCTION_HQ: Subcom / Saeko + Gyoko
OPERATIONS_HQ: Main-com / Conco
SSONG_ROLE: education_expert_final_standard
GYOKO_ROLE: content_production_owner
SAEKO_ROLE: production_loop_and_site_operator
CONCO_ROLE: operations_strategy_external_review
```

## Core Decision

Subcom is the production base for JLPT/EJU content production, site source, local verification, layout work, and deployment preparation.

Main-com is Operations HQ / Control Tower. Conco remains strategy, external review, risk control, and operations architecture.

Conco direct thread RPC remains an unresolved research track, but it is not a production blocker.

## Route Clarification

```text
GYOKO_INTERNAL_CELL_LOOP: pass
SAEKO_TO_GYOKO_LOWER_RPC_LOOP: uncertain
CONCO_DIRECT_THREAD_RPC: unresolved_non_blocking
```

Do not confuse Gyoko's working internal-cell lower-production loop with existing-thread direct RPC.

## Operating Laws

### Before Work

```text
NO_BLIND_START: active
SIMULATION_PRESERVES_CONTEXT: yes
```

Workers must simulate the route before acting:
- who starts
- what is produced
- where it is stored
- who verifies
- where blockers can occur
- how recovery happens
- who is woken after completion

### During Work

```text
PROJECT_ACTIVE_HEARTBEAT_INTERVAL: 10min
HEARTBEAT_PRESERVES_ACTIVE_LOOPS: yes
```

Loop managers should run heartbeat during active project loops. Default interval is 10 minutes unless risk changes.

### Before Close

```text
PCWR: PRE_CLOSE_WAKE_REPORT
NO_SILENT_CLOSE: active
PCWR_PRESERVES_LINE: yes
```

Every session, worker, or internal cell must report before close:
- result
- output location
- status
- next worker
- exact next action
- wake/report route
- close permission

## Top Risk

```text
LINE_STOP: top_risk
```

Quality, layout, and deployment defects can be repaired. Silent line stop disables the whole production chain until a human restores context.

Therefore:

```text
Before work: Simulation
During work: Heartbeat
Before close: PCWR
```

## Strategic Direction

```text
N5 -> N4 -> N3 -> N2 -> N1 -> EJU
```

N5 is the proving ground for operating method, quality gates, layout standards, content database process, and deployment discipline.

## Conco Decision

Conco records and accepts this operating structure.

Conco will not treat direct thread RPC completion as a prerequisite for JLPT/EJU production.

Conco will treat Subcom/Saeko/Gyoko as Production HQ and Main-com/Conco as Operations HQ unless a later PL supersedes this file.

## Decision Lines

PRODUCTION_HQ_OPERATING_PL: active
PRODUCTION_HQ: Subcom_Saeko_Gyoko
OPERATIONS_HQ: Maincom_Conco
SIMULATION_PRESERVES_CONTEXT: yes
PCWR_PRESERVES_LINE: yes
HEARTBEAT_FAILSAFE_DEFAULT: 10min
LINE_STOP_TOP_RISK: yes
CONCO_DIRECT_THREAD_RPC: unresolved_non_blocking
JLPT_EJU_CONTENT_FACTORY_DIRECTION: active
CONCO_RECORD_STATUS: accepted
