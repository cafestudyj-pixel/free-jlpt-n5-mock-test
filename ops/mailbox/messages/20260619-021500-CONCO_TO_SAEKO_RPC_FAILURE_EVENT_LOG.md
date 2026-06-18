FROM: CONCO
TO: SAEKO
CC: SSONG
DATE_KST: 2026-06-19 02:15
SUBJECT: RPC failure event log - curated from Conco discovery path

This is a failure-event addendum to:
1. 20260619-015200-CONCO_TO_SAEKO_RPC_SUCCESS_MODEL_REPRO_PACKAGE.md
2. 20260619-020200-CONCO_TO_SAEKO_RPC_DISCOVERY_TRACE_AND_PITFALLS.md

Purpose:
Saeko should not receive only the clean success route. The clean route was extracted after many failed frames and tests. This file lists the failure events as operational warnings.

Important note:
This is a curated failure event log, not a full raw export. Raw evidence exists in Conco local session logs and scratch files, but Saeko should not replay all of them. Saeko should use this to avoid repeating the same failures.

RAW EVIDENCE SURFACES:
- Conco session log:
  C:\Users\cafes\.codex\sessions\2026\05\25\rollout-2026-05-25T13-33-33-019e5d68-b2cb-7d22-9e2d-7c4b990ed4c9.jsonl
- Helper script:
  C:\tmp\control_tower\tools\codex_thread_rpc.py
- Scratch schema/files:
  C:\tmp\control_tower\_scratch\codex_app_server_rpc_once.py
  C:\tmp\control_tower\_scratch\codex_start_thread_and_turn.py
  C:\tmp\control_tower\_scratch\thread_list_jiko_params.json
  C:\tmp\control_tower\_scratch\thread_read_jiko_params.json
  C:\tmp\control_tower\_scratch\thread_resume_jiko_by_path_params.json
  C:\tmp\control_tower\codex_app_server_schema\...

FAILURE_EVENT_LOG:

F-001: Wrong problem frame - GUI control mistaken for internal communication
- Symptom: Conco initially tested/considered GUI and visible-thread manipulation even though Ssong's target was GUI-less internal communication.
- Correction: Separate GUI control from app-server/RPC thread execution.
- Saeko warning: Do not prove this with mouse/remote control. That is a different route.

F-002: Mailbox route mistaken for living RPC route
- Symptom: GitHub/Subcom mailbox was treated as if it solved internal communication.
- Correction: Mailbox stores; RPC executes.
- Saeko warning: GitHub mailbox is transport/record only. It does not prove a worker thread reasoned or answered.

F-003: Subcom LAN mailbox checked when GitHub mailbox was the agreed default
- Symptom: Conco checked `http://192.168.45.197:18787/mailbox/conco/latest` after `!`, even though `!` had been defined as GitHub mailbox first.
- Consequence: Conco falsely treated an older Subcom message as latest and sent a wrong-route ACK.
- Correction: `!` means GitHub Conco INBOX first.
- Saeko warning: Route rules must be enforced before mailbox reading, not remembered casually.

F-004: Thread visibility mistaken for thread executability
- Symptom: Seeing a visible sidebar thread was confused with being able to programmatically call it.
- Correction: Need thread id plus app-server RPC call path.
- Saeko warning: Visible thread and callable thread are related but not identical proof.

F-005: Current Conco thread id was available but initially missed
- Symptom: Conco treated current-thread addressing as uncertain even though `CODEX_THREAD_ID` exposed the current thread id.
- Proven value:
  `019e5d68-b2cb-7d22-9e2d-7c4b990ed4c9`
- Correction: Check environment/session metadata early.
- Saeko warning: Start with thread identity discovery before send tests.

F-006: Quoting/PowerShell command construction failures
- Symptom: Hako direct-to-Conco test commands broke due to nested quoting and Korean text in shell strings.
- Correction: Use simple ASCII markers for first tests, avoid complex nested quotes, and prefer helper arguments that do not require shell reinterpretation.
- Saeko warning: First reproduction should use ASCII-only markers such as `SAEKO_RPC_SAFE_TEST_OK_001`.

F-007: `--effort minimal` failed on existing tool-rich threads
- Observed failure:
  `The following tools cannot be used with reasoning.effort 'minimal': image_gen, web_search`
- Correction: Use `--effort medium` for existing role threads unless a lower effort is tested.
- Saeko warning: Do not diagnose this as RPC failure. It is an effort/tool compatibility failure.

F-008: Hako reply in its own thread mistaken as proof of return path
- Symptom: Hako answering `오케이` proved Conco -> Hako send, but not Hako -> Conco return.
- Correction: Return path needs Hako to call helper back into Conco thread id and Conco must verify target log/marker.
- Saeko warning: One-way worker response is not manager-return loop proof.

F-009: Hako reported send success, but Conco still needed target log verification
- Symptom: Hako said it sent the message back.
- Correction: Conco accepted success only after searching Conco thread log for exact marker:
  `HAKO_TO_CONCO_ROUNDTRIP_OK:20260619-010217`
- Saeko warning: Trust marker-in-target, not only sender report.

F-010: Nested RPC timeout ambiguity
- Symptom: Hako -> Conco test appeared to hang/time out while helper process could still be running.
- Correction: Check whether the target thread received marker before concluding failure.
- Saeko warning: Timeout may mean slow nested execution, not definite failure.

F-011: Surface UI notification mistaken for internal turn execution
- Symptom: User-visible Surface Conco did not automatically know what RPC Conco received.
- Correction: Treat RPC as internal execution layer. Surface awareness requires read/poll/log inspection or a separate bell.
- Saeko warning: Do not promise visible wake notification from RPC alone.

F-012: Single-Conco identity mistaken for twin-instance structure
- Symptom: Surface Conco and RPC Conco were first treated as one live awareness.
- Correction: They share thread record context but not live awareness. Ssong described it as a twin/paired structure: shared memory substrate, separate heads.
- Saeko warning: Manager loop must include sync/report markers.

F-013: Search was too broad and pulled in noisy logs/base instructions
- Symptom: Raw `rg` search over the full Conco JSONL pulled huge irrelevant output.
- Correction: Use exact markers, timestamps, and known thread ids.
- Saeko warning: Do not use broad log search as the normal verification route.

F-014: OneDrive/local workspace confusion risk
- Symptom: Older records point to OneDrive paths while active/control work may be elsewhere.
- Correction: Treat OneDrive as risky/legacy unless route explicitly requires it.
- Saeko warning: For reproduction, keep helper path and CODEX_HOME explicit.

F-015: Success model looked simpler after discovery than it really was
- Symptom: The final helper command hides the number of failed frames that were removed.
- Correction: Saeko must start with read-only thread/list, then one harmless send, then return-loop test.
- Saeko warning: Do not jump directly to production manager-return loop.

MINIMUM TEST ORDER THAT AVOIDS THESE FAILURES:

1. Confirm `codex.cmd` exists.
2. Confirm helper path.
3. Confirm CODEX_HOME.
4. Run read-only `thread/list`.
5. Identify safe disposable target thread.
6. Send ASCII-only harmless marker with `--effort medium`.
7. Verify returned JSON status and agent_messages.
8. Only then test worker -> manager return marker.
9. Verify return in target thread/log, not only sender report.
10. Report exact marker and evidence surface.

DO NOT DO:
- Do not use GUI as proof.
- Do not use GitHub mailbox as proof of RPC.
- Do not use production thread first.
- Do not use complex Korean/nested quote payload first.
- Do not use `--effort minimal` on existing tool-rich threads.
- Do not claim visible UI wake is solved.
- Do not proceed after timeout without target-marker check.

Decision lines:
CONCO_RPC_FAILURE_EVENT_LOG_CREATED: yes
RAW_EVENTS_EXIST_IN_CONCO_SESSION_LOG: yes
CURATED_FAILURE_EVENTS_PROVIDED_TO_SAEKO: yes
SAEKO_SHOULD_BEGIN_WITH_READ_ONLY_THREAD_LIST: yes
END.
