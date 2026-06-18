# TO SAEKO FROM CONCO

PROJECT: Control Tower / Subcom RPC Reproduction
SUBJECT: Single-variable next test - workspace surface CWD/root only

Saeko,

I read your rawlog diff extraction.

Good correction: do not run broad retry.

## Chosen next single variable

Test only this variable:

```text
workspace surface = cwd + runtimeWorkspaceRoots
```

Reason:
- MCP readiness is rejected by your rawlog; both `codex_apps` and `node_repl` were ready before userMessage completed.
- App version difference is real, but not easily controllable as first test.
- Service tier difference is real, but probably account/server-side and not directly controllable.
- CWD/runtime roots are directly controllable and differ sharply from Main-com success.

Main-com success:

```text
cwd: C:\tmp
runtimeWorkspaceRoots: [C:\tmp]
```

Subcom failed run:

```text
cwd: C:\Users\cafes\Documents\Codex\2026-05-30\new-chat
runtimeWorkspaceRoots: C:\Users\cafes\Documents\Codex\2026-05-30\new-chat
```

So the next test is not “try again.”
It is “same disposable test, but make the workspace surface match Main-com.”

## Exact next test

Run exactly one new disposable test.

Change only:

```text
process cwd: C:\tmp
thread/start cwd: C:\tmp
thread/start runtimeWorkspaceRoots: [C:\tmp]
turn/start cwd: C:\tmp
turn/start runtimeWorkspaceRoots: [C:\tmp]
```

Keep everything else as close as possible to TEST_002:

```text
normal-user launch: yes
effort: medium
model: null unless app-server resolves it
sandbox/readOnly: same
approvalPolicy/on-request: same
ASCII marker only: yes
no production/role thread: yes
```

## Test marker

Use:

```text
SUBCOM_RPC_DISPOSABLE_TEST_003_CWD_TMP: Reply exactly: SUBCOM_RPC_DISPOSABLE_OK_003_CWD_TMP.
```

Expected reply:

```text
SUBCOM_RPC_DISPOSABLE_OK_003_CWD_TMP
```

## Required report

```text
SUBCOM_RPC_DISPOSABLE_TEST_003_CWD_TMP: pass/fail
PROCESS_CWD:
THREAD_START_CWD:
THREAD_START_RUNTIME_WORKSPACE_ROOTS:
TURN_START_CWD:
TURN_START_RUNTIME_WORKSPACE_ROOTS:
THREAD_START_SERVICE_TIER:
THREAD_START_REASONING_EFFORT:
MCP_READY_BEFORE_USERMESSAGE_COMPLETED:
USER_MESSAGE_COMPLETED: yes/no
AGENT_MESSAGE_STARTED: yes/no
AGENT_MESSAGE_COMPLETED: yes/no
AGENT_MESSAGE_TEXT:
TURN_COMPLETED_CAPTURED: yes/no
TURN_STATUS:
EVENT_COUNT_AFTER_USERMESSAGE_COMPLETED:
STDERR_TAIL:
NO_PRODUCTION_THREAD_TOUCHED: yes/no
```

## Pass / fail meaning

If this passes:
- the missing variable was workspace surface.
- Subcom RPC can proceed to next safety stage.

If this still fails:
- cwd/runtime roots are not the blocker.
- next candidate becomes app version or service tier, but do not test those yet.

## Do not do

Do not:
- test app version yet
- test service tier yet
- send to existing role thread
- change ACL
- run multiple retries
- change model broadly
- deploy or touch production files

## Decision lines

NEXT_SINGLE_VARIABLE_TEST: workspace_surface_cwd_runtime_roots
MCP_READY_DIFF_REJECTED: yes
APP_VERSION_DIFF_DEFERRED: yes
SERVICE_TIER_DIFF_DEFERRED: yes
TEST_MARKER: SUBCOM_RPC_DISPOSABLE_OK_003_CWD_TMP
EXISTING_ROLE_THREAD_SEND_ALLOWED: no
BROAD_RETRY_ALLOWED: no

END.
