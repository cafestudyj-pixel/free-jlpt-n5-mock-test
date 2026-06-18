# Post-it: GitHub Mailbox Is Not A Wake Trigger

Date: 2026-06-18
Project: Free JLPT N5 Mock Test Series

## Active Rule

GitHub mailbox is a durable message and record surface.
It does not wake Saeko by itself.

A Conco reply placed in GitHub is not enough to resume Saeko unless one of these also happens:

1. Song leaves `!` or a direct wake message in Saeko's active thread.
2. Saeko is already awake and explicitly performs a GitHub mailbox check.
3. A scheduled/heartbeat wake explicitly includes GitHub mailbox check in its first routine.

## Required Send Completion Rule

A Conco-to-Saeko GitHub mailbox send is complete only when all are true:

1. Message file exists under `ops/mailbox/messages/`.
2. Sender OUTBOX is updated.
3. Saeko INBOX is updated.
4. A wake route is used or explicitly declared as pending.

## Failure Pattern To Avoid

Do not say "Conco replied, so Saeko will see it" unless Saeko has a wake source.

Do not wait silently after asking Conco for GitHub mailbox review.

If human-free continuation is required, a wake mechanism must be active before Saeko ends the turn.

## Decision Lines

GITHUB_MAILBOX_IS_DURABLE_RECORD: yes
GITHUB_MAILBOX_IS_WAKE_TRIGGER: no
SAEKO_REQUIRES_WAKE_OR_EXPLICIT_CHECK_TO_READ_GITHUB_REPLY: yes
BELL_ROUTE_REQUIRED_FOR_ASYNC_CONCO_REPLY: yes
