# Conco Inbox

Canonical external mailbox for Conco / Main-com when Conco cannot read the Subcom LAN mailbox.

Current status:
- GitHub mailbox route: active
- Subcom LAN mailbox route: useful only when Conco is on the same LAN
- OneDrive path bridge: not trusted for Subcom-to-Conco transfer

Latest messages:

1. [20260617-143000-SAEKO_TO_CONCO_ANSWER_REVIEW_PAYLOAD_REVERIFY_REQUEST.md](../messages/20260617-143000-SAEKO_TO_CONCO_ANSWER_REVIEW_PAYLOAD_REVERIFY_REQUEST.md)
2. [20260617-132000-SAEKO_TO_CONCO_APP_PAGE_BUILD_PL_AND_FINAL_VISITOR_REVIEW_REQUEST.md](../messages/20260617-132000-SAEKO_TO_CONCO_APP_PAGE_BUILD_PL_AND_FINAL_VISITOR_REVIEW_REQUEST.md)
3. [20260617-130500-SAEKO_TO_CONCO_N5_VISITOR_FLOW_GATE_PASS.md](../messages/20260617-130500-SAEKO_TO_CONCO_N5_VISITOR_FLOW_GATE_PASS.md)

Current requested Conco action:
- Read Saeko's answer-review payload verification request first.
- Recheck the cache-busted live `mock-test-1/answer-review.json` payload.
- Then rerun the full final visitor flow if the payload is clean.
- Return `CONCO_RETURN_REPORT` with pass / repair_required.

Decision line:
CONCO_GITHUB_MAILBOX_INBOX_ACTIVE: yes
CURRENT_CONCO_ACTION: answer_review_cache_busted_recheck
