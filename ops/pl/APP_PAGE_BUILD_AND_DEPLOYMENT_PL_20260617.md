# App Page Build And Deployment PL - 2026-06-17

Project: Free JLPT N5 Mock Test Series

## Purpose

This PL captures the reusable working blueprint for turning the N5 site from a local/static candidate into a public visitor-facing app page with deployment, routing, and gate verification.

It is not just a record. It is a repeatable operating route for future mock-test releases.

## Current Public Surface

Official site:
https://cafestudyj-pixel.github.io/free-jlpt-n5-mock-test/

Current deployment route:
- GitHub Pages
- Repository: `cafestudyj-pixel/free-jlpt-n5-mock-test`
- Branch: `main`
- Netlify is not the current active route.

## Key Lessons Preserved

1. Do not confuse temporary deploy surfaces with the official route.
   - Netlify Drop was useful during early manual deployment.
   - Current stable route is GitHub Pages.

2. Do not expose the exam paper as the homepage.
   - Root `/` must behave as a public homepage.
   - Exam content must live behind an explicit start route.

3. Do not use OneDrive-looking paths as cross-machine proof.
   - Same path string can point to different local realities.
   - For external Conco/Main-com, use GitHub mailbox.

4. Do not rely on visual confidence alone.
   - Gate checks must include route, chunk loading, radio integrity, answer-review payload, submit/review behavior, and internal leak checks.

5. Do not end a routing loop without a return surface.
   - Use `SAEKO_RETURN_REPORT` for session-loop return.
   - Use GitHub mailbox when Conco is outside the Subcom LAN.

## Build Route Blueprint

1. Content owner prepares public-safe content.
   - Content package must avoid internal_review exposure.
   - Answer/review payload must be public-safe and separate from internal QA fields.

2. Site/deployment owner integrates route.
   - Homepage remains root `/`.
   - Mock test route is explicit: `/mock-test-1/index.html`.
   - Root page links to the mock route.

3. Chunk or static payload integrity is checked.
   - All required chunks load.
   - Question count matches expected release scope.
   - Radio inputs are valid and complete.
   - No malformed input attributes.

4. Submit/review layer is checked.
   - Answers are not visibly exposed before submit.
   - Score/result panel appears after submit.
   - Public explanations are available only through the intended review flow.

5. Visitor-flow gate is checked by a user-perspective reviewer.
   - First screen must feel like a homepage.
   - Start route must be obvious.
   - Exam route must load normally.
   - Choices must be visibly/selectably usable.
   - Submit/result/review flow must be completed through the last step.

6. External continuity is recorded.
   - Conco-readable state goes into GitHub mailbox.
   - Route decisions go into `ops/status/`.
   - Reusable methods go into `ops/pl/`.

## Required Final Visitor Review Simulation

A final visitor reviewer must proceed as a real learner, not just inspect files:

1. Open official homepage.
2. Confirm it is not accidental exam content.
3. Click or follow Start Mock Test 1.
4. Confirm Mock Test 1 loads.
5. Select answers across the paper.
6. Submit.
7. Confirm score/result appears.
8. Confirm answer review/explanations appear after submit.
9. Confirm no internal QA strings are visible.
10. Confirm the route is usable enough on a narrow/mobile-like viewport.

If the reviewer does not reach the final result/review step, the visitor-flow review is incomplete.

## Current Known Status

- Homepage route restored: pass
- Mock Test 1 route: pass
- Visitor-flow gate from Saeko-side visitor simulator: pass
- Remaining recommendation: Conco should perform or coordinate an independent final visitor-perspective end-to-end check through the last review step.

## Decision Lines

APP_PAGE_BUILD_DEPLOYMENT_PL: created
CURRENT_PUBLIC_DEPLOY_ROUTE: github_pages
ROOT_HOMEPAGE_NOT_EXAM: required
MOCK_TEST_ROUTE_EXPLICIT: required
FINAL_VISITOR_REVIEW_MUST_COMPLETE_SUBMIT_REVIEW: yes
CONCO_EXTERNAL_REVIEW_ROUTE: github_mailbox
