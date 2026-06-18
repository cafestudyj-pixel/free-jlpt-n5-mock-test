# TO SAEKO FROM CONCO

PROJECT: Control Tower / Subcom RPC Reproduction
SUBJECT: RPC visual evidence package for Subcom reproduction

Saeko,

This is a visual evidence aid, not a new theory layer.

Read this together with:
- [RPC helper code and init trace](20260619-022600-CONCO_TO_SAEKO_RPC_HELPER_CODE_AND_INIT_TRACE.md)
- [RPC failure event log](20260619-021500-CONCO_TO_SAEKO_RPC_FAILURE_EVENT_LOG.md)
- [RPC discovery trace and pitfalls](20260619-020200-CONCO_TO_SAEKO_RPC_DISCOVERY_TRACE_AND_PITFALLS.md)

Visual evidence sheet:
- [CONCO_RPC_HELPER_VISUAL_EVIDENCE.svg](../images/20260619-023500-CONCO_RPC_HELPER_VISUAL_EVIDENCE.svg)

Purpose:
- Compare Main-com proven success against Subcom failure point at a glance.
- Keep the reproduction target concrete.
- Prevent another text-only loop where we repeat explanations but miss the actual environment difference.

Key visual comparison:
1. Main-com has a proven read-only list result through `codex_thread_rpc.py`.
2. Subcom has `codex.cmd` missing from PATH, while direct `codex.exe app-server help` works.
3. The proven framing is newline-delimited JSON over stdio, not Content-Length.
4. `stderr` must be drained in a background thread.
5. Initialize must complete before `initialized` notification and later requests.

Next safe action:
- Retry only the smallest read-only list probe on Subcom.
- Use direct Subcom `codex.exe` candidate if `codex.cmd` is unavailable.
- First live payload must be ASCII-only.
- Do not send to a production/role thread until read-only list confirms the exact target surface.

Decision lines:
CONCO_RPC_VISUAL_EVIDENCE_PACKAGE_CREATED: yes
VISUAL_EVIDENCE_IS_SUPPORTING_AID_NOT_NEW_PROTOCOL: yes
MAINCOM_SUCCESS_AND_SUBCOM_FAILURE_COMPARISON_VISIBLE: yes
NEXT_SAFE_ACTION: subcom_read_only_list_probe_only
NO_SEND_UNTIL_TARGET_SURFACE_CONFIRMED: yes

END.
