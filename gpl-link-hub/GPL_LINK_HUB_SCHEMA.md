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
- `youtube_url`: canonical verified YouTube URL, or null if uploaded but link recovery is still needed
- `youtube_status`: current YouTube-side state
- `distribution_status`: current Kakao/external distribution state
- `kakao_room`: target room if distributed through Kakao
- `updated_at`: latest status date
- `verified`: boolean
- `notes`: short operational note

Allowed status values:

```text
rendered
uploaded
uploaded_unlisted_made_for_kids
link_verified
distribution_pending
distributed
not_distributed
link_recovery_needed
needs_check
blocked
```

Rule:

If `status` is `distributed`, `youtube_url` must be a verified URL and `kakao_room` should be filled.


## deployment_targets.json

Canonical deployment target file. This removes repeated context reconstruction for KakaoTalk distribution.

Target fields:

- `target_id`: stable machine id, e.g. `kakao_japanese_written_language_study_committee`
- `platform`: target platform, e.g. `kakaotalk`
- `room_name`: exact visible KakaoTalk room name
- `room_name_aliases`: short search strings allowed for room lookup
- `route`: execution route, currently `chat_tab_search`
- `precheck`: required checks before sending
- `fire`: minimal send sequence
- `verify`: success confirmation rule
- `send_format`: message format, usually `{youtube_url}`
- `stop_conditions`: conditions requiring stop and Ssong confirmation

Rule:

`links.json` and `schedule.json` items should use `target_id` and resolve the actual room name and route from `deployment_targets.json`.
