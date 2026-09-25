---
draft_file: drafts/2026-09-16-ubuntu-just-replaced-its-gpl-coreutils-with-mit.md
source_post: posts/2026/09-16-ubuntu-just-replaced-its-gpl-coreutils-with-mit-licensed-rus.md
topic_family: other
source_type: news
lane: news
reach_tier: t2-universal
scored_at_ideation: 2
landed_in_band: t0-vendor-paper-or-self
pillar: null
published_url: 'https://www.linkedin.com/feed/update/urn:li:activity:7505974022212382721/'
published_at: '2026-09-16T13:01:01.149Z'
impressions_72h: 107
impressions_24h: null
likes_72h: null
comments_72h: null
shares_72h: null
scrape_age_hours: 41
# Own cohort (under 48h) is n=1, this post. The nearest populated cohort is named
# so the comparison can be rechecked; the ratio is against that one.
cohort: 1 to 4 weeks (nearest populated; own under-48h cohort is n=1)
cohort_median_at_run: 597
beat_median_impressions: false
beat_peer_group: false
discussion_validated: null
hook_matched_body: true
decision: modify
summary: Pre-scored t2 on ls, cp and Rust, published at 107 — inside t0's 78-236 band and the third pre-scored t2 miss — with a runnable firsthand artifact in the body. The tool was t2; the argument was about its license, which the reader has never fought with.
wiki_candidate: A pre-scored t2 subject lands in t0's band when the post's argument is about a property of the tool (its license) rather than the tool the reader has fought with; the tier test has to be applied to the argued property, not the noun in the hook.
wiki_pages: [audience]
wiki_ingested: true
---

# Retro — Ubuntu just replaced its GPL coreutils with MIT-licensed Rust

**Lane:** news. **Impressions:** 107 (frozen at first scrape, ~41 hours after
publishing). Likes, comments, and shares all failed to scrape (`null`).

## Beat its cohort?

No, with a caveat about the cohort. Scraped at 41 hours, the post is the only
member of the **under 48h** news cohort (n=1), so there is no cohort median to
beat. Against the nearest populated cohort (1 to 4 weeks, n=36, median 597) it sits
at 18%; against the 2-to-7-day cohort (n=1, 876) at 12%. The number is young and
may still move, but not by the ~50x that would take it to the t2 floor of 5,154.
Within the news lane this is a miss on every available comparison.

## Tier and where it landed

The brief scored `reach_ceiling: 2`, `t2-universal`, citing the Rust exemplar
(07-10, 32,731) and "every developer has typed cp and sort." That is the right kind
of argument — not heat, not name recognition — and the tool passes it. The post
landed at 107, **inside t0's observed band (78–236)** on [[audience]], which makes
this the third pre-scored t2 to land under the page's `t2_miss_below: 1000`
trigger, after the 08-10 auto-mode post (163) and the 08-25 Windows Paint post (78).

The two earlier misses had names: heat is not size, famous is not used. This one
fails a third way. The hook names a t2 tool; the body argues about a t0 property of
it. "Has the reader lost an afternoon to this" is true of `cp` and false of copyleft.
The 32,731 Rust post argued about rewrites shipping, which is a thing the reader has
done or refused to do. This post's wedge — "did anyone actually choose to drop
copyleft?" — is a governance question the audience holds an opinion on roughly once
a year. The room was measured for the noun in line one and the post spent its body
in a different one.

## Firsthand signal

Present, and it is the first *runnable* artifact in a news post: blazediff-png
decodes the same bytes as spng, rejects the same malformed inputs, single thread,
SIMD. So the lane's one validated anti-pattern (news without firsthand signal, 0.67x)
does not apply. What the artifact evidences is "a rewrite is entirely my code"; the
claim the post turns on is that a license was quietly dropped, and the codec says
nothing about that. [[audience]]'s open question — does a runnable artifact promote
a t0 subject — stays open, because here it was attached to a t2-scored subject that
landed in t0's band anyway.

One difference between the draft and the published text: the post carries a
`lnkd.in` link as its last line, which the draft did not. The brand bundle says body
links cut reach; the corpus's ending-type flag for this is discredited (n=4, 2.21x),
so it is noted, not counted.

## Hook to body

Accurate. Ubuntu 26.10 did replace GPL GNU coreutils with MIT-licensed uutils, and
the body says exactly that. `hook_matched_body: true`.

## Discussion angle

The intended angle was that the license swap, not the memory safety, was the story.
No comment data scraped; `null`, not inferred from silence.

## The cause, and the decision

The craft was fine and the room was small — smaller than it was scored, because the
score measured the tool and the post argued its license. Record the miss in
`disputed` on [[audience]] as an assignment error of a third kind: the tier test
applied to the wrong object.

**Decision: modify.** The coreutils subject is t2 and still worth a post; the license
wedge is what to change. A coreutils post that argues a behaviour the reader will hit
— a flag that changed, output that diverged, a script that broke on 26.10 — is in the
room it was scored for, and the codec rewrite would then be a matching receipt
instead of a receipt for a different claim.
