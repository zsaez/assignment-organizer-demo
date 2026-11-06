# Security Review

Review date: November 5, 2026. Scope: the separate public-site copy of the static Assignment Organizer demo. This is an AI-assisted source review and targeted functional/security check, not a professional penetration test or a guarantee that every vulnerability is absent.

## What was reviewed

The entire HTML/JavaScript file, typed estimate inputs, DOM insertion, outbound communication, browser storage, credentials, dependencies, and GitHub Pages publication scope. There is no server, account system, database, or privileged action to authenticate.

## Findings and changes

- No directly exploitable injection vulnerability was identified in the reviewed source. User-visible strings use textContent; typed estimates are not inserted as HTML, evaluated, or used in URLs.
- The original page lacked a Content Security Policy. This was a defense-in-depth gap, not proof of an existing exploit. Added a policy allowing only the exact SHA-256-hashed script and stylesheet. It blocks other scripts, eval, network connections, images, frames, workers, objects, base URL changes, and form submission.
- Added a no-referrer policy to reduce referrer disclosure if outbound navigation is later introduced.
- Numeric estimates already reject empty, nonnumeric, nonpositive, fractional, reversed, and unsafe-integer values. Added a 32-character input limit to bound typed input size. Last-valid estimates remain after refusal.
- Reviewed for secret keys, credentials, network APIs, dynamic HTML execution, and persistent storage; none were found in the site file. No external JavaScript/CSS libraries or package dependencies are used.
- Added an independent-demo notice and temporary-state disclosure. Only site files and this review are intended for publication; no transcript, real student records, or previous assignment submission files are included.

## Tests

Completed checks on the local HTTP preview, November 5, 2026:

- JavaScript syntax check passed.
- Recomputed both SHA-256 hashes and verified they match the CSP.
- Static checks found no inline HTML event attributes, external asset URLs, dangerous HTML sinks, network/storage APIs, or GitHub token patterns.
- The browser rendered the page and a valid 20–30 estimate edit worked with the restrictive policy active.
- All six invalid estimate pairs were refused and retained 20–30: blank/30, text/30, 0/30, -5/30, 10.5/30, 40/20.
- A typed `<img src=x onerror=alert(1)>` payload was refused; the valid estimate remained and no img element was inserted into the page.
- Completing Short quiz moved it into Completed with the correct session-completion label.
- Browser console contained no errors or warnings during these checks.

These tests are AI-performed checks of the separate public-site copy, not retroactive student results for Chapter 10. Hosted HTTPS behavior will be verified after deployment.

## Limits

The hosting provider still receives normal HTTP requests when someone visits the site. No claim is made that GitHub records no visitor metadata. A meta-delivered CSP cannot enforce every HTTP-header-only protection, including frame-ancestors; clickjacking prevention is therefore not asserted. Hosting configuration and HTTPS must be checked after publication. Changing the hashed script or stylesheet requires regenerating the corresponding CSP hash. This review does not establish security for future real course access, accounts, file uploads, or AI integrations.

References: https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/CSP and https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site
