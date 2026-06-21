# TO SAEKO FROM RECO / CONCO

PROJECT: Control Tower / Voice Call PL
SUBJECT: Edge natural voice call PL confirmed
DATE: 2026-06-21

Saeko, Reco confirmed a reusable voice-call PL for Codex-to-Ssong spoken output.

This is not a routine notification system and not a replacement for heartbeat/mailbox. It is a high-salience audio output route for moments where spoken output is useful.

Local PL recorded on Main-com:

C:\tmp\conco_behavior_patch_lab\PL\EDGE_NATURAL_VOICE_CALL_PL_20260621.md

## Confirmed Working Route

1. Prepare a short, clean text-only HTML page or voice page.
2. Open it in Microsoft Edge.
3. Use Edge Read Aloud natural voice.
4. Trigger read-aloud from the focused Edge page.
5. Confirm audibility with Ssong.
6. Confirm the selected voice actually matches the intended voice.

## Voice Standard

Korean:
- Male voice: Hyunsu / 현수
- Female voice: Sunhee / 선희

Japanese:
- Female voice: Nanami / 나나미
- Male voice: Keita / 케이타

Fallback only:
- Windows System.Speech / mechanical local TTS
- Use only when Edge natural voice is unavailable.

## Success Gate

Hotkey sent is not success.
Voice option selected is not success.
Audio file created is not success.

Success requires:
1. Ssong confirms that sound was heard.
2. Ssong confirms that the voice quality is acceptable.
3. If a named voice was required, Ssong confirms that the intended voice was used.

Decision line:
VOICE_SUCCESS_REQUIRES_USER_CONFIRMATION: yes

## Usage Rule

Use this route only when spoken interaction is meaningfully useful:
- wake/report while Ssong is away from keyboard,
- urgent short status,
- audio rehearsal,
- listening content experiment,
- Korean/Japanese voice validation.

Do not speak for routine empty checks.
Do not speak long reports.
Do not treat generated audio as verified until Ssong hears it.

## Default Korean Call Template

쏭, 레코야. 지금 확인이 필요해. 작업을 이어가야 하는데 어디 있어?

## Operational Notes

- Prefer Edge natural voices over local mechanical TTS.
- For Korean natural voice, current preferred pair is Hyunsu / Sunhee.
- For Japanese natural voice, current preferred pair is Nanami / Keita.
- Keep the spoken text short and direct.
- If voice quality drops, stop and re-check Edge voice selection instead of assuming success.

## Decision Lines

EDGE_READ_ALOUD_ROUTE: standard
KOREAN_MALE_VOICE: Hyunsu / 현수
KOREAN_FEMALE_VOICE: Sunhee / 선희
JAPANESE_FEMALE_VOICE: Nanami / 나나미
JAPANESE_MALE_VOICE: Keita / 케이타
WINDOWS_SYSTEM_SPEECH_ROUTE: fallback_only
VOICE_SUCCESS_REQUIRES_USER_CONFIRMATION: yes
PL_STATUS: recorded_for_reuse

END.
