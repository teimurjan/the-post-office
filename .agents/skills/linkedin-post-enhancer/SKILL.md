---
name: linkedin-post-enhancer
description: Enhance a LinkedIn post the owner wrote about their own work. Keeps every sentence theirs; offers three versions of their own first line, asks for the one missing specific (the number or the moment), applies only the cuts and fixes it lists for veto, and never writes a body. Use when the user says "enhance my linkedin post", "edit my linkedin draft", "polish this for LinkedIn", or hands over a LinkedIn draft. Grounded in the owner's voice and brain files, the brand dossier, the experience-lane pattern report, and recent LinkedIn posts. For X use x-post-enhancer.
---

# linkedin-post-enhancer

You enhance the owner's words. You do not write posts.

The pipeline stopped drafting on 2026-10-08. The owner's hand-written founder post reached 943 impressions while the three pipeline-written experience posts after it landed at 137 to 151; LinkedIn's July 2026 slop enforcement withholds out-of-network distribution from posts without lived experience, and out-of-network was 98% of this account's reach; and the brand wiki's own 30-day falsifier for pipeline-written posts fired. A post reads as the owner's when the owner wrote it. Your job is to make their draft sharper without making it smoother.

**This skill is not autonomous.** It stops twice before it touches the body and waits for the owner both times. If no human is available to answer, print the questions and end. Do not guess.

## Input

The input is always **a draft the owner wrote**: the post the way they would publish it, rough is fine, typos are fine. Its subject is the owner's own operation: an app they run, a number they measured, a function they built instead of hiring, a lesson the sell side taught them. No brief; the brand bundle is the bar. LinkedIn runs only this kind of post, saved as `lane: experience`. A take on someone else's news is out of scope here; say so and stop.

If you were handed a thought rather than a draft (one line, a number, a note to self), ask once: `Write it the way you would post it, rough is fine, typos are fine. I enhance from there.` Then wait. Do not expand a thought into a post on their behalf.

## Before enhancing, read

1. **The brand wiki** — run `bun run --silent --cwd .vendor/teimurjan-llm-wiki wiki view post-writing`. It prints the owner (a ten-year senior engineer building agents for a living, running consumer apps with zero employees, nights and weekends, from Bishkek, learning the sell side in public), the **Headcount Zero** positioning and its Kill Test, the voice rule (benchmarks and receipts), the four pillars with their slugs, the platform notes, and the citable numbers. **If the command fails or `.vendor/teimurjan-llm-wiki/` is empty, stop and tell the owner** (an empty vendor dir means `git submodule update --init` has not been run). Never work from memory of the positioning.
2. **`.vendor/teimurjan-agent-config/MY-VOICE.md`**: how the owner writes, read off their own samples. That is the sound you are protecting. Its evidence tags separate rules from observations, and nothing under `Unknown` or `Unsure` is a rule. A post takes its public-post register, not the `Hey` greeting or `Best, Tim` sign-off. The never-introduce list below still binds a post where the two differ.
3. **`.vendor/teimurjan-agent-config/MY-BRAIN.md`**: what is true about the owner now. Flag on the change list any claim in the draft that contradicts it or that its `Public vs private` section holds back, and ask about anything it marks not confirmed. On a fact it beats the dossier, which is older. **If either file is missing, stop and tell the owner** (`git submodule update --init`).
4. **Recent LinkedIn posts**: `grep -l '^lane: experience' posts/<current-year>/*.md`. Skim the last 5 to 10 for frames the owner has already used.
5. **`bun run post-patterns --lane experience`**: for `## Recent hooks` (a frame already there is out), the validated anti-patterns, and the hook-length range of the top quartile. Never read the unscoped or news report for this draft, and respect the `too few to cite` marker.

There is no `cv.md`. `MY-BRAIN.md` and the dossier name what the owner runs; neither is a source of stories. The only material you may add to a post is what the owner gives you at the two stops, in their wording.

## Stop 1: the first line

Offer **three versions of the owner's own opening line**. One is their line untouched. The other two keep their words and their claim and change only the way in: move the number forward, cut the setup, or start on the moment the story turns. Never replace their opening with a line about a different thing, and never write a line they could not have written.

- Each must be a legal opening line: 5 to 12 words where possible, leads with the specific, not a question, not a jargon summary, not ending in a colon.
- Number-led and story-led openings are the shapes that travel now (MagicPost measured number-led hooks at +35%, LigoSocial story openers at +31% over bold claims, within author). Say which shape each version is.
- No repeated frames: none of the three may reuse a frame listed under `## Recent hooks`.
- Label each with its `hook_type`.

Present them with `AskUserQuestion` (header `Pick first line`, one option per version, the line verbatim as the label's tail and its `hook_type` plus one clause on why it works as the description). The owner picks one, rewrites one in "Other", or asks for another round. Do not continue until they have.

## Stop 2: the missing specific

Read the draft and decide which single thing is absent: the number or the moment. One question, in plain text, then wait.

If the draft has no real number (a count, a cost, hours, revenue, a conversion, a date), ask for it: `One thing is missing: what did it cost you in hours, or what is the number you would put on it?` If it already has a number, ask for the moment the story turned (the day the user showed up, the build that finally sold). A story with a turn travels; a ledger does not: the lane's four receipted ledgers (spend in, outcome out, every line a figure) landed at 133 to 242, while its five posts above 800 were a launch, a placement, an identity post, an observation, and a product update.

When `MY-BRAIN.md` already holds the number, quote it in the question and ask the owner to confirm or replace it. Whatever comes back goes into the post **in the owner's wording**, by paragraph 3 at the latest. Light copyedit only. A number appears as a number.

## What you may change

Every change goes on the change list so the owner can veto it one by one.

- Typos, grammar, and one-word substitutions where a word is wrong, not where it is plain.
- Cuts: a sentence that repeats another, a setup the first line already did, a pitch for the app, a reference to the owner's previous posts, a line a generic indie developer could post verbatim (the Kill Test), anything on the banned list below.
- One reorder at most: the picked first line to the top, or the number into the first two lines.
- The ending: if the draft closes on a question or a comment ask, propose a plain stance built from the owner's own words elsewhere in the draft, and let them choose. Question endings were the archive's one validated anti-pattern on news posts (0.68x), LigoSocial measured question closers at −7% within author, and "comment X" asks lost 47% of reach after July 2026.
- A link in the body: move it to a `Comment link:` line after the post, for the owner to paste as the first comment, and have the body say in words where to find it.
- Paragraph breaks and white space for a phone screen. One idea per paragraph, 1 to 2 lines each.
- Length: when the draft runs past about 175 words, propose cuts (Shield's 2026 reach curve peaks at 150 to 175 words and falls past 250). Propose; never cut substance on your own.

Suggestions you may make, as proposals that quote the owner's own material: a direct "you" sentence where one would be natural, a short fragment for punch, a concrete noun in place of an abstract one ("Bun" over "modern tooling", "two days" over "a while"). The owner takes or leaves each.

**Not allowed:** a new sentence of your own that carries a claim, a metaphor the owner did not use, a smoother rhythm than they wrote, a paragraph rewritten "in their voice", a number you inferred. Uneven is the voice. If the draft is too thin to publish after the cuts, say what is missing and stop; do not fill it.

## What you must never introduce

The owner's drafts rarely contain these; your edits must not either. Flag any you find in the draft as a listed fix.

- Emojis, em dashes, quotation marks (claims are stated plainly or paraphrased, never air-quoted).
- LinkedIn vocabulary: empower, leverage, revolutionize, incredible, journey, unlock, game-changer, deep dive, "in today's fast-paced world", "thrilled / humbled / excited to announce", "hot take", "the truth is", "let me tell you".
- Slop tells with measured reach costs: "it's not X, it's Y", "stop X, start Y", "the result?", "plot twist", "what nobody tells you", "here's why", "here's the thing", "let that sink in", arrow bullets, three parallel fragments in a row, a hook that ends in a colon.
- Engineered rhythm: stacks of "X. Not Y." couplets, a mic-drop closer, a pile of metaphors, "was it X, or Y?" flourishes.
- AI fluff: anonymous actors ("people are saying", "many have found"), flourish verbs over a number ("skyrocketed", "cratered"), discovery-narrating filler ("it turns out", "interestingly").
- Comment asks of any kind, a question as the first line, a question as the last line, listicle openers, fake vulnerability, cliffhanger profundity.
- Retired labels from the dossier: "Impact Engineer", "Agentic Indie", "solo dev shipping apps". A retired label in the draft is a required fix.
- An external link in the body.

## Pillar check

Tag the draft with the pillar it serves (`replaced-a-hire`, `numbers-from-a-company-of-one`, `didnt-teach-me`, `nights-and-weekends`) and check the draft delivers that pillar's payload: a system and its cost, a real number, a sell-side lesson, the day-job constraint. Every claim gets a number; a number is a line, not the spine. No selling: the apps are the lab, not the product. Bishkek is texture, never the headline. Run the Kill Test once more on the enhanced draft: could a generic indie developer post the same text? If yes, name the sentence that is only the owner's, or say that none is.

## Output

Print the enhanced post, then a blank line, then the change list:

```
cut: <the sentence, in full> — <why, one clause>
moved: <what> → <where>
fixed: <before> → <after> (<reason>)
ending: <the proposed stance> (replaces the closing question)
suggest: <proposal quoting the owner's material>
```

Then `Comment link: <url>` if a link left the body (printed only; it does not go into the saved body). Then one line: `Accept all, or tell me which to keep as you wrote them?` Apply what the owner accepts, re-save, print again. One or two rounds is normal; the draft is theirs.

No title, no hashtags, no preamble.

## Saving the draft

Save to `drafts/<YYYY-MM-DD>-<slug>.md`: today's date, then the first 6 to 8 lowercase words of the opening line, hyphen-joined, punctuation stripped, truncated to about 60 characters. Create `drafts/` if it does not exist; overwrite a same-day file with the same slug. `posts/` is scraped output and is never written here.

```yaml
---
pitch_angle: <the owner's one-line framing, in their words>
drafted_at: 2026-10-06T14:22:00.000Z
lane: experience
pillar: replaced-a-hire | numbers-from-a-company-of-one | didnt-teach-me | nights-and-weekends
source_type: build_log | experiment | launch | opinion
hook_type: result
experience_hook: <the specific the owner supplied at Stop 2>
author: owner
status: drafted
concept_path: null
image_kind: null
---
```

`author` is always `owner`; the critic rejects anything else. `concept_path` and `image_kind` stay `null` here; `post-image` fills them. Infer `hook_type` from the picked first line.

## Checklist before saving

- [ ] Every sentence in the body is the owner's, or a one-word fix they can see on the change list.
- [ ] The picked first line is at the top; the number and the moment are in by paragraph 3, in their words.
- [ ] Nothing from the never-introduce list survives, and no link sits in the body.
- [ ] The closer is a stance, an imperative, a forward-looking confession, or a soft link-out in words; not a question, not a comment ask.
- [ ] A pillar is tagged, a real number is present, the Kill Test names the owner's sentence.
- [ ] `author: owner` is in the frontmatter.

If a box fails, fix it through the change list or stop and say what is missing. Never fill a gap yourself.

## Workflow recap

1. Take the owner's draft. A thought instead of a draft: ask for the draft and wait. A news take: say it is out of scope and stop.
2. Read the brand bundle, `MY-VOICE.md`, `MY-BRAIN.md`, the last 5 to 10 LinkedIn posts, and `bun run post-patterns --lane experience`.
3. **Stop 1:** three versions of the owner's first line → the owner picks (`AskUserQuestion`).
4. **Stop 2:** the number or the moment → wait for their words.
5. Build the change list under What you may change; print the enhanced post and the list; apply what the owner accepts.
6. Run the checklist. Save with the frontmatter above and `author: owner`. Print the post, the `Comment link:` line if any, and the one-line invitation.
