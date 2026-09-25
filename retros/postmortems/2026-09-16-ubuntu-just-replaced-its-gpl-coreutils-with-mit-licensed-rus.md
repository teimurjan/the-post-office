---
kind: postmortem
source_post: posts/2026/09-16-ubuntu-just-replaced-its-gpl-coreutils-with-mit-licensed-rus.md
topic_family: other
source_type: news
lane: news
hook_type: claim
reach_tier: t2-universal
scored_at_ideation: 2
landed_in_band: t0-vendor-paper-or-self
impressions: 107
likes: null
comments: null
shares: null
scrape_age_hours: 41
# Own cohort (under 48h) is n=1 — this post. The nearest populated cohort is used
# for the comparison and named here so the number can be rechecked.
cohort: 1 to 4 weeks (nearest populated; own under-48h cohort is n=1)
cohort_median_at_run: 597
beat_median: false
likely_failure_modes:
  - a t2 tool named in the hook, a t0 property argued in the body (the license of coreutils, not coreutils)
  - the runnable firsthand artifact (blazediff-png) supports the rewrite claim, not the license claim the post turns on
  - number is 41 hours old and its own scrape cohort is empty; the 72h retro is the better judge
decision: modify
summary: Pre-scored t2 on the strength of ls, cp and Rust, landed at 107 — inside t0's 78-236 band — because the argument was about copyleft, a property of the tool the audience has never fought with, and the firsthand codec rewrite did not bear on it.
wiki_candidate: Naming a t2 tool in the hook does not build the room when the argument is about a property of that tool the reader has not personally fought with; the license of coreutils is a t0 subject wearing a t2 name.
wiki_pages: [audience]
wiki_ingested: true
generated_at: 2026-09-21T09:42:49.000Z
---

The post took Ubuntu 26.10's switch from GNU coreutils to the Rust uutils and argued that the story was not memory safety but a license swap: a behaviour-compatible rewrite is new code, the rewrite ships under MIT, and nobody chose to drop copyleft.

It was scraped 41 hours after publishing at 107 impressions. Its own scrape-age cohort (under 48h) contains only itself, so there is no honest cohort median; against the nearest populated cohort (1 to 4 weeks, n=36, median 597) it sits at 18%, and 107 is inside t0's observed band (78 to 236) on `wiki/audience.md`. The number may still move, and the 72-hour retro on the draft is the place to settle that. It will not move by the 50x needed to reach the t2 floor of 5,154.

This was the third post pre-scored `reach_ceiling: 2`, and the brief's case was the right shape for once — not heat, not name recognition, but "every developer has typed cp and sort." That test passes for the tool and fails for the argument. The Rust exemplar at 32,731 argued about Rust rewrites shipping, which is a thing the reader has done or refused to do. This post's hook names ls, cp and Rust, and then its wedge is GPL versus MIT: a governance question a working builder has an opinion on at most once a year. The room was measured for the noun in the first line, and the post spent its body in a different one. The only validated anti-pattern in the lane, news without firsthand signal, does not apply — the post has a firsthand paragraph — so this is not a craft miss the corpus already knows about.

That firsthand paragraph is worth a separate note because it is the first *runnable* artifact in a news post, the thing the tier page's open question asks about. blazediff-png is real: same bytes decoded as spng, same malformed inputs rejected, single thread, SIMD. What it evidences is "a rewrite is entirely my code." It says nothing about choosing a license, which is the claim the post ends on, so the firsthand layer and the wedge point in different directions. The hook is honest to the body — Ubuntu did replace GPL coreutils with MIT-licensed Rust — so this is not an overpromise failure either.

The single change: when a t2 tool is the hook and the wedge is about one of its properties, apply the tier test to the property. "Has the reader lost an afternoon to this" is true of `cp` and false of copyleft. A coreutils post that argued a behaviour difference the reader would hit — a flag that changed, output that diverged, a script that broke on 26.10 — would have been arguing in the room it was scored for, and the codec rewrite would have been a matching receipt.
