# Banned patterns

Read this file before writing or rewriting any copy. It has the 11 patterns that make interface copy read as generated, each with a bad example and a fixed example written for UI copy specifically. Referenced from `SKILL.md` step 0.

All examples below are invented for illustration - no real product, client, or user is named.

| Pattern | Bad example (interface copy) | Fixed example |
|---|---|---|
| Inflated significance | "Congratulations! You've unlocked a whole new way to manage your projects." | "Project created." |
| Promotional adjective | "Enjoy a seamless, effortless checkout experience." | "Checkout takes about 2 minutes." |
| Negative parallelism | "This isn't just a delete button - it's peace of mind." | "Delete removes the file. This can't be undone." |
| Vague attribution | "Studies show users love a clean inbox." | "Archived items move here automatically." |
| Filler phrase | "In order to save your changes, please click the button below." | "To save your changes, click Save." |
| Copula avoidance | "This toggle serves as a way to enable dark mode." | "This toggle turns on dark mode." |
| Forced rule of three | "Fast, simple, and powerful project tracking." | "Track projects without leaving your inbox." |
| Em dash | "Your export is ready — download it before the link expires." | "Your export is ready. Download it before the link expires." |
| Title Case in labels | "Save Changes" (button) | "Save changes" |
| Generic positive closer | "You're all set! Enjoy the app!" | "You're all set. Next: invite your team." |
| Decorative emoji | "Upload complete! 🎉" | "Upload complete." |

## Notes on specific rows

- **Vague attribution**: interface copy rarely needs a citation at all - if a claim needs a source to be true, it usually doesn't belong in a button or a toast. Cut it, or replace it with the actual behavior the user can see.
- **Forced rule of three**: two real, specific properties beat three where the third is padding. Don't add a third adjective just to complete a pattern.
- **Em dash**: the row was called "em-dash overuse" until 2026-08-10, and the name was the bug. One em dash in a button, a toast, or an error is already the tell, and an interface line is rarely long enough to carry two, so a threshold of two meant the check almost never fired while single-dash copy shipped. The threshold is one. An en dash (–) used between words in place of an em dash counts the same. The only survivor is an em dash inside a string quoted verbatim, and the output should say it was left on purpose.
- **Decorative emoji**: emoji used inside the skill's own output examples (like the row above) are for illustration only. In shipped copy, an emoji is allowed only where the product's own established format already uses one - never added by a rewrite to look friendlier.

## How to use this table

In write mode, check a draft against every row before it ships. In strip mode, name the specific row(s) that applied to the original copy in the "Removed" line of the output - "Removed: promotional adjective, em dash" is more useful to the user than "Removed: AI tells".
