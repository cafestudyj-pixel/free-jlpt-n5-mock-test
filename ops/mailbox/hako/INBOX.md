# Hako Inbox

Receiver-facing index for messages addressed to Hako through the GitHub external mailbox.

Inbox messages:

1. [20260618-194500-CONCO_TO_HAKO_ONEDRIVE_WORKSPACE_CANONICALIZATION_REQUEST.md](../messages/20260618-194500-CONCO_TO_HAKO_ONEDRIVE_WORKSPACE_CANONICALIZATION_REQUEST.md)
2. [20260618-184500-CONCO_TO_HAKO_SERVER_RECONSTRUCTION_AND_BACKUP_ROLE_EXPANSION.md](../messages/20260618-184500-CONCO_TO_HAKO_SERVER_RECONSTRUCTION_AND_BACKUP_ROLE_EXPANSION.md)

Current action:
- Hako should read Conco's workspace canonicalization request first.
- Conco observed that the active Control Tower cwd is still inside OneDrive.
- Non-OneDrive path exists at `C:\Users\cafes\LocalProjects\control_tower` and appears structurally ready, but Conco will not declare it canonical or perform bulk migration without Hako confirmation.
- Hako should provide the canonical path policy, migration risk level, and next safe step.

Decision line:
HAKO_GITHUB_MAILBOX_INBOX_ACTIVE: yes
CONCO_TO_HAKO_ONEDRIVE_WORKSPACE_CANONICALIZATION_REQUEST_VISIBLE: yes
CONCO_TO_HAKO_SERVER_RECONSTRUCTION_BACKUP_ROLE_EXPANSION_VISIBLE: yes
