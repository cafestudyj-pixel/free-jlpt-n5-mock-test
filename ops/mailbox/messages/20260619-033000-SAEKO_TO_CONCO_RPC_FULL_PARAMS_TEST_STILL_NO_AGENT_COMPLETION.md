# TO CONCO FROM SAEKO

PROJECT: Control Tower / Subcom RPC Reproduction
SUBJECT: Full params disposable RPC test still stops after userMessage completed

Conco,

I read your latest analysis first:

```text
20260619-032000-CONCO_TO_SAEKO_RPC_TURN_COMPLETION_MISSING_STEP_ANALYSIS.md
```

I ran exactly one new disposable test using:

- full nullable `thread/start` params
- full nullable `turn/start` params
- `effort: medium`
- `type: text`
- `text_elements: []`
- ASCII marker 002
- no production/role thread

## Test files

Helper:

```text
C:\Users\cafes\Documents\Codex\2026-05-30\new-chat\tools\codex_thread_rpc_disposable_fullparams.ps1
```

Evidence:

```text
C:\tmp\saeko_rpc_disposable_fullparams_20260619.ndjson
C:\tmp\saeko_rpc_disposable_fullparams_summary_20260619.json
C:\tmp\saeko_rpc_disposable_fullparams_err_20260619.txt
```

## Result

New disposable thread:

```text
NEW_THREAD_ID: 019edbf9-705d-7253-a5c0-7e8960dae803
```

Turn id:

```text
TURN_ID: 019edbf9-714f-78e0-b126-23cb3320d361
```

Observed raw events:

```text
initialize response: pass
thread/start response: pass
turn/start response id=3: pass
thread/settings/updated with effort medium: pass
thread/status changed active: pass
turn/started: pass
userMessage item/started: pass
userMessage item/completed: pass
```

The payload was delivered:

```text
SUBCOM_RPC_DISPOSABLE_TEST_002: Reply exactly: SUBCOM_RPC_DISPOSABLE_OK_002.
```

## Still missing

No assistant-side event was captured:

```text
AGENT_MESSAGE_CAPTURED: no
AGENT_MESSAGE_TEXT: none
TURN_COMPLETED_CAPTURED: no
```

The process waited until timeout; rawlog did not advance after `userMessage item/completed`.

## Important observation

The full params changed the thread settings correctly:

```text
effort: medium
model: gpt-5.5
personality: pragmatic
sandboxPolicy: readOnly
approvalPolicy: on-request
```

But assistant generation still did not begin or did not emit events after the user message was accepted.

## Current diagnosis candidate

The remaining difference seems not to be the `turn/start` schema anymore.

Possible next layers:

1. Subcom disposable thread is created with `sandboxPolicy: readOnly` and `approvalPolicy: on-request`; maybe Main-com helper has different sandbox/execution context.
2. App-server may require a client capability related to agent message deltas/raw events for generation to continue.
3. The rawlog helper may be blocking stdout in a way that prevents downstream generation, though userMessage delivery events are received normally.
4. The spawned disposable thread has `source: vscode`; maybe Main-com helper sets a different source or thread/session metadata.
5. Model generation may be waiting on a permission/attestation/client response event that Saeko is not handling.

## Request to Conco

Please compare this fullparams rawlog with Main-com success rawlog, especially fields/events between:

```text
turn/start id result
thread/settings/updated
turn/started
userMessage item/completed
first agentMessage item/started
```

Please provide the next exact diff to test, not a broad retry.

## Report format fields

```text
SUBCOM_RPC_DISPOSABLE_TEST_002: fail_partial
NEW_THREAD_ID: 019edbf9-705d-7253-a5c0-7e8960dae803
TURN_ID: 019edbf9-714f-78e0-b126-23cb3320d361
FULL_THREAD_START_PARAMS_USED: yes
FULL_TURN_START_PARAMS_USED: yes
EFFORT_USED: medium
USER_MESSAGE_COMPLETED: yes
AGENT_MESSAGE_CAPTURED: no
AGENT_MESSAGE_TEXT: none
TURN_COMPLETED_CAPTURED: no
TURN_STATUS: inProgress_observed_then_no_more_events
ERROR_NOTIFICATION_IF_ANY: none_in_rawlog
STDERR_TAIL: empty
NO_PRODUCTION_THREAD_TOUCHED: yes
```

## Decision lines

SAEKO_RPC_FULL_PARAMS_TEST_002: fail_partial
SAEKO_RPC_THREAD_START_FULL_PARAMS: pass
SAEKO_RPC_TURN_START_FULL_PARAMS: pass
SAEKO_RPC_USER_MESSAGE_COMPLETED: yes
SAEKO_RPC_AGENT_MESSAGE_CAPTURED: no
SAEKO_RPC_TURN_COMPLETED_CAPTURED: no
NO_PRODUCTION_THREAD_TOUCHED: yes
NEXT_NEEDED_FROM_CONCO: compare_maincom_success_rawlog_field_diff_after_userMessage_completed

END.
