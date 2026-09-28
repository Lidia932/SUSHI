# Counter diagnostics fixtures

Project: 208347. The public project identifier and counter loader are copied
from the existing SUSHI index.html. No integration webhooks or other widgets
are copied. Existing site pages remain unchanged.

The index is counter-free. Each scenario is a separate static HTML document.
Use its exact URL when running server-side diagnostics. Changing only the
browser DOM or using DevTools Overrides does not change server-fetched HTML.

- 01-missing-head-close.html: One counter; missing head closing tag; 1 inline script(s).
- 02-two-counters.html: Two distinct counter scripts for the same project; 2 inline script(s).
- 03-head-only.html: One counter in head; 1 inline script(s).
- 04-body-only.html: One counter in body; 1 inline script(s).
- 05-no-head.html: No explicit head element; one counter in body; 1 inline script(s).
- 06-no-body.html: No explicit body element; one counter in head; 1 inline script(s).
- 07-other-project.html: Counter for project 257999; diagnose from project 208347; 1 inline script(s).
- 08-legacy-counter.html: Legacy counter for project 208347 supplied by the developer; 1 inline script(s).
- 09-gtm-counter.html: Project 208347 counter installed through GTM-W3Z29JKH; 1 inline script(s).

Case 02 deliberately runs two loaders. The second uses js.async = true instead
of js.async = 1, so the script source differs while the project remains the same.
Cases 01, 05 and 06 intentionally omit HTML tags. Do not autoformat or repair them.
Browsers may repair the DOM; inspect the HTTP response source for these cases.

Cases 01, 03 and 04 must not report multiple counters; case 02 must still report
multiple counters. For cases 05 and 06, compare diagnostics with the baseline
behavior and the developer's regression expectation.

Case 07 uses the public installation key read from project 257999 settings.
Run diagnostics from project 208347 to exercise the other-project warning.
Case 08 uses the legacy snippet supplied by the developer in the PR discussion
on 2026-09-28, with CLOUD_DOMAIN and PROJECT_KEY set to cloud.roistat.com and
the existing project 208347 key. It omits roistatPage and roistatReferrer.

Case 09 embeds only the user-provided GTM-W3Z29JKH installation snippets.
There is no direct Roistat loader in this HTML. Configure a Custom HTML tag in
GTM with the current project 208347 loader and fire it on Page View, restricted
to hostname lidia932.github.io and path /SUSHI/qa/counter-diagnostics/09-gtm-counter.html.
Publish the container before using this fixture for acceptance.

Not included: the customer website reproduction. Do not treat fixture validation as a passed
Roistat diagnostic check. Run the actual diagnostics on the required beta build.
