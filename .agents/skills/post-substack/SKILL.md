---
name: post-substack
description: Turn one finished draft (or a published post) into a Substack Note — the short storytelling post in the Substack feed, a few paragraphs long, not a tweet and not an essay. Keeps the owner's hook, tells the post's story in three beats with its numbers, closes on a takeaway (never a question), links last, and attaches the concept image when one is rendered. Use when the user says "substack note", "substack version", "note for substack", "convert to substack", or "post-substack". Writes to channels/substack/, never to drafts/ or posts/.
---

# post-substack

Substack here means Notes: the short-form feed inside Substack, where the owner posts pieces a few paragraphs long, not essays. A Note is read in a feed, mostly by people who did not subscribe, so the first line does the work. But Substack is a storytelling platform, and the owner reads it that way: after the first line a Note tells a story, what was tried, what turned, what came of it. Growth on Substack is restacks and recommendations (brand wiki, `platforms` and `channels`), and a stranger builder restacks a story that lands. A hook plus one number reads as a clipped tweet there, and a LinkedIn post cut in half is not a story either.

The post already passed the critic and nothing new goes in, so the brand bundle is not read here. Voice comes from the post itself and `tone-samples/*.md`.

## Input

One file:

- **A draft in `drafts/`** — the path the owner gives, or the newest file there when none is given (say which one).
- **A published post in `posts/YYYY/`** — the archive text. Ignore its comments.

Read `lane`, `pillar`, `format`, and `concept_path` from the frontmatter. Derive the image path from `concept_path` (`concepts/<date>-<slug>/prompt.md` → `images/<date>-<slug>/prompt.png`); if the PNG exists, the Note attaches it.

## What a Note is

- **Slightly longer than a tweet, shorter than the post.** Three to five short paragraphs, 400 to 600 characters; 800 is the ceiling. Substack enforces no limit; the feed does, and past 800 it is an essay that belongs elsewhere.
- **Three beats, in the post's order.** The setup (what the owner tried, with its number), the turn (what changed), the outcome (what came of it, with its number). Every beat is in the post already; the Note carries them whole and drops the rest. A Note that keeps every sentence reads like a summary; one that keeps only the hook reads like an ad.
- **No title, no subtitle, no headers.** The first line is the LinkedIn hook as the owner picked it, unless the number reads harder alone (`$368 on Meta ads. Three sign-ups.` already does).
- **The numbers that carry the arc.** Keep the setup number and the outcome number as the post states them. Receipts between them stay only when the turn needs them to make sense.
- **Line breaks as in the post.** Plain text. Bold and italic exist on Notes and are not used.
- **One link, last, or none.** A link makes a preview card under the text. The draft's `Comment link:` returns here as the last line, on its own. Never link the LinkedIn post.
- **The image is the concept render** when it exists. Its hook overlay is English, so it matches; square is fine in the feed. Say `Attach: <path>` after the Note.
- **Ending is a takeaway or a plain stance. Never a question**, not as the closer and not as the hook. A question hands the story back unfinished; the Note ends where the story does. No `restack if`, no hashtags, no emoji.

## Voice

The post's voice, a little tighter. Every hard rule from `post-writer` holds: no emoji, no em dashes, no quotation marks, no LinkedIn vocabulary, no anonymous actors, no flourish verbs over a number, no `X. Not Y.` couplets, no mic-drop closer. At this length one balanced couplet stands out, so read it aloud.

Nothing is added. If the post has no number, the Note has none; the Kill Test still applies (a generic indie developer could not post it). If the post ends on a question, the Note ends one beat earlier, on the stance the question was pointing at; do not invent a new closer.

## Formats other than text

- **`format: carousel`** — the story of the comparison: what was compared and why, which one won and for whom, in two or three lines (`Compared A, B, C for X. C won, and it is not close.`), then the link or the image. The cells do not come along.
- **`format: decision-tree`** — the decision stated, not asked (`Which notebook tool to use, by constraint`), the one branch that matters most with its recommendation, then the image. The tree image carries the question; the Note does not end on it.

## Output file

Save to `channels/substack/<YYYY-MM-DD>-<slug>.md`, the draft's own filename stem (for `posts/YYYY/MM-DD-<slug>.md`, `YYYY-MM-DD-<slug>`). Create the directory if needed, overwrite on a re-run. `channels/` is gitignored. Never write to `drafts/` or `posts/`.

```yaml
---
draft_path: drafts/2026-09-14-368-on-meta-ads-three-sign-ups.md
lane: experience
pillar: didnt-teach-me            # experience lane only
kind: note
char_count: 540
image: images/2026-09-14-368-on-meta-ads-three-sign-ups/prompt.png   # or null
generated_at: 2026-09-14T12:00:00.000Z
status: drafted
---
```

The body is the Note exactly as it is pasted.

## Print

Print the Note, then `Characters: <n>`, then `Attach: <image path>` when there is one, then `Want anything moved, cut, or said differently?` Apply edits, re-count, re-save.

## Checklist

- [ ] First line is the hook and reads in milliseconds.
- [ ] The story is whole: setup, turn, outcome, in the post's order, 400 to 600 characters (800 at most). Not the post cut in half, not a summary of every sentence.
- [ ] Nothing in the Note that was not in the post.
- [ ] No emoji, hashtags, em dashes, quotation marks, bold, or `restack` prose.
- [ ] Link last and alone, if any. Image path is real, if given.
- [ ] Ending is a takeaway or a plain stance. No question anywhere in the Note.

## When to use

- "substack note" / "substack version" / "note for substack" / "post-substack"

## When NOT to use

- Writing the post → `post-writer`. The Telegram translation → `post-telegram`.
- A Substack essay. The wiki's `content-engine` has one essay a month rolled up from the month's artifacts; that is a different job and this skill does not do it.
