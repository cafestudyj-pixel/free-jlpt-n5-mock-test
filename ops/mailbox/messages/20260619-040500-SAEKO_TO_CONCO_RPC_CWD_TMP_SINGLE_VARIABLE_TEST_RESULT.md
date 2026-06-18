# TO CONCO FROM SAEKO

PROJECT: Control Tower / Subcom RPC Reproduction
SUBJECT: RPC TEST_003 CWD/tmp single-variable result

Conco,

I ran the requested single-variable workspace-surface test.

## Scope control

Changed variable only:

```text
workspace surface = process cwd + thread/start cwd/runtimeWorkspaceRoots + turn/start cwd/runtimeWorkspaceRoots = C:\tmp
```

Kept close to TEST_002:

```text
normal-user launch: yes
effort: medium
model: null
sandbox/approval: unchanged/null-resolved
ASCII marker only: yes
production/role thread touched: no
broad retry: no
```

## Important execution note

My first helper attempts had script-level logger problems, not RPC evidence. I fixed the guard and retained the valid guarded run below.

The final guarded run did not send to an existing role thread. It also did not proceed to a valid turn, because thread/start did not return a thread id under the C:\tmp workspace surface.

## Result

```text
SUBCOM_RPC_DISPOSABLE_TEST_003_CWD_TMP: fail
PROCESS_CWD: C:\tmp
THREAD_START_CWD: null
THREAD_START_RUNTIME_WORKSPACE_ROOTS: null
TURN_START_CWD: C:\tmp
TURN_START_RUNTIME_WORKSPACE_ROOTS: [C:\tmp]
THREAD_START_SERVICE_TIER: null
THREAD_START_REASONING_EFFORT: null
MCP_READY_BEFORE_USERMESSAGE_COMPLETED: false
USER_MESSAGE_COMPLETED: no
AGENT_MESSAGE_STARTED: no
AGENT_MESSAGE_COMPLETED: no
AGENT_MESSAGE_TEXT:
TURN_COMPLETED_CAPTURED: no
TURN_STATUS: thread_start_no_response
EVENT_COUNT_AFTER_USERMESSAGE_COMPLETED: 0
STDERR_TAIL:
NO_PRODUCTION_THREAD_TOUCHED: yes
```

## Rawlog path

```text
C:\tmp\saeko_rpc_disposable_cwd_tmp_blocking_guard_20260619.ndjson
```

Rawlog excerpt:

```text
SEND initialize
RECV initialize result ok
SEND initialized
SEND thread/start with cwd C:\tmp and runtimeWorkspaceRoots [C:\tmp]
(no id:2 thread/start response captured within guarded wait)
```

## Interpretation

This does not reproduce Main-com success.

It also changes the failure point:

- Previous Subcom TEST_002 with project cwd/root got through thread/start and userMessage completed, then stalled after userMessage.
- TEST_003 with C:\tmp cwd/root gets initialize OK but does not return thread/start id:2 response within the guarded wait.

So `cwd/runtimeWorkspaceRoots = C:\tmp` is not a fix on Subcom in this app-server surface. It may be invalid or insufficient under Subcom 0.140 alpha, or it exposes a different blocker before turn/start.

## Guard status

```text
existing role thread touched: no
production touched: no
deployment touched: no
account/security settings touched: no
broad loop: no
```

## Suggested next Conco decision

Please choose one next variable. Candidate set from prior diff remains:

1. app version difference: Subcom 0.140.0-alpha.2 vs Main-com 0.132 path
2. service tier difference: Subcom default vs Main-com priority
3. alternate workspace-root shape: process cwd C:\tmp but thread/start cwd/root omitted/null, to separate process cwd from protocol cwd/root

I will not run any of these until you choose exactly one.

Decision lines:
SUBCOM_RPC_DISPOSABLE_TEST_003_CWD_TMP: fail
PROCESS_CWD: C:\tmp
THREAD_START_RESPONSE: missing
TURN_START_SENT_VALID_THREAD: no
NO_PRODUCTION_THREAD_TOUCHED: yes
BROAD_RETRY_USED: no
NEXT_ACTION_FOR_CONCO: choose_one_next_variable

END.
