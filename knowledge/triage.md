# Triage card

**Trigger:** a message that starts with `triage` followed by one or more page URLs, for example `triage https://example.com/`.

Reply with one card per URL, in the order given, and nothing else: no intro, no explanation, no follow-up question. Put each card in a code block so its four lines stay on separate lines:

```
🟡 Mostly ready · ~5 h
Reuses: hero, cards, columns · New: carousel
Watch out: newsletter form (its back end stays where it is)
Next: say "migrate it" to start
```

## How to fill it in

1. Read the page once, with `curl` or a browser tool. Don't start a migration, page analysis or site scope: a triage takes seconds, not minutes.
2. List this project's blocks: the folder names under `blocks/`.
3. Go through the page's sections from top to bottom, skipping the header, footer and cookie banner. A section is either default content (headings, text, images, plain links and buttons), which needs no block, or a block. Use an existing block when it fits the section's layout; otherwise it's a new block, named in lowercase kebab-case (`carousel`, `logo-wall`).
4. Fill in the four lines from those sections only. A search box or sign-in link in the header doesn't count.

| Line | What goes in it |
|---|---|
| 1 | The light, its label and the hours |
| 2 | `Reuses:` the existing blocks the page needs, or `none`, then `· New:` the blocks to build, or `none` |
| 3 | `Watch out:` the one biggest risk, with a few words on why. Pick the first that applies: sign-in or account area, site search, personalization, forms, embedded video or maps, other third-party widgets. Otherwise `nothing obvious` |
| 4 | Always `Next: say "migrate it" to start` |

## The light

| Light | Label | When |
|---|---|---|
| 🟢 | Ready | No new blocks |
| 🟡 | Mostly ready | 1 or 2 new blocks |
| 🔴 | Needs work | 3 or more new blocks, or the page has a sign-in or account area, site search or personalization |

## The hours

`1 h for the page + 4 h per new block`, in whole hours. The example above is 1 + 4 = 5 h.

These are sample team rates for this PoC, not measured ones. Replace them with real figures once a pilot gives you some, and every agent's cards change with them.

## If the page can't be read

Reply with one line instead of the card: `⚪ Can't triage <url>: <reason>`, for example a 403, a sign-in page or a timeout. Never guess a card.
