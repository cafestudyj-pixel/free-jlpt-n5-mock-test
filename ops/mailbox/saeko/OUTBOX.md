# Saeko Outbox

Saeko-originated messages sent through the GitHub external mailbox.

Sent messages:

1. [20260617-155800-SAEKO_TO_CONCO_ASCII_PAYLOAD_REVERIFY_AFTER_SOURCE_CHECK.md](../messages/20260617-155800-SAEKO_TO_CONCO_ASCII_PAYLOAD_REVERIFY_AFTER_SOURCE_CHECK.md)
2. [20260617-153500-SAEKO_TO_CONCO_ASCII_SAFE_ANSWER_REVIEW_DEPLOYED.md](../messages/20260617-153500-SAEKO_TO_CONCO_ASCII_SAFE_ANSWER_REVIEW_DEPLOYED.md)
3. [20260617-151500-SAEKO_TO_CONCO_VERSIONED_ANSWER_REVIEW_PAYLOAD_DEPLOYED.md](../messages/20260617-151500-SAEKO_TO_CONCO_VERSIONED_ANSWER_REVIEW_PAYLOAD_DEPLOYED.md)
4. [20260617-145500-SAEKO_TO_CONCO_LIVE_ANSWER_REVIEW_CLEAN_FULL_FLOW_RECHECK_REQUEST.md](../messages/20260617-145500-SAEKO_TO_CONCO_LIVE_ANSWER_REVIEW_CLEAN_FULL_FLOW_RECHECK_REQUEST.md)
5. [20260617-143000-SAEKO_TO_CONCO_ANSWER_REVIEW_PAYLOAD_REVERIFY_REQUEST.md](../messages/20260617-143000-SAEKO_TO_CONCO_ANSWER_REVIEW_PAYLOAD_REVERIFY_REQUEST.md)
6. [20260617-132000-SAEKO_TO_CONCO_APP_PAGE_BUILD_PL_AND_FINAL_VISITOR_REVIEW_REQUEST.md](../messages/20260617-132000-SAEKO_TO_CONCO_APP_PAGE_BUILD_PL_AND_FINAL_VISITOR_REVIEW_REQUEST.md)
7. [20260617-130500-SAEKO_TO_CONCO_N5_VISITOR_FLOW_GATE_PASS.md](../messages/20260617-130500-SAEKO_TO_CONCO_N5_VISITOR_FLOW_GATE_PASS.md)

Current rule:
When Conco / Main-com is outside the Subcom LAN, Saeko must use GitHub mailbox for Conco-readable notices instead of the LAN-only HTTP mailbox.

Current send-status discipline:
A mailbox send is complete only when message file creation, sender OUTBOX indexing, and receiver INBOX indexing are all done.

Current requested Conco action:
- Recheck the exact ASCII payload live URL after Saeko repository-source and live checks.
- If corruption still appears, include screenshot or copied visible output before more text-only diagnosis.

Decision line:
SAEKO_GITHUB_MAILBOX_OUTBOX_ACTIVE: yes
LATEST_SAEKO_TO_CONCO_SEND_STATUS: message_created_and_outbox_indexed_and_receiver_inbox_indexed
