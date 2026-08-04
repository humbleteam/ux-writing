<div align="center">

<h1>UX writing</h1>

**Turn a UI component or flow into interface copy that reads human, or strip AI-generated tells out of copy you already have - a Claude Code skill built for design teams and the engineers who ship their work.**

[![CI](https://img.shields.io/github/actions/workflow/status/humbleteam/ux-writing/validate.yml?branch=main&style=for-the-badge&logo=github&label=CI)](https://github.com/humbleteam/ux-writing/actions/workflows/validate.yml)
[![GitHub stars](https://img.shields.io/github/stars/humbleteam/ux-writing?style=for-the-badge&logo=github&color=181717)](https://github.com/humbleteam/ux-writing/stargazers)
[![Last commit](https://img.shields.io/github/last-commit/humbleteam/ux-writing?style=for-the-badge&color=339933)](https://github.com/humbleteam/ux-writing/commits/main)
[![License](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude_Code-skill-D97757?style=for-the-badge&logo=anthropic&logoColor=white)](https://github.com/humbleteam/ux-writing/blob/main/SKILL.md)

</div>

ux-writing takes a UI component or flow - a button, an error message, an empty state, a confirmation dialog - and returns copy ready to ship: a verb-led label, a plain-language error, a consequence-named confirmation. Given copy that already exists, it switches to strip mode and rewrites it line by line, naming the pattern each fix removed. A pre-ship self-check keeps either mode from drifting into generic filler: eight yes/no questions run against every draft, and one "yes" sends the line back for a rewrite.

## Table of contents

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Usage](#usage)
- [Example output](#example-output)
- [How it works](#how-it-works)
- [How is this different from just asking the model?](#how-is-this-different-from-just-asking-the-model)
- [FAQ](#faq)
- [Related skills](#related-skills)
- [Who maintains this](#who-maintains-this)

## What it does

- Writes microcopy for buttons, errors, empty states, confirmations, placeholders, tooltips, and toasts - one shippable line per element.
- Rewrites existing copy that reads AI-generated, in strip mode, line by line, with Before/After pairs.
- Runs every draft through an eight-question pre-ship self-check; a failed check forces a rewrite, not a footnote.
- Names the outcome in every button label instead of a bare verb like "Submit" or "OK".
- Writes error copy as what happened plus how to fix it, with no blame and no bare apology.
- Defers to a provided brand voice guide wherever its rules conflict with the defaults here.

## Quick start

**Personal - available in every project:**

```bash
git clone https://github.com/humbleteam/ux-writing ~/.claude/skills/ux-writing
```

**Project-scoped - checked into one repo:**

```bash
git clone https://github.com/humbleteam/ux-writing .claude/skills/ux-writing
```

**Any other agent:** the skill is plain markdown in the Agent Skills format. Paste `SKILL.md` into the system prompt of Cursor, Codex, or any other LLM agent - no Claude-specific runtime required.

To verify: restart Claude Code, then ask it to list its skills. Skills load automatically from `~/.claude/skills/` (personal) and `.claude/skills/` (project); `ux-writing` should appear.

## Usage

- **"Write the button, confirmation, and error copy for this delete-project flow."** - write mode: breaks the flow into its elements and writes each to its type's rule.
- **"This error message sounds like an AI wrote it: 'Oops! Something went wrong. Please try again later.'"** - strip mode: rewrites the line and names the patterns removed.
- **"Draft the empty-state copy for a project list with zero projects."** - write mode against a single element: what's missing, plus the one action that fills it.

## Example output

Example write-mode output for a fictional delete-project flow - names invented for illustration:

```
## Delete project flow

**Button (destructive):** Delete project

**Confirmation dialog:** Delete "Q3 Roadmap"? This removes the project and
all 14 tasks inside it. This can't be undone.

**Buttons:** Cancel / Delete project

**Error (delete failed):** The project didn't delete because it still has
2 members assigned. Remove the members first, then try again.

**Toast (success):** Project deleted.
```

## How it works

- **Mode detection first.** A component or flow with no existing copy triggers write mode; a string of copy, or a request to fix copy that "sounds AI", triggers strip mode.
- **The pattern table loads before either mode runs.** `references/banned-patterns.md` holds 11 AI-tell patterns, each with a bad and fixed example, checked before a draft is done.
- **Buttons name the outcome.** Verb first, then the object, sentence case - never a bare "Submit" or "OK" when a concrete outcome exists to name.
- **Errors state cause, then fix.** What happened, then how to fix it - no blame language, no meaningless apology.
- **Empty states name what's missing and the one action that fills it.** Never a bare "Nothing here yet" with no next step.
- **Destructive confirmations name the consequence.** What gets removed, how much, whether it's reversible - never a generic "Are you sure?"
- **Placeholder text is never a label's substitute.** If removing it would leave a field unlabeled, that's a bug to flag, not a copy choice.
- **The eight-question self-check runs before every output ships.** One "yes" sends the line back for a rewrite.
- **Legal or compliance-reviewed copy gets flagged, not silently rewritten.** A meaning-changing edit needs a human sign-off first.

## How is this different from just asking the model?

A bare "write me a button label" prompt tends to return exactly the copy this skill exists to catch: "Submit", or an error that opens with "Oops! Something went wrong" and gives no next step. It also drifts toward promotional filler - "seamlessly", "effortlessly" - words that sound confident but tell the user nothing to do. This skill pins the shape down per element type (button = verb plus outcome, error = cause plus fix, confirmation = named consequence) and runs a fixed eight-question check before the draft ships, so the output holds shape run to run. It does not know your product's actual voice - a provided brand voice guide wins where its rules conflict with the defaults here.

## FAQ

**How do I make AI writing sound human?**
Cut patterns that read as generated before the copy ships: promotional adjectives (seamless, effortless), negative parallelism ("it's not just X - it's Y"), filler openers ("in order to"), and copula avoidance ("serves as" instead of "is"). This skill checks every draft against eight questions; `references/banned-patterns.md` has the full table.

**What are AI writing tells?**
Patterns that show up disproportionately in generated text: promotional adjectives, negative parallelism, vague attributions, forced rule-of-three lists, em dash overuse, generic upbeat closers. In interface copy they also show up as Title Case buttons and "Oops!" errors with no fact. `references/banned-patterns.md` lists all 11 with a before/after example each.

**How do I write good error messages?**
State what happened, then how to fix it. "The project didn't delete because it still has 2 members assigned. Remove the members first, then try again" beats "Oops! Something went wrong" - it gives a fact and an action, not an apology. Never blame the user.

**Should button labels be Title Case?**
No - sentence case. "Save changes", not "Save Changes". Title Case reads as a menu item or a headline, not an action. Sentence case is Material Design's default; Apple's Human Interface Guidelines leave the choice between title-style and sentence-style to each app, favoring title-style for navigation titles.

**What is UX writing?**
The words in a product's interface - buttons, errors, empty states, tooltips, confirmations - chosen deliberately, not left as engineering placeholders. This skill works at the sentence level: what makes one label or error clear, and what makes copy read as generated instead of written for its screen.

**Can Claude write microcopy for my app?**
Yes, with real product context. Describe the component or flow - what it does, what happens if it fails, what a destructive action removes - and this skill returns a label, error, or confirmation. Less context produces a more generic draft, same as for a person.

## Related skills

Part of a 10-skill open-source kit for design teams by Humbleteam.

- [design-review](https://github.com/humbleteam/design-review) - structured UX critique with a 0-4 score, Before/After/Why fixes, and a citation for every claim.
- [ascii-wireframes](https://github.com/humbleteam/ascii-wireframes) - three distinct layout hypotheses as ASCII wireframes before any hi-fi work.
- [html-mockup](https://github.com/humbleteam/html-mockup) - census-first HTML mockups that match a reference screenshot: exact palette, item counts, component states.
- [extract-design-tokens](https://github.com/humbleteam/extract-design-tokens) - pull palette, type, spacing, radii, and shadows from a URL or screenshot into CSS variables and JSON.
- [audit-design-tokens](https://github.com/humbleteam/audit-design-tokens) - find token drift in a codebase: raw hex values, off-scale spacing, near-duplicate colors.
- [design-qa](https://github.com/humbleteam/design-qa) - a pre-ship design QA gate: states, contrast, touch targets, breakpoints, keyboard paths.
- [design-handoff](https://github.com/humbleteam/design-handoff) - turn a finished mockup into a dev-ready spec: tokens, states, accessibility annotations, open questions.
- [accessibility-audit](https://github.com/humbleteam/accessibility-audit) - WCAG 2.2-grounded accessibility review with success-criterion citations and severity levels.
- [design-brief](https://github.com/humbleteam/design-brief) - extract a 5-bullet design brief from messy project inputs, with a gap report for what is missing.

## Who maintains this

Maintained by [Humbleteam](https://humbleteam.com/ai), a design and AI-engineering studio that builds AI infrastructure for design teams. This skill is distilled from the internal playbooks we run on client work. Issues and PRs welcome.

MIT - see [LICENSE](LICENSE).
