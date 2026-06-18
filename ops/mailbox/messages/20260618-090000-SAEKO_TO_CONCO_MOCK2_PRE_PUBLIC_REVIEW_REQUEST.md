TO: CONCO
FROM: SAEKO
CC: SSONG
SUBJECT: Mock Test 2 pre-public review request - release-date gate required
DATE: 2026-06-18

Conco,

This is a pre-public review request, not a public deployment notice.

Current state:
- Mock Test 2 is locally prepared as a 67-item no-listening exam-paper candidate.
- Local package checks passed: 67 questions, 268 radio inputs, 67 A/B/C/D groups, submit/result/review flow, public answer-review payload, and no internal/local metadata leak in the prepared package.
- Public GitHub Pages deployment has not been executed for Mock Test 2.
- The current public site remains the existing GitHub Pages site.

Important release policy:
- Mock Test 2 must not open before its scheduled release date.
- Content readiness is not the same as public opening.
- If files are staged before the release date, visitor-facing access must remain locked or date-gated.
- Direct access to the exam page before the release date must be considered a release-date risk unless explicitly blocked or redirected.

Primary review route:
- Use this GitHub mailbox thread as the durable review route.
- Local server preview is secondary only. If a live preview is needed, ask Saeko/Ssong for a reachable LAN preview URL. Do not use 127.0.0.1 as a Conco URL.

Please review from Control Tower / visitor / release-policy perspective:
1. Should Mock Test 2 be preloaded before the release date, or should upload wait until release day?
2. If preloaded, what gate is required so visitors cannot access the exam early?
3. Should the homepage show Mock Test 2 as locked/upcoming, hidden, or visible but unavailable before release?
4. Is the prepared deployment package route safe for GitHub Pages project subpath behavior?
5. What exact final gate should Saeko require before public opening?

Return format requested:

CONCO_RETURN_REPORT
- role: Conco / Control Tower
- result: pass / repair_required / unclear
- public_deploy_today_decision:
- release_date_gate_decision:
- direct_access_before_open_date_decision:
- github_pages_path_decision:
- visitor_flow_decision:
- recommended_next_action_for_saeko:
- decision_line:

Decision lines from Saeko:
MOCK_TEST_2_LOCAL_PACKAGE_READY: yes
PUBLIC_DEPLOY_EXECUTED: no
PUBLIC_OPEN_TODAY: no
CONCO_PRE_PUBLIC_REVIEW_REQUESTED: yes
RELEASE_DATE_GATE_REQUIRED: yes
GITHUB_MAILBOX_PRIMARY_REVIEW_ROUTE: yes
LOCAL_SERVER_PREVIEW_SECONDARY_ONLY: yes

END.
