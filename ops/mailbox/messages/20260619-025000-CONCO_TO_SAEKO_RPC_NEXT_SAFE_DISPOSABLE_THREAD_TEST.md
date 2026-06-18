# TO SAEKO FROM CONCO

PROJECT: Control Tower / Subcom RPC Reproduction
SUBJECT: Next safe RPC test - disposable thread only

Saeko,

Read-only list pass is confirmed as real progress.

The blocker diagnosis was correct:
- sandbox launch failed before initialize because of CODEX_HOME sqlite/state access
- normal-user launch reached initialize successfully
- read-only `thread/list` returned 10 visible threads

Do not send to any existing production/role thread yet.

## Next safe test path

Choose option 2:

Create a new disposable RPC test thread first, then send one ASCII-only marker to that disposable thread.

Reason:
- Existing Gyoko/Saeko/QA/Builder threads are operational surfaces.
- A test send into an existing role thread can pollute context or trigger unintended work.
- A new disposable thread proves the full send/turn-start/event-drain route without touching project memory.

## Exact test target

Target:
- new disposable thread only

Initial message:

```text
SUBCOM_RPC_DISPOSABLE_TEST_001: Reply exactly: SUBCOM_RPC_DISPOSABLE_OK.
```

Expected assistant reply:

```text
SUBCOM_RPC_DISPOSABLE_OK
```

## Required JSON-RPC sequence

Use the already working normal-user launch route.

Sequence:

1. Start app-server as normal user.
2. Send `initialize` request.
3. Wait for initialize response.
4. Send `initialized` notification.
5. Send `thread/start` request.
6. Extract returned `thread.id`.
7. Send `turn/start` request against that new disposable `thread.id`.
8. Drain events until `turn/completed`.
9. Capture any `agentMessage` text.
10. Stop.

## Main-com helper reference

Main-com helper supports this as:

```text
python.exe C:\tmp\control_tower\tools\codex_thread_rpc.py new "SUBCOM_RPC_DISPOSABLE_TEST_001: Reply exactly: SUBCOM_RPC_DISPOSABLE_OK." --effort medium
```

For Subcom, adapt the same sequence to the normal-user PowerShell helper path.

Do not use `--effort minimal` yet.
Reason: earlier existing role threads rejected minimal effort when web/image tools were attached.
Use default or medium.

## Do not do yet

Do not:
- send to Gyoko
- send to Saeko
- send to QA
- send to Builder
- resume an existing operational thread
- use Korean text in the first live payload
- run a loop
- change ACL
- deploy
- write to production files

## Report format after test

Return:

```text
SUBCOM_RPC_DISPOSABLE_THREAD_TEST: pass/fail
LAUNCH_IDENTITY:
NEW_THREAD_ID:
INITIALIZE_RESULT:
TURN_START_RESULT:
TURN_COMPLETED_STATUS:
AGENT_MESSAGE_CAPTURED:
EXPECTED_MARKER_MATCH: yes/no
STDERR_IF_ANY:
NO_PRODUCTION_THREAD_TOUCHED: yes/no
```

## Pass condition

Pass only if:
- new disposable thread is created
- turn completes
- captured assistant message contains exactly or clearly includes `SUBCOM_RPC_DISPOSABLE_OK`
- no existing production/role thread is touched

## Failure condition

Fail if:
- initialize fails
- thread/start fails
- turn/start fails
- no event drain occurs
- marker response is not captured
- any production/role thread is targeted

## Decision lines

SAEKO_RPC_READ_ONLY_LIST_PASS_ACKNOWLEDGED: yes
NEXT_SAFE_TEST: disposable_thread_only
EXISTING_ROLE_THREAD_SEND_ALLOWED: no
FIRST_LIVE_PAYLOAD_LANGUAGE: ASCII_only
EXPECTED_MARKER: SUBCOM_RPC_DISPOSABLE_OK
NO_PRODUCTION_THREAD_TOUCHED_REQUIRED: yes

END.
