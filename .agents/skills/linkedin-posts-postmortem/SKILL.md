---
name: linkedin-posts-postmortem
description: Generate retrospective failure analyses for the worst-performing published posts so the enhancer and critic learn from misses, not just wins. Reads the bottom-5 posts by impressions from `posts/`, classifies each, and writes one postmortem file per post to `retros/postmortems/<post-date>-<slug>.md`. Use when the user says "run postmortems", "analyze bottom posts", "what failed", "post-mortem the losers", or "refresh failure analyses". Scoped to the experience lane, so the archive's old news posts are never ranked against LinkedIn's current posts.
---

# linkedin-posts-postmortem

This skill produces structured failure analyses for the worst-performing posts in the archive. `linkedin-post-retro` covers the recent post you just shipped — this skill covers the bottom of the corpus so the enhancer and critic know which patterns reliably miss.

## Inputs

1. `bun run top-posts --json --lane experience` — the JSON includes the bottom-5 by impressions for the lane. Read it to know which posts to analyze.
2. `bun run post-patterns --lane experience` — for the lane's median impressions and the existing classification per post.
3. The post files themselves, at `posts/YYYY/MM-DD-<slug>.md`. Read each one in full.

If `bun run top-posts --json` does not surface bottom posts directly, fall back to sorting the JSON by impressions and taking the bottom 5 (where `impressions` is non-null).

## Inputs the user may pass

- When the experience cohort is under 10 posts, say so and stop rather than postmortem half the lane.
- `--n N` (optional): override the bottom-count, default 5.
- A list of explicit post paths: run postmortems for those specific files instead of auto-picking from impressions. A post whose `lane` is not `experience` is an old news post; skip it and say so.

## What each postmortem must answer

For each underperforming post:

1. How far below its **scrape-age cohort** median did it land? Use the `## Impressions by scrape age` section, not the pooled corpus median — impressions freeze at first scrape, so the pooled figure mixes fresh and mature numbers.
2. Which **pillar** did it serve, per `wiki/experience.md` and the brand bundle? Was the room large enough for the post to have worked at all?
3. Which flags under `## Validated anti-patterns` does it match? **Only that list.** Do not cite anything under `## Tested and discredited` — those have been checked against the corpus and do not mark weaker posts; "no concrete numbers" and "announcement hook" mark *stronger* ones, and "news without firsthand signal" marks the two biggest posts in the archive.
4. Was the hook accurate to the body or did it overpromise?
5. What single concrete thing would have changed the outcome? A bigger room is a valid and common answer — say so plainly rather than reaching for a craft fault that the corpus does not support.

Answers must be grounded in the post's actual text. Do not speculate beyond the file and the patterns report.

`topic_family` is bookkeeping. It comes from a keyword cascade that mislabels, and it carries no reach signal — do not build a failure mode on it, and do not claim a family was "saturated" without a confirmed streak in `## Cooling families`.

## Output artifact

One markdown file per analyzed post at:

```
retros/postmortems/<post-date>-<slug>.md
```

Use the post's date and slug from its filename (`posts/2026/05-21-alibaba-launched-qwen-...md` → `retros/postmortems/2026-05-21-alibaba-launched-qwen-....md`).

### Frontmatter

```yaml
---
kind: postmortem
source_post: posts/2026/09-14-368-on-meta-ads-three-sign-ups-...md
topic_family: other
source_type: experiment
lane: experience
hook_type: result
pillar: didnt-teach-me
impressions: 160
likes: 2
comments: 1
shares: 0
cohort: 1 to 4 weeks
cohort_median_at_run: 394
beat_median: false
likely_failure_modes:
  - ledger with no turn
  - hook overpromised, body underdelivered
decision: modify
summary: One-sentence summary tying pillar + failure mode + what to change next time.
wiki_candidate: A spend-and-outcome ledger with no turn lands below the experience cohort median.
wiki_pages: [experience]
wiki_ingested: false
generated_at: 2026-05-25T13:30:00.000Z
---
```

`wiki_candidate` is the lesson as one falsifiable claim, `wiki_pages` names the pages it bears on (`experience`; never `audience`, which holds the old news posts), and `wiki_ingested` starts `false`. `wiki-curator` absorbs them later. **Do not write to `wiki/` from this skill** — a single run writes several files, and concurrent edits to the same wiki page would clobber each other.

`decision` reuses the existing `RetroDecision` enum:

- `repeat` — not applicable here. Postmortems are for misses.
- `modify` — same topic family worth attempting again with a different angle, hook, or source type.
- `block` — stop pitching this topic-family + source-type combo entirely (or until a new artifact justifies it).

`likely_failure_modes` should pull from the anti-pattern vocabulary in `bun run post-patterns` where it applies, plus one or two post-specific observations.

### Body

3 to 5 short paragraphs. Concrete and grounded. Structure:

1. What the post tried to do (1 sentence, derived from its hook and topic).
2. Where it landed numerically vs the corpus median.
3. The 1 or 2 specific failure modes you identified, named with evidence from the post text.
4. The single concrete thing to change next time on this topic family / source type.

Do not write a generic "be more specific" lecture. Name the actual missing element ("no firsthand benchmark," "hook said the model is the agent frontier, body never explained what that meant," "topic family `agents` had two other posts within 7 days").

## Workflow

1. Run `bun run top-posts --json --lane experience` and `bun run post-patterns --lane experience`.
2. Identify the bottom 5 posts (or `--n N`) by impressions within the lane, excluding posts with `null` impressions.
3. For each:
   - Read the post file in full.
   - Classify topic family, source type, hook type from the post text (mirrors `bun src/analytics/cli/post-patterns.ts` heuristics).
   - Pick 1 to 3 anti-patterns from the patterns report that this post exhibits.
   - Decide `modify` vs `block`.
   - Write a one-sentence summary and a 3-to-5-paragraph body.
   - Save to `retros/postmortems/<post-date>-<slug>.md`.
4. Print a one-line index of generated files at the end.

## Idempotency

If a postmortem already exists for a post, overwrite it. The bottom-5 set can shift as new posts get scraped, so old postmortems may become stale. Track via `generated_at`.

## Output

Print only the index, one line per file:

```
retros/postmortems/2026-05-21-alibaba-launched-qwen-3-7-max-yesterday-and-called-it-the-ag.md
retros/postmortems/2026-04-29-it-only-knows-the-world-up-to-1930-no-internet-no-wwii-no-mo.md
...
```

No preamble. No summary table. The patterns CLI will surface the aggregated failure modes when it loads `retros/postmortems/`.

## Hard rules

- Never analyze a post with `null` impressions. Lack of data is not failure.
- Never invent a failure mode that is not supported by the post's text or the patterns report.
- Never produce postmortems for posts already in the top quartile.
- Always reuse the anti-pattern vocabulary from `bun run post-patterns` where it applies. Add a post-specific observation only as a second or third bullet.
- Always set `kind: postmortem` so the patterns CLI can distinguish these from success retros, and `lane` so it files the failure under the right cohort.

## When NOT to use

- The user just published a draft and wants to retro it. Use `linkedin-post-retro` instead.
- The user wants performance scoring of a single named post they already have. Use `linkedin-post-retro` with manual inputs.
- The corpus is smaller than 10 posts. The bottom 5 would dominate the signal. Skip until there is enough corpus.
