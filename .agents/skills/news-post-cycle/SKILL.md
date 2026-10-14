---
name: news-post-cycle
description: Run the news-lane LinkedIn pipeline end-to-end in one go — the one-news-post-a-week cap, briefing (if missing), news-lane top-posts + patterns context, ideator shortlist gated on subjects the owner has touched (with an interactive pick that shows each idea's one-line gist, score out of 10, and the artifact the owner is expected to have), the owner's own draft written from the brief and enhanced around that artifact, critic verdict, and a cover image that is a real screenshot or photo the owner supplies. Use when the user says "news cycle", "run the news pipeline", "news-post-cycle", "give me a news post end to end", or wants a single command that replaces invoking topics-briefing, post-ideator, post-enhancer, post-critic, and post-image separately for a post about an external event. For a post about the owner's own work, use experience-post-cycle instead. Optionally accepts an idea number to skip the pick.
---

# news-post-cycle

Orchestrates the **news lane** end-to-end so the user does not run each skill by hand. You are the conductor. The underlying skills (`topics-briefing`, `posts-postmortem`, `post-retro`, `wiki-curator`, `post-ideator`, `post-enhancer`, `post-critic`, `post-image`) own their logic and each runs standalone. Do not duplicate their rules. Do not skip them.

**Lanes.** Every post belongs to one of two lanes. A `news` post reacts to an external event and comes out of the briefing. An `experience` post is about the owner's own work and operation and comes straight from a thought the owner typed; that lane has its own conductor, `experience-post-cycle`. The two are analyzed separately, so every context command in this cycle is scoped with `--lane news`. If the user's request is really a thought about their own work, stop and point them at `experience-post-cycle` rather than forcing it through the briefing.

## Inputs

`args` (optional) carries an integer `1..5` picking a specific idea from the freshly generated shortlist, no prompt, and/or `--force` to ignore the weekly cap for this run. With no number, step 4 asks the user to pick interactively. Every post is a text post with the owner's own screenshots or photos, or none; there is no format to choose.

## Human in the loop

This cycle is not autonomous. It pauses at four points and waits for the owner:

1. **The weekly cap** (step 0): if a news post went out in the last seven days, the cycle stops and asks before continuing.
2. **The idea pick** (step 4), unless an idea number was passed, followed by the artifact confirmation: the owner says whether they have the thing the brief expects them to show. A `none` drops the idea.
3. **The draft, then the enhancer's two questions** (step 5): the owner writes the post from the brief; then the first-line pick and the artifact, if the draft does not carry it. Never write the draft for them and never answer on their behalf.
4. **The image** (step 7): the owner supplies a real screenshot or photo, or says `none` for text-only.

Everything else runs without stopping unless a step truly fails.

## Workflow

Run the steps in order. Each step produces a concrete artifact on disk.

### 0. Weekly cap

The news lane publishes at most one post a week; the freed slots go to the owner's own experience post and to commenting on other people's posts, which is where followers now come from. Run the check `post-ideator` documents under its Weekly cap. If it prints a news post or news draft from the last seven days, print the status line `cap: held — <post>` and end. Continue only if `args` carries `--force` or the owner says to ignore the cap for this run.

### 1. Briefing (only if missing)

Check if today's briefing exists:

```sh
test -f "briefings/$(date +%Y-%m-%d).md" && echo present || echo missing
```

- `present`: skip to step 1.5 — do not regenerate.
- `missing`: invoke the `topics-briefing` skill. Wait for it to finish writing `briefings/$(date +%Y-%m-%d).md`.

Briefings are dated. Yesterday's file does not count as today's; only same-day matches.

### 1.5. Postmortems (only if stale)

The enhancer and critic need failure context, not just success context. Postmortems live in `retros/postmortems/` and are slow-changing, so they do not regenerate every cycle.

Check freshness:

```sh
test -d retros/postmortems && \
  find retros/postmortems -type f -name '*.md' -mtime -14 -print | head -1
```

- If the command prints at least one path, postmortems are fresh enough — skip.
- If the directory is empty or the newest postmortem is older than 14 days, invoke the `posts-postmortem` skill with `--lane news`. It writes one file per underperforming news post to `retros/postmortems/`.

If `posts-postmortem` fails (corpus too small, etc.), surface the warning and continue. A missing postmortem corpus is not a pipeline failure.

### 1.6. Retro sweep (pending, last 3 months only)

The 72-hour retro has no trigger of its own — a post is drafted here, but it goes live and matures *after* this cycle ends, so nothing comes back for it. Sweep for that debt at the top of every cycle: any published post old enough to have stable numbers but still missing its retro. The sweep covers drafts of **both lanes** — `post-retro` reads each draft's `lane` and compares it against the right cohort.

A post is a retro candidate when **all** hold:

1. It has a local draft in `drafts/` (post-retro reads the draft; posts without one can't be retro'd and are skipped).
2. It is published — a matching file exists under `posts/`, which is also where the 72h metrics come from.
3. Its `posted_at` is **more than 72 hours ago** (numbers have settled) **and within the last 3 months** (older posts are out of scope — do not retro them).
4. No `retros/<YYYY-MM-DD-slug>.md` exists yet.

List the candidates:

```sh
for d in drafts/*.md; do
  base=$(basename "$d" .md)                                          # YYYY-MM-DD-slug
  post=$(find "posts/${base:0:4}" -maxdepth 1 -name "${base:5}*.md" 2>/dev/null | head -1)
  [ -z "$post" ] && continue                                         # not published yet
  test -f "retros/$base.md" && continue                             # already retro'd
  posted=$(grep -m1 '^[[:space:]]*posted_at:' "$post" | sed "s/^[^:]*: *//;s/[\"']//g")
  echo "$base | posted=$posted"
done
```

Archive post slugs are often longer than the draft slug (the scraper keeps more of the first line), so match by prefix with `find` rather than an exact path — an exact match would miss every published post. The retro filename keys off the **draft** slug (`$base`), the same name `post-retro` writes, so the existence check stays consistent.

For each line printed, compare `posted` to now: skip if newer than 72h (not ready) or older than 3 months (out of scope); otherwise invoke the `post-retro` skill with that `YYYY-MM-DD-slug` as its argument. Run them one at a time. If a retro fails (missing metrics, etc.), surface the warning and continue — a stuck retro never blocks the rest of the cycle.

### 1.7. Absorb retro lessons into the wiki

A retro's conclusion reaches no downstream consumer on its own — `post-patterns` surfaces only `decision` and `summary`, capped at three summaries per decision, so lessons expire silently as retros accumulate. Anything the sweep just wrote is still unabsorbed.

```sh
grep -rl "wiki_ingested: false" retros/ 2>/dev/null | wc -l
```

If the count is above zero, invoke **wiki-curator** in `ingest` mode. It absorbs one lesson at a time, reconciles it against the existing pages, appends to `wiki/log.md`, and flips the flag. Soft failure: if it errors, surface the warning and continue — an unabsorbed lesson does not block a draft.

Skip when the count is zero.

### 2. Archive context (news lane only)

Run all three and keep their output in context for the ideator and critic:

```sh
bun run top-posts --n 10 --lane news
bun run post-patterns --lane news
bun run wiki lint
```

The `--lane news` scope matters: experience posts (the owner's own launches, build logs, founder updates) live in a different room and would drag the news medians. The report's `## Lanes` table still shows both lanes' sizes so nobody mistakes the scoped corpus for the whole archive.

If `top-posts` or `post-patterns` fails, surface the error and stop — the ideator and critic both depend on `post-patterns`.

`wiki lint` is advisory here: report any error it prints and carry on. A stale wiki page still beats no wiki page, and the ideator falls back to the pattern report when `wiki/` is missing entirely.

**Two cautions when passing this context on.** Bucket sections cover only the quartiles and print their own sample size — respect the `too few to cite` marker. And cite a fault only from `## Validated anti-patterns`; the `## Tested and discredited` list has been checked against the corpus and does not mark weaker posts.

### 3. Ideate

Invoke the `post-ideator` skill. It will:

- Read the latest briefing and the brand bundle (`bun run --silent --cwd .vendor/teimurjan-llm-wiki wiki view post-writing`).
- Use the news-lane `post-patterns` and `top-posts` context already gathered.
- Dedup against recent drafts and published posts.
- Gate every candidate on `touched_it` (the owner has personally run, built, migrated, or been bitten by the subject) and name the `expected_artifact`.
- Emit 3 to 5 scored idea briefs, each with a one-line `gist`, and write shortlisted entries into `ideas/$(date +%Y-%m-%d).md` with `lane: news`.

Do not draft yet. Wait for the ideator to finish.

### 4. Pick an idea

- If `args` has a number `N`, pick the Nth idea from the just-written `ideas/$(date +%Y-%m-%d).md` (order = order in file) — an explicit number is a direct override, skip the interactive pick below entirely.
- If the pick is out of range, stop and ask the user which idea to use.
- Otherwise (no number in `args`), run the interactive pick below.

**Interactive pick.** Read every shortlisted idea's `gist`, `score` (out of 12), `opinion_wedge`, `reach_ceiling`, and `risk` from `ideas/$(date +%Y-%m-%d).md`. Rank by `score` descending. Ask the user to choose with `AskUserQuestion`, one option per idea:

- Cap at 4 options (the tool's hard max). With 5 shortlisted ideas, offer the top 4 by the ranking above and say in the question text that a 5th exists and can be reached by typing its number into "Other".
- Option label: rank + display score, e.g. `#1 · 8/10`. Convert the ideator's `score` (out of 12) to the friendlier out-of-10 shown here: `round(score * 10 / 12)`.
- Option description: **the `gist` first, verbatim, as its own line** — the owner has to see in one plain sentence what the post would be about before reading anything else. Then one line **Artifact:** the `expected_artifact`. Then one line of **Pros:** the `opinion_wedge`, plus the `reach_ceiling` note when it's `2` (a bigger room). Then one line of **Cons:** the `risk` field, plus the `reach_ceiling` note when it's `1` (capped at a sub-community). Do not invent judgment beyond what the brief already says. Keep the whole description under ~50 words.
- Question header: `Pick idea`. Question text: `Which idea should we draft next?`

Map the answer back to its `idea_id`. If `AskUserQuestion` cannot be presented (no interactive channel available), stop and print the shortlist with gists — do not pick on the owner's behalf.

Mark the chosen idea's `status` in `ideas/$(date +%Y-%m-%d).md` to `approved` via Edit. Leave the others as `shortlisted`.

**Confirm the artifact.** Ask in plain text: `The brief expects you to show <expected_artifact>. Do you have it, or something else from your own work on this? Say none if not.` Wait. On `none`, set the idea back to `shortlisted`, say the news lane runs only on subjects the owner has touched, and end the cycle; do not fall through to the next idea on the owner's behalf.

### 5. The owner writes, the enhancer enhances

Print the approved brief in full: `gist`, `angle`, `opinion_wedge`, `why_now`, `evidence_points`, `source_url`, `expected_artifact`. Then ask in plain text and wait: `Write the post the way you would publish it, with <expected_artifact> in it. Rough is fine, typos are fine; the enhancer edits from there.` Never write a line of it yourself, and never proceed on a guessed draft.

Invoke the `post-enhancer` skill with the owner's draft and the `idea_id`. It reads the brief from the ledger, fact-checks the draft against the source, stops twice (three versions of the owner's first line; the artifact if the draft does not carry it), applies only the edits on its change list, and saves to `drafts/$(date +%Y-%m-%d)-<slug>.md` with `lane: news` and `author: owner`. Relay the owner's answers verbatim. If the enhancer ends without saving because the draft has no artifact, the cycle ends there too.

Capture the draft path for the next step.

### 6. Critique

Invoke the `post-critic` skill with the draft path from step 5. The critic will read the idea brief, the news-lane patterns report, and the draft, then emit either an approval scorecard or a rewrite plan.

If the critic rejects, stop here. Do not generate a concept image for a draft that is not going to publish.

### 7. Image (only if critic approved)

Invoke `post-image` with the approved draft. It names two candidate artifacts from the post and asks the owner for one to four real screenshots or photos, or `none` for text-only. Each file is checked for size, legibility, and leaks, filed under `images/<date>-<slug>/`, and described with alt text in `concepts/<date>-<slug>/prompt.md`; the draft gets `concept_path` and `image_kind`. Nothing is generated. Wait for the owner; never make an artifact up.

If `post-image` fails to file the artifact, surface the error and stop; the draft is already saved and approved, and the owner can re-run `/post-image <draft>`.

## Output

Print, in order:

1. A one-line status per step: `cap: clear | held — <post>`, `briefing: created | reused`, `postmortems: refreshed | fresh | skipped`, `retros: N swept | none pending`, `ideation: N briefs`, `pick: interactive | direct (arg N)`, `chosen: <idea_id> — <gist>`, `draft: <path>`, `critic: approved | rejected`, `concept: <path> | skipped`, `image: artifact (N files) | none (text-only)`.
2. The full draft text (so the user can read it without opening the file).
3. The critic's verdict block verbatim.
4. `post-image`'s output block verbatim; the files are already under `images/<date>-<slug>/` and the alt text is in the block.
5. One closing line for after publishing: reply to every comment within two hours in your own words, and spend the day's 20 minutes commenting on the target accounts. The pipeline does neither, and they are the first lever on reach now.

If the critic rejected the draft, stop after step 3. Do not auto-revise and do not generate a concept image. The rewrite plan is the user's call.

## Failure handling

- Briefing step fails: report the failure and stop. The rest of the pipeline depends on a current briefing.
- `bun run top-posts` or `bun run post-patterns` fails: report and stop.
- Ideator returns zero passing briefs: stop and tell the user the shortlist was empty. Do not invent an angle.
- Enhancer fails to save the draft: stop. Do not retry without the user.
- Critic rejects: this is not a pipeline failure. Print the rewrite plan and end normally.
- The owner does not answer a question: stop and wait. Never proceed past a human-in-the-loop stop with a guessed answer.
- The owner has no artifact for the picked idea: not a failure. Drop the idea, say why, and end.

## What this skill does not do

- It does not draft experience posts. That is `experience-post-cycle`.
- It does not publish to LinkedIn.
- It does not bypass the critic. A rejected draft stays a draft.
- It does not edit `posts/`. Those are scraped output.
- It does not pick a hook, an artifact, or an image on the owner's behalf, and it does not write a sentence of the post.
- It does not run more than one news post a week.

## When to use

Trigger phrases:

- "run the news cycle"
- "news-post-cycle"
- "give me a news post end to end"
- "pipeline a post from the briefing"
- "ideate, draft, and critique"

If the user already has a draft and just wants it critiqued, use `post-critic` directly. If they already wrote the post from a brief, use `post-enhancer` directly. If the user typed a thought about their own work, use `experience-post-cycle`. This skill is for the cold start on external news.
