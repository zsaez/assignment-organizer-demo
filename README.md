# Assignment Organizer Demo

Interactive static website made with AI assistance for a class website assignment. It extends an earlier classroom prototype; the original Chapter 10 submission remains separate.

## Try it

Open index.html or visit the GitHub Pages URL once published. Switch date/class views, expand assignments, mark them complete and undo completion, and edit estimated work-time ranges. The testing area switches fictional failure and recovery scenarios.

## Limits

All records are fictional. There is no login, real course integration, homework-answer generation, submission, live AI, analytics, or persistent storage. Calendar, Add assignment, and AI chat are labeled planned features. October 2026 mock dates are intentionally preserved, so they appear overdue after those dates. Page reload discards edits. This is an independent student demo, not an official BYU, Canvas, or Learning Suite service.

## Security

See SECURITY_REVIEW.md for the review, hardening changes, tests, and limitations. The page uses textContent for displayed data, validates estimate ranges, and uses hash-based Content Security Policy to restrict executable content and block outbound connections and form submission. Keep the CSP hashes in sync if JavaScript or styles change.

## GitHub Pages

Publish the main branch from the root folder using Settings → Pages → Deploy from a branch → main / (root). An empty .nojekyll file disables Jekyll processing. Do not upload the earlier coursework ZIP, conversation, or private materials.
