---
name: linkedin-post-cycle
description: The LinkedIn cycle. Take a LinkedIn post the owner wrote about their own work through the pipeline — the owner's own first line picked from three versions of it, an edit pass that keeps every sentence theirs, critic verdict, and a real screenshot or photo as the cover. No briefing, no ideator, no drafting; the owner's text is the post. Use when the user says "linkedin cycle", "linkedin-post-cycle", "edit my linkedin post", "polish this for linkedin", "founder update", or hands over a LinkedIn draft (or a thought, which the cycle asks them to write out) about their apps, their numbers, a system they built instead of hiring, or something ten years of engineering didn't teach them. For an X post use x-post-cycle; for a generic "edit my post" ask which platform.
---

# linkedin-post-cycle

Orchestrates LinkedIn end-to-end. LinkedIn runs one kind of post, the experience post; news posts left this repo on 2026-11-02 (they live in `news/` and run elsewhere). Every draft still carries `lane: experience` so the scraper stamps it on the published post and the lane-scoped reports keep the archive's old news posts out of its numbers. The input is a draft the owner wrote; the output is that draft, edited and not rewritten: the owner's own first line moved to the front, cuts and fixes they approved one by one, a critic verdict, and a real artifact as the cover image. The pipeline stopped writing experience posts on 2026-10-08: the owner's hand-written founder post reached 943 impressions, the three pipeline-written posts after it landed at 137 to 151, and the brand wiki's 30-day falsifier for the reworked pipeline fired. You are the conductor. The underlying skills (`linkedin-post-retro`, `wiki-curator`, `linkedin-post-enhancer`, `linkedin-post-critic`, `post-image`) own their logic and each runs standalone. Do not duplicate their rules. Do not skip them.

**What a LinkedIn post is.** A post whose subject is the owner's own operation: an app they run, a number they measured, a function they built instead of hiring for, a lesson the sell side taught them, the nights-and-weekends constraint. The brand wiki in `.vendor/teimurjan-llm-wiki/` defines it — its four pillars, its voice (benchmarks and receipts), and what it is not (indie-dev generic, "agentic" slogans, retired labels). Read it before anything else in this cycle with `bun run --silent --cwd .vendor/teimurjan-llm-wiki wiki view post-writing`. It is the reason this cycle exists.

**What it is not.** A take on someone else's news: this repo no longer runs news posts, so say so and stop. Not an X post either: X gets its own posts, written separately through `x-post-cycle`, and a LinkedIn draft is never reused there or the other way round. A thought that is about the owner's *posting* (metrics, streaks, this pipeline) fails the critic's navel-gazing rule — say so before drafting.

## Inputs

`args` carries the owner's draft, as typed: the post the way they would publish it, rough is fine, typos are fine. It can include a number, a link to the app, a half-formed opinion.

- If `args` is empty, ask once: `What happened? One thing you built, measured, shipped, or learned this week, written the way you'd post it.` Then wait.
- If `args` is a thought rather than a draft (one line, a number, a note to self), ask once: `Write it the way you would post it, rough is fine. I edit from there.` Then wait. Do not expand it on the owner's behalf; the enhancer will refuse to.

## Human in the loop

This cycle pauses twice inside the enhancer, once on the edit list, and once inside the image step, and waits for the owner each time:

1. **The first line** — the enhancer offers three versions of the owner's own opening line (one untouched), the owner picks or rewrites one.
2. **The missing specific** — the enhancer asks for exactly one thing the draft does not yet carry (a number, a name, the moment the story turned, a cost). The owner answers in their own words.
3. **The edit list** — the enhancer prints the edited draft and every cut, move, and fix as a list; the owner accepts or vetoes each.
4. **The image** — the owner supplies one to four real screenshots or photos, or says `none` for text-only.

Never answer any of these for the owner. The post is theirs, sentence by sentence.

## Workflow

### 0. Read the dossier

Read the brand bundle in full: `bun run --silent --cwd .vendor/teimurjan-llm-wiki wiki view post-writing`. If it fails, stop and tell the owner rather than drafting from memory. Carry into the enhancer and critic: the four pillars (`replaced-a-hire`, `numbers-from-a-company-of-one`, `didnt-teach-me`, `nights-and-weekends`), the voice rule (every claim gets a number), the platform notes (links in the body cut reach — they go in the first comment), and the Kill Test (if a competitor could say the same sentence, it is not ownable).

### 1. Retro sweep (last 3 months)

The 72-hour retro has no trigger of its own, so sweep for pending debt at the top of the cycle. Only `lane: experience` drafts count; an old news draft left in `drafts/` is skipped.

A draft is a retro candidate when **all** hold:

1. It sits in `drafts/` with `lane: experience` in its frontmatter.
2. It is published — a matching file exists under `posts/` (match by prefix; archive slugs are longer than draft slugs).
3. Its `posted_at` is more than 72 hours ago and within the last 3 months.
4. No `retros/<YYYY-MM-DD-slug>.md` exists yet.

```sh
for d in $(grep -l '^lane: experience' drafts/*.md 2>/dev/null); do
  base=$(basename "$d" .md)
  post=$(find "posts/${base:0:4}" -maxdepth 1 -name "${base:5}*.md" 2>/dev/null | head -1)
  [ -z "$post" ] && continue
  test -f "retros/$base.md" && continue
  posted=$(grep -m1 '^[[:space:]]*posted_at:' "$post" | sed "s/^[^:]*: *//;s/[\"']//g")
  echo "$base | posted=$posted"
done
```

For each candidate in the window, invoke `linkedin-post-retro` with the `YYYY-MM-DD-slug`, one at a time. Soft failure: a stuck retro never blocks the draft.

Then, if `grep -rl "wiki_ingested: false" retros/ | wc -l` is above zero, invoke `wiki-curator` in `ingest` mode. Soft failure as well.

### 2. Archive context

```sh
bun run top-posts --n 10 --lane experience
bun run post-patterns --lane experience
bun run wiki lint
```

Keep the output in context for the enhancer and critic. The `--lane experience` scope is the point: the archive still holds the old news posts, a different room with a different median, and they must never be compared. The `## Lanes` table in the report shows how thin the experience cohort still is — respect its `too few to cite` marker, and say so in the output when it fires.

`wiki lint` is advisory; report and carry on. `wiki/audience.md` is the old news posts' tier model and does not bind here. The judgment page is `wiki/experience.md`; pass it to the critic.

If `post-patterns` fails, surface the error and stop.

### 3. Edit (human in the loop)

Invoke `linkedin-post-enhancer` with the owner's draft as the single input. The enhancer reads the dossier, `MY-VOICE.md`, and `MY-BRAIN.md`, offers three versions of the owner's first line, asks for the one missing specific, then applies only the edits its change list names and tags the draft with a `pillar` and `author: owner`. It saves to `drafts/$(date +%Y-%m-%d)-<slug>.md` with `lane: experience`.

Relay the owner's answers verbatim. Do not paraphrase, soften, or fill in a number the owner did not give, and do not let a rewritten paragraph through: the critic rejects an experience draft whose `author` is not `owner`.

### 4. Critique

Invoke `linkedin-post-critic` with the draft path. The critic reads the draft's `lane`, scores it against the experience-lane report, and applies the lane's receipts rule (a claim without a number is a specificity failure), the navel-gazing rule (the owner's operation is the subject by design; the owner's posting metrics are not), the authorship precondition, the slop-tell rule, and the ledger check (a spend-and-hours ledger with no turn drops discussion potential).

If the critic rejects, stop here. Print the rewrite plan. Do not generate an image.

### 5. Cover image (only if critic approved)

Invoke `post-image` with the draft path. It names two candidate artifacts from the post (the ads manager, App Store Connect, the terminal, the dashboard) and asks the owner for one to four real screenshots or photos, or `none` for text-only. Each file is checked for size, legibility, and leaks, filed under `images/<date>-<slug>/`, and described with alt text in `concepts/<date>-<slug>/prompt.md`; the draft gets `concept_path` and `image_kind`. Nothing is generated. Wait for the owner; never make an artifact up.

## Output

Print, in order:

1. One status line per step: `retros: N swept | none pending`, `context: experience lane, N posts (too few to cite | citable)`, `pillar: <pillar>`, `author: owner`, `draft: <path>`, `edits: N accepted, K vetoed`, `critic: approved | rejected`, `image: artifact (N files) | none (text-only)`.
2. The full draft text.
3. The `Comment link:` line the enhancer printed, if the post has a link to move out of the body.
4. The critic's verdict block verbatim.
5. `post-image`'s output block verbatim.
6. One closing line for after publishing: reply to every comment within two hours in your own words. The pipeline does not, and it is the first lever on reach now.

If the critic rejected, stop after step 4.

## Failure handling

- No thought supplied and the owner does not answer: stop. Never invent the owner's experience.
- `bun run post-patterns --lane experience` fails: report and stop.
- Enhancer fails to save: stop. Do not retry without the user.
- Critic rejects: not a pipeline failure. Print the rewrite plan and end normally.
- The owner does not answer a human-in-the-loop question: stop and wait.

## What this skill does not do

- It does not read the briefing or run the ideator. The owner's draft is the post.
- It does not write or rewrite a sentence of the post.
- It does not publish to LinkedIn.
- It does not bypass the critic.
- It does not edit `posts/` or `wiki/`.
- It does not pick a first line, a number, or an image on the owner's behalf.

## When to use

Trigger phrases:

- "linkedin cycle" / "linkedin-post-cycle"
- "edit my linkedin post"
- "polish this for linkedin"
- "founder update"
- a LinkedIn draft (or a raw thought the cycle asks them to write out) about the owner's apps, numbers, replaced hires, or lessons

If the user only wants the edit pass, use `linkedin-post-enhancer` directly. If they only want a verdict on an existing draft, use `linkedin-post-critic`. If they only want the image, use `post-image`. This skill is for the whole LinkedIn cycle in one go.
