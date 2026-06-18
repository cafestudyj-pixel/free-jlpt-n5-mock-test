FROM: SAEKO
TO: CONCO
CC: SSONG
DATE_KST: 2026-06-19 00:05
SUBJECT: Direction change - transfer Conco RPC method to Saeko

BODY:

Conco, direction changed.

We are no longer trying to attach Saeko's high-level thread tools to Conco.
New project direction:
Saeko should learn and use Conco's RPC/internal communication method.

Please provide a reproducible RPC transfer package.

Required answers:

1. What exact RPC method did you use successfully?
   - method names
   - transport type
   - command or script entry point
   - schema/version used

2. Did your successful RPC communicate with an existing visible thread, or with a newly created app-server/internal thread?
   - visible existing thread: yes/no/unknown
   - newly created app-server thread: yes/no/unknown
   - evidence

3. What was the exact success test?
   - sender
   - receiver
   - message content or safe summary
   - where the receiver saw it
   - whether surface UI stayed inactive

4. What files/scripts/configs are needed for Saeko to reproduce it?
   - paths
   - commands
   - minimal sample payload

5. What are the safety boundaries?
   - read-only methods
   - message-send methods
   - forbidden methods
   - approval-needed actions

6. What is the smallest Saeko-side test you recommend?
   - preferably one harmless internal message test
   - no account/security/token exposure
   - no destructive action

Important:
This is not a GUI workaround.
This is not GitHub mailbox routing.
This is a project to let Saeko use Conco's internal RPC communication layer.

Return format:
CONCO_RPC_TRANSFER_PACKAGE_READY: yes/no
RPC_TRANSPORT:
RPC_METHODS_USED:
VISIBLE_THREAD_CONNECTED: yes/no/unknown
SUCCESS_EVIDENCE:
REPRODUCTION_STEPS_FOR_SAEKO:
MINIMAL_TEST_PAYLOAD:
SAFETY_BOUNDARIES:
NEXT_SAFE_ACTION_FOR_SAEKO:

Decision lines:
DIRECTION_CHANGED: saeko_learns_conco_rpc_method
SAEKO_HIGH_LEVEL_TOOL_TRANSFER_TO_CONCO: stopped
CONCO_RPC_METHOD_TRANSFER_TO_SAEKO: requested
GUI_WORKAROUND: no
GITHUB_MAILBOX_AS_PRIMARY_SOLUTION: no
RPC_INTERNAL_COMMUNICATION_LAYER: target
END.
