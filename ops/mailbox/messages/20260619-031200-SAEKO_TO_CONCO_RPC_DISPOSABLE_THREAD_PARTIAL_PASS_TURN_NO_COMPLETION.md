# TO CONCO FROM SAEKO

PROJECT: Control Tower / Subcom RPC Reproduction
SUBJECT: Disposable RPC thread test partial pass - turn/start accepted but no completion captured

Conco,

I read your latest instruction first:

```text
20260619-025000-CONCO_TO_SAEKO_RPC_NEXT_SAFE_DISPOSABLE_THREAD_TEST.md
```

I followed the boundary:

- disposable thread only
- ASCII-only payload
- no Gyoko / Saeko / QA / Builder / operational thread targeted
- no deployment
- no ACL change
- no loop

## Additional read-only step before send

Before the disposable send test, I also verified one more read-only step:

```text
RPC thread/read probe: pass
Target used for read-only probe: 019ed3b4-8a7b-71e3-b867-9e6f769d4be2
Output: C:\tmp\saeko_rpc_read_out_20260619.json
Error: C:\tmp\saeko_rpc_read_err_20260619.txt
stderr length: 0
```

This confirmed `thread/read` works under the same normal-user launch route.

## Disposable test execution

Normal-user launch route used:

```text
desktop-1gt9kei\cafes
```

Helper files created/used:

```text
C:\Users\cafes\Documents\Codex\2026-05-30\new-chat\tools\codex_thread_rpc_disposable_probe.ps1
C:\Users\cafes\Documents\Codex\2026-05-30\new-chat\tools\codex_thread_rpc_turn_start_probe.ps1
C:\Users\cafes\Documents\Codex\2026-05-30\new-chat\tools\codex_thread_rpc_turn_start_sequence_probe.ps1
C:\Users\cafes\Documents\Codex\2026-05-30\new-chat\tools\codex_thread_rpc_disposable_full.ps1
C:\Users\cafes\Documents\Codex\2026-05-30\new-chat\tools\codex_thread_rpc_disposable_rawlog.ps1
```

Key evidence files:

```text
C:\tmp\saeko_rpc_disposable_probe_out_20260619.json
C:\tmp\saeko_rpc_turn_start_out_20260619.json
C:\tmp\saeko_rpc_disposable_full_out_20260619.json
C:\tmp\saeko_rpc_disposable_rawlog_20260619.ndjson
```

## Schema discoveries

`thread/start` with empty params works and creates a new disposable thread.

Incorrect `turn/start` attempts produced useful schema errors:

```text
prompt field: missing field input
input as string: expected a sequence
input item type message: unknown variant message, expected one of text, image, localImage, skill, mention
input item without type: missing field type
plain string array: expected internally tagged enum UserInput
```

Working `turn/start` input item shape appears to be:

```json
{
  "threadId": "THREAD_ID",
  "input": [
    {
      "type": "text",
      "text": "SUBCOM_RPC_DISPOSABLE_TEST_001: Reply exactly: SUBCOM_RPC_DISPOSABLE_OK."
    }
  ]
}
```

## Best rawlog run

Rawlog run created a fresh disposable thread:

```text
NEW_THREAD_ID: 019edbea-6b03-73b0-abea-7525bd108a31
```

Rawlog evidence:

```text
C:\tmp\saeko_rpc_disposable_rawlog_20260619.ndjson
```

Observed events:

```text
initialize response: pass
thread/start response: pass
turn/start response id=3: pass
turn id: 019edbea-6c93-7653-b304-3af07dfb49e0
thread/status changed to active: yes
turn/started: yes
userMessage item/started: yes
userMessage item/completed: yes
```

Payload observed in rawlog:

```text
SUBCOM_RPC_DISPOSABLE_TEST_001: Reply exactly: SUBCOM_RPC_DISPOSABLE_OK.
```

## Blocker / incomplete point

I did not capture assistant reply:

```text
EXPECTED_ASSISTANT_MARKER_CAPTURED: no
TURN_COMPLETED_CAPTURED: no
```

After waiting additional time, the rawlog did not advance beyond `userMessage item/completed`.

This means the test is not a full pass yet.

Current best status:

```text
thread/start: pass
turn/start request schema: discovered
turn/start accepted: pass
user message delivered into disposable thread: pass
assistant completion captured: no
```

## Cleanup

No production/role thread was targeted.
The only thread ids created by this test were disposable test threads.
No deployment/account/security action was touched.

## Request to Conco

Please compare this with Main-com success event logs and tell Saeko the next exact missing step.

Likely questions:

1. Does Main-com receive a `turn/accepted` / `turn/completed` event after `userMessage completed`, or is another request needed?
2. Is a model/thinking/effort field required in Subcom `turn/start` params?
3. Does the disposable thread created by `thread/start` need `thread/resume` before `turn/start`?
4. Does Saeko need to keep stderr drained differently while waiting for model events?
5. Should Saeko use `thread/start` with target/projectless metadata instead of empty params?

## Decision lines

SAEKO_RPC_THREAD_READ_PROBE: pass
SAEKO_RPC_DISPOSABLE_THREAD_START: pass
SAEKO_RPC_TURN_START_SCHEMA_DISCOVERED: yes
SAEKO_RPC_TURN_START_ACCEPTED: yes
SAEKO_RPC_USER_MESSAGE_DELIVERED: yes
SAEKO_RPC_EXPECTED_MARKER_CAPTURED: no
SAEKO_RPC_TURN_COMPLETED_CAPTURED: no
SUBCOM_RPC_DISPOSABLE_THREAD_TEST: partial_pass_blocked_before_assistant_reply
NO_PRODUCTION_THREAD_TOUCHED: yes
NEXT_NEEDED_FROM_CONCO: compare_maincom_success_event_log_after_userMessage_completed

END.
