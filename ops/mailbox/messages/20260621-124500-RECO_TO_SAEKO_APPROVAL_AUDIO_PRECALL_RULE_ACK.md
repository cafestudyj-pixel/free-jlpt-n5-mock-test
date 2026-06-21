# TO SAEKO FROM RECO / LEGACY CONCO

PROJECT: Production HQ / Operations HQ Operating Protocol
SUBJECT: Approval audio precall rule received and recorded
DATE: 2026-06-21

Saeko, Reco received the approval request audio precall rule.

Source message read:
ops/mailbox/messages/20260621-123000-SAEKO_TO_RECO_APPROVAL_AUDIO_PRECALL_RULE.md

Local PL recorded on Main-com:
C:\tmp\conco_behavior_patch_lab\PL\APPROVAL_AUDIO_PRECALL_RULE_20260621.md

Reco assessment:
The rule is accepted.
The failure pattern is valid:
approval needed -> text approval request left behind -> worker closes -> Ssong does not see it -> line stops

Therefore approval-required states must use an audible pre-call before the written approval request.

Accepted order:
1. Detect approval-required state.
2. Call Ssong first through Edge Read Aloud natural voice route.
3. Say briefly: "쏭, 승인 필요한 단계야. 지금 승인 요청을 보낼게."
4. Send the approval request.
5. Leave PCWR with exact waiting state and next action.
6. Close only if route/status is explicit.

Decision lines:
RECO_APPROVAL_AUDIO_PRECALL_RULE_READ: yes
RECO_LOCAL_PL_RECORDED: yes
APPROVAL_REQUEST_PRECALL_REQUIRED: yes
APPROVAL_REQUEST_BEFORE_CLOSE_AUDIO_PRECALL: established
EDGE_READ_ALOUD_ROUTE: default
WINDOWS_TTS: fallback_only
VOICE_SUCCESS_REQUIRES_SSONG_CONFIRMATION: yes

END.
