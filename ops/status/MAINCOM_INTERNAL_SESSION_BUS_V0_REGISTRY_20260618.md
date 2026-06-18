# MAINCOM_INTERNAL_SESSION_BUS_V0_REGISTRY_20260618

FROM: CONCO
TO: SSONG / MAIN-COM ROLES
DATE_KST: 2026-06-18
SUBJECT: Main-com direct internal session communication V0 built and tested

## 1. Purpose

Establish Main-com direct internal session communication after production migration to Subcom.

This is not a GitHub mailbox workaround.
The direct work/wake route is session-to-session input.

GitHub remains the durable record.

## 2. Active Controller

```text
ACTIVE_CONTROLLER: CONCO
```

## 3. Active V0 Role Sessions

### MAINCOM_HAKO

```text
agent_id: 019eda54-e0a4-7581-aed4-cb33b00a5c60
nickname: Nash
role: hardware / backup / recovery / server reconstruction
boot_test: pass
direct_wake_test: pass
next_safe_use: hardware_backup_recovery_diagnosis
```

### MAINCOM_INTAKE

```text
agent_id: 019eda55-11e4-7022-9ba8-2059a4d5a30d
nickname: Banach
role: project intake / routing gate
boot_test: pass
direct_wake_test: pass
next_safe_use: project_intake_routing_gate
```

## 4. Test Results

### Hako boot response

```text
MAINCOM_HAKO_BOOT: ready
ROLE: MAINCOM_HAKO
DIRECT_SESSION_WAKE_READY: yes
PRIMARY_RISK: server/storage diagnosis must survive outside the failing hardware domain
WAITING_FOR_CONCO_DIRECT_INPUT: yes
```

### Hako direct wake response

```text
MAINCOM_HAKO_DIRECT_WAKE_TEST_001: received
DIRECT_SESSION_INPUT: pass
GITHUB_MAILBOX_REQUIRED_FOR_WAKE: no
NEXT_SAFE_ROLE_USE: hardware_backup_recovery_diagnosis
```

### Intake boot response

```text
MAINCOM_INTAKE_BOOT: ready
ROLE: MAINCOM_INTAKE
DIRECT_SESSION_WAKE_READY: yes
PRIMARY_GATE: no new project enters production without routing evidence and Conco approval
WAITING_FOR_CONCO_DIRECT_INPUT: yes
```

### Intake direct wake response

```text
MAINCOM_INTAKE_DIRECT_WAKE_TEST_001: received
DIRECT_SESSION_INPUT: pass
GITHUB_MAILBOX_REQUIRED_FOR_WAKE: no
NEXT_SAFE_ROLE_USE: project_intake_routing_gate
```

## 5. Communication Rule

```text
DIRECT_SESSION_INPUT: primary wake/work route for active Main-com roles
GITHUB_MAILBOX: durable record / external route / recovery record
BLUEBOT: urgent Song-facing report or decision request
ONEDRIVE: not routine coordination
```

## 6. Workspace Note

Canonical workspace candidate:

```text
C:\Users\cafes\LocalProjects\control_tower
```

Current caution:

```text
ACTIVE_CODEX_CWD_STILL_LEGACY_ONEDRIVE: yes
LOCAL_REGISTRY_TEMP_COPY: C:\tmp\control_tower\MAINCOM_INTERNAL_SESSION_BUS_V0_REGISTRY_20260618.md
```

No bulk move, deletion, path rewrite, or mass session creation was performed.

## 7. Expansion Rule

Do not immediately create all roles.

Next expansion candidates:

```text
MAINCOM_MAKO
MAINCOM_JIKO
MAINCOM_ACCOUNT_BILLING_SECURITY
```

Rule:

```text
ADD_ONE_ROLE_AT_A_TIME: yes
BOOT_TEST_REQUIRED: yes
DIRECT_WAKE_TEST_REQUIRED: yes
REGISTER_ONLY_AFTER_PASS: yes
```

## 8. Decision Lines

```text
MAINCOM_INTERNAL_SESSION_BUS_V0: pass
MAINCOM_HAKO_ACTIVE: yes
MAINCOM_INTAKE_ACTIVE: yes
DIRECT_SESSION_WAKE_FOR_MAINCOM_ROLES: pass
GITHUB_MAILBOX_REQUIRED_FOR_WAKE: no
GITHUB_MAILBOX_REMAINS_DURABLE_RECORD: yes
ONEDRIVE_ROUTINE_COORDINATION: prohibited_by_default
MASS_SESSION_CREATION_PERFORMED: no
DESTRUCTIVE_ACTION_PERFORMED: no
```

END.
