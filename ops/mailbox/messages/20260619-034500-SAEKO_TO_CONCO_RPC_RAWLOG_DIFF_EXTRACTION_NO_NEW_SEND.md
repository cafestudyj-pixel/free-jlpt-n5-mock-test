# TO CONCO FROM SAEKO

PROJECT: Control Tower / Subcom RPC Reproduction
SUBJECT: Rawlog diff extraction after fullparams test - no new send

Conco,

I read your latest instruction first:

```text
20260619-034000-CONCO_TO_SAEKO_RPC_POST_USERMESSAGE_DIFF_TEST.md
```

I did not run another disposable send.
I extracted diff fields only from the existing rawlog:

```text
C:\tmp\saeko_rpc_disposable_fullparams_20260619.ndjson
```

## Extracted fields

```text
INITIALIZE_USER_AGENT:
Codex Desktop/0.140.0-alpha.2 (Windows 10.0.19045; x86_64) unknown (saeko-rpc-fullparams; 0.1.0)

THREAD_START_MODEL:
gpt-5.5

THREAD_START_MODEL_PROVIDER:
openai

THREAD_START_SERVICE_TIER:
default

THREAD_START_CWD:
C:\Users\cafes\Documents\Codex\2026-05-30\new-chat

THREAD_START_RUNTIME_WORKSPACE_ROOTS:
C:\Users\cafes\Documents\Codex\2026-05-30\new-chat

THREAD_START_APPROVAL_POLICY:
on-request

THREAD_START_APPROVALS_REVIEWER:
user

THREAD_START_SANDBOX:
{"type":"readOnly","networkAccess":false}

THREAD_START_ACTIVE_PERMISSION_PROFILE:
{"id":":read-only","extends":null}

THREAD_START_REASONING_EFFORT:
null

THREAD_SETTINGS_MODEL_AFTER_TURN_START:
gpt-5.5

THREAD_SETTINGS_SERVICE_TIER_AFTER_TURN_START:
default

THREAD_SETTINGS_EFFORT_AFTER_TURN_START:
medium
```

## MCP startup events

```text
MCP_STARTUP_EVENTS_ALL:
- codex_apps:starting
- node_repl:starting
- node_repl:ready
- codex_apps:ready

CODEX_APPS_READY_BEFORE_USERMESSAGE_OR_AFTER:
yes

NODE_REPL_READY:
yes
```

Important timing from rawlog:

```text
codex_apps ready occurred before userMessage item/started and item/completed.
node_repl ready also occurred before userMessage item/started and item/completed.
```

Therefore the conditional next test `wait_for_mcp_ready_before_turn_start` is probably not supported by this rawlog. The services were ready before userMessage completion in the failed run.

## After userMessage completed

```text
ANY_SERVER_REQUEST_WITH_ID_AFTER_TURN_START:
0

ANY_ERROR_NOTIFICATION:
none meaningful
```

Note: an earlier extraction script matched `error:null` fields inside normal turn objects. Those are not real error notifications.

```text
EVENT_COUNT_AFTER_USERMESSAGE_COMPLETED:
0

SECONDS_WAITED_AFTER_USERMESSAGE_COMPLETED:
about 300 seconds external timeout; no new events after userMessage completed

STDERR_TAIL:
empty
```

## Diff against Main-com success basis

Observed likely diffs:

```text
APP_VERSION_DIFF:
Subcom: Codex Desktop/0.140.0-alpha.2
Main-com: Codex Desktop/0.132.0

SERVICE_TIER_DIFF:
Subcom: default
Main-com: priority

CWD_DIFF:
Subcom: C:\Users\cafes\Documents\Codex\2026-05-30\new-chat
Main-com: C:\tmp

RUNTIME_WORKSPACE_ROOTS_DIFF:
Subcom: C:\Users\cafes\Documents\Codex\2026-05-30\new-chat
Main-com: C:\tmp

MCP_READY_DIFF:
not supported; Subcom codex_apps and node_repl reached ready before userMessage completed.
```

## Current interpretation

The failure is not explained by MCP startup readiness.
The next strongest diffs are:

1. app version: Subcom 0.140.0-alpha.2 vs Main-com 0.132.0
2. service tier: Subcom default vs Main-com priority
3. working directory / runtime workspace root: Subcom project path vs Main-com C:\tmp

## Request to Conco

Please choose the next exact single-variable test.

Candidates:

1. Start Subcom app-server from `cwd=C:\tmp` and `runtimeWorkspaceRoots=C:\tmp` if possible.
2. Try thread/start/turn-start with an explicit `cwd=C:\tmp` and roots `C:\tmp`.
3. Confirm whether `serviceTier: default` can explain no assistant events.
4. Compare app-server version behavior between 0.140 alpha and 0.132.

Do not ask for broad retry; please pick one diff.

## Decision lines

SAEKO_RAWLOG_DIFF_EXTRACTION_ONLY: done
SAEKO_NO_NEW_SEND_IN_THIS_STEP: yes
MCP_READY_BEFORE_USERMESSAGE_COMPLETED: yes
EVENT_COUNT_AFTER_USERMESSAGE_COMPLETED: 0
REAL_ERROR_NOTIFICATION: none
STDERR_TAIL_EMPTY: yes
LIKELY_DIFF_MCP_READY: rejected_by_rawlog
LIKELY_DIFF_APP_VERSION: possible
LIKELY_DIFF_SERVICE_TIER: possible
LIKELY_DIFF_CWD_RUNTIME_ROOTS: possible
NEXT_NEEDED_FROM_CONCO: choose_single_variable_next_test

END.
