# Wiki log

Append-only. Newest entries at the bottom. One entry per ingest, query-filed-back, or
lint pass. Entry headings follow `## [YYYY-MM-DD] <op> | <title>` so the log stays
greppable: `grep "^## \[" wiki/log.md | tail -5`.

Every entry names the corpus fingerprint it was written against, what changed, and
what it contradicted. The `contradicted:` line is required even when the answer is
`none` — without it, an ingest can quietly overwrite a claim and leave no trace.

## [2026-08-17] ingest | seed the wiki with the standing-audience tier model

- corpus: 50 posts, median 439 (435 with the top post removed)
- trigger: manual — review of the post-generation skills against the LLM-wiki pattern
- changed:
  - wiki/audience.md — created, `confidence: medium`, `evidence_n: 24`
  - wiki/brand/index.md — created
  - wiki/log.md — created
- claim added: subject recognizability separates reach in this corpus; three
  non-overlapping bands across 24 posts (t0 max 236 < t1 min 1271, t1 max 3570 < t2
  min 5144)
- contradicted: `post-ideator` held that `topic_family: other` is a tell for
  `reach_ceiling` 0 or 1. `other` (n=4, median 3472) contains the #4 and #6 posts;
  the claim is backwards and was cut. Also corrected the "55-impression post" cited
  six times across three skills: no post in the corpus has 55 impressions. The
  navel-gazing post it referred to is at 181, and the corpus worst is 76 (a company
  milestone announcement), a different failure mode.

## [2026-08-17] ingest | retro 2026-08-10 auto-mode classifier

- corpus: 50 posts, median 439
- trigger: retros/2026-08-10-humans-catch-136-of-dangerous-agent-commands.md (decision: modify)
- changed:
  - wiki/audience.md — first `disputed` entry (Claude Code auto mode default, pre-scored 2, published 135, `t2_miss_below` trigger); `counter_posts` seeded with the same post; `promotion_review` gained `pre_scored_posts_so_far: 1` / `pre_scored_missed: 1`; body gained the "Heat is not size" rule under "How to assign a tier"
- claim added: a `reach_ceiling` of 2 argued from topical heat does not hold; the score
  has to be argued from subject recognizability, and a process-level firsthand line does
  not promote a t0 subject
- evidence_n: unchanged at 24 — the post was already a t0 exemplar, so this ingest adds
  a prospective test, not a new data point
- contradicted: nothing on the page. The tier bands predicted this post correctly (135
  sits inside t0's 76-236); what failed was the ideator's route to the score. Recorded
  as an assignment error so the bands are not revised on a procedure fault. `confidence`
  held at `medium` rather than lowered, because the miss is inside a band, not between two.

## [2026-08-17] ingest | retro 2026-08-13 sqlite-tailscale

- corpus: 50 posts, median 439
- trigger: retros/2026-08-13-a-16-year-old-sqlite-bug-cost-tailscale.md (decision: repeat)
- changed:
  - wiki/audience.md — `promotion_review` now 2 prospective posts, 1 held / 1 missed;
    `context_stats` gained the 2-to-7-day cohort (n=5, median 393) both scored posts are
    measured against; body gained "The controlled pair" under "Heat is not size" and a
    paragraph stating firsthand signal is not required at t2; the firsthand open question
    was split into its evidenced half and its unevidenced half
- claim added: a t2 subject reaches multi-thousand impressions with no firsthand signal,
  so firsthand work buys a floor under a small subject rather than reach on a large one;
  and a `reach_ceiling: 2` argued from subject recognizability holds where the same score
  argued from heat did not
- evidence_n: unchanged at 24 — already a t2 exemplar; this ingest adds the prospective
  hold, not a new data point
- contradicted: nothing on this page, but it weakens the standing of `experience_hook` as
  a reach lever, which the ideator and critic still treat as one. The pair is the useful
  part: same rubric, same week, matching scores of 12, 6565 vs 135. Recorded rather than
  used to raise `confidence`, which stays `medium` at 2 of 8 prospective posts.

## [2026-08-21] ingest | retro 2026-08-17 stop-reporting-merge-rate

- corpus: 52 posts, median 506 (was 50 / 439 at last revision)
- trigger: retros/2026-08-17-stop-reporting-how-much-code-your-ai-writes.md (decision: repeat)
- changed:
  - wiki/audience.md — counter_posts +1 (08-17 merge-rate, a t0 subject at 749); fingerprint
    posts_covered 50 -> 52, corpus_median_at_revision 439 -> 506, last_revised -> 2026-08-21;
    context_stats agents 18/310 -> 20/373, other_median 3472 -> 3886; body family-median
    citations refreshed to match; "Heat is not size" gains the t0-overshoot note
- claim added: a t0 vendor metric can clear its band when the wedge reframes a discourse the
  audience is already arguing — recorded as a bounded counter-example, not a scoring rule
- confidence: unchanged at medium — the overshoot (749) is below the page's own
  t0_beat_above: 3000 trigger, so the tier holds; one post does not move the floor
- contradicted: the crispness of t0's 236 ceiling. Not the tier model itself — 749 sits in the
  t0–t1 gap, below every dispute trigger. Recorded as counter-evidence with an explicit warning
  that "my wedge reframes a discourse" must not become a heat-loophole for scoring t0 subjects up.

## [2026-08-25] ingest | retro 2026-08-19 cursor-origin-runs-on-github

- corpus: 53 posts, median 569
- trigger: retros/2026-08-19-cursor-built-a-github-competitor-that-still-runs.md (decision: repeat)
- changed:
  - wiki/audience.md — t2 exemplars +1 (Cursor/GitHub 100064, pre_scored), observed_n 7 -> 8, observed_median 32731 -> 33509; evidence_n 24 -> 25; promotion_review pre_scored_posts_so_far 2 -> 3, pre_scored_held 1 -> 2
  - wiki/audience.md — open question "is there a tier above t2" closed in the body; t2's range now spans 5154-128280 with two six-figure tool subjects
  - wiki/audience.md — rescrape drift corrected: SQLite exemplar 6565 -> 7411, band_overshoot 749 -> 867, corpus_median_at_revision 506 -> 569, cohort_2to7d_median 393 -> 876
- claim added: the 100k band sits inside t2, not above it — the Linus post is t2's ceiling, not a separate tier
- contradicted: none

## [2026-08-25] ingest | retro 2026-08-21 github-failover-plan

- corpus: 53 posts, median 569
- trigger: retros/2026-08-21-your-database-has-a-failover-plan-github-doesnt.md (decision: modify)
- changed:
  - wiki/audience.md — new `sequel_discount` frontmatter block and "The sequel discount" body section (confidence: low, evidence_n 2)
  - wiki/audience.md — counter_posts +1 (08-21 failover, a pre-scored t2 that landed at 1746, below t2's 5154 floor)
  - wiki/audience.md — promotion_review gains pre_scored_near_miss: 1, pre_scored_posts_so_far 3 -> 4; the post cleared t2_miss_below (1000) so it is not a dispute
- claim added: a t2 subject discounts toward t1 reach when it is the account's second post on that subject inside seven days — cap reach_ceiling at 1
- contradicted: none directly, but it qualifies "tier is a property of the subject" — the first modifier this page has ever applied to a tier after assignment. The tier bands are unchanged; only the assignment procedure gains a cap.

## [2026-09-02] ingest | session summary — six lessons absorbed, lane bleed resolved

- corpus: 56 posts, median 439 (news n=38 median 664, experience n=18 median 362)
- trigger: six retro/postmortem lessons carrying `wiki_ingested: false`, swept oldest first
- changed:
  - wiki/audience.md — recomputed news-only, two new failure modes recorded, fingerprint refreshed
  - wiki/experience.md — created to hold the five experience-lane posts that were miscited on [[audience]]
  - wiki/brand/index.md — catalog regenerated, [[experience]] linked from the body
- claim added: see the per-lesson entries that follow this one
- contradicted: [[audience]]'s published tier bands, which were computed over a pool mixing both lanes. Details in the per-lesson entries below.

## [2026-09-02] ingest | postmortem 2026-05-25 paper-benchmark

- corpus: 56 posts, median 439
- trigger: retros/postmortems/2026-05-25-a-new-paper-benchmarks-llm-coding-agents-on-100-back-end-tas.md (decision: block)
- changed:
  - wiki/audience.md — none. The claim ("a paper recap without a reproduction stays inside the t0 band") is already what the t0 tier says, and the post is already a t0 exemplar at 184.
- claim added: none — reinforces an existing claim
- contradicted: none

## [2026-09-02] ingest | postmortem 2026-06-19 vercel-agent-directory

- corpus: 56 posts, median 439
- trigger: retros/postmortems/2026-06-19-vercel-just-bet-your-agent-is-a-directory-not-code-they-open.md (decision: block)
- changed:
  - wiki/audience.md — none structurally. The claim ("a contrarian wedge does not raise a t0 subject's ceiling") restates the tier's own "a sharp wedge does not rescue this"; the post is already a t0 exemplar at 163.
- claim added: none — reinforces an existing claim
- contradicted: none

## [2026-09-02] ingest | postmortem 2026-07-23 openai-benchmark-escape

- corpus: 56 posts, median 439
- trigger: retros/postmortems/2026-07-23-openai-s-benchmark-agents-escaped-and-stole-the-answers-open.md (decision: modify)
- changed:
  - wiki/audience.md — new `frame_reuse_watch` frontmatter block (confidence: anecdote, evidence_n 1) and a paragraph under "The sequel discount"
  - wiki/audience.md — t0 exemplar impressions corrected 121 -> 185 (the postmortem's prior revision carried a pre-rescrape number)
- claim added: reusing a *frame* within seven days may take the same discount as reusing a subject — the 07-23 containment post ran the 07-17 frame six days later, 1380 -> 185
- contradicted: nothing on the page, but it is deliberately kept OUT of `sequel_discount`, whose evidence_n of 2 depends on subject identity. Folding it in would have inflated that count with a different effect.

## [2026-09-02] ingest | postmortem 2026-08-10 auto-mode classifier (second pass)

- corpus: 56 posts, median 439
- trigger: retros/postmortems/2026-08-10-humans-catch-13-6-of-dangerous-agent-commands-a-classifier-c.md (decision: modify)
- changed:
  - wiki/audience.md — "On firsthand signal" section rewritten; `firsthand_flag` frontmatter block added
  - wiki/audience.md — 08-10 impressions corrected 135 -> 163 across the t0 exemplar and the `disputed` entry (rescrape drift)
  - wiki/audience.md — `firsthand_promotion` on t1 changed `true` -> `unevidenced`
- claim added: a firsthand line without a number does not lift a post out of the news-without-firsthand band
- contradicted: **yes.** The page asserted "post-patterns reports the news-without-firsthand flag as discredited at 0.77x across 27 posts" and told skills not to score its absence. Under `--lane news` that flag is a **validated anti-pattern** (n=25, 443 vs 750, 0.59x); the 0.76x/n=29 reading is the unscoped one, which mixes lanes. The lane-scoped number governs a news draft. The page now carries both, twinned in frontmatter.

## [2026-09-02] ingest | postmortem 2026-08-25 windows-paint

- corpus: 56 posts, median 439
- trigger: retros/postmortems/2026-08-25-windows-paint-bakes-a-server-issued-guid-into-your-pixels-xu.md (decision: block)
- changed:
  - wiki/audience.md — t0 exemplars +1 (72), observed_n 12 -> 9 (see the lane-bleed entry below), observed_min 76 -> 72, observed_median 192 -> 185
  - wiki/audience.md — t2 label changed from "every working developer already knows" to "the reader has used or fought with"; new "Famous is not used" section
  - wiki/audience.md — new `sub_band_watch` block (confidence: anecdote) and "Below the band" section
  - wiki/audience.md — `disputed` +1 (resolved), counter_posts +1, promotion_review pre_scored_posts_so_far 4 -> 5, pre_scored_missed 1 -> 2
- claim added: recognizability is not the property that builds a room — having used the artifact is. A pre-scored t2 argued from name recognition (Microsoft Paint) landed at 72, the lowest post in the lane and below every band.
- contradicted: the t2 label's own wording. "Every working developer already knows" was satisfied by this subject and still produced the worst post in the corpus, so the label was the defect, not its application.

## [2026-09-02] ingest | retro 2026-08-25 windows-paint

- corpus: 56 posts, median 439
- trigger: retros/2026-08-25-windows-paint-bakes-a-server-issued-guid-into-your-pixels.md (decision: block)
- changed:
  - wiki/audience.md — none beyond the postmortem entry above; the retro carries the same claim from the draft side and adds no separate evidence
- claim added: none — same claim, already absorbed
- contradicted: none

## [2026-09-02] lint-fix | lane bleed on audience.md, and wiki/experience.md created

- corpus: 56 posts, median 439 (news n=38 median 664, experience n=18 median 362)
- trigger: recomputing t0's `observed_*` for the ingests above was impossible without resolving this first
- changed:
  - wiki/audience.md — five experience-lane posts removed from the tiers: 12-09 Avatune (1271, t1), 08-06 commit log (210, t0), 04-21 memory benchmarks (200, t0), 05-28 posting performance (181, t0), 02-28 company milestone (76, t0)
  - wiki/audience.md — recomputed news-only: t1 n=5 -> 4, median 2192 -> 2637, min 1271 -> 1380; t0 n=12 -> 9, median 192 -> 185, min 76 -> 163 -> 72 (72 arriving from the windows-paint ingest). t2 unchanged at n=8, median 33509.
  - wiki/audience.md — impressions refreshed after rescrape drift: 08-19 100064 -> 100588, 08-13 7411 -> 7416, 08-21 1746 -> 1895, 08-17 867 -> 874, 08-10 135 -> 163
  - wiki/audience.md — t1's "or the owner's own shipped work" clause removed; its only evidence was the Avatune post, now on [[experience]]
  - wiki/audience.md — fingerprint 53/569 -> 56/439, evidence_n 25 -> 21, `lane: news` added
  - wiki/experience.md — created, `status: provisional`, `confidence: low`, evidence_n 5, holding the relocated posts and the lane's own stats
  - wiki/brand/index.md — catalog regenerated, [[experience]] linked
- claim added: the experience lane's whole range (76–1271) sits below the news lane's t1 floor, and its five charted posts split into shipped software (1271) versus reports on the owner's own process (181–210)
- contradicted: **yes.** [[audience]] presented t0's floor as 76 and t1's floor as 1271; both numbers came from experience-lane posts and were never valid for a news draft. The news-only t0 floor before windows-paint was 163. Every band this page has published since it was written was computed over a mixed pool.

## [2026-09-16] ingest | session summary — two retros absorbed

- corpus: 60 posts, median 439 (news n=40 median 664, experience n=20 median 362)
- trigger: two retro lessons carrying `wiki_ingested: false`, swept oldest first
- changed:
  - wiki/audience.md — t0 exemplars +1 (09-08 agents/skill-file), evidence_n 21 -> 22, windows-paint rescrape 72 -> 78, fingerprint refreshed
  - wiki/experience.md — observed +1 (09-09 dashboards, first pillar post), evidence_n 5 -> 6, lane grew 18 -> 20, image-differ rescrape 143 -> 179, fingerprint refreshed
- claim added: see the two per-lesson entries that follow this one
- contradicted: none in either page. Noted for a later pass: the CLI now reports "news without firsthand signal" as discredited where [[audience]] still records it validated.

## [2026-09-16] ingest | retro 2026-09-08 agents-skipped-skill-file

- corpus: 60 posts, median 439
- trigger: retros/2026-09-08-agents-that-skipped-the-skill-file-wrote-better.md (decision: modify)
- changed:
  - wiki/audience.md — t0 exemplars +1 (09-08 agents/skill-file 143, subject "one agent-testing study"), observed_n 9 -> 10, median unchanged at 185, evidence_n 21 -> 22
  - wiki/audience.md — windows-paint impressions 72 -> 78 across t0 exemplar, observed_min, sub_band_watch, disputed, and body (rescrape drift; cleared the standing stale-numeric error)
  - wiki/audience.md — firsthand-doesn't-promote-t0 negative half 2 -> 3 exemplars; the new post carried a process-level firsthand line and still landed inside the band
  - wiki/audience.md — fingerprint 56/439 -> 60/439, "21 of 38" -> "22 of 40" tier-carrying posts
- claim added: a process-level firsthand line does not promote a single-study (t0) subject out of the t0 band
- contradicted: none. Reinforces `firsthand_promotion: unevidenced`. (Noted separately, not acted on here: the CLI now reports "news without firsthand signal" as discredited (0.99x) where this page still records it validated at 0.59x — a later ingest/lint call.)

## [2026-09-16] ingest | retro 2026-09-09 dashboards-eat-your-evening

- corpus: 60 posts, median 439
- trigger: retros/2026-09-09-the-dashboards-will-eat-your-evening-before-the.md (decision: modify)
- changed:
  - wiki/experience.md — observed +1 (09-09 dashboards 138, shape "internal tooling automation", first pillar post replaced-a-hire, first with a receipt), evidence_n 5 -> 6
  - wiki/experience.md — lane grew 18 -> 20: lane_stats n 18->20, p25 210->200, cohort_1to4w_n 6->8, above_400_n 8->9; bottom_five recomputed to 76/96/138/179/181
  - wiki/experience.md — image-differ impressions 143 -> 179 (rescrape drift) across counter_evidence, bottom_five, and body
  - wiki/experience.md — floor claim reframed from "four of five in bottom five" to "process/tooling-report cluster near half the lane median"; receipts open question gains its first data point (receipt necessary, not sufficient); pillars section notes the first replaced-a-hire post
  - wiki/experience.md — fingerprint 56/439 -> 60/439
- claim added: in the experience lane a concrete before/after receipt does not lift a report on the owner's own internal tooling out of the bottom (process-report) cluster
- contradicted: none. Reinforces the process-report floor and begins answering the "Nothing about receipts" open question.

## [2026-09-21] ingest | session summary — two retros and one postmortem absorbed

- corpus: 61 posts, median 435 (news n=41 median 578, experience n=20 median 362)
- trigger: three lessons carrying `wiki_ingested: false`, swept oldest first
- changed:
  - wiki/experience.md — evidence +1 (09-14 Meta-ads, first didnt-teach-me post), evidence_n 6 -> 7, receipts signal n=2 -> 3, fingerprint refreshed
  - wiki/audience.md — t0 exemplars +1 (09-16 coreutils license, third pre-scored t2 miss), evidence_n 22 -> 23, new assignment rule "the noun is not the argument", fingerprint refreshed
  - wiki/index.md — catalog rows refreshed by hand (see the lint-fix entry at the end of the day)
- claim added: see the per-lesson entries that follow this one
- contradicted: none in either page

## [2026-09-21] ingest | retro 2026-09-14 meta-ads-three-sign-ups

- corpus: 61 posts, median 435 (experience lane n=20, median 362)
- trigger: retros/2026-09-14-368-on-meta-ads-three-sign-ups.md (decision: modify)
- changed:
  - wiki/experience.md — evidence_posts +1 (Meta-ads 125), evidence_n 6 -> 7; `bottom_five` entry for this post rescraped 96 -> 125; `cohort_1to4w` 8/226 -> 9/210; new `receipt_bearing_low` twin (n=3) and `pillars_observed` twin (replaced-a-hire n=1, didnt-teach-me n=1); floor observation widened from "process/tooling reports" to "reports on the owner's own operation with no outcome the reader can act on"; open question added on the 09-01 founder post (943) vs this one (125), same app
- claim added: a fully-receipted report of the owner's own experiment that ends before the outcome is known lands in the experience lane's bottom cluster; the receipt does not lift it (reinforces the receipts signal, now n=3, still `low`)
- contradicted: none

## [2026-09-21] ingest | retro 2026-09-16 ubuntu-gpl-coreutils-mit

- corpus: 61 posts, median 435 (news lane n=41, median 578)
- trigger: retros/2026-09-16-ubuntu-just-replaced-its-gpl-coreutils-with-mit.md (decision: modify)
- changed:
  - wiki/audience.md — t0 exemplars +1 (coreutils license 107, pre_scored), observed_n 10 -> 11, observed_median 185 -> 184; 09-08 exemplar rescraped 143 -> 147; evidence_n 22 -> 23; counter_posts +1; `disputed` +1 (third pre-scored t2 miss, resolved by the retro as an assignment error of a third kind); promotion_review 5 scored / 2 missed -> 6 / 3; new section "The noun is not the argument" and a third assignment rule; new `runnable_artifact_watch` twin (n=1, anecdote); context_stats, cohort and firsthand_flag twins recomputed from the 2026-09-21 report (agents n=15 median 750, firsthand ratio 0.67 on n=27, 1-to-4-week cohort 597); two open questions extended
- claim added: a pre-scored t2 subject lands in t0's band when the argument is about a property of the tool the reader has not fought with (its license); the tier test applies to the argued property, not the noun in the hook
- contradicted: none — the bands held; the assignment procedure missed for a third named reason. Confidence stays `medium` with an explicit drop-to-`low` trigger on the next pre-scored t2 miss

## [2026-09-21] ingest | postmortem 2026-09-16 ubuntu-gpl-coreutils-mit

- corpus: 61 posts, median 435 (news lane n=41, median 578)
- trigger: retros/postmortems/2026-09-16-ubuntu-just-replaced-its-gpl-coreutils-with-mit-licensed-rus.md (decision: modify)
- changed: nothing — same post and same claim as the 09-16 retro absorbed in the entry above; the postmortem names the same three failure modes (t0 property on a t2 noun, artifact for a different claim, 41h cohort of n=1). Reinforces, adds no evidence.
- claim added: none (duplicate of the retro's)
- contradicted: none

## [2026-09-21] lint-fix | index catalog refreshed by hand

- corpus: 61 posts, median 435
- trigger: `bun run wiki index` looks for `wiki/brand/index.md`, which this repo does not have (the index is `wiki/index.md`), so the catalog rows were two revisions stale
- changed:
  - wiki/index.md — catalog rows audience n=21/56 posts/2026-09-02 -> n=23/61/2026-09-21, experience n=5 -> n=7, last_revised bumped
- claim added: none
- contradicted: none. Follow-up for the tooling: point the `index` subcommand at `wiki/index.md`.

## [2026-09-25] ingest | retro 2026-09-21 jev-will-not-replace-your-model

- corpus: 63 posts, median 415 (news lane n=43, median 443)
- trigger: retros/2026-09-21-jev-will-not-replace-your-model-it-goes-in-front.md (decision: modify)
- changed:
  - wiki/audience.md — t0 exemplars +1 (Jev 224, pre_scored, scored_at_ideation 0, owner-overridden), observed_n 11 -> 12, observed_median 184 -> 185; evidence_n 23 -> 24; promotion_review 6 scored / 2 held -> 7 / 3, new `pre_scored_t0_held: 1` (the first prospective t0, a hold); "On firsthand signal" gains the override lesson as the fourth negative exemplar; open questions 1 and 3 extended (the 09-16 post now sits under the 150 sub-band threshold and is explicitly not counted); context_stats, cohort and firsthand_flag twins recomputed from the 2026-09-25 report (news n=43 median 443, agents n=16 median 593, 1-to-4-week cohort 443, 2-to-7-day cohort n=2 median 550)
  - wiki/audience.md — rescraped numbers refreshed from posts/: 09-08 147 -> 164, 09-16 107 -> 129 (the `disputed` entry and `runnable_artifact_watch` keep the 41h reading as `first_scrape_*` twins), Cursor 100588 -> 100618, GitHub failover 1895 -> 1905; the sequel_discount ratio is unchanged at 1.9% / 53x
  - wiki/index.md — audience row n=23 / 61 posts / 2026-09-21 -> n=24 / 63 posts / 2026-09-25
- claim added: a firsthand experience line does not lift a pre-scored t0 subject out of t0's band; overriding a 0 for the sake of a firsthand layer buys the top of the band at most
- contradicted: the page's own `firsthand_flag` verdict — `validated` (0.67x on n=27, read 2026-09-21) is now `discredited` (0.93x on n=27, read 2026-09-25; unscoped 1.12x on n=32). The body no longer calls the flag a rule in either direction and both readings stay twinned. The bands themselves held: the first pre-scored t0 landed inside t0's band
