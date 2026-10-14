---
draft_file: drafts/2026-09-28-one-superuser-did-what-657-of-ads.md
source_post: posts/2026/09-28-one-superuser-did-what-657-of-ads-could-not-657-on-meta-ads.md
topic_family: other
source_type: experiment
lane: experience
reach_tier: null
pillar: didnt-teach-me
published_url: 'https://www.linkedin.com/feed/update/urn:li:activity:7510324271773265921/'
published_at: '2026-09-28T13:07:21.468Z'
impressions_72h: 133
scrape_age_hours: 184
impressions_24h: null
likes_72h: null
comments_72h: null
shares_72h: null
cohort: 1 to 4 weeks
cohort_n: 11
cohort_median_at_run: 200
beat_median_impressions: false
beat_peer_group: false
discussion_validated: null
hook_matched_body: true
ending_type: question
# The classifier reads this post as sourceType news with hasFirsthandSignal false, which puts it
# inside the lane's one validated anti-pattern. Read as text it is first person throughout. Both recorded.
classifier_source_type: news
classifier_has_firsthand_signal: false
matched_validated_flags: [news posts without firsthand signal]
# The post this one continues: 09-14, $368 on Meta ads, now 151 on rescrape (125 at its retro).
prior_post: posts/2026/09-14-368-on-meta-ads-three-sign-ups-week-one-of-running-ads-for-w.md
prior_post_impressions: 151
days_after_prior: 14
decision: modify
summary: Second didnt-teach-me post and the follow-up the 09-14 retro asked for, filed with the outcome in hand ($602 of ads, two lifetime purchases at $83 each), at 133 impressions — 67% of the 1-to-4-week experience cohort and second-lowest in the lane. The outcome arriving did not move the number; the filing moment was not the variable.
wiki_candidate: In the experience lane, a receipted report of the owner's own experiment lands in the bottom cluster whether or not it carries the outcome; filing after the result is known does not lift it.
wiki_pages: [experience]
wiki_ingested: true
---

# Retro — One superuser did what $657 of ads could not.

**Lane:** experience. **Pillar:** didnt-teach-me. **Impressions:** 133, frozen at
first scrape about 184 hours (7.7 days) after publishing. Likes, comments and shares
failed to scrape (`null`). The tier model on `wiki/audience.md` does not apply here;
the room is the owner's own following.

## Beat its cohort?

No. Scraped at 7.7 days, the post sits in the **1 to 4 weeks** experience cohort
(n=11, median 200) and landed at 133, 67% of that median. It is under the lane median
too (330, n=21), and it is the second-lowest post in the lane, above only the 76
company-milestone announcement from 2025. The 09-14 post it continues has been
rescraped from 125 to 151 and now sits two places above it.

## Pillar and receipt

Pillar: **didnt-teach-me**. The engineering fixes (page, audience, funnel) did nothing
because the idea itself read as AI slop to that audience, and the product shaped
around one real person's problem is the one that sold. The receipt is complete: $657
and 46k impressions to five sign-ups and zero purchases; 5 versions and 35 builds;
three campaigns at $602, 192 clicks for nothing on the first two, then two lifetime
purchases at $83 of ads each. Every line has a number. **The number did not carry the
post.**

This is the second `didnt-teach-me` post ingested and the second about the sell side.
It is also the fourth receipt-bearing experience post to land in the lane's low end,
after the 06-17 PNG encoder (242), the 09-09 dashboards post (147 on rescrape) and the
09-14 Meta-ads post (151 on rescrape). The early read on [[experience]], that a receipt
is necessary and not sufficient, holds a fourth time.

## What this post tested

The 09-14 retro's decision was to file the next experiment post when the result was
in, so the lesson would be the owner's measured outcome rather than a hypothesis about
it. This post is that: the ads were stopped, the second app's campaigns ran, two
purchases arrived on 24 September, and the post went out four days later with the
figure. It landed 18 impressions under the mid-course post. One pair is not a finding,
but it is the direct test of the 09-14 hypothesis, and the hypothesis did not hold: the
moment of filing was not the variable.

## Hook to body

Accurate in substance, with one compression. The hook sets one superuser against $657
of ads; the body shows the purchases arriving through a further $602 of ads on the app
the superuser shaped. The contrast the hook draws is between the two apps, not between
people and ads, and a reader reaches paragraph four before seeing that.
`hook_matched_body: true`.

## Validated flags and ending

The experience lane's one validated anti-pattern is news posts without firsthand signal
(n=6, median 179 against 393, 0.46x), and by the classifier's reading this post is in that
set: it labels the post `sourceType: news` and `hasFirsthandSignal: false`. Read as text,
every paragraph is the owner's own ($657 spent, 35 builds, two purchases), so the heuristic
is keying on something other than first person. Both readings are recorded, as
[[audience]] does for the 08-10 and 09-16 news posts. The 09-14 post, same subject and
same shape, is read as `build_log` with firsthand signal, so the two Meta-ads posts sit on
opposite sides of a flag that did not separate them (151 against 133).
"Posts with no concrete numbers" is discredited in this lane (flagged posts do 2.17x
better) and is not cited. The post ends on a question ("Where did your first purchase
come from, an audience or one person?"); question endings are validated in the news
lane and not in this one, so it is recorded here as an observation only. The 09-09
dashboards post (147) also ended on a question. No comment data, so
`discussion_validated: null`.

## The cause, and the decision

The craft was fine and the shape landed where the lane's floor shapes land, for the
second time in a row on this subject. What the two Meta-ads posts share with the
process reports [[experience]] tracks is the shape: a ledger of the owner's own
operation, dollars in, outcomes out. One had the outcome and one did not, and the
reader did not distinguish them. The lane's five posts above 800 are not ledgers: the
Avatune launch (1271), the HackerNoon placement (1055), the 09-01 founder post on this
same app (943, still uncharted, and with no local draft `post-retro` cannot cover it),
the tiny-models observation (881), and the Speechify update (865). Five against two is
a direction to test, not a conclusion.

**Decision: modify.** Keep the pillar and the receipts; the dossier requires them.
Stop varying the timing, since it has now been tried both ways. Change the frame: the
next post on this app should be about the thing the owner learned or built, with the
dollar figures as one line of support rather than the spine of the body. A third
Meta-ads ledger under 200 would be grounds to block the ledger shape, not the pillar.
