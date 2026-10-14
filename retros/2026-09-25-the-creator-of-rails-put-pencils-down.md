---
draft_file: drafts/2026-09-25-the-creator-of-rails-put-pencils-down.md
source_post: posts/2026/09-25-the-creator-of-rails-put-pencils-down-at-53-dhh-told-rails-w.md
idea_id: 2026-09-25-01
topic_family: agents
source_type: news
# The classifier reads this post as sourceType build_log, hookType result, hasFirsthandSignal true,
# endingType question; source_type above is the draft's.
lane: news
reach_tier: t2-universal
scored_at_ideation: 2
landed_in_band: t1-subcommunity
pillar: null
published_url: 'https://www.linkedin.com/feed/update/urn:li:activity:7509236824347869184/'
published_at: '2026-09-25T13:06:13.798Z'
impressions_72h: 2638
scrape_age_hours: 256
impressions_24h: null
likes_72h: null
comments_72h: null
shares_72h: null
cohort: 1 to 4 weeks
cohort_n: 40
cohort_median_at_run: 446
beat_median_impressions: true
# Peer group here is the agents family (n=17, median 750); bookkeeping only.
beat_peer_group: true
discussion_validated: null
hook_matched_body: true
ending_type: question
decision: repeat
summary: Pre-scored t2 (score 12) on DHH and Rails, landed at 2638 — 5.9x the 1-to-4-week news cohort and the best news post since 08-19, but inside t1's band and half the t2 floor. The name was t2; the argued thing was one company's policy. Ended on a question and beat the cohort anyway.
wiki_candidate: A t2 name (DHH, Rails) attached to one company's policy lands in t1's band, not t2's; the name is used, the policy is not.
wiki_pages: [audience]
wiki_ingested: true
---

# Retro — The creator of Rails put pencils down at 53%.

**Lane:** news. **Idea:** 2026-09-25-01, scored 12/12, `reach_ceiling: 2`,
`reach_tier: t2-universal`, risk `rehash`. **Impressions:** 2638, frozen at first
scrape about 256 hours (10.7 days) after publishing, so this is a settled number
rather than a 72-hour one. Likes, comments and shares failed to scrape (`null`).

## Beat its cohort?

Yes. Scraped at 10.7 days, the post sits in the **1 to 4 weeks** news cohort (n=40,
median 446) and landed at 2638, 5.9x that median. It also clears the lane median
(449, n=45) and the agents family median (750, n=17; bookkeeping only). It is the
highest news post since the 08-19 Cursor/GitHub post (100,618) and the only one of
the last eight news posts to clear 1,500.

## Tier and band

Pre-scored t2 on DHH and Rails. It landed at 2638: inside t1's observed band (1380 to
3570), under t2's floor (5154) by 2x, and over the page's `t2_miss_below` trigger
(1000). On `wiki/audience.md`'s own taxonomy that is a **near-miss**, not a dispute;
it would be the second (`pre_scored_near_miss: 1` today).

The tier test asks whether the reader has used the thing named in five words. Rails:
yes, or holds an opinion on it. DHH: known. But what the post argued was 37signals'
internal policy ("writing code by hand is now the exception") and a Rails-core
benchmark published two days earlier: one company's decision and one benchmark, each a
t0 shape on its own. The post is the mirror of the 09-16 coreutils miss. There a t2
noun carried a property nobody had fought with (a license) and landed in t0's band;
here a t2 name carried a debate the reader is already in (whether to stop hand-writing
code) and landed in t1's. The name brought the room to the door; the argument set how
many came in.

The one precedent for a famous maintainer's stance on AI-written code is the 05-29
Linus post at 128,280, and this is 2% of it. Nothing the corpus has validated explains
the gap, and this retro does not guess at it.

## Hook to body

Accurate. "Put pencils down at 53%" is DHH's phrase plus the benchmark's own best
number, and the body delivers both within four sentences: GPT-6 Astra at 53%, Claude
at 32%, 20 real tickets. `hook_matched_body: true`.

## Firsthand layer

The owner's line is "I built blazediff-agent around the same idea. Deterministic CLI
steps do the work, and the agent only handles the reasoning." It is a process-level
line with no number, the shape the tier page records as not promoting a t0. The
subject here was not t0, so this post says nothing about promotion either way. The
lane-scoped firsthand flag is discredited in the current report (0.76x) and is not
cited.

## Ending

The post ends on a question: "Did any of your fixes last week make the next run
better?" Question endings are the lane's one validated anti-pattern (n=5, median 305
against 514 without, 0.59x). This post is one of those five, and it is the one that
beat the cohort; the flag held at 0.59x with it included, which means the other four
landed well under 305. One post against four is not a reversal. No comment data
scraped, so whether the question drew replies is `null`, not inferred from silence.

## Decision

**Repeat.** A t2 name's stance on a debate the reader is already in, with the
benchmark number in the hook, is the best-performing shape in the lane since August
and should run again when the next one happens. One change: the body earned a stance
("the rule is about where a failure goes") and the last line gave it away to a
question. End on the stance. And score the shape as what it is: a t2 name carrying one
company's policy lands in t1, so pre-score it 1 and treat anything over 3570 as a
surprise rather than a hold.
