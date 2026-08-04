---
name: ux-writing
description: Write interface microcopy for buttons, error messages, empty states, and confirmations, or strip AI-generated tells out of copy you already have. Use for "write the button copy for...", "draft an error message for...", "this copy sounds AI-generated", "write empty state copy", or "rewrite this confirmation dialog". Do not use for marketing pages or long-form content - interface microcopy only.
---

# UX writing

Write interface copy that reads like someone thought about the specific screen, or rewrite copy that reads like a model generated it.

## Step 0 - load the pattern table

Before writing or rewriting anything, read [references/banned-patterns.md](references/banned-patterns.md) if it is not already in context. It has the 11 AI-tell patterns this skill checks for, each with a bad and fixed example in interface copy. Do not skip this even if the patterns look familiar - the exact wording matters for a consistent check every run.

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

### 2c. Output format - write mode

```
## <Component or flow name>

**<Element type>:** <copy>
**<Element type>:** <copy>
**<Element type>:** <copy>
```

One line per element, labeled by type, in the order a user would meet them. For a multi-element flow (a delete confirmation, say), that order is usually: button, confirmation dialog, error, success toast.

## Step 3 - strip mode

### 3a. Identify the element type

If the user names it, use that. If not, infer it from shape - a short imperative phrase reads as a button, a sentence describing a problem reads as an error, a question with an implied yes/no reads as a confirmation - and name the inferred type in the output so the user can correct it.

### 3b. Check against the pattern table

Compare the copy against every row of [references/banned-patterns.md](references/banned-patterns.md), plus these element-specific tells:

- Title Case on a button or label instead of sentence case.
- An error message that opens with an apology ("Oops!", "Sorry!") and states no fact.
- A confirmation that asks "Are you sure?" without naming what happens if the user says yes.
- An exclamation mark carrying no information ("You're all set!" with nothing after it).
- A decorative emoji the product's own established format did not already use.

### 3c. Rewrite, keep the meaning and the facts

Preserve every number, name, and specific claim in the original exactly - a rewrite that fixes tone but changes a fact is a worse bug than the tone. If the copy contains no real facts to preserve (pure filler), the rewrite can be shorter than the original.

### 3d. Output format - strip mode

```
### <Element type - short label>
- Before: "<original copy>"
- After: "<rewrite>"
- Removed: <pattern name(s) from banned-patterns.md, comma-separated>
```

One block per string the user gave. If the copy already reads fine, say so and skip the rewrite - do not manufacture a change to justify a response.

## Step 4 - pre-ship self-check (run before either mode's output ships)

Scan the draft against these eight questions. **A single "yes" sends the line back for a rewrite** - this is a gate, not a suggestion.

1. **Preamble?** Does the line open with framing like "Here's your..." or "This will..." instead of stating the message directly? -> Delete the opener.
2. **Negative parallelism?** Any shape like "not just a button - it's peace of mind"? -> Drop the negative half, state the positive claim directly.
3. **Em-dash count?** More than one em dash in the line? -> Replace with a period or " - ".
4. **Promotional adjective?** "Seamless", "effortless", "powerful", "intuitive", "robust", "cutting-edge"? -> Cut it, or replace with the concrete fact it was standing in for.
5. **Title Case?** A button or label capitalized like a headline instead of sentence case? -> Lowercase everything but the first word and proper nouns.
6. **Filler verb?** "In order to", "serves as", "is used to" where "to" or "is" would do? -> Replace with the plain verb.
7. **Generic closer?** "Enjoy!", "Happy exploring!", or an exclamation mark with nothing after it? -> Delete it, or replace with the actual next step.
8. **Unverifiable claim?** A number, guarantee, or capability stated as fact that isn't confirmed by the input? -> Cut it, or flag it for the user to confirm before it ships.

## Edge cases

| Situation | What to do |
|---|---|
| Copy is legal or compliance-reviewed (terms, consent language, pricing disclaimers) | Flag it as compliance copy instead of rewriting the meaning. Fix only surface AI-tells (em dashes, Title Case) if asked, and say plainly that a meaning-changing edit needs human sign-off first. |
| A brand voice guide is provided | It wins over the defaults in this skill wherever the two conflict. Apply the voice guide's rules first, and fall back to this skill's rules for anything the guide doesn't cover. |
| Request is for non-English copy | The structural rules hold in any language (verb-led buttons, cause-then-fix errors, named consequences). Say plainly that the vocabulary list in `references/banned-patterns.md` is English-specific and does not transfer word for word. |
| Element type isn't stated (write mode) | Infer it from context, write the copy, and name the inferred type in the output so the user can correct it. |
| Existing copy already reads fine (strip mode) | Say so and skip the rewrite. An empty "nothing to fix" is a valid result, not a failure to find something. |
| Copy contains a real number or fact from the product | Preserve it exactly. Never invent or round a count, price, or limit that isn't in the input. |

## Rules that hold in both modes

- Sentence case for every button, label, and heading in shipped copy - no exceptions.
- No em dash in shipped copy. Use a period, a comma, or " - " instead.
- Never invent a number, a guarantee, or a capability that isn't in the input.
- A failed self-check item means a rewrite, not a footnote explaining the tradeoff.
- Compliance-reviewed copy needs a human sign-off before a meaning-changing edit ships.
- Keep the tone direct. No hedging ("this might possibly need a better label") - either fix it or leave it.
