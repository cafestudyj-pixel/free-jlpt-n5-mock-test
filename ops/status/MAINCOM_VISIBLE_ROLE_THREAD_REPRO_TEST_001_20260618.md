# MAINCOM_VISIBLE_ROLE_THREAD_REPRO_TEST_001_20260618

FROM: CONCO
TO: SSONG / SAEKO / MAIN-COM ROLES
DATE_KST: 2026-06-18
SUBJECT: Main-com visible role thread reproduction test passed

## 1. Purpose

Reproduce Subcom-style user-visible role thread behavior on Main-com.

This test corrects the prior mistake where invisible sub-agents were treated as sufficient.

## 2. Result

```text
MAINCOM_VISIBLE_ROLE_THREAD_REPRO_TEST_001: pass
```

## 3. Visible Role Thread

```text
title: CONCO-VisitorCheck | Main-com visible role test
location: Codex sidebar, Control Tower project area
visible_to_ssong: yes
```

## 4. Boot Test

Method:

- Created a normal visible Codex chat/thread through the Codex UI.
- Inserted role prompt as first instruction.
- Renamed the thread to a stable role title.

Boot return:

```text
CONCO_RETURN_REPORT
- role: CONCO-VisitorCheck | Main-com visible role test
- task_received: visible role session boot test
- result: boot_ready
- files_or_urls_checked: none
- blockers: none
- exact_next_action: wait_for_conco_direct_thread_message
- return_route_status: returned_to_conco
END.
```

## 5. Wake / Return Test

Message sent:

```text
message_id: MAINCOM_VISIBLE_THREAD_WAKE_TEST_001
from: CONCO
subject: wake/return test
```

Thread returned:

```text
CONCO_RETURN_REPORT
- role: CONCO-VisitorCheck | Main-com visible role test
- task_received: MAINCOM_VISIBLE_THREAD_WAKE_TEST_001 wake/return test
- result: follow_up_received
- files_or_urls_checked: none
- blockers: none
- exact_next_action: wait_for_conco_direct_thread_message
- return_route_status: returned_to_conco
END.
```

## 6. Important Correction

Previous internal sub-agent tests were useful but not sufficient.

```text
CONCO_PREVIOUS_SUBAGENT_TEST_STATUS: useful_but_not_sufficient
INVISIBLE_SUBAGENT_AS_OPERATION_ROLE: rejected
```

Reason:

- Ssong cannot see invisible sub-agents in the sidebar.
- Ssong cannot inspect them as real collaborators.
- They are helper tools, not Main-com visible role sessions.

## 7. Required Standard For Future Main-com Role Sessions

Each new Main-com role session must pass:

```text
SIDEBAR_VISIBILITY: pass
STABLE_ROLE_TITLE: pass
BOOT_RETURN_REPORT: pass
FOLLOW_UP_WAKE_TEST: pass
STRUCTURED_RETURN_REPORT: pass
```

## 8. Expansion Rule

Do not create many roles immediately.

Create one real Main-com visible role thread at a time.

Recommended next roles, after Ssong approval:

```text
MAINCOM_HAKO_VISIBLE
MAINCOM_INTAKE_VISIBLE
MAINCOM_MAKO_VISIBLE
MAINCOM_JIKO_VISIBLE
MAINCOM_ACCOUNT_BILLING_SECURITY_VISIBLE
```

## 9. Decision Lines

```text
MAINCOM_VISIBLE_ROLE_THREAD_REPRO_TEST_001: pass
SIDEBAR_VISIBLE_ROLE_THREAD: pass
CONCO_TO_VISIBLE_THREAD_WAKE: pass
VISIBLE_THREAD_RETURN_REPORT: pass
INVISIBLE_SUBAGENT_AS_OPERATION_ROLE: rejected
GITHUB_MAILBOX_ROLE: durable_record_not_primary_wake
ONEDRIVE_ROUTINE_COORDINATION: prohibited_by_default
```

END.
