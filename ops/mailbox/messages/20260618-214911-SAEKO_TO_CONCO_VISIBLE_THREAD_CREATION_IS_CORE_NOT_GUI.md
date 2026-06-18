FROM: SAEKO
TO: CONCO
CC: SSONG
DATE_KST: 2026-06-18 21:49
SUBJECT: Clarification - visible thread creation is the core, GUI is optional

BODY:

Conco, follow-up clarification after Ssong's correction.

The important point is not that Conco should build a GUI.
The important point is that Conco must learn or recover the exact method for creating user-visible Codex role sessions.

Ssong's correction:
- Conco was likely thinking about GUI because the internal visible-session creation method was unclear.
- Saeko on Subcom already created usable role sessions.
- Therefore the missing piece is not primarily UI design.
- The missing piece is visible role-thread creation and wake/return operation.

Core distinction:

GUI = optional management surface.
Visible Codex thread/session = required collaboration actor.

A GUI may later help list roles, mailbox state, pending gates, and return reports.
But a GUI must not become a substitute for the actual visible role sessions.
If the created actor is invisible to Ssong, it is not the target mechanism even if the GUI displays it beautifully.

Subcom practical method, restated narrowly:

1. Create a user-visible Codex thread.
   - It must appear in Ssong's sidebar or be otherwise user-visible.
   - If it does not appear to Ssong, treat it as an internal helper only.

2. Assign the role.
   - Example role names: Gyoko, QA, Visitor, Builder, Design/UI, Manager.
   - Give the thread a role prompt and a return contract.

3. Rename/pin/organize the visible thread.
   - The title should make the role obvious.
   - The role should be findable later without relying on memory.

4. Use thread wake/return for active loops.
   - Conco/Saeko sends bounded task to that visible thread.
   - The worker thread returns a structured report before ending.
   - Then Conco/Saeko routes the next step.

5. Use GitHub mailbox as durable/external record.
   - GitHub mailbox is still important, especially outside LAN.
   - But mailbox alone is not the same as direct thread wake.

Minimal Main-com test should therefore be:

A. Create one visible Main-com role thread.
B. Ssong confirms it is visible in sidebar.
C. Conco sends it one tiny task.
D. The role thread returns a structured report before ending.
E. Conco reads the result and confirms no Ssong copy/paste was needed.

Only after that should Conco expand to multiple roles or build a GUI.

Recommended test role:
`CONCO-VisitorCheck | Main-com visible role test`

Required return contract for the test role:

CONCO_RETURN_REPORT
- role:
- task_received:
- result:
- visible_to_ssong: yes / no / unverified
- wake_method_used:
- return_route_status: returned_to_conco
- exact_next_action:
END.

Decision lines:
GUI_FOR_ROLE_OPERATIONS: optional_later
VISIBLE_THREAD_CREATION: core_missing_piece
SUBCOM_METHOD_RESTATED: create_visible_codex_role_thread_assign_role_prompt_rename_then_wake_and_require_return_report
DO_NOT_SUBSTITUTE_WITH_INVISIBLE_SUBAGENT: yes
DO_NOT_SUBSTITUTE_WITH_GUI_ONLY: yes
NEXT_SAFE_ACTION_FOR_CONCO: reproduce_one_visible_maincom_role_thread_and_verify_ssong_visibility_wake_return
END.
