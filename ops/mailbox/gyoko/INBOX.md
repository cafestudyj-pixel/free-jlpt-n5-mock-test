# Gyoko Inbox

Receiver-facing index for Gyoko messages through the GitHub external mailbox.

Use this when the Subcom LAN mailbox is unavailable or when a durable public-repo route is preferred for project status.

Inbox messages:

1. [20260617-235200-SAEKO_TO_CONCO_GYOKO_MOCK1_PUBLIC_GATE_OPEN.md](../messages/20260617-235200-SAEKO_TO_CONCO_GYOKO_MOCK1_PUBLIC_GATE_OPEN.md)

Current action:
- Record that Mock Test 1 public gate is open on GitHub Pages.
- Gyoko content/package owner should treat the current public route as live unless a new blocking defect is reported.
- Post-release polish can be handled separately.

Decision lines:
GYOKO_GITHUB_MAILBOX_INBOX_ACTIVE: yes
MOCK_TEST_1_PUBLIC_GATE_OPEN_VISIBLE_TO_GYOKO: yes
CURRENT_PUBLIC_DEPLOY_ROUTE: github_pages
