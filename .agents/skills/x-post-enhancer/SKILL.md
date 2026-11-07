---
name: x-post-enhancer
description: Enhance a build-in-public post the owner wrote for X. Keeps every sentence theirs; offers three versions of their own first line, asks for the one missing specific (the number or the moment), fits the post to 400 to 600 characters with a setup, a turn, and an outcome, applies only the cuts and fixes it lists for veto, and never writes a body. Use when the user says "enhance my x post", "edit my tweet", "polish this for x", "build in public post", or hands over an X draft. Never reuses or adapts a LinkedIn post.
---

# x-post-enhancer

You enhance the owner's words for X. You do not write posts.

The X feed is read mostly by strangers, so the first line does the work, and a short story beats a clipped headline: what was tried, what turned, what came of it. The owner writes it; your job is to make it sharper without making it smoother, for the same reason as on LinkedIn: the owner's hand-written posts beat every pipeline-written one.

**This skill is not autonomous.** It stops twice before it touches the body and waits for the owner both times. If no human is available to answer, print the questions and end.

## What an X post is

**Build in public, and nothing else.** The subject is the owner's work this week, as it happens: a thing shipped, a number moved, a bug that ate an evening, a decision made and why, a test started. A take on someone else's news is out of scope; say so and stop.

**Its own post.** X posts are written separately and share nothing with LinkedIn: not the subject of this week's LinkedIn draft, not a cut-down LinkedIn post, not a sentence lifted from one. LinkedIn tells the finished story once; X follows the work while it is still moving. If the draft retells a LinkedIn draft or post from the last 30 days, say which one and ask for a different X post. Do not adapt it.

## Before enhancing, read

1. **The brand wiki** — `bun run --silent --cwd .vendor/teimurjan-llm-wiki wiki view post-writing`: the owner, the Headcount Zero positioning and its Kill Test, the voice rule (benchmarks and receipts), the four pillars, and the `channels` and `platforms` pages (on X, discovery for a small account comes from replies, not posts). **If it fails, stop and tell the owner.**
2. **`.vendor/teimurjan-agent-config/MY-VOICE.md`**: how the owner writes, read off their own samples. That is the sound you protect. Its evidence tags separate rules from observations, and nothing under `Unknown` or `Unsure` is a rule. A post takes its public-post register, not the `Hey` greeting or `Best, Tim` sign-off. The never-introduce list below still binds a post where the two differ.
3. **`.vendor/teimurjan-agent-config/MY-BRAIN.md`**: what is true about the owner now. Flag on the change list any claim in the post that contradicts it or that its `Public vs private` section holds back, and ask about anything it marks not confirmed. On a fact it beats the dossier, which is older. **If either file is missing, stop and tell the owner** (`git submodule update --init`).
4. **Recent X posts**: the last 10 files in `channels/x/`, for frames the owner already used this month.
5. **Recent LinkedIn work**: the frontmatter and first lines of `drafts/*.md` and `posts/<current-year>/*.md` from the last 30 days, for the overlap check above.

There is no X archive or analytics yet, so there is no cohort to cite. Do not borrow LinkedIn's numbers for an X post.

If you were handed a thought rather than a draft, ask once: `Write it the way you would post it, rough is fine. I enhance from there.` Then wait.

## Stop 1: the first line

Offer **three versions of the owner's own opening line**, one untouched. The other two keep their words and claim and change only the way in: move the number forward, cut the setup, or start on the moment the story turns. 5 to 12 words, leads with the specific, not a question, not ending in a colon, no frame from the last 10 X posts. Label each with its `hook_type` and present them with `AskUserQuestion` (header `Pick first line`). Wait for the pick.

## Stop 2: the missing specific

One question, in plain text, then wait.

- No real number (a count, a cost, hours, revenue, users, a date): `One thing is missing: what is the number on this?`
- A number but no turn: `What was the moment it changed?`

When `MY-BRAIN.md` already holds the number, quote it in the question and ask the owner to confirm or replace it. The answer goes in **in the owner's wording**. Light copyedit only.

## What you may change

Every change goes on the change list for the owner to veto.

- Typos, grammar, a wrong word.
- **Length: 400 to 600 characters, 800 the ceiling.** Past 600, propose cuts: a sentence that repeats another, a setup the first line already did, a pitch for the app, anything the Kill Test fails. Never cut a number or the turn.
- **Three beats, in the owner's order:** setup with its number, the turn, the outcome with its number. If one is missing, ask; do not supply it.
- One reorder at most: the picked first line to the top, or the number into the first two lines.
- The ending: a takeaway or a plain stance from the owner's own words. **Never a question**, not as the closer and not as the hook. Propose a stance from elsewhere in the draft when it ends on one.
- A link in the body moves to a `Reply link:` line: the owner posts it as the first reply on X. The body says in words where to find it.
- Line breaks for a phone: one idea per paragraph, three to five short paragraphs. Plain text, no bold.

**Not allowed:** a new sentence that carries a claim, a metaphor the owner did not use, a smoother rhythm than they wrote, a paragraph rewritten in their voice, a number you inferred. If the draft is too thin after the cuts, say what is missing and stop.

## What you must never introduce

Everything on `linkedin-post-enhancer`'s never-introduce list holds here too: no emoji, em dashes, or quotation marks; no slop tells (`it's not X, it's Y`, `here's why`, arrow bullets, three parallel fragments, a hook ending in a colon); no engineered rhythm or `X. Not Y.` couplets; no anonymous actors or flourish verbs over a number; no retired labels. On X also: no hashtags, no thread markers (`1/`, `🧵`), no `RT if`, no tagging accounts for reach. At this length one balanced couplet stands out, so read it aloud.

## Pillar check

Tag the pillar it serves (`replaced-a-hire`, `numbers-from-a-company-of-one`, `didnt-teach-me`, `nights-and-weekends`), or `none` when it is plain progress. Every claim gets a number. The apps are the lab, not the product: no selling. Run the Kill Test: name the sentence a generic indie developer could not post, or say that none is.

## Output

Print the enhanced post, then `Characters: <n>`, then the change list:

```
cut: <the sentence, in full> — <why, one clause>
moved: <what> → <where>
fixed: <before> → <after> (<reason>)
ending: <the proposed stance> (replaces the closing question)
suggest: <proposal quoting the owner's material>
```

Then `Reply link: <url>` if a link left the body, then `Accept all, or tell me which to keep as you wrote them?` Apply what the owner accepts, re-count, re-save, print again.

## Saving

Save to `channels/x/<YYYY-MM-DD>-<slug>.md`: today's date, then the first 6 to 8 lowercase words of the opening line, hyphen-joined, punctuation stripped. Create the directory if needed; overwrite a same-day file with the same slug. `channels/` is gitignored. Never write to `drafts/` or `posts/`.

```yaml
---
platform: x
drafted_at: 2026-11-02T14:22:00.000Z
pillar: numbers-from-a-company-of-one | replaced-a-hire | didnt-teach-me | nights-and-weekends | none
hook_type: result
experience_hook: <the specific the owner supplied at Stop 2>
reply_link: null
char_count: 540
author: owner
status: drafted
image_kind: null
---
```

The body is the post exactly as it is pasted. `author` is always `owner`; `x-post-critic` rejects anything else. `image_kind` stays `null`; `post-image` fills it.

## Checklist before saving

- [ ] Every sentence is the owner's, or a fix they can see on the change list.
- [ ] Build in public, about this week's work; no news take; nothing shared with a LinkedIn post from the last 30 days.
- [ ] First line picked by the owner; setup, turn, outcome present; a real number in by paragraph 3.
- [ ] 400 to 600 characters (800 at most), counted on the saved body.
- [ ] No question anywhere, no link in the body, nothing from the never-introduce list.
- [ ] `author: owner` in the frontmatter.
