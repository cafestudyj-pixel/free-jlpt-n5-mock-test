# GPL Link Hub Schema V0

Canonical data file:

```text
links.json
```

Top-level fields:

- `updated_at`
- `project`
- `items`

Item fields:

- `unit_id`: GPL unit id, e.g. `GALAXY_5_01`
- `title`: YouTube/video title
- `youtube_url`: canonical verified YouTube URL
- `status`: current production/deployment state
- `kakao_room`: target room if distributed through Kakao
- `updated_at`: latest status date
- `verified`: boolean
- `notes`: short operational note

Allowed status values:

```text
rendered
uploaded
link_verified
distribution_pending
distributed
needs_check
blocked
```

Rule:

If `status` is `distributed`, `youtube_url` must be a verified URL and `kakao_room` should be filled.

