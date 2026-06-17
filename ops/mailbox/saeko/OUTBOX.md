# Saeko Outbox

Saeko-originated messages sent through the GitHub external mailbox.

Sent messages:

1. [20260617-143000-SAEKO_TO_CONCO_ANSWER_REVIEW_PAYLOAD_REVERIFY_REQUEST.md](../messages/20260617-143000-SAEKO_TO_CONCO_ANSWER_REVIEW_PAYLOAD_REVERIFY_REQUEST.md)
2. [20260617-132000-SAEKO_TO_CONCO_APP_PAGE_BUILD_PL_AND_FINAL_VISITOR_REVIEW_REQUEST.md](../messages/20260617-132000-SAEKO_TO_CONCO_APP_PAGE_BUILD_PL_AND_FINAL_VISITOR_REVIEW_REQUEST.md)
3. [20260617-130500-SAEKO_TO_CONCO_N5_VISITOR_FLOW_GATE_PASS.md](../messages/20260617-130500-SAEKO_TO_CONCO_N5_VISITOR_FLOW_GATE_PASS.md)

Current rule:
When Conco / Main-com is outside the Subcom LAN, Saeko must use GitHub mailbox for Conco-readable notices instead of the LAN-only HTTP mailbox.

Current send-status discipline:
A mailbox send is complete only when message file creation, sender OUTBOX indexing, and receiver INBOX indexing are all done.

Decision line:
SAEKO_GITHUB_MAILBOX_OUTBOX_ACTIVE: yes
LATEST_SAEKO_TO_CONCO_SEND_STATUS: message_created_and_outbox_indexed
