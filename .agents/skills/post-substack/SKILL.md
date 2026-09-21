---
name: post-substack
description: Turn one finished draft (or a published post) into a Substack Note — the short, tweet-length post in the Substack feed, not an essay. Keeps the owner's hook and the one number, cuts the rest, links last, and attaches the concept image when one is rendered. Use when the user says "substack note", "substack version", "note for substack", "convert to substack", or "post-substack". Writes to channels/substack/, never to drafts/ or posts/.
---

# post-substack

Substack here means Notes: the short-form feed inside Substack, where the owner posts tweet-length pieces, not essays. A Note is read in a feed, mostly by people who did not subscribe, so it works like a tweet: the first line does the work, one specific, one stance, done. Growth on Substack is restacks and recommendations (brand wiki, `platforms` and `channels`), so the target is a Note a stranger builder would restack. A LinkedIn post cut in half is not that.

The post already passed the critic and nothing new goes in, so the brand bundle is not read here. Voice comes from the post itself and `tone-samples/*.md`.

## Input

One file:

- **A draft in `drafts/`** — the path the owner gives, or the newest file there when none is given (say which one).
- **A published post in `posts/YYYY/`** — the archive text. Ignore its comments.

Read `lane`, `pillar`, `format`, and `concept_path` from the frontmatter. Derive the image path from `concept_path` (`concepts/<date>-<slug>/prompt.md` → `images/<date>-<slug>/prompt.png`); if the PNG exists, the Note attaches it.

## What a Note is

- **Tweet-length.** One to four short lines. Under 300 characters is the target, 500 the ceiling. Substack enforces no limit; the feed does.
- **No title, no subtitle, no headers.** The first line is the LinkedIn hook as the owner picked it, unless the number reads harder alone (`$368 on Meta ads. Three sign-ups.` already does).
- **One number, one stance.** Keep the hook, the single strongest specific, and the closer's stance or question. The middle of the post is what gets cut, not compressed. A Note that tries to keep every beat of the post reads like a summary.
- **Line breaks as in the post.** Plain text. Bold and italic exist on Notes and are not used.
- **One link, last, or none.** A link makes a preview card under the text. The draft's `Comment link:` returns here as the last line, on its own. Never link the LinkedIn post.
- **The image is the concept render** when it exists. Its hook overlay is English, so it matches; square is fine in the feed. Say `Attach: <path>` after the Note.
- **Ending is a stance or a real question.** A question does more on Notes than on LinkedIn because replies are the feed. No `restack if`, no hashtags, no emoji.

## Voice

The post's voice, tighter. Every hard rule from `post-writer` holds: no emoji, no em dashes, no quotation marks, no LinkedIn vocabulary, no anonymous actors, no flourish verbs over a number, no `X. Not Y.` couplets, no mic-drop closer. At this length a single balanced couplet is the whole Note, so the tell is louder; read it aloud.

Nothing is added. If the post has no number, the Note has none; the Kill Test still applies (a generic indie developer could not post it).

## Formats other than text

- **`format: carousel`** — the takeaway stance and the tool names in one or two lines (`Compared A, B, C for X. C, and it is not close.`), then the link or the image. The cells do not come along.
- **`format: decision-tree`** — the root question as the first line, the one branch that matters most as the second, or the question alone plus the image.

## Output file

Save to `channels/substack/<YYYY-MM-DD>-<slug>.md`, the draft's own filename stem (for `posts/YYYY/MM-DD-<slug>.md`, `YYYY-MM-DD-<slug>`). Create the directory if needed, overwrite on a re-run. `channels/` is gitignored. Never write to `drafts/` or `posts/`.

```yaml
---
draft_path: drafts/2026-09-14-368-on-meta-ads-three-sign-ups.md
lane: experience
pillar: didnt-teach-me            # experience lane only
kind: note
char_count: 212
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
- [ ] One number, one stance, under 300 characters (500 at most). The middle of the post is gone, not summarized.
- [ ] Nothing in the Note that was not in the post.
- [ ] No emoji, hashtags, em dashes, quotation marks, bold, or `restack` prose.
- [ ] Link last and alone, if any. Image path is real, if given.
- [ ] Ending is a stance or a real question.

## When to use

- "substack note" / "substack version" / "note for substack" / "post-substack"

## When NOT to use

- Writing the post → `post-writer`. The Telegram translation → `post-telegram`.
- A Substack essay. The wiki's `content-engine` has one essay a month rolled up from the month's artifacts; that is a different job and this skill does not do it.
