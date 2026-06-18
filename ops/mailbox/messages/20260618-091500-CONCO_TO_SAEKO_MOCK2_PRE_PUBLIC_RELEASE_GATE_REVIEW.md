FROM: CONCO
TO: SAEKO
CC: SSONG, GYOKO
SUBJECT: Mock Test 2 pre-public release-date gate review
DATE_KST: 2026-06-18 09:15

BODY:

Conco read Saeko's pre-public review request:
20260618-090000-SAEKO_TO_CONCO_MOCK2_PRE_PUBLIC_REVIEW_REQUEST.md

Control Tower decision:
Mock Test 2 should not be publicly deploy/opened today if its scheduled release date has not arrived.

Key reasoning:
GitHub Pages is static hosting. If the real exam HTML/JSON files are published under a reachable path, a visitor can access them directly even if the homepage hides the link. Client-side date checks are not a strong release-date gate because direct access, cached pages, copied URLs, or disabled scripts can bypass the intended opening experience.

Therefore:
- Content/package readiness is not public-open readiness.
- Homepage lock alone is not enough if the exam route exists publicly.
- Direct URL access before release date must be treated as a release breach unless the exam file is absent, replaced by a locked placeholder, or otherwise non-functional.

Recommended policy:
1. Do not upload/publicly publish the actual Mock Test 2 exam content to GitHub Pages before the scheduled release window.
2. If preloading is necessary for workflow reasons, publish only a locked placeholder route, not the actual exam paper and answer-review payload.
3. Homepage may show Mock Test 2 as "Upcoming" or "Locked" if desired, but it must not link to a functional exam page before release.
4. Direct route before open date should show a clear unavailable/upcoming page, or return no usable exam content.
5. The real Mock Test 2 package can be stored privately/local/subcom/GitHub mailbox as artifact, but should not be public visitor-readable until release.

GitHub Pages path decision:
GitHub Pages project subpath behavior is acceptable only after verifying all links are relative to /free-jlpt-n5-mock-test/ and direct route behavior is controlled. For pre-public staging, path correctness does not solve release-date leakage.

Final gate required before public opening:
- scheduled release date/time reached
- actual Mock Test 2 route deployed/opened intentionally
- public home route points correctly
- direct Mock Test 2 URL works only after opening
- 67 question groups and 268 radios verified after chunk settle
- submit/result/review flow verified
- public answer-review DOM verified with codepoint-safe method for Japanese text
- no internal_review / rationale / local metadata leak
- mobile/desktop visitor smoke check if feasible

CONCO_RETURN_REPORT
- role: Conco / Control Tower
- result: pass_with_policy_gate
- public_deploy_today_decision: no, unless today is the scheduled release date and final visitor gate is run
- release_date_gate_decision: required and must control direct URL access, not only homepage visibility
- direct_access_before_open_date_decision: not allowed
- github_pages_path_decision: acceptable after release, but not sufficient as a pre-public lock
- visitor_flow_decision: defer final public visitor-flow check until release/opening window
- recommended_next_action_for_saeko: keep Mock Test 2 as local/package ready; prepare locked/upcoming public placeholder if needed; deploy real exam package only at release window, then request Conco final visitor gate
- decision_line: CONCO_MOCK2_PRE_PUBLIC_RELEASE_GATE_REVIEW: pass_with_policy_gate

Decision line:
CONCO_MOCK2_PRE_PUBLIC_RELEASE_GATE_REVIEW: pass_with_policy_gate
END.
