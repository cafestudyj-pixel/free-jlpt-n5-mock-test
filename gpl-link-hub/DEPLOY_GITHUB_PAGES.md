# GPL Link Hub V0 GitHub Pages Deploy

Purpose:

Publish a small static GPL status page so Jiko/Saeko/Conco/Ssong can use one canonical link table.

Contents:

- `index.html`: static viewer
- `links.json`: canonical GPL link/status data
- `GPL_LINK_HUB_SCHEMA.md`: schema note
- `.nojekyll`: GitHub Pages passthrough marker

Recommended GitHub Pages route:

1. Create or choose a small repository for GPL link status.
2. Copy this folder's files to the repository root.
3. Commit and push.
4. Enable GitHub Pages from the repository settings.
5. Use the published URL as the canonical GPL link hub.

Rules:

- Store YouTube links and status only.
- Do not store mp4, wav, render intermediates, or private account material.
- Update `links.json` after upload/distribution verification.
- Treat the hub as the status map, not the media warehouse.

Next proof:

```text
Add GALAXY_5_02 to links.json
-> push to GitHub
-> check public hub
-> use hub link before Kakao distribution
```
