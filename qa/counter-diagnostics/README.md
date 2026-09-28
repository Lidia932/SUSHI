# Counter diagnostics fixtures

Project: 208347. The public project identifier and counter loader are copied
from the existing SUSHI index.html. No integration webhooks or other widgets
are copied. Existing site pages remain unchanged.

The index is counter-free. Each scenario is a separate static HTML document.
Use its exact URL when running server-side diagnostics. Changing only the
browser DOM or using DevTools Overrides does not change server-fetched HTML.

- 01-missing-head-close.html: One counter; missing head closing tag; 1 inline counter script(s).
- 02-two-counters.html: Two distinct counter scripts for the same project; 2 inline counter script(s).
- 03-head-only.html: One counter in head; 1 inline counter script(s).
- 04-body-only.html: One counter in body; 1 inline counter script(s).
- 05-no-head.html: No explicit head element; one counter in body; 1 inline counter script(s).
- 06-no-body.html: No explicit body element; one counter in head; 1 inline counter script(s).

Case 02 deliberately runs two loaders. The second uses js.async = true instead
of js.async = 1, so the script source differs while the project remains the same.
Cases 01, 05 and 06 intentionally omit HTML tags. Do not autoformat or repair them.
Browsers may repair the DOM; inspect the HTTP response source for these cases.

Cases 01, 03 and 04 must not report multiple counters; case 02 must still report
multiple counters. For cases 05 and 06, compare diagnostics with the baseline
behavior and the developer's regression expectation.

Not included: another project's counter, a verified legacy snippet, GTM, or
the customer website reproduction. Do not treat fixture validation as a passed
Roistat diagnostic check. Run the actual diagnostics on the required beta build.
