# Changelog

## [1.1.0] - 2026-08-10

- Fixed the em dash gate, which could not enforce the rule it existed for. Self-check question 3 fired only on "more than one em dash in the line", while the rules list says no em dash at all in shipped copy - so a button or a toast carrying exactly one em dash passed the gate and shipped, and interface lines are short enough that the two-dash case almost never occurs. The threshold is now one.
- An en dash used between words in place of an em dash now counts as the same tell.
- Renamed the `references/banned-patterns.md` row from "em-dash overuse" to "em dash", with a single-dash bad example, and noted why the count is one. Strip-mode output now reports `Removed: em dash`.
- New edge case: an em dash inside a string that has to stay verbatim (a legal clause, a third-party product name, text the user typed) stays, the ones around it get fixed, and the output names the one left behind.

## [1.0.0] - 2026-07-12

- Initial release: write mode (button, error, empty state, confirmation, placeholder, tooltip, toast, and label copy) and strip mode for rewriting existing copy that reads AI-generated.
- Added `references/banned-patterns.md` with an 11-pattern table of AI-tell copy, each with a bad and fixed example.
- Added the eight-question pre-ship self-check that runs before any draft ships in either mode.
- Documented edge cases: compliance-reviewed copy, a provided brand voice guide, non-English requests, and copy that already reads fine.
