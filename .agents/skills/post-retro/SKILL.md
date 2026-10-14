---
name: post-retro
description: Run the 72-hour retrospective on a published draft, fold in the owner's per-post analytics (in-network share, saves, sends, members reached) when they paste them, and save the conclusion in retros/. Use when the user says "retro this post", "review how this performed", pastes a post's analytics panel, or wants to update the draft lifecycle after publishing.
---

# post-retro

Run this 72 hours after a draft is published.

## Office UI sync

This is the **analyst** stage — emit `end` once the retro file is written, per [office-emit-end](../office-emit-end.md).

## Inputs to read first

1. The published draft in `drafts/YYYY-MM-DD-<slug>.md`. Read its `lane` (`news` or `experience`; absent means `news`). The lane decides which cohort the post is measured against and which wiki page the lesson goes to.
2. **The matching published post under `posts/`** — this is where the metrics come from. Match by prefix, since archive slugs are longer than draft slugs:
   ```sh
   find "posts/${base:0:4}" -maxdepth 1 -name "${base:5}*.md" | head -1
   ```
   If the draft has no `lane`, fall back to the post's `lane` frontmatter, then to `news`.
3. `bun run post-patterns --lane <lane>` — for the scrape-age cohort, the validated anti-patterns, and the family distribution **of this lane only**. A news post's cohort says nothing about an experience post's reach, and the experience cohort is small enough that its `too few to cite` marker may fire; when it does, name the cohort size instead of a median and say the comparison is thin.
4. `wiki/audience.md` — for the subject tier, **news lane only**. For the experience lane, the tier model does not apply; the room is the owner's own following, and the relevant frame is the pillar in the draft's frontmatter and the brand bundle (`bun run --silent --cwd .vendor/teimurjan-llm-wiki wiki view post-writing`).
5. **The owner's per-post analytics, if pasted**: LinkedIn's post analytics page gives impressions, the in-network / out-of-network split, members reached, reactions, comments, reposts, saves, and sends. Read them from the invocation text, or from an `analytics:` block the owner added to the draft's frontmatter. Do not ask for them inside a cycle's sweep; at the end of the retro print one line asking for them if they are missing, and update the retro file when they arrive.
6. Any comment summary or performance notes the user provides

## Preconditions

**One metric is required: `impressions`, read from the published post's frontmatter.** Do not ask the user for it. Everything else is optional and usually absent — across the existing retros, `impressions_24h` is filled on 3 of 17, shares on 7, comments on 9, because LinkedIn's engagement counts mostly fail to scrape. Record whatever the post file carries and leave the rest `null`.

Only ask the user for a number when the post file has no `impressions` at all. Never block a retro on an engagement field. The scraper's likes, comments, and shares have been null on every post since 2026-08-25, so the owner's pasted analytics panel is the only source of engagement; when it is present it wins over the scraped fields, and `impressions` from the panel replaces the frozen scrape.

## Comparison baseline

Compare against the **scrape-age cohort** from the `## Impressions by scrape age` section, not the pooled corpus median. Impressions freeze at first scrape, so a 72-hour number measured against a median that mixes fresh and mature posts is biased against itself. Name the cohort you used.

## Questions to answer

Every retro must answer:

1. Did the post beat its **scrape-age cohort** median, within its lane? (Name the lane, the cohort, and its median.)
2. News lane: what **subject tier** was it, per `wiki/audience.md`, and did it land inside that tier's observed band? Experience lane: which **pillar** did it serve, and did the receipt (the number) carry it?
3. Was the hook accurate to the body?
4. Did comments validate the intended discussion angle, **if comment data exists**? Answer `null` when it does not — do not infer engagement from silence, since the metric usually failed to scrape.
5. Should this pattern be repeated, modified, or blocked?
6. **Did it leave the owner's network, and did readers do anything?** From the pasted analytics, when present: in-network impressions and the out-of-network share, engagement per impression (reactions + comments + reposts + saves + sends, over impressions), saves, and sends. Compare against the account's 90-day baseline read on 2026-10-08 (2% in-network, about 140 in-network impressions per post, 0.19% engagement per impression, about one save and two comments per post) and against the median of prior retros in this lane that carry the fields. In-network impressions are the number to watch first: since 2026-10-08 the plan is to rebuild in-network reach through conversation before expecting out-of-network pickup, so an in-network count rising off the 140 baseline is progress even when the total is flat. Answer `null` when nothing was pasted; do not infer.
7. **Who wrote it and what did it show?** Record `author` and `image_kind` from the draft, and the ending shape. These are the variables the six-week test (to 2026-11-20) changes; a retro that does not record them cannot say whether the change worked.

### Naming the failure

Name the cause in terms of **subject tier and room size** first. Do not reach for the flags in the `## Tested and discredited` list — "news without firsthand signal", "no concrete numbers", and "announcement hook" have all been tested against the corpus and do not mark weaker posts; two of them mark *stronger* ones. Only cite a flag that appears under `## Validated anti-patterns`.

If the honest answer is "the craft was fine and the room was small," say that. It is the most common real cause in this archive and the hardest to see from inside a draft.

Since July 2026 there is a second honest answer: **the post never left the owner's network.** LinkedIn's slop enforcement (reports from 2026-07-30, 40% fewer views on flagged content by 2026-08-20) withholds out-of-network distribution from posts without concrete detail or lived experience, and this account's reach was 98% out-of-network. When the pasted analytics show an in-network share far above the 2% baseline with a low total, the post was shown to followers and not pushed further; look at substance (an artifact the owner touched, a story with a turn) and the slop tells in `post-critic` before blaming the subject. In the experience lane, name the ledger shape when the body is dollars in and outcomes out with no turn; it is the lane's floor at n=4, `confidence: low`.

## Output artifact

Save one markdown file to `retros/YYYY-MM-DD-<slug>.md` with YAML frontmatter:

```yaml
---
draft_file: drafts/YYYY-MM-DD-<slug>.md
source_post: posts/YYYY/MM-DD-<archive-slug>.md
topic_family: security
source_type: news
lane: news
reach_tier: t0-vendor-paper-or-self   # news lane only; experience retros record pillar instead
pillar: null                           # experience lane only, from the draft
published_url: ...
published_at: ...
impressions_72h: 190
impressions_24h: null
likes_72h: null
comments_72h: null
shares_72h: null
author: owner                          # from the draft: owner | writer
image_kind: artifact                   # from the draft: artifact | none
ending_type: stance                    # stance | question | link-out
in_network_pct: null                   # the next eight come from the owner's pasted analytics, else null
out_of_network_pct: null
in_network_impressions: null
members_reached: null
reactions: null
reposts: null
saves: null
sends: null
engagement_per_impression: null        # (reactions + comments + reposts + saves + sends) / impressions
cohort: 2 to 7 days
cohort_median_at_run: 393
beat_median_impressions: false
beat_peer_group: false
discussion_validated: null
hook_matched_body: true
decision: modify
summary: Firsthand hook and a clean wedge, at half the cohort median. The failure was room size, not craft.
wiki_candidate: A firsthand hook cannot carry a t0 subject the audience is not already in.
wiki_pages: [audience]
wiki_ingested: false
---
```

`topic_family` is recorded for bookkeeping only. It comes from a keyword cascade that mislabels, and it carries no reach signal — never build the conclusion on it.

The body should explain the decision in a few short paragraphs and name one concrete thing to repeat, modify, or stop.

## Handing the lesson to the wiki

A retro's prose is read by people, not by code: `post-patterns` surfaces only `decision` and `summary`, at most three summaries per decision. So a lesson left in the body reaches nothing, and past the ninth retro even the summary stops surfacing.

Set three fields so the conclusion survives:

- `wiki_candidate` — the lesson as **one claim**, phrased so it could be true or false about future posts. Not a description of this post.
- `wiki_pages` — which wiki pages it bears on. News-lane lessons usually go to `audience`. Experience-lane lessons go to `experience` — a page that may not exist yet; routing a lesson at a missing page is how the wiki learns it needs one, and `wiki-curator` creates it on the first ingest. Never route an experience lesson at `audience`: that page's tiers were calibrated on news posts and the two rooms must not be mixed.
- `wiki_ingested: false` — always. `wiki-curator` flips it after absorbing the claim.

Do not edit `wiki/` yourself. Writing a claim into a page requires reconciling it against every other page and appending to `wiki/log.md`; that is `wiki-curator`'s job, and doing it from here would race the postmortem sweep, which writes several files in one run.
