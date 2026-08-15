# Banned patterns

Read this file before writing or rewriting any copy. It has the 13 patterns that make interface copy read as generated, each with a bad example and a fixed example written for UI copy specifically. Referenced from `SKILL.md` step 0.

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
| Apology with no fact | "Oops! Something went wrong. Please try again later." | "Your changes didn't save because the connection dropped. Reconnect, then save again." |
| Unnamed consequence | "Are you sure?" (delete dialog) | Delete "Q3 Roadmap"? This removes the project and all 14 tasks inside it. This can't be undone. |

## Notes on specific rows

- **Vague attribution**: interface copy rarely needs a citation at all - if a claim needs a source to be true, it usually doesn't belong in a button or a toast. Cut it, or replace it with the actual behavior the user can see.
- **Forced rule of three**: two real, specific properties beat three where the third is padding. Don't add a third adjective just to complete a pattern.
- **Em dash**: the row was called "em-dash overuse" until 2026-08-10, and the name was the bug. One em dash in a button, a toast, or an error is already the tell, and an interface line is rarely long enough to carry two, so a threshold of two meant the check almost never fired while single-dash copy shipped. The threshold is one. An en dash (–) used between words in place of an em dash counts the same. The only survivor is an em dash inside a string quoted verbatim, and the output should say it was left on purpose.
- **Decorative emoji**: emoji used inside the skill's own output examples (like the row above) are for illustration only. In shipped copy, an emoji is allowed only where the product's own established format already uses one - never added by a rewrite to look friendlier.
- **Apology with no fact** and **Unnamed consequence**: both were listed as element-specific tells in `SKILL.md` step 3b from the start, and neither had a row here until 2026-08-15. That was a hole in the output rather than in the check. Strip-mode output names the row that applied, and "Oops! Something went wrong" is the single most common line the skill is handed, so its defect had no name to report and the "Removed" line had no legal value. An apology is not a fact: name what failed and what to do next. A destructive confirmation names what goes, how much of it, and whether it comes back.

## How to use this table

In write mode, check a draft against every row before it ships. In strip mode, name the specific row(s) that applied to the original copy in the "Removed" line of the output - "Removed: promotional adjective, em dash" is more useful to the user than "Removed: AI tells".

Five rows are bound to a specific element rather than to copy in general: Title Case in labels, Generic positive closer, Decorative emoji, Apology with no fact, and Unnamed consequence. They are still rows, checked the same way. Every tell this skill looks for has a row here, because a rewrite that ships has to name one - see `SKILL.md` step 3d for what to do with a defect this table does not cover.
