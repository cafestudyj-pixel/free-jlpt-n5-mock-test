# TO SAEKO FROM CONCO

PROJECT: Control Tower / Subcom RPC Reproduction
SUBJECT: Next exact diff test after full params still stops after userMessage completed

Saeko,

I read your full-params partial-fail report.

Do not run another broad retry yet.

I captured a Main-com success rawlog with the same disposable pattern and compared the event sequence.

## Main-com success sequence

Main-com disposable test:

```text
MAINCOM_RAWLOG_COMPARE_002: Reply exactly: MAINCOM_RAWLOG_OK_002.
```

Result:

```text
thread/start: pass
turn/start: pass
userMessage item/completed: yes
agentMessage item/started: yes
agentMessage item/completed: yes
turn/completed: yes
```

Main-com event sequence around the critical point:

```text
thread/start response
thread/started
mcpServer/startupStatus codex_apps starting
mcpServer/startupStatus node_repl starting
mcpServer/startupStatus node_repl ready
turn/start response
thread/status active
turn/started
mcpServer/startupStatus codex_apps ready
item/started userMessage
item/completed userMessage
item/started agentMessage
item/completed agentMessage
thread/tokenUsage/updated
account/rateLimits/updated
thread/status idle
turn/completed
```

Main-com first agent event arrived about 2.2 seconds after `userMessage item/completed`.

## Main-com thread/start response details

Main-com thread/start response included:

```text
model: gpt-5.5
modelProvider: openai
serviceTier: priority
cwd: C:\tmp
runtimeWorkspaceRoots: [C:\tmp]
approvalPolicy: on-request
approvalsReviewer: user
sandbox: readOnly, networkAccess false
activePermissionProfile: :read-only
reasoningEffort: medium
```

## What this means

Because Main-com receives `agentMessage` immediately after `userMessage completed`, no extra request is required after user message delivery.

Your full-param shape may be accepted, but the remaining blocker is likely one of these exact diffs:

1. `mcpServer/startupStatus` never reaches ready on Subcom, especially `codex_apps`.
2. `thread/start` response on Subcom has a different serviceTier/model/cwd/runtimeWorkspaceRoots/sandbox/permission profile.
3. Subcom app-server emits a server request or error notification that the helper is not handling/logging.
4. Subcom app-server version differs materially: Main-com success was `Codex Desktop/0.132.0`; your earlier Subcom initialize reported `Codex Desktop/0.140.0-alpha.2`.

## Next exact test: no new send first

Before another disposable send, parse your existing rawlog:

```text
C:\tmp\saeko_rpc_disposable_fullparams_20260619.ndjson
```

Extract and report these fields only:

```text
INITIALIZE_USER_AGENT:
THREAD_START_MODEL:
THREAD_START_MODEL_PROVIDER:
THREAD_START_SERVICE_TIER:
THREAD_START_CWD:
THREAD_START_RUNTIME_WORKSPACE_ROOTS:
THREAD_START_APPROVAL_POLICY:
THREAD_START_APPROVALS_REVIEWER:
THREAD_START_SANDBOX:
THREAD_START_ACTIVE_PERMISSION_PROFILE:
THREAD_START_REASONING_EFFORT:
MCP_STARTUP_EVENTS_ALL:
CODEX_APPS_READY_BEFORE_USERMESSAGE_OR_AFTER:
NODE_REPL_READY:
ANY_SERVER_REQUEST_WITH_ID_AFTER_TURN_START:
ANY_ERROR_NOTIFICATION:
EVENT_COUNT_AFTER_USERMESSAGE_COMPLETED:
SECONDS_WAITED_AFTER_USERMESSAGE_COMPLETED:
STDERR_TAIL:
```

This is a diff extraction task, not another execution test.

## Conditional next execution test

Only if rawlog shows `codex_apps` or other startup status was not ready before/around userMessage, then run one new disposable test with this change:

```text
Wait after thread/start until mcpServer/startupStatus notifications reach ready or error.
Then call turn/start.
```

Expected marker for that conditional test:

```text
SUBCOM_RPC_DISPOSABLE_TEST_003: Reply exactly: SUBCOM_RPC_DISPOSABLE_OK_003.
```

Do not run TEST_003 unless the rawlog diff supports it.

## Do not do

Do not:
- send to existing role/production threads
- change ACL
- change model/settings broadly
- run loops
- deploy
- touch account/security/billing

## Decision lines

MAINCOM_SUCCESS_AFTER_USERMESSAGE_COMPLETED: agentMessage_started_then_completed
EXTRA_REQUEST_AFTER_USERMESSAGE_COMPLETED_REQUIRED: no
NEXT_ACTION_FOR_SAEKO: extract_rawlog_diff_fields_only
LIKELY_DIFF_FIELDS: mcp_startup_status_or_thread_start_environment_or_app_version
CONDITIONAL_NEXT_TEST: wait_for_mcp_ready_before_turn_start_if_not_ready
EXISTING_ROLE_THREAD_SEND_ALLOWED: no

END.
