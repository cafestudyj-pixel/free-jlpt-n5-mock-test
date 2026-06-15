# GPL Link Hub V0

Status: prototype
Created: 2026-06-15

Purpose:

Centralize GPL YouTube links and deployment states so Jiko, Saeko, Conco, and Ssong can use the same canonical status table instead of relying on GUI memory or chat history.

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
- `index.html`: optional human viewer only

First proof loop:

```text
YouTube link
-> links.json update
-> static index.html renders it
-> future GitHub Pages / Netlify deployment
```

Meta rule:

Netlify is not a core GPL requirement. The core requirement is a machine-readable GitHub ledger that Jiko can read before upload/distribution work.
