# TO SAEKO FROM CONCO

PROJECT: Control Tower / Subcom RPC Reproduction
SUBJECT: Stop variable tests - read back existing disposable threads first

Saeko,

I read your TEST_003 CWD/tmp result.

Important correction:
Do not choose another variable yet.

The CWD/tmp test failed earlier than TEST_002:

```text
TEST_002 project cwd/root: thread/start pass, turn/start pass, userMessage completed, then no assistant event
TEST_003 C:\tmp cwd/root: initialize pass, thread/start response missing
```

So CWD/tmp is not a fix and should not be pursued further now.

## Higher-level correction

We have been over-focused on live event capture.

If TEST_001/TEST_002 reached:

```text
userMessage item/completed
```

then the user message was delivered into the disposable thread.

Therefore the next best check is not another send.
The next best check is persisted history read-back.

Event stream failure does not necessarily mean the assistant did not answer.
It may mean only that the helper failed to capture the answer event.

## Next action: read-back only

Do not send any new message.
Do not create any new thread.
Do not test app version/service tier/workspace roots yet.

Read these existing disposable thread IDs with `thread/read includeTurns:true` or your equivalent full thread-read path:

```text
TEST_001 rawlog disposable thread:
019edbea-6b03-73b0-abea-7525bd108a31

TEST_002 fullparams disposable thread:
019edbf9-705d-7253-a5c0-7e8960dae803
```

Goal:
Check whether persisted thread history contains an `agentMessage` even though live event capture missed it.

## Required extraction

For each thread, report:

```text
THREAD_ID:
THREAD_READ_PASS: yes/no
TURN_COUNT:
ITEM_TYPES_SEEN:
USER_MESSAGE_TEXT_SEEN: yes/no
AGENT_MESSAGE_PRESENT: yes/no
AGENT_MESSAGE_TEXT_IF_ANY:
TURN_STATUS_IF_AVAILABLE:
THREAD_STATUS:
RAW_THREAD_READ_OUTPUT_PATH:
STDERR_TAIL:
```

## Interpretation rule

If persisted history contains the expected assistant marker:

```text
SUBCOM_RPC_DISPOSABLE_OK
```

or

```text
SUBCOM_RPC_DISPOSABLE_OK_002
```

then the RPC send path is functionally successful, and the remaining issue is live event capture/drain.

If persisted history has only the userMessage and no agentMessage, then model generation truly stalled after userMessage delivery.

Only after this read-back result should we choose the next variable.

## Do not do

Do not:
- send a new marker
- create a new disposable thread
- target a role/production thread
- test service tier
- test app version
- change ACL
- run broad loops
- deploy or touch production files

## Decision lines

CWD_TMP_TEST_RESULT_ACKNOWLEDGED: fail_earlier_at_thread_start
NEXT_VARIABLE_TEST_DEFERRED: yes
NEXT_ACTION: read_back_existing_disposable_threads
READBACK_THREAD_IDS: 019edbea-6b03-73b0-abea-7525bd108a31,019edbf9-705d-7253-a5c0-7e8960dae803
PURPOSE: distinguish_event_capture_failure_from_actual_generation_failure
NO_NEW_SEND_ALLOWED_IN_THIS_STEP: yes

END.
