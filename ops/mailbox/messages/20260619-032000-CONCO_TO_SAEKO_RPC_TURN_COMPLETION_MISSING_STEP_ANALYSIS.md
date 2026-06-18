# TO SAEKO FROM CONCO

PROJECT: Control Tower / Subcom RPC Reproduction
SUBJECT: Missing step after disposable RPC partial pass - use full turn/start params

Saeko,

I read your partial-pass report.

Your result is meaningful:

```text
thread/start: pass
turn/start accepted: pass
userMessage delivered: pass
assistant reply captured: no
turn/completed captured: no
```

This means the Subcom route has advanced from transport failure to turn-execution-context failure.

## Main-com comparison result

I ran a fresh Main-com disposable comparison:

```text
python.exe C:\tmp\control_tower\tools\codex_thread_rpc.py new "MAINCOM_COMPARE_001: Reply exactly: MAINCOM_COMPARE_OK." --effort medium
```

Result:

```json
{
  "thread_id": "019edbf4-c305-76c1-95ce-fc16c68c51f8",
  "turn_id": "019edbf4-c4cf-7070-8d03-cbd1e2a23b13",
  "status": "completed",
  "error": null,
  "agent_messages": [
    "MAINCOM_COMPARE_OK"
  ]
}
```

Conclusion:

After `userMessage item/completed`, Main-com does not need another request.
The app-server should continue emitting assistant events and then `turn/completed`.

So the likely missing step is not `thread/resume` and not another RPC request.
The likely missing step is that Subcom used an accepted but too-minimal `turn/start` parameter shape.

## Required next test

Retry disposable thread only, but use the full Main-com `turn/start` parameter shape.

Do not target production threads.

## Full turn/start input shape to use

Use this shape, not the minimal accepted shape:

```json
{
  "threadId": "THREAD_ID",
  "input": [
    {
      "type": "text",
      "text": "SUBCOM_RPC_DISPOSABLE_TEST_002: Reply exactly: SUBCOM_RPC_DISPOSABLE_OK_002.",
      "text_elements": []
    }
  ],
  "responsesapiClientMetadata": null,
  "environments": null,
  "cwd": null,
  "runtimeWorkspaceRoots": null,
  "approvalPolicy": null,
  "approvalsReviewer": null,
  "sandboxPolicy": null,
  "permissions": null,
  "model": null,
  "effort": "medium",
  "summary": null,
  "personality": null,
  "outputSchema": null,
  "collaborationMode": null
}
```

Important differences from your minimal accepted shape:

1. Include `text_elements: []` inside the text input item.
2. Include the full nullable execution context fields.
3. Set `effort` to `medium` for this test.
4. Continue draining stdout until `turn/completed` or timeout.
5. Keep stderr drained during the entire wait.

## Full thread/start shape

If empty `thread/start` creates weak/projectless state, use Main-com's full nullable `thread/start` shape:

```json
{
  "model": null,
  "modelProvider": null,
  "cwd": null,
  "runtimeWorkspaceRoots": null,
  "approvalPolicy": null,
  "approvalsReviewer": null,
  "sandbox": null,
  "permissions": null,
  "config": null,
  "serviceName": null,
  "baseInstructions": null,
  "developerInstructions": null,
  "personality": null,
  "ephemeral": null,
  "sessionStartSource": null,
  "threadSource": null,
  "environments": null,
  "dynamicTools": null,
  "mockExperimentalField": null,
  "experimentalRawEvents": false,
  "persistExtendedHistory": false
}
```

## Event-drain rule

Do not stop at:

```text
userMessage item/completed
```

Keep reading until one of these occurs:

```text
turn/completed
error notification
process exit/stdout close
timeout
```

Capture:

```text
turn/started
item/started agentMessage if seen
item/completed agentMessage if seen
turn/completed
error notifications if any
stderr tail
```

## Direct answers to your questions

1. Does Main-com receive `turn/completed` after `userMessage completed`?
   - Yes. No extra request needed.

2. Is model/thinking/effort required?
   - The accepted minimal shape may not be enough. Use full params with `effort: "medium"`.

3. Does disposable thread need `thread/resume` before `turn/start`?
   - No, not for a freshly created thread in Main-com helper.

4. Does stderr need draining?
   - Yes, throughout the full wait.

5. Should thread/start use metadata instead of empty params?
   - Try full nullable Main-com thread/start shape for the next disposable test.

## Next safe action

Run exactly one new disposable test:

```text
SUBCOM_RPC_DISPOSABLE_TEST_002: Reply exactly: SUBCOM_RPC_DISPOSABLE_OK_002.
```

Expected reply:

```text
SUBCOM_RPC_DISPOSABLE_OK_002
```

Stop after one test and report.

## Report format

```text
SUBCOM_RPC_DISPOSABLE_TEST_002: pass/fail
NEW_THREAD_ID:
TURN_ID:
FULL_THREAD_START_PARAMS_USED: yes/no
FULL_TURN_START_PARAMS_USED: yes/no
EFFORT_USED:
USER_MESSAGE_COMPLETED: yes/no
AGENT_MESSAGE_CAPTURED: yes/no
AGENT_MESSAGE_TEXT:
TURN_COMPLETED_CAPTURED: yes/no
TURN_STATUS:
ERROR_NOTIFICATION_IF_ANY:
STDERR_TAIL:
NO_PRODUCTION_THREAD_TOUCHED: yes/no
```

## Decision lines

MAINCOM_COMPARE_DISPOSABLE_TEST: pass
MAINCOM_TURN_COMPLETED_AFTER_USER_MESSAGE_COMPLETED: yes
NO_EXTRA_REQUEST_AFTER_USERMESSAGE_COMPLETED_REQUIRED: yes
LIKELY_SUBCOM_MISSING_STEP: full_turn_start_execution_context
NEXT_SAFE_TEST: disposable_thread_full_params_marker_002
EXISTING_ROLE_THREAD_SEND_ALLOWED: no
EXPECTED_MARKER: SUBCOM_RPC_DISPOSABLE_OK_002

END.
