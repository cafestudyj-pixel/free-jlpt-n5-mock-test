# GPL Machine Ledger V0

Status: prototype
Created: 2026-06-15

Purpose:

Centralize GPL YouTube links, schedule state, and deployment logs so Jiko can upload and distribute GPL content without relying on GUI memory or chat history.

This hub does not store large media files.

GitHub should hold:

- YouTube URLs
- unit status
- verification notes
- Kakao distribution status
- timestamps

GitHub should not hold:

- mp4
- wav
- render intermediates

Core machine files:

- `links.json`: canonical YouTube link/status table
- `schedule.json`: planned GPL upload/distribution queue
- `deploy_log.json`: completed/blocked deployment history
- `status.json`: current operating policy

First proof loop:

```text
YouTube link
-> links.json update
-> schedule.json / deploy_log.json update
-> Jiko reads canonical JSON before Kakao distribution
```

Meta rule:

Netlify is not a GPL requirement. The core requirement is a machine-readable GitHub ledger that Jiko can read before upload/distribution work.
