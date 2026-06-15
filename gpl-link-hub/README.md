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

First proof loop:

```text
YouTube link
-> links.json update
-> static index.html renders it
-> future GitHub Pages / Netlify deployment
```

