# MAINCOM_INTERNAL_SESSION_COMMUNICATION_PL_V0_20260618

FROM: CONCO
TO: SSONG / HAKO / SAEKO / MAIN-COM ROLES
DATE_KST: 2026-06-18
SUBJECT: Main-com restructure after production migration to Subcom

## 1. Situation

The core production loop has naturally moved from Main-com to Subcom.

Subcom now functions as the production headquarters for long-running content work, including Gyoko-centered educational content production, layout, review, upload, and local server operations.

Main-com must therefore stop behaving like a partial production floor.

Main-com should become the control tower:

- strategy
- approval
- routing
- external access
- billing/account/security
- hardware/recovery supervision
- final gate judgment
- cross-project registry and PL maintenance

## 2. Core Problem

Main-com still contains fragments of the old structure.

If these fragments are merely patched together, Main-com will remain confused:

- some sessions will think they are production workers,
- some will use OneDrive-era routes,
- some will expect Song to carry messages manually,
- and some will fail to know whether communication should be direct, mailbox-based, or human-mediated.

This must be redesigned, not patched.

## 3. Target Direction

Main-com needs an internal session communication structure similar in function to Subcom.

The goal is not only to leave files.
The goal is to allow Main-com roles to coordinate as an operating body.

## 4. Communication Priority

Main-com communication priority should be:

1. Internal session-to-session communication when the Codex environment exposes a usable internal route.
2. GitHub mailbox as the durable external coordination record.
3. Bluebot only for Song notification, urgent decision, or human-facing report.
4. OneDrive must not be used as routine coordination or bridge storage.

Decision:

```text
MAINCOM_INTERNAL_COMMUNICATION_GOAL: direct_session_coordination_first
GITHUB_MAILBOX_ROLE: durable_record_and_external_route
BLUEBOT_ROLE: human_notification_and_urgent_escalation
ONEDRIVE_ROUTINE_COORDINATION: prohibited_by_default
```

## 5. Required Main-com Roles

Minimum Main-com roles:

- CONCO_CONTROL: control tower, strategy, approval, route discipline, PL governance
- HAKO_HARDWARE: hardware, backup, recovery, server reconstruction from outside the server domain
- MAKO_MARKET: market thesis, revenue logic, external opportunity analysis
- JIKO_DISTRIBUTION: distribution, announcement routes, external publication flow
- ACCOUNT_BILLING_SECURITY: billing, accounts, subscription exposure, security gates
- PROJECT_INTAKE_MANAGER: decides whether a new project belongs on Main-com or should be routed to Subcom

Production-heavy roles should not be recreated on Main-com by default.

## 6. Internal Communication Rule

Main-com roles should not depend on Song as courier.

Preferred pattern:

1. Sender writes or sends the task through the strongest available internal route.
2. Sender writes a durable GitHub mailbox record when the instruction affects project state.
3. Receiver acknowledges through the same route or mailbox.
4. If no reply appears after two expected cycles, diagnose the route before repeating content.

Two no-reply cycles mean bottleneck diagnosis, not passive waiting.

## 7. Pre-action Mailbox / State Check

Before sending an instruction, a Main-com role should check whether a newer related message already exists.

Reason:
Sending without checking can overwrite context, duplicate work, or reply to the wrong message.

Minimum schema for durable messages:

```text
message_id:
sent_at_kst:
from:
to:
subject:
reply_to_message_id:
related_task_id:
latest_message_checked:
action_required:
decision_line:
```

## 8. OneDrive Boundary

Hako has already identified OneDrive as a risk to Main-com stability and not only as a weak communication route.

Therefore:

```text
ONEDRIVE_FILE_BRIDGE: not_trusted
ONEDRIVE_AS_ROUTINE_AI_COORDINATION_LAYER: no
ONEDRIVE_HEALTH_WATCH: active
MAINCOM_CANONICAL_LOCAL_WORKSPACE: pending_hako_confirmation
```

Conco currently observed a workspace mismatch:

```text
CURRENT_CONCO_CWD: C:\Users\cafes\OneDrive\Documents\컨트롤타워
LOCALPROJECTS_CANDIDATE: C:\Users\cafes\LocalProjects\control_tower
```

No bulk migration, deletion, or path rewrite is allowed until Hako confirms the canonical workspace policy.

## 9. Main-com vs Subcom Division

Subcom:

- production loops
- education content generation
- review/layout/upload cycles
- local server execution
- long running task chains

Main-com:

- control tower
- cross-project approval
- external communication routes
- billing/security/account gates
- GitHub governance
- hardware/recovery oversight
- project intake and routing

Decision:

```text
SUBCOM_ROLE: production_headquarters
MAINCOM_ROLE: control_tower_and_external_governance
GYOKO_ROLE_LOCATION: subcom_production_core
CONCO_ROLE_LOCATION: maincom_control_core
HAKO_ROLE_LOCATION: outside_server_domain
```

## 10. Next Step

Do not immediately create many new sessions.

First establish the Main-com communication spine:

1. Confirm Hako canonical workspace policy.
2. Define Main-com role list.
3. Define internal route availability.
4. Define durable mailbox schema.
5. Create or reopen only the minimum required Main-com roles.
6. Test one direct role-to-role communication.
7. Record the pass/fail result.

## 11. Decision Lines

```text
MAINCOM_RESTRUCTURE_REQUIRED: yes
MAINCOM_SHOULD_NOT_REBUILD_OLD_PRODUCTION_STRUCTURE: yes
MAINCOM_INTERNAL_SESSION_COMMUNICATION_REQUIRED: yes
SUBCOM_PRODUCTION_MIGRATION_ACCEPTED: yes
GITHUB_MAILBOX_REMAINS_DURABLE_RECORD: yes
ONEDRIVE_ROUTINE_COORDINATION_PROHIBITED: yes
HAKO_CANONICAL_WORKSPACE_CONFIRMATION_REQUIRED: yes
MAINCOM_INTERNAL_SESSION_COMMUNICATION_PL_V0: issued
```

END.
