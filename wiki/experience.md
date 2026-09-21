---
page: experience
kind: audience
title: What reaches in the experience lane
status: provisional
confidence: low
evidence_n: 6
lane: experience
evidence_posts:
  - posts/2025/12-09-i-finally-get-to-share-something-i-ve-been-working-on-for-we.md
  - posts/2026/08-06-eleven-of-my-last-twenty-commits-say-chore-uptodate-an-agent.md
  - posts/2026/04-21-most-llm-memory-demos-you-see-are-benchmarked-on-50-session.md
  - posts/2026/05-28-four-linkedin-posts-lost-in-a-row-same-shape-every-time-toda.md
  - posts/2025/02-28-i-m-thrilled-to-share-one-of-our-biggest-milestones-yet-at-r.md
  - posts/2026/09-09-the-dashboards-will-eat-your-evening-before-the-code-does-up.md
# Shipped-work posts that landed at or below the process-report cluster. They are why
# this page makes no claim that shipping something is enough.
counter_posts:
  - posts/2026/08-28-i-shipped-an-image-differ-the-speed-was-the-easy-part-visual.md
  - posts/2026/06-17-single-thread-no-parallelism-3-8x-faster-than-libspng-i-buil.md
counter_evidence:
  - post: posts/2026/08-28-i-shipped-an-image-differ-the-speed-was-the-easy-part-visual.md
    impressions: 179
    shape: launch of the owner's own shipped software
  - post: posts/2026/06-17-single-thread-no-parallelism-3-8x-faster-than-libspng-i-buil.md
    impressions: 242
    shape: the owner's own benchmarked PNG encoder
posts_covered: 60
corpus_median_at_revision: 439
patterns_generated_at: 2026-09-02
last_revised: 2026-09-16
revised_by: wiki-curator
supersedes: []
# Lane-scoped, from `bun run post-patterns --lane experience`. Twins every number
# quoted in the body.
lane_stats:
  n: 20
  median: 362
  p25: 200
  p75: 733
  min: 76
  max: 1271
  median_minus_top: 330
  cohort_2to7d_n: 3
  cohort_2to7d_median: 282
  cohort_1to4w_n: 8
  cohort_1to4w_median: 226
  above_400_n: 9
  above_400_threshold: 400
# The bottom five of the lane after it grew to 20 posts. Two are uncharted here (the
# 09-14 Meta-ads post and the 08-28 image-differ counter-post); the other three are
# charted. Twins the numbers in "What the posts show".
bottom_five:
  - impressions: 76
    post: posts/2025/02-28-i-m-thrilled-to-share-one-of-our-biggest-milestones-yet-at-r.md
  - impressions: 96
    post: posts/2026/09-14-368-on-meta-ads-three-sign-ups-week-one-of-running-ads-for-w.md
  - impressions: 138
    post: posts/2026/09-09-the-dashboards-will-eat-your-evening-before-the-code-does-up.md
  - impressions: 179
    post: posts/2026/08-28-i-shipped-an-image-differ-the-speed-was-the-easy-part-visual.md
  - impressions: 181
    post: posts/2026/05-28-four-linkedin-posts-lost-in-a-row-same-shape-every-time-toda.md
# Five posts relocated here from [[audience]] on 2026-09-02, plus the 09-09 dashboards
# post, the first ingested from an experience-lane retro. Each with its subject shape.
observed:
  - post: posts/2025/12-09-i-finally-get-to-share-something-i-ve-been-working-on-for-we.md
    impressions: 1271
    shape: launch of the owner's own shipped software (Avatune)
    note: the lane maximum
  - post: posts/2026/08-06-eleven-of-my-last-twenty-commits-say-chore-uptodate-an-agent.md
    impressions: 210
    shape: the owner's own commit log
  - post: posts/2026/04-21-most-llm-memory-demos-you-see-are-benchmarked-on-50-session.md
    impressions: 200
    shape: the owner's own benchmarking niche
  - post: posts/2026/05-28-four-linkedin-posts-lost-in-a-row-same-shape-every-time-toda.md
    impressions: 181
    shape: the owner's own LinkedIn posting performance
  - post: posts/2026/09-09-the-dashboards-will-eat-your-evening-before-the-code-does-up.md
    impressions: 138
    shape: the owner's own internal tooling automation (App Store ops)
    note: first pillar-carrying post (replaced-a-hire), first to carry a receipt
  - post: posts/2025/02-28-i-m-thrilled-to-share-one-of-our-biggest-milestones-yet-at-r.md
    impressions: 76
    shape: a company milestone announcement
    note: the lane minimum
---

# What reaches in the experience lane

The experience lane is the owner's own operation: an app they run, a number they
measured, a function they built instead of hiring, a lesson the sell side taught them.
It is defined by the brand wiki (`bun run --silent --cwd .vendor/teimurjan-llm-wiki wiki view post-writing`) and drafted by `experience-post-cycle`.

This page exists because [[audience]] was calibrated on news posts and had five
experience posts cited in its tiers. Those five were moved here on 2026-09-02. The
lanes are analyzed separately (`bun run post-patterns --lane experience`), so a number
computed across both is a number nobody can recompute.

Catalogued in [[index]]. Revision history in [[log]].

## The lane's own scale

n=20, median 362 impressions, p25 200, p75 733, range 76–1271. Drop the top post and
the median is 330. The whole lane fits inside the bottom third of the news lane's
range, and its maximum (1,271) would rank below the news lane's t1 floor.

**That comparison is the one thing this page forbids.** A news post's reach says
nothing about an experience post's. The lane has a different room — the owner's own
following rather than a standing crowd around a public artifact — and its numbers are
only meaningful against each other.

## What the five posts show

Ordered by reach, they fall into a shape the news-lane tier model does not describe:

| Shape | Impressions |
|---|---|
| Launch of the owner's own shipped software | 1271 |
| The owner's own commit log | 210 |
| The owner's own benchmarking niche | 200 |
| The owner's own LinkedIn posting performance | 181 |
| A company milestone announcement | 76 |

The launch is 6x the next post and is the lane maximum. The three middle posts cluster
tightly at 181–210, around the lane's p25 (200). The milestone announcement is the
lane minimum and the smallest post in the whole archive.

**The tempting reading is wrong, and the rest of the cohort says so.** The
obvious conclusion from this table — that the lane rewards a thing the owner built and
punishes a report on the owner's own process — does not survive contact with the rest of
the cohort. The 08-28 image-differ post is shipped software and landed at 179, in the
same low cluster as the process reports on this page. The 06-17 PNG-encoder post is
shipped software with a 3.8x benchmark in the hook and landed at 242. Both are recorded
as `counter_posts`. Shipping something is not sufficient, and the 1,271 launch is one post.

What survives is the narrower, negative half: **the owner's process- and tooling-report
posts cluster around half the lane median.** Four are now charted — the commit log (210),
the benchmarking setup (200), the posting retrospective (181), and the 09-09 dashboards
post (138) — against a lane median of 362. As the lane grew to 20 posts, two newer
entries (the 09-14 Meta-ads post at 96 and the dashboards post at 138) took over the
strict bottom of the range, but the process-report cluster stayed low regardless. The
milestone announcement (76) is the floor and is the one charted post with no technical
artifact in it at all. `evidence_n: 6`, `confidence: low`: this is a floor observation
about one shape, not a theory of the lane.

[[audience]] independently reached the same exclusion from the news side: it records that
a firsthand line about the owner's *process* does not promote a subject, citing the
commit-log post. That is the same underlying post, so it is agreement, not confirmation.

## What this page cannot say yet

- **Almost nothing about pillars.** The brand wiki defines four
  (`replaced-a-hire`, `numbers-from-a-company-of-one`, `didnt-teach-me`,
  `nights-and-weekends`). The five relocated posts predate the axis and were labelled
  post-hoc; mapping them now would be inventing evidence. The 09-09 dashboards post is
  the first drafted against a pillar (`replaced-a-hire`) to be ingested here — one post,
  enough to start the work, not to characterize a pillar. At n=1 the only honest read is
  that a `replaced-a-hire` post built purely as an internal-tooling receipt landed at 138,
  in the process-report cluster.
- **Nothing with a tier model.** Five posts across five different shapes cannot produce
  bands. Do not import [[audience]]'s t0/t1/t2 here; the tiers measure a standing public
  audience, which is not what this lane draws on.
- **A first data point on receipts.** `post-critic` zeroes `specificity` on an
  experience post with no number, and the dossier requires the receipt. This page now
  has two posts that carried a clear number and still landed low: the 06-17 PNG-encoder
  (a 3.8x benchmark, 242) and the 09-09 dashboards post (a day-to-two-minutes automation
  receipt, 138). Two posts is not a finding, but the early signal is that a receipt is
  necessary, not sufficient — it does not lift a post out of the low cluster on its own.
- **Nothing about the lane's upper half.** Nine of the twenty posts clear 400
  impressions and not one of them is charted here, because none had a retro to ingest.
  Every claim above is drawn from the bottom of the lane.

## Open questions

- What separates the 1,271 launch from the 179 launch? Both are the owner shipping
  software. This is the lane's central open question and nothing on this page answers it.
- Is the process-report floor real, or is it four posts that were separately weak? They
  cluster around half the lane median of 362, which is suggestive at n=4 and nothing more.
- What do the nine posts above 400 have in common? The lane's entire upper half is
  uncharacterized, and until a retro covers one, this page describes only how the lane
  fails.
