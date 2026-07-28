# GPL Yomigana–Narration Handoff Gate

Status: LOCKED  
Effective: 2026-07-28  
Owner: Ssong / Wonko / Jiko

## Purpose

원고의 요미가나와 나나미의 실제 낭독이 달라지는 문제를 원고 인계 단계에서 차단한다.

## Canonical reading source

- 쏭이 지정한 유튜브 낭독 영상의 실제 발음을 해당 제작물의 최우선 읽기 기준으로 삼는다.
- 사전·원문 주석·통상 독음과 영상 낭독이 다르면 영상에서 실제로 들리는 읽기를 채택한다.
- 차이가 있는 독음은 `reading_exceptions`에 기록한다.
- 원코는 영상을 직접 재생해 확인하지 않은 읽기를 추정하거나 관행적인 독음으로 확정해서는 안 된다.
- 영상에서 소리가 불분명한 항목은 `확인 불가`로 기록하고, 확인된 값처럼 인계하지 않는다.

## Wonko gate before handoff

원코는 각 문장마다 다음을 직접 확인한다.

- 선택 문장과 원문의 일치
- 어휘에 표시할 모든 요미가나
- 기준 영상에서 실제로 들리는 문장과 핵심 어휘의 발음
- 작품의 지정 읽기와 일반 사전식 읽기의 차이
- 고어·이표기·특수 독음
- 나나미가 오독할 가능성이 있는 한자
- 나나미가 기준 발음대로 읽도록 조정한 `voicevox_text`

각 문장에는 영상 확인 시작·종료 타임코드를 남긴다. 별도 확인이 필요한 어휘는 어휘별 실제 발음도 남긴다.

## Required handoff fields

각 문장 인계 데이터에 다음 필드를 반드시 기록한다.

- `yomigana_checked: true`
- `narration_reference_checked: true`
- `voice_reading_checked: true`
- `reading_reference`: 기준 영상 URL과 문장별 시작·종료 타임코드
- `narration_actual_reading`: 영상에서 직접 확인한 문장 또는 핵심 어휘의 실제 읽기
- `display_yomigana`: 학습 화면에 표시할 요미가나
- `voicevox_text`: 나나미에게 전달할 최종 음성 입력문
- `reading_exceptions`: 일반 독음과 다른 항목, 세 표기 사이의 차이와 대응 관계

필수 필드가 없거나 세 확인값 중 하나라도 `false`이면 지코는 인계를 반려하고 음성을 생성하지 않는다.

## Three-way match

다음 세 항목은 같은 발음 결과를 가져야 한다.

1. 학습 화면의 `display_yomigana`
2. 기준 영상의 `narration_actual_reading`
3. 나나미에 전달되는 `voicevox_text`

표기 방식이 서로 다르더라도 실제 발음이 같아야 한다. 차이가 필요한 경우 그 이유를 `reading_exceptions`에 기록한다.

## Jiko audio gate

지코는 음성 생성 전후에 다음을 확인한다.

- 요미가나와 `voicevox_text`의 읽기 일치
- `reading_exceptions`의 반영
- 수정된 입력문으로 음성이 실제 재생성되었는지
- 이전 캐시 음성이 재사용되지 않았는지
- 나나미의 실제 출력 음성을 직접 들었는지
- 핵심 한자어, 장단, 촉음, 숫자, 고유명사, 고어의 오독이 없는지

오독이 하나라도 있으면 `voicevox_text`를 수정하고 음성을 다시 생성한다.

## Render block

다음 조건을 모두 만족하기 전에는 렌더링하지 않는다.

- 원코의 문장별 유튜브 낭독 확인 완료
- 세 확인값이 모두 `true`
- 나나미 실제 음성 청취 완료
- 오독 0개
- 검수 JSON에 확인 상태 저장

쏭은 1차 요미가나 오류를 찾아내는 검수자가 아니다. 원코와 지코가 이 게이트를 완료한 결과만 쏭에게 전달한다.
