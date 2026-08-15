# Changelog

## [1.2.0] - 2026-08-15

- Fixed strip mode's `Removed:` line, which had no legal value on the copy this skill is handed most often. Step 3b checked five element-specific tells on top of the pattern table, and two of them - an error that opens with an apology and states no fact, and a confirmation that asks "Are you sure?" without naming the consequence - had no row in `references/banned-patterns.md`. Step 3d requires that line to name rows from that file, so the rewrite of "Oops! Something went wrong. Please try again later." had to either report nothing, which reads as "no change was needed" next to a line that was visibly rewritten, or invent a pattern name pointing at a reference file that does not have it.
- Added the two missing rows, `Apology with no fact` and `Unnamed consequence`, each with a bad and fixed example. The table is now 13 patterns; step 3b maps each element-specific tell to the row that reports it.
- A shipped rewrite and a named row now imply each other: at least one row applied means rewrite and name every row that applied, and no row applied means the copy reads fine and the rewrite is skipped rather than manufactured.
- A defect the table does not cover is reported on a `Note:` line under the block instead of being dressed up as a row name, so tightening the rule cannot produce a new deadlock.
- Added a worked strip-mode example to the README, which showed write mode only while naming strip mode in its second usage line.

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
