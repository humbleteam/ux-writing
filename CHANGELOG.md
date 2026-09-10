# Changelog

## [1.4.0] - 2026-09-10

- Fixed strip mode on the two lines the skill is handed most often. Step 3b maps "Oops! Something went wrong. Please try again later." to the `Apology with no fact` row and "Are you sure?" to `Unnamed consequence`, and both of those rows are fixed by adding a fact - what failed, what gets removed - rather than by cutting one. Neither input carries that fact. Step 3d says a row that applied means a rewrite ships, so skipping was closed; self-check 8 said "in strip mode, cut it", and there is nothing invented in "Are you sure?" to cut. The only remaining move was a plausible cause or count, which is the failure this skill exists to catch, and the README already promised the opposite - that the skill asks for the fact instead of picking one - without any shape in `SKILL.md` for the asking.
- Step 3c now carries the write-mode remedy: a fact the fix itself needs and neither the original nor the request supplies is written as a named slot (`because <cause>`, `all <n> <items> inside it`) and asked for on a `Needs:` line. A rewrite carrying a slot is a draft, exactly as in write mode.
- The two cases are told apart by where the fact came from, not by how it looks: a claim the original made and the input never confirmed is still cut, a fact the fix needs becomes a slot. Self-check 8 and the both-modes rule now say both halves.
- Strip-mode output format gained the optional `Needs:` line, one question per slot, never shipped empty. A slot never appears on the `Before:` line - the original is quoted as the user gave it.
- `references/banned-patterns.md` now says that the fixed examples for those two rows are the filled form, and gives the slot form that ships without the facts. Two of the 13 rows are fixed by adding a fact and 11 by cutting something, so those two are the only rows that can produce a slot.
- Added a worked strip-mode example to the README for the same error with no cause supplied, next to the existing one where the user supplies it, plus a new edge case in `SKILL.md`.

## [1.3.0] - 2026-09-05

- Fixed write mode's version of the deadlock strip mode lost on 2026-08-15. Two of the element rules in step 2b turn on a fact about the product rather than about the element: a destructive confirmation names how much goes and whether it comes back, and an error names what happened. A request usually describes the flow and not the data - "write the copy for deleting a project" says nothing about what a project holds or about what blocks a delete - while self-check 8 forbids shipping a number or a cause the input never confirmed. The line had a rule it could not satisfy and a gate it could not pass, and the only routes on offer were a plausible invention or a confirmation with no consequence named, which is the pattern this skill exists to catch.
- New step 2c: a fact the request never gave is written as a named slot in the position it belongs (`all <n> tasks inside it`), and asked for under the block. A line carrying a slot is a draft; elements whose rules need no product fact still ship as finished copy in the same block.
- The write-mode output format gained a `Needs:` line, one question per slot, present only when a line carries one - an empty `Needs:` is never shipped, the same way an empty `Removed:` is not. Answered, the block is re-emitted with the slots filled and the line dropped.
- Self-check 8's "flag it" now names its two shapes instead of leaving them to the reader: a slot and a `Needs:` question in write mode, a cut in strip mode. A guessed fact does not ship with a caveat attached.
- Fixed the README's write-mode example, which had the bug in miniature: on a request that named the flow and nothing else, it returned a confirmation counting 14 tasks and an error blaming 2 assigned members, both invented, under a caption that excused invented names only. It now shows the slot form for that request and the filled block once the facts are supplied.

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
