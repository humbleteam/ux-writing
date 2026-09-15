---
name: ux-writing
description: Write interface microcopy for buttons, error messages, empty states, and confirmations, or strip AI-generated tells out of copy you already have. Use for "write the button copy for...", "draft an error message for...", "this copy sounds AI-generated", "write empty state copy", or "rewrite this confirmation dialog". Do not use for marketing pages or long-form content - interface microcopy only.
---

# UX writing

Write interface copy that reads like someone thought about the specific screen, or rewrite copy that reads like a model generated it.

## Step 0 - load the pattern table

Before writing or rewriting anything, read [references/banned-patterns.md](references/banned-patterns.md) if it is not already in context. It has the 13 AI-tell patterns this skill checks for, each with a bad and fixed example in interface copy. Do not skip this even if the patterns look familiar - the exact wording matters for a consistent check every run. The table is one of the two checks strip mode runs, not the whole of it: the other is the element's own rule in step 2b.

## Step 1 - pick a mode

- **Write mode**: the request describes a component or flow with no existing copy to work from - a button, a form, an error state, an empty state, a delete flow.
- **Strip mode**: the request includes an actual string of existing copy, or says the copy sounds generated, robotic, or "too AI".

If the request gives neither a component to write for nor a string to rewrite, ask what needs copy instead of guessing.

## Step 2 - write mode

### 2a. Identify the element type

If the user names the element (button, error, empty state), use it directly. If they only describe a flow ("write the copy for deleting a project"), break it into the elements that flow actually needs - usually a button, a confirmation, an error, and a success message - and write each one.

### 2b. Apply the rule for that element type

| Element | Rule | Shape |
|---|---|---|
| Button / link | Start with a verb, name the outcome. Sentence case. Never a bare "Submit", "OK", or "Learn more" if a specific outcome can be named instead. | `<Verb> <object>` - "Save changes", "Delete project", "Invite teammate" |
| Error message | State what happened, then how to fix it, in that order. No blame, no bare apology. | `<What happened>. <How to fix it>.` |
| Empty state | Name what belongs in the space, then the one action that fills it. Never a bare "Nothing here yet" with no next step. | `<What's missing>. <Action>.` plus one button |
| Confirmation (destructive) | Name the specific consequence: what gets removed, how much, whether it's reversible. Never a bare "Are you sure?" | `<Action> "<item>"? <Consequence>. <Reversible or not>.` |
| Placeholder text | An example value inside a field. Never a substitute for a persistent label - if removing the placeholder would leave the field unlabeled, that is a bug, not a copy choice. | short example value, not an instruction |
| Tooltip | One sentence. States what the control does, or why it's disabled. Never a restatement of its own label. | `<What it does or why it's disabled>` |
| Toast / inline notification | States the result, past tense. No exclamation mark unless a provided brand voice guide calls for it. | `<Object> <past-tense result>.` - "Project deleted." |
| Field label | Sentence case. Names the field's content, not an instruction. | short noun phrase |

### 2c. Facts the line needs and the input does not have

Two of the rules in 2b turn on a fact about the product rather than on the element: a destructive confirmation names how much goes and whether it comes back, and an error names what happened. A request often describes the flow and not the data - "write the copy for deleting a project" says nothing about what a project holds or about what blocks a delete - and self-check 8 forbids shipping a number or a cause the input never confirmed. That leaves the line with a rule it cannot satisfy and a gate it cannot pass.

Do not pick a plausible value. Write the line with the missing fact as a named slot in the position it belongs, and ask for it under the block:

- **Slot, not a guess.** Angle brackets around what is needed: `all <n> tasks inside it`, never `all 14 tasks inside it` on a request that never mentioned tasks.
- **A line carrying a slot is a draft.** It does not ship until the slot is filled, and the `Needs:` line says so by existing.
- **One question per slot**, in the order the slots appear, each naming the element it belongs to.
- **Answered, the block is re-emitted whole** with the slots filled and the `Needs:` line dropped.

Elements whose rules need no product fact ship as finished copy in the same block. A missing count in the confirmation does not hold up the button label next to it.

### 2d. Output format - write mode

```
## <Component or flow name>

**<Element type>:** <copy>
**<Element type>:** <copy>
**<Element type>:** <copy>

**Needs:** <one question per slot, semicolon-separated>
```

One line per element, labeled by type, in the order a user would meet them. The `Needs:` line appears only when a line in the block carries a slot - an empty one is never shipped, the same way an empty `Removed:` is not. For a multi-element flow (a delete confirmation, say), that order is usually: button, confirmation dialog, error, success toast.

## Step 3 - strip mode

### 3a. Identify the element type

If the user names it, use that. If not, infer it from shape - a short imperative phrase reads as a button, a sentence describing a problem reads as an error, a question with an implied yes/no reads as a confirmation - and name the inferred type in the output so the user can correct it.

### 3b. Two checks, not one

**Check 1 - the pattern table.** Compare the copy against every row of [references/banned-patterns.md](references/banned-patterns.md). Five of those rows are bound to a specific element rather than to copy in general, and they catch what the general rows miss:

| What you see | Row it belongs to |
|---|---|
| Title Case on a button or label instead of sentence case | Title Case in labels |
| An error that opens with an apology ("Oops!", "Sorry!") and states no fact | Apology with no fact |
| A confirmation that asks "Are you sure?" without naming what happens if the user says yes | Unnamed consequence |
| An exclamation mark carrying no information ("You're all set!" with nothing after it) | Generic positive closer |
| A decorative emoji the product's own established format did not already use | Decorative emoji |

Every tell named here has a row, because 3d has to report one. A tell with no row is a gap in the table, not a licence to invent a name for it.

**Check 2 - the element's own rule.** Look up the type named in 3a in the table in step 2b and read its rule against the original. The two checks do not overlap: the table asks whether the copy carries a tell, and the rule asks whether the line does the job its element type exists to do. A line can pass all 13 rows and still fail its rule, and the strings this skill is handed most often are exactly that shape:

| Copy | Rows that apply | The 2b rule it fails |
|---|---|---|
| "Nothing here yet." (empty state) | none | Names what belongs in the space, then the one action that fills it |
| "Submit" (button) | none | Starts with a verb and names the outcome |
| "Save changes" as the tooltip on a Save changes button | none | States what the control does, never a restatement of its own label |
| "Your project will be deleted." (toast after the delete ran) | none | States the result, past tense |

"Nothing here yet." is the sharpest of them: step 2b names that exact wording as the empty-state failure, so a check that reads the table alone reports the skill's own banned line as copy that reads fine.

A row that applied and a rule that failed are both defects, and either one ships a rewrite. They are reported on separate lines because they are opposite moves - a row names something taken out, a rule names something the line never had (3d). A 2b rule failure is not a gap in the table and never gets a row invented for it.

Where the rule turns on something the string alone cannot show - the placeholder rule turns on whether the field has a persistent label, which no amount of reading the placeholder reveals - say what the rule turns on and ask. Do not assume the label is there, and do not report the bug on the assumption that it is not.

### 3c. Rewrite: keep the facts, slot the ones the fix needs

Preserve every number, name, and specific claim in the original exactly - a rewrite that fixes tone but changes a fact is a worse bug than the tone. If the copy contains no real facts to preserve (pure filler), the rewrite can be shorter than the original.

Two of the rows in check 1 are only fixable by adding a fact. `Apology with no fact` is fixed by naming what happened; `Unnamed consequence` is fixed by naming what goes and whether it comes back. "Oops! Something went wrong. Please try again later." and "Are you sure?" are the two lines this skill is handed most often, and neither one carries the fact its own fix needs. Cutting is not available - there is nothing invented in the original to cut - and the row applied, so 3d has already ruled out skipping the rewrite. That leaves a plausible guess, which is the thing this skill exists to stop.

The write-mode remedy holds here too. Where the missing fact came from decides which way it goes:

- **The original claims it and the input never confirmed it** -> cut it. The rewrite carries the facts the original carried and no others. This is self-check 8's original case, unchanged.
- **The fix needs it and neither the original nor the request carries it** -> write it as a named slot in the position it belongs (`all <n> <items> inside it`, `because <cause>`) and ask for it on a `Needs:` line under the block.

A rewrite carrying a slot is a draft, exactly as in write mode: it does not ship until the slot is filled, and the `Needs:` line says so by existing. Answered, the block is re-emitted with the slots filled and the line dropped. A slot never appears on the `Before:` line - the original is quoted as the user gave it, tells and all.

Check 2 produces slots the same way, and on copy where no row applied at all. Three of the 2b rules are satisfied by adding a fact the line never had: an empty state names what belongs in the space and the action that fills it, a button names the outcome, an error names what happened. "Nothing here yet." needs both of the empty state's, "Submit" needs the outcome of the form it sits under, and a request that hands over the string alone carries none of them. Slot each one and ask for it, exactly as above. A rule fixed by cutting instead - a tooltip that restates its own label, a toast in the wrong tense - needs nothing from the user and ships finished.

### 3d. Output format - strip mode

```
### <Element type - short label>
- Before: "<original copy>"
- After: "<rewrite>"
- Removed: <pattern name(s) from banned-patterns.md, comma-separated>
- Rule: <the 2b rule for this element type that the original failed>
- Needs: <one question per slot the rewrite carries>
```

One block per string the user gave.

`Needs:` appears only on a block whose rewrite carries a slot (3c), one question per slot, in the order the slots appear. An empty `Needs:` is never shipped, and neither is an empty `Removed:` or an empty `Rule:`.

The two report lines are not interchangeable. `Removed:` carries row names from `references/banned-patterns.md` - what came out of the copy. `Rule:` carries the 2b rule the original failed - what the copy never did. A fix that adds a fact has nothing to put on `Removed:`, and a fix that cuts an adjective has nothing to put on `Rule:`, so each line is present only when its own check found something:

- **At least one row applied, or the 2b rule failed** -> rewrite the line. Name every row that applied on `Removed:`, not just the first, and name the failed rule on `Rule:`.
- **Neither check found anything** -> the copy reads fine. Say so and skip the rewrite. Do not manufacture a change to justify a response, and never invent a pattern name to fill the line.

A block that ships a rewrite carries at least one of `Removed:` and `Rule:`, and a block that carries neither is the skip branch. "No row applied" on its own is not a verdict: it is one check out of two, and on a bare empty state or a bare "Submit" it is the expected result of the check that was never going to catch them.

If a line is plainly wrong and neither check covers it, ship the rewrite, put whatever each check did find on its own line, and add a `Note:` line under the block naming the remaining defect in plain words and saying neither the table nor the 2b rule covers it. An honest gap belongs in the output; an invented row name sends the user to a reference file that does not have it.

## Step 4 - pre-ship self-check (run before either mode's output ships)

Scan the draft against these eight questions. **A single "yes" sends the line back for a rewrite** - this is a gate, not a suggestion.

1. **Preamble?** Does the line open with framing like "Here's your..." or "This will..." instead of stating the message directly? -> Delete the opener.
2. **Negative parallelism?** Any shape like "not just a button - it's peace of mind"? -> Drop the negative half, state the positive claim directly.
3. **Em dash?** Any em dash (—) at all, or an en dash (–) doing an em dash's job between words? The threshold is zero, not two: one em dash in a shipped line already breaks the rule below, and a line short enough to be a button, a toast, or an error rarely holds two, so a "more than one" gate never fires on real interface copy. -> Replace it with a period, a comma, or " - ". A string quoted verbatim is the only exception (see edge cases).
4. **Promotional adjective?** "Seamless", "effortless", "powerful", "intuitive", "robust", "cutting-edge"? -> Cut it, or replace with the concrete fact it was standing in for.
5. **Title Case?** A button or label capitalized like a headline instead of sentence case? -> Lowercase everything but the first word and proper nouns.
6. **Filler verb?** "In order to", "serves as", "is used to" where "to" or "is" would do? -> Replace with the plain verb.
7. **Generic closer?** "Enjoy!", "Happy exploring!", or an exclamation mark with nothing after it? -> Delete it, or replace with the actual next step.
8. **Unverifiable claim?** A number, guarantee, or capability stated as fact that isn't confirmed by the input? -> In write mode, turn it into a slot and ask for it on the `Needs:` line (2c). In strip mode it turns on where the fact came from (3c): a claim the original made and the input never confirmed is cut, and a fact the fix itself needs becomes a slot and a `Needs:` question. "Flag it" means one of those shapes; a guessed fact does not ship with a caveat attached to it.

## Edge cases

| Situation | What to do |
|---|---|
| Copy is legal or compliance-reviewed (terms, consent language, pricing disclaimers) | Flag it as compliance copy instead of rewriting the meaning. Fix only surface AI-tells (em dashes, Title Case) if asked, and say plainly that a meaning-changing edit needs human sign-off first. |
| A brand voice guide is provided | It wins over the defaults in this skill wherever the two conflict. Apply the voice guide's rules first, and fall back to this skill's rules for anything the guide doesn't cover. |
| Request is for non-English copy | The structural rules hold in any language (verb-led buttons, cause-then-fix errors, named consequences). Say plainly that the vocabulary list in `references/banned-patterns.md` is English-specific and does not transfer word for word. |
| Element type isn't stated (write mode) | Infer it from context, write the copy, and name the inferred type in the output so the user can correct it. |
| An element's rule needs a product fact the request never gave (how many items a delete removes, why an upload fails) | Write the line with a named slot where the fact belongs and ask for it on the `Needs:` line. Never fill a slot with a plausible value, and never drop the element to avoid the question - a confirmation with no consequence named is the pattern this skill exists to catch. |
| The row that applied is only fixable by adding a fact the input never gave ("Are you sure?", "Oops! Something went wrong.") | Rewrite with a named slot where the fact belongs and ask for it on the `Needs:` line. Do not skip the rewrite - a row applied, so the copy is not fine - and do not fill the slot with a plausible cause or count. |
| Strip mode is handed a line with no tell that still fails its element's rule ("Nothing here yet.", "Submit", a tooltip repeating its own label) | Rewrite it. No row applied is the expected result of check 1 here, not a verdict - check 2 is the one that catches these. Leave `Removed:` off the block, name the failed rule on `Rule:`, and slot any fact the fix needs. |
| Strip mode is handed a placeholder and the input never says whether the field has a label | The placeholder rule turns on the label, which the string cannot show. Say what the rule turns on and ask. Do not assume a label is there, and do not report the bug on the assumption that it is not. |
| Existing copy already reads fine (strip mode) | Say so and skip the rewrite. "Reads fine" means both checks came back clean, not only the table. An empty "nothing to fix" is a valid result, not a failure to find something. |
| Copy contains a real number or fact from the product | Preserve it exactly. Never invent or round a count, price, or limit that isn't in the input. |
| Copy quotes a string that has to stay verbatim (a legal clause, a third-party product name, text the user typed) | An em dash inside the quotation stays. Fix the ones outside it, and name the one you left and why. An exact quote beats a clean dash count. |

## Rules that hold in both modes

- Sentence case for every button, label, and heading in shipped copy - no exceptions.
- No em dash in shipped copy, and no en dash standing in for one. Zero, not "not too many". Use a period, a comma, or " - " instead. A verbatim quotation is the only place one survives.
- Never invent a number, a guarantee, or a capability that isn't in the input. A fact the line's own rule needs becomes a slot and a `Needs:` question, in either mode; a claim the original made and the input never confirmed is cut.
- Strip mode runs both checks, the pattern table and the element's own rule from 2b. A clean pass on the table is one check out of two, not a verdict that the copy reads fine.
- A failed self-check item means a rewrite, not a footnote explaining the tradeoff.
- Compliance-reviewed copy needs a human sign-off before a meaning-changing edit ships.
- Keep the tone direct. No hedging ("this might possibly need a better label") - either fix it or leave it.
