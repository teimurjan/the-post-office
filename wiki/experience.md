---
page: experience
kind: audience
title: What reaches in the experience lane
status: provisional
confidence: low
evidence_n: 10
lane: experience
evidence_posts:
  - posts/2025/12-09-i-finally-get-to-share-something-i-ve-been-working-on-for-we.md
  - posts/2026/08-06-eleven-of-my-last-twenty-commits-say-chore-uptodate-an-agent.md
  - posts/2026/04-21-most-llm-memory-demos-you-see-are-benchmarked-on-50-session.md
  - posts/2026/05-28-four-linkedin-posts-lost-in-a-row-same-shape-every-time-toda.md
  - posts/2025/02-28-i-m-thrilled-to-share-one-of-our-biggest-milestones-yet-at-r.md
  - posts/2026/09-09-the-dashboards-will-eat-your-evening-before-the-code-does-up.md
  - posts/2026/09-14-368-on-meta-ads-three-sign-ups-week-one-of-running-ads-for-w.md
  - posts/2026/09-28-one-superuser-did-what-657-of-ads-could-not-657-on-meta-ads.md
  - posts/2026/10-13-yesterday-i-made-my-fourth-ios-app-building-ios-apps-with-ag.md
  - posts/2026/10-15-2-users-who-left-after-trial-told-me-the-same-thing-it-s-too.md
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
posts_covered: 69
corpus_median_at_revision: 415
patterns_generated_at: 2026-10-21
last_revised: 2026-10-21
revised_by: wiki-curator
supersedes: []
# Lane-scoped, from `bun run post-patterns --lane experience`. Twins every number
# quoted in the body.
lane_stats:
  n: 23
  median: 330
  p25: 200
  p75: 865
  min: 76
  max: 73129
  median_minus_top: 307
  prior_max: 1271
  cohort_2to7d_n: 3
  cohort_2to7d_median: 284
  cohort_1to4w_n: 12
  cohort_1to4w_median: 205
  above_400_n: 10
  above_400_threshold: 400
# The bottom five of the lane at 23 posts, all charted except the 08-28 image-differ
# counter-post. Rescrape since the last revision: 09-28 133 -> 172. Twins the numbers
# in "What the posts show".
bottom_five:
  - impressions: 76
    post: posts/2025/02-28-i-m-thrilled-to-share-one-of-our-biggest-milestones-yet-at-r.md
  - impressions: 147
    post: posts/2026/09-09-the-dashboards-will-eat-your-evening-before-the-code-does-up.md
  - impressions: 151
    post: posts/2026/09-14-368-on-meta-ads-three-sign-ups-week-one-of-running-ads-for-w.md
  - impressions: 172
    post: posts/2026/09-28-one-superuser-did-what-657-of-ads-could-not-657-on-meta-ads.md
  - impressions: 179
    post: posts/2026/08-28-i-shipped-an-image-differ-the-speed-was-the-easy-part-visual.md
# Five posts relocated here from [[audience]] on 2026-09-02, plus every post ingested
# from an experience-lane retro since. Each with its subject shape.
observed:
  - post: posts/2025/12-09-i-finally-get-to-share-something-i-ve-been-working-on-for-we.md
    impressions: 1271
    shape: launch of the owner's own shipped software (Avatune)
    note: the lane maximum until 2026-10-13
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
    impressions: 147
    shape: the owner's own internal tooling automation (App Store ops)
    note: first pillar-carrying post (replaced-a-hire), first to carry a receipt
  - post: posts/2025/02-28-i-m-thrilled-to-share-one-of-our-biggest-milestones-yet-at-r.md
    impressions: 76
    shape: a company milestone announcement
    note: the lane minimum
  - post: posts/2026/09-14-368-on-meta-ads-three-sign-ups-week-one-of-running-ads-for-w.md
    impressions: 151
    rescrape_history: [96, 125, 151]
    shape: the owner's own failed marketing experiment, filed before the fix had a number
    note: first didnt-teach-me pillar post; first about the sell side rather than the owner's tooling
  - post: posts/2026/09-28-one-superuser-did-what-657-of-ads-could-not-657-on-meta-ads.md
    impressions: 172
    rescrape_history: [133, 172]
    shape: the owner's own ad experiment, filed with its outcome ($602 of ads to two lifetime purchases)
    note: second didnt-teach-me pillar post; the follow-up the 09-14 retro asked for, and the test of its hypothesis
  - post: posts/2026/10-13-yesterday-i-made-my-fourth-ios-app-building-ios-apps-with-ag.md
    impressions: 73129
    scrape_age_hours: 190
    shape: build story of the owner's fourth app shipped with agents, turning on the marketing the automation could not do; ad results in one paragraph with no dollar figure
    note: third didnt-teach-me pillar post, same operation as the two Meta-ads ledgers; the lane maximum; author owner, cover four real app screenshots; analytics panel not supplied
  - post: posts/2026/10-15-2-users-who-left-after-trial-told-me-the-same-thing-it-s-too.md
    impressions: 284
    scrape_age_hours: 142
    shape: two churned users' words, the owner's design gap, and a plan to try an unusual-design niche; text-only, link in the comments
    note: fourth didnt-teach-me pillar post, two days after the 10-13 breakout; never went through post-image; analytics panel not supplied
# Receipt-bearing posts that landed in the low end anyway. Twins "A first data point
# on receipts". n=5, so this is still an early signal, not a finding.
receipt_bearing_low:
  evidence_n: 5
  lane_median: 330
  evidence:
    - post: posts/2026/06-17-single-thread-no-parallelism-3-8x-faster-than-libspng-i-buil.md
      impressions: 242
      receipt: a 3.8x benchmark
    - post: posts/2026/09-09-the-dashboards-will-eat-your-evening-before-the-code-does-up.md
      impressions: 147
      receipt: a full day to two minutes across 17 languages
    - post: posts/2026/09-14-368-on-meta-ads-three-sign-ups-week-one-of-running-ads-for-w.md
      impressions: 151
      receipt: $368, 42k impressions, three sign-ups
    - post: posts/2026/09-28-one-superuser-did-what-657-of-ads-could-not-657-on-meta-ads.md
      impressions: 172
      receipt: $657 to zero purchases, then $602 to two lifetime purchases at $83 of ads each
    - post: posts/2026/10-15-2-users-who-left-after-trial-told-me-the-same-thing-it-s-too.md
      impressions: 284
      receipt: 6% impression-to-install, 9 of 10 new users gone after trial
# Pillar-tagged posts ingested so far. Nothing here is a claim about a pillar; n=1 and n=4.
pillars_observed:
  replaced-a-hire:
    evidence_n: 1
    post: posts/2026/09-09-the-dashboards-will-eat-your-evening-before-the-code-does-up.md
    impressions: 147
  didnt-teach-me:
    evidence_n: 4
    posts:
      - post: posts/2026/09-14-368-on-meta-ads-three-sign-ups-week-one-of-running-ads-for-w.md
        impressions: 151
      - post: posts/2026/09-28-one-superuser-did-what-657-of-ads-could-not-657-on-meta-ads.md
        impressions: 172
      - post: posts/2026/10-13-yesterday-i-made-my-fourth-ios-app-building-ios-apps-with-ag.md
        impressions: 73129
      - post: posts/2026/10-15-2-users-who-left-after-trial-told-me-the-same-thing-it-s-too.md
        impressions: 284
# The post after the lane's breakout, named behind the open question on carry-over. n=1.
breakout_followup:
  post: posts/2026/10-15-2-users-who-left-after-trial-told-me-the-same-thing-it-s-too.md
  impressions: 284
  days_after_breakout: 2
  breakout_post: posts/2026/10-13-yesterday-i-made-my-fourth-ios-app-building-ios-apps-with-ag.md
  breakout_impressions: 73129
  cohort_2to7d_median_excluding_self: 338
# Uncharted upper-half post named in "Open questions" as the pair for the Meta-ads posts.
# Not evidence; a pointer to the retro that would make it evidence.
uncharted_pair:
  post: posts/2026/09-01-10-years-as-an-engineer-0-years-as-a-founder-why-for-most-of.md
  impressions: 943
  days_before_0914: 13
  days_before_0928: 27
# The lane's posts above 800, named so the open question about the ledger shape has
# twins. Only the 10-13 post has a retro; the other five are uncharted.
upper_half_observed:
  evidence_n: 6
  threshold: 800
  posts:
    - post: posts/2026/10-13-yesterday-i-made-my-fourth-ios-app-building-ios-apps-with-ag.md
      impressions: 73129
      shape: build story of the owner's fourth app, turning on what the automation could not do
    - post: posts/2025/12-09-i-finally-get-to-share-something-i-ve-been-working-on-for-we.md
      impressions: 1271
      shape: launch of the owner's own shipped software
    - post: posts/2025/03-24-my-article-made-it-to-hackernoon-s-top-stories-i-recently-wr.md
      impressions: 1055
      shape: a placement of the owner's writing
    - post: posts/2026/09-01-10-years-as-an-engineer-0-years-as-a-founder-why-for-most-of.md
      impressions: 943
      shape: the owner's identity, ten years an engineer and zero a founder
    - post: posts/2026/03-10-tiny-models-are-getting-weirdly-useful-i-ve-been-experimenti.md
      impressions: 881
      shape: an observation about small models
    - post: posts/2025/11-25-i-m-excited-to-share-a-new-update-we-ve-been-working-on-at-s.md
      impressions: 865
      shape: a product update from the owner's employer
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

n=23, median 330 impressions, p25 200, p75 865, range 76–73,129. Drop the top post and
the median is 307. The top post is the 10-13 fourth-iOS-app post, 57x the previous lane
maximum (the Avatune launch at 1,271); it sits alone, and every other number on this
page describes the lane without it.

**Never compare this lane's numbers with the news lane's.** A news post's reach says
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

The launch is 6x the next post in this table and was the lane maximum until 2026-10-13.
The three middle posts cluster tightly at 181–210, around the lane's p25 (200). The
milestone announcement is the lane minimum and the smallest post in the whole archive.

**The tempting reading is wrong, and the rest of the cohort says so.** The
obvious conclusion from this table — that the lane rewards a thing the owner built and
punishes a report on the owner's own process — does not survive contact with the rest of
the cohort. The 08-28 image-differ post is shipped software and landed at 179, in the
same low cluster as the process reports on this page. The 06-17 PNG-encoder post is
shipped software with a 3.8x benchmark in the hook and landed at 242. Both are recorded
as `counter_posts`. Shipping something is not sufficient, and the 1,271 launch is one post.

What survives is the narrower, negative half: **the owner's process- and tooling-report
posts cluster around half the lane median.** Four are charted — the commit log (210),
the benchmarking setup (200), the posting retrospective (181), and the 09-09 dashboards
post (147) — against a lane median of 330. The milestone announcement (76) is the floor
and is the one charted post with no technical artifact in it at all.

The 09-14 Meta-ads post (151, rescraped from 96 and 125) widens that floor by one shape. It is
not a tooling report; it is the owner's own failed ad experiment, receipts on every
line, and it landed in the lane's bottom three. What it shares with the process reports
is that the reader is handed an account of the owner's week with nothing to use — the
post ends before the narrowed audience has a number. At the 09-14 ingest the floor was described as reports on the owner's own operation
with no outcome the reader can act on.

The 09-28 follow-up is the test of that description, and the description fails it.
Filed with the outcome in hand ($602 of ads to two lifetime purchases at $83 each, after
$657 to none), it first landed at 133 and now reads 172 on rescrape: fourth-lowest in
the lane, next to the mid-course post it continued. The outcome being present did not
lift it out of the bottom four, so the missing outcome was not the variable. What the
two Meta-ads posts share with the process reports is the shape, a ledger of the owner's
own operation, dollars or hours in and outcomes out, and the reader did not distinguish
the ledger with a result from the one without. So the floor is better described as
**ledgers of the owner's own operation, whether or not the outcome is in**.

## The first charted post from the top

The 10-13 post is the third `didnt-teach-me` post and the third about the same
operation as the two Meta-ads ledgers, and it is the lane maximum at 73,129, frozen at
first scrape 190 hours in. Its shape is not a ledger: a build story (the owner's fourth
iOS app, idea to MVP in 3-4 days with agents) that turns on what the automation could
not do (marketing, where the owner delegates less the deeper he goes), with the ad
results told in one paragraph and no dollar figure. It is the frame the 09-28 retro
prescribed, and its retro decision is `repeat`.

That makes it the first test of the ledger question from inside one operation: same
apps, same ad campaigns, two ledgers at 151 and 172 and one build story at 73,129. It
points the same way as `upper_half_observed`, where none of the six posts above 800 is
a ledger. It does not isolate the shape. The subject (shipping apps with coding agents,
which a large share of builders have tried), the cover (four real app screenshots, the
first experience post under the native-image rule) and the author rule all changed at
once, and the owner's analytics panel was not supplied, so how far the post went out of
network is unrecorded. An outlier this size is an anecdote for any single cause. It is
recorded as evidence that the ledger floor is a floor of the shape, not of the subject
(Meta ads) or the pillar.

The floor claim rests on nine of this page's `evidence_n: 10` posts, eight from the
bottom of the lane and one from the top; the tenth, the 10-15 post at 284, sits in the
middle and neither supports nor tests it. `confidence: low` is held: the one top post changed four variables at once.

[[audience]] independently reached the same exclusion from the news side: it records that
a firsthand line about the owner's *process* does not promote a subject, citing the
commit-log post. That is the same underlying post, so it is agreement, not confirmation.

## What this page cannot say yet

- **Almost nothing about pillars.** The brand wiki defines four
  (`replaced-a-hire`, `numbers-from-a-company-of-one`, `didnt-teach-me`,
  `nights-and-weekends`). The five relocated posts predate the axis and were labelled
  post-hoc; mapping them now would be inventing evidence. Five pillar-tagged posts have
  been ingested (`pillars_observed`): the 09-09 dashboards post (`replaced-a-hire`, 147)
  and four `didnt-teach-me` posts — the two Meta-ads ledgers (151 and 172), the 10-13
  build story (73,129) and the 10-15 churn post (284). One pillar holds the lane maximum,
  a middle post and two of the bottom four, so the pillar is not what sets the floor.
  That is all n=4 supports.
- **Nothing with a tier model.** Do not import [[audience]]'s t0/t1/t2 here; the tiers
  measure a standing public audience, which is not what this lane draws on.
- **An early signal on receipts.** `post-critic` zeroes `specificity` on an
  experience post with no number, and the dossier requires the receipt. This page has
  five posts that carried a clear number and still landed under the lane median
  (`receipt_bearing_low`): the 06-17 PNG-encoder (a 3.8x benchmark, 242), the 09-09
  dashboards post (a day-to-two-minutes automation receipt, 147), the 09-14 Meta-ads
  post ($368, 42k impressions, three sign-ups — 151), the 09-28 follow-up ($657 to
  zero purchases, then $602 to two — 172), and the 10-15 churn post (6%
  impression-to-install, 9 of 10 gone after trial — 284, under the median of 330 but
  above the bottom cluster). The 10-13 post carried build numbers too, so
  receipts sit at both ends of the lane: a receipt is necessary, not sufficient, and
  does not lift a post on its own.
- **Almost nothing about the lane's upper half.** Ten of the twenty-three posts clear
  400 impressions and one of them is charted, the 10-13 outlier, which is no guide to
  the other nine.

## Open questions

- What separates the 1,271 launch from the 179 launch? Both are the owner shipping
  software. Nothing on this page answers it.
- What separates the 09-01 founder post (943, uncharted) from the two Meta-ads posts
  (151 and 172)? Same app, thirteen and twenty-seven days apart, one in the lane's top
  five and two in its bottom four. The 09-01 post has no local draft, so `post-retro`
  cannot cover it; charting it would take a query pass against the post file itself.
- Is the ledger shape the variable? The 10-13 build story is the first charted test and
  points the same way as the six posts above 800, none a ledger. The next experience post
  in the build-story shape, with the money out of the spine, is the test that would
  separate the shape from the subject; a second ledger above the lane median would break
  the floor claim.
- Did the 10-13 post leave the owner's network? The analytics panel would say. No
  experience post has an in-network split on record, so the lane has no reading yet of
  which room a breakout comes from.
- Does a breakout lift the next post? The 10-15 post went out two days after the 10-13
  breakout and landed at 284, the 2-to-7-day cohort median itself (338 without it). It
  was text-only and on a narrower subject, so it does not separate carry-over from
  subject; one follow-up is an anecdote. If the next experience post after a breakout
  also lands at its cohort median, the breakout's room was not the owner's following.
- Is the process-report floor real, or is it four posts that were separately weak? They cluster around half the lane median of 330, which is suggestive at n=4 and nothing more.
