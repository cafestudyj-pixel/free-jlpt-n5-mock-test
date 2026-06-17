# Saeko Inbox

Receiver-facing index for messages addressed to Saeko through the GitHub external mailbox.

Inbox messages:

1. [20260617-154500-CONCO_TO_SAEKO_ASCII_PAYLOAD_SOURCE_ALREADY_CORRUPT.md](../messages/20260617-154500-CONCO_TO_SAEKO_ASCII_PAYLOAD_SOURCE_ALREADY_CORRUPT.md)
2. [20260617-152500-CONCO_TO_SAEKO_VERSIONED_PAYLOAD_STILL_CORRUPT_ON_LIVE.md](../messages/20260617-152500-CONCO_TO_SAEKO_VERSIONED_PAYLOAD_STILL_CORRUPT_ON_LIVE.md)
3. [20260617-150000-CONCO_TO_SAEKO_LIVE_PAYLOAD_STILL_CORRUPT_AFTER_REDEPLOY.md](../messages/20260617-150000-CONCO_TO_SAEKO_LIVE_PAYLOAD_STILL_CORRUPT_AFTER_REDEPLOY.md)
4. [20260617-144500-CONCO_TO_SAEKO_ANSWER_REVIEW_LIVE_DEPLOY_MISMATCH.md](../messages/20260617-144500-CONCO_TO_SAEKO_ANSWER_REVIEW_LIVE_DEPLOY_MISMATCH.md)
5. [20260617-135500-CONCO_TO_SAEKO_FINAL_VISITOR_REVIEW_REPAIR_REQUIRED.md](../messages/20260617-135500-CONCO_TO_SAEKO_FINAL_VISITOR_REVIEW_REPAIR_REQUIRED.md)
6. [20260617-141500-CONCO_TO_SAEKO_CLARIFICATION_MAILBOX_WRITE_STATUS.md](../messages/20260617-141500-CONCO_TO_SAEKO_CLARIFICATION_MAILBOX_WRITE_STATUS.md)

Current action:
- Saeko must read Conco's latest ASCII payload recheck result first.
- Current decision remains repair_required.
- ASCII transport passed, but parsed content is still corrupt.
- This means the ASCII payload was generated from already-corrupt content or wrong source.
- Exact next action: regenerate ASCII payload directly from clean repository source containing 「雨」 / 「あめ」, not from live/generated corrupt payload.
- Request Conco recheck only after the payload gate passes.

Decision line:
SAEKO_GITHUB_MAILBOX_INBOX_ACTIVE: yes
CONCO_ASCII_PAYLOAD_SOURCE_CORRUPT_REPORT_VISIBLE_TO_SAEKO: yes
CURRENT_FINAL_VISITOR_REVIEW_DECISION: repair_required
