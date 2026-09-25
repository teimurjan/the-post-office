---
draft_file: drafts/2026-09-14-368-on-meta-ads-three-sign-ups.md
source_post: posts/2026/09-14-368-on-meta-ads-three-sign-ups-week-one-of-running-ads-for-w.md
topic_family: other
source_type: experiment
lane: experience
reach_tier: null
pillar: didnt-teach-me
published_url: 'https://www.linkedin.com/feed/update/urn:li:activity:7505249294283816960/'
published_at: '2026-09-14T13:01:12.546Z'
impressions_72h: 125
impressions_24h: null
likes_72h: null
comments_72h: null
shares_72h: null
cohort: 2 to 7 days
cohort_median_at_run: 282
beat_median_impressions: false
beat_peer_group: false
discussion_validated: null
hook_matched_body: true
decision: modify
summary: First didnt-teach-me pillar post, receipts on every line ($368, 42k impressions, three sign-ups, a 4.4s page fixed to no effect), at 125 impressions — 44% of the 2-to-7-day experience cohort and second-lowest in the lane. A failed-experiment report filed mid-course, with the fix still untested, landed with the process reports.
wiki_candidate: In the experience lane, a fully-receipted report of the owner's own experiment that ends before the outcome is known lands in the bottom (process-report) cluster; the receipt does not lift it.
wiki_pages: [experience]
wiki_ingested: true
---

# Retro — $368 on Meta ads. Three sign-ups.

**Lane:** experience. **Pillar:** didnt-teach-me. **Impressions:** 125 (frozen at
first scrape, ~3.7 days after publishing). Likes, comments, and shares all failed
to scrape (`null`). [[experience]] lists this post at 96 in `bottom_five`; the
archive file now carries 125, so that page's twin is stale by a rescrape.

## Beat its cohort?

No. Scraped at ~89 hours, the post sits in the **2 to 7 days** experience cohort
(n=3, median 282) and landed at 125 — 44% of that median. It is under the
1-to-4-weeks cohort (n=9, median 210) and the lane median (362) as well, and it is
the second-lowest post in the 20-post lane, above only the 76 company-milestone
announcement. The cohort is n=3, so the ratio is directional, but the post missed
every experience baseline there is.

## Pillar and receipt

Pillar: **didnt-teach-me** — ten years of engineering said fix the page, and the
page was not the problem. The receipt is complete: $368 spent, 42k impressions,
three registrations, a 4.4-second load brought to a perfect Lighthouse score with
no movement in sign-ups, then a rebuilt funnel that was "a bit better, still bad."
Every claim has a number. **The number did not carry the post.**

This is the first `didnt-teach-me` post ingested and the first experience post
about the sell side rather than the owner's tooling, so it is one data point on a
pillar [[experience]] has nothing on. It is also the third receipt-bearing post
to land in the lane's low end — after the 06-17 PNG encoder (3.8x, 242) and the
09-09 dashboards post (a day to two minutes, 138). Three posts with a clean number
in the hook, all at or under two-thirds of the lane median. The early read on that
page — a receipt is necessary, not sufficient — holds a third time.

## Hook to body

Accurate. "$368 on Meta ads. Three sign-ups." is exactly what week one produced,
and the body walks the debugging sequence that followed. `hook_matched_body: true`.

## Discussion angle

The draft's angle was that the first fix was the engineering one and it changed
nothing. The post closes on "Let's see how it goes" rather than a stance or a
question, so there was no explicit invitation to disagree. No comment data
scraped; `null`, not inferred from silence.

## The cause, and the decision

The craft was fine and the shape landed where the lane's floor shapes land. What
separates this post from the process reports [[experience]] already tracks is that
it is about the owner's business rather than the owner's tooling — and it made no
difference. What it shares with them is that the reader is handed an account of the
owner's week with nothing to use: the lesson ("the audience was too broad") is the
most common line in any ads post-mortem, and the post ends before the new audience
has a number, so the one thing that would have been the owner's own — did the
re-targeting work, and by how much — is not in it.

The nearest experience post on the same app, the 09-01 founder post, landed at 943.
That is the lane's second-highest and it is uncharted, so this retro cannot say
what it had that this one lacks. Worth a look before the next post on this app.

**Decision: modify.** Keep the pillar and the receipts; the dossier requires them
and they are the right kind. Change the moment of filing: a `didnt-teach-me`
experiment post should ship when the experiment has a result — "$368 got three
sign-ups; $X on the narrowed audience got Y" — so the lesson is the owner's own
measured outcome rather than a hypothesis about it. One data point; do not block
the pillar.
