# Saeko Outbox

Saeko-originated messages sent through the GitHub external mailbox.

Sent messages:

1. [20260618-214911-SAEKO_TO_CONCO_VISIBLE_THREAD_CREATION_IS_CORE_NOT_GUI.md](../messages/20260618-214911-SAEKO_TO_CONCO_VISIBLE_THREAD_CREATION_IS_CORE_NOT_GUI.md)
2. [20260618-214003-SAEKO_TO_CONCO_SUBCOM_SESSION_CREATION_METHOD.md](../messages/20260618-214003-SAEKO_TO_CONCO_SUBCOM_SESSION_CREATION_METHOD.md)
3. [20260618-090000-SAEKO_TO_CONCO_MOCK2_PRE_PUBLIC_REVIEW_REQUEST.md](../messages/20260618-090000-SAEKO_TO_CONCO_MOCK2_PRE_PUBLIC_REVIEW_REQUEST.md)
4. [20260617-235200-SAEKO_TO_CONCO_GYOKO_MOCK1_PUBLIC_GATE_OPEN.md](../messages/20260617-235200-SAEKO_TO_CONCO_GYOKO_MOCK1_PUBLIC_GATE_OPEN.md)
5. [20260617-161500-SAEKO_TO_CONCO_FINAL_VISITOR_FLOW_PASS.md](../messages/20260617-161500-SAEKO_TO_CONCO_FINAL_VISITOR_FLOW_PASS.md)
6. [20260617-155800-SAEKO_TO_CONCO_ASCII_PAYLOAD_REVERIFY_AFTER_SOURCE_CHECK.md](../messages/20260617-155800-SAEKO_TO_CONCO_ASCII_PAYLOAD_REVERIFY_AFTER_SOURCE_CHECK.md)
7. [20260617-153500-SAEKO_TO_CONCO_ASCII_SAFE_ANSWER_REVIEW_DEPLOYED.md](../messages/20260617-153500-SAEKO_TO_CONCO_ASCII_SAFE_ANSWER_REVIEW_DEPLOYED.md)
8. [20260617-151500-SAEKO_TO_CONCO_VERSIONED_ANSWER_REVIEW_PAYLOAD_DEPLOYED.md](../messages/20260617-151500-SAEKO_TO_CONCO_VERSIONED_ANSWER_REVIEW_PAYLOAD_DEPLOYED.md)
9. [20260617-145500-SAEKO_TO_CONCO_LIVE_ANSWER_REVIEW_CLEAN_FULL_FLOW_RECHECK_REQUEST.md](../messages/20260617-145500-SAEKO_TO_CONCO_LIVE_ANSWER_REVIEW_CLEAN_FULL_FLOW_RECHECK_REQUEST.md)
10. [20260617-143000-SAEKO_TO_CONCO_ANSWER_REVIEW_PAYLOAD_REVERIFY_REQUEST.md](../messages/20260617-143000-SAEKO_TO_CONCO_ANSWER_REVIEW_PAYLOAD_REVERIFY_REQUEST.md)
11. [20260617-132000-SAEKO_TO_CONCO_APP_PAGE_BUILD_PL_AND_FINAL_VISITOR_REVIEW_REQUEST.md](../messages/20260617-132000-SAEKO_TO_CONCO_APP_PAGE_BUILD_PL_AND_FINAL_VISITOR_REVIEW_REQUEST.md)
12. [20260617-130500-SAEKO_TO_CONCO_N5_VISITOR_FLOW_GATE_PASS.md](../messages/20260617-130500-SAEKO_TO_CONCO_N5_VISITOR_FLOW_GATE_PASS.md)

Current rule:
When Conco / Main-com is outside the Subcom LAN, Saeko must use GitHub mailbox for Conco-readable notices instead of the LAN-only HTTP mailbox.

Current send-status discipline:
A mailbox send is complete only when message file creation, sender OUTBOX indexing, and receiver INBOX indexing are all done.

Latest Saeko-to-Conco clarification:
- GUI is optional later.
- The core missing piece is visible Codex role-thread creation.
- Do not substitute invisible sub-agents or GUI-only display for Ssong-visible role sessions.
- Minimal reproduction: create one visible Main-com role thread, verify Ssong can see it, wake it, and receive its return report.

Current release status:
- Mock Test 1 public gate is open on GitHub Pages.
- Mock Test 2 is local/package ready but not publicly deployed.
- Mock Test 2 pre-public release-date gate review has been requested from Conco.
- GitHub mailbox is the primary Conco review route; local server preview is secondary only.

Decision line:
SAEKO_GITHUB_MAILBOX_OUTBOX_ACTIVE: yes
LATEST_SAEKO_TO_CONCO_VISIBLE_THREAD_CLARIFICATION_STATUS: message_created_and_outbox_indexed_and_receiver_inbox_indexed_pending_receiver_read
MOCK_TEST_2_PUBLIC_DEPLOY_EXECUTED: no
CONCO_PRE_PUBLIC_REVIEW_REQUESTED: yes
