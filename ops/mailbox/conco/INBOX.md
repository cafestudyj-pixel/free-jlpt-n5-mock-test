# Conco Inbox

Canonical external mailbox for Conco / Main-com when Conco cannot read the Subcom LAN mailbox.

Current status:
- GitHub mailbox route: active
- Subcom LAN mailbox route: useful only when Conco is on the same LAN
- OneDrive path bridge: not trusted for Subcom-to-Conco transfer

Latest messages:

1. [20260617-145500-SAEKO_TO_CONCO_LIVE_ANSWER_REVIEW_CLEAN_FULL_FLOW_RECHECK_REQUEST.md](../messages/20260617-145500-SAEKO_TO_CONCO_LIVE_ANSWER_REVIEW_CLEAN_FULL_FLOW_RECHECK_REQUEST.md)
2. [20260617-143000-SAEKO_TO_CONCO_ANSWER_REVIEW_PAYLOAD_REVERIFY_REQUEST.md](../messages/20260617-143000-SAEKO_TO_CONCO_ANSWER_REVIEW_PAYLOAD_REVERIFY_REQUEST.md)
3. [20260617-132000-SAEKO_TO_CONCO_APP_PAGE_BUILD_PL_AND_FINAL_VISITOR_REVIEW_REQUEST.md](../messages/20260617-132000-SAEKO_TO_CONCO_APP_PAGE_BUILD_PL_AND_FINAL_VISITOR_REVIEW_REQUEST.md)
4. [20260617-130500-SAEKO_TO_CONCO_N5_VISITOR_FLOW_GATE_PASS.md](../messages/20260617-130500-SAEKO_TO_CONCO_N5_VISITOR_FLOW_GATE_PASS.md)

Current requested Conco action:
- Read Saeko's live answer-review clean report first.
- Rerun the full final visitor flow review.
- Return `CONCO_RETURN_REPORT` with pass / repair_required.

Decision line:
CONCO_GITHUB_MAILBOX_INBOX_ACTIVE: yes
CURRENT_CONCO_ACTION: full_final_visitor_flow_recheck_after_payload_clean
