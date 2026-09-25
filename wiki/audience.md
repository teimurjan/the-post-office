---
page: audience
kind: audience
title: Standing-audience tiers for scoring reach_ceiling
status: active
confidence: medium
evidence_n: 23
lane: news
# The page's own predictive use has now failed three times out of six pre-scored posts.
# Kept here, not buried in prose.
counter_posts:
  - posts/2026/08-10-humans-catch-13-6-of-dangerous-agent-commands-a-classifier-c.md
  - posts/2026/08-17-stop-reporting-how-much-code-your-ai-writes-anthropic-let-cl.md
  - posts/2026/08-21-your-database-has-a-failover-plan-github-doesn-t-on-august-1.md
  - posts/2026/08-25-windows-paint-bakes-a-server-issued-guid-into-your-pixels-xu.md
  - posts/2026/09-16-ubuntu-just-replaced-its-gpl-coreutils-with-mit-licensed-rus.md
posts_covered: 61
corpus_median_at_revision: 435
patterns_generated_at: 2026-09-21
last_revised: 2026-09-21
revised_by: wiki-curator
supersedes: []
# Lane-scoped family medians quoted in the body, so they can be rechecked against
# `bun run post-patterns --lane news` rather than drifting silently.
context_stats:
  lane_news_n: 41
  lane_news_median: 578
  agents_n: 15
  agents_median: 750
  agents_min: 107
  agents_max: 128280
  security_n: 11
  security_median: 408
  other_n: 4
  other_median: 3898
  # The scrape-age cohort every prospectively-scored post is compared against.
  cohort_2to7d_n: 1
  cohort_2to7d_median: 876
  cohort_1to4w_n: 36
  cohort_1to4w_median: 597
# The firsthand flag flips sign under lane scoping. Both readings twinned so the
# body's claim is recomputable from either.
firsthand_flag:
  news_lane_n: 27
  news_lane_flagged_median: 443
  news_lane_unflagged_median: 664
  news_lane_ratio: 0.67
  news_lane_verdict: validated
  unscoped_n: 29
  unscoped_ratio: 0.76
  unscoped_verdict: discredited
# Thresholds for promoting this page's confidence. See "Confidence" below.
promotion_review:
  pre_scored_posts_required: 8
  pre_scored_posts_so_far: 6
  pre_scored_held: 2
  pre_scored_missed: 3
  # Pre-scored t2 that landed under t2's observed floor but over t2_miss_below,
  # so it is neither a clean hold nor a dispute. Counted on its own line.
  pre_scored_near_miss: 1
  t2_miss_below: 1000
  t0_beat_above: 3000
tiers:
  - id: t2-universal
    score: 2
    label: A named artifact the reader has used or fought with, not merely one they can name
    observed_n: 8
    observed_median: 33509
    observed_min: 5154
    observed_max: 128280
    exemplars:
      - post: posts/2026/05-29-linus-torvalds-spent-the-week-telling-people-to-stop-sending.md
        impressions: 128280
        subject: Linus Torvalds / the kernel
      - post: posts/2026/07-01-google-s-tabfm-beats-tuned-xgboost-without-training-on-your.md
        impressions: 108960
        subject: XGBoost
      - post: posts/2026/08-19-cursor-built-a-github-competitor-that-still-runs-on-github-o.md
        impressions: 100588
        subject: GitHub
        pre_scored: true
      - post: posts/2026/07-15-your-dependency-bot-should-be-three-days-late-github-just-ch.md
        impressions: 34287
        subject: dependency bots / Dependabot
      - post: posts/2026/07-10-rewrite-it-in-rust-used-to-be-a-joke-this-week-it-shipped-th.md
        impressions: 32731
        subject: Rust
      - post: posts/2026/08-13-a-16-year-old-sqlite-bug-cost-tailscale-19-corrupted-databas.md
        impressions: 7416
        subject: SQLite
        pre_scored: true
      - post: posts/2026/06-01-everyone-read-4b-params-i-read-0-93-gigabytes-bonsai-image-4.md
        impressions: 7360
        subject: model parameter counts
      - post: posts/2026/08-03-typescript-7-is-11x-faster-your-linter-still-can-t-run-it-mi.md
        impressions: 5154
        subject: TypeScript
  - id: t1-subcommunity
    score: 1
    label: A namable sub-community with an active audience
    observed_n: 4
    observed_median: 2637
    observed_min: 1380
    observed_max: 3570
    # The "or the owner's own shipped work" clause was removed on 2026-09-02: its
    # only evidence was an experience-lane post, which now lives on [[experience]].
    firsthand_promotion: unevidenced
    exemplars:
      - post: posts/2026/03-11-solidjs-v2-beta-is-out-and-it-quietly-changes-how-async-ui-w.md
        impressions: 3570
        subject: SolidJS
      - post: posts/2026/06-29-a-job-application-goes-in-nothing-comes-back-the-screener-th.md
        impressions: 3082
        subject: AI hiring screens
      - post: posts/2026/05-17-vercel-labs-dropped-a-new-systems-language-called-zero-the-p.md
        impressions: 2192
        subject: Vercel Zero
      - post: posts/2026/07-17-grok-build-uploaded-a-file-it-refused-to-read-cereblab-ran-g.md
        impressions: 1380
        subject: Grok Build
  - id: t0-vendor-paper-or-self
    score: 0
    label: One vendor's product, one paper, one configuration nobody else is in
    observed_n: 11
    observed_median: 184
    observed_min: 78
    observed_max: 236
    exemplars:
      - post: posts/2026/05-22-google-is-sunsetting-gemini-cli-and-gemini-code-assist-on-ju.md
        impressions: 236
        subject: one vendor's product sunset
      - post: posts/2026/05-20-yesterday-i-posted-about-teampcp-and-637-malicious-npm-versi.md
        impressions: 211
        subject: a sequel to the owner's own prior post
      - post: posts/2026/05-21-alibaba-launched-qwen-3-7-max-yesterday-and-called-it-the-ag.md
        impressions: 200
        subject: one vendor's model release
      - post: posts/2026/04-29-it-only-knows-the-world-up-to-1930-no-internet-no-wwii-no-mo.md
        impressions: 198
        subject: one novelty model
      - post: posts/2026/07-23-openai-s-benchmark-agents-escaped-and-stole-the-answers-open.md
        impressions: 185
        subject: one paper
      - post: posts/2026/05-25-a-new-paper-benchmarks-llm-coding-agents-on-100-back-end-tas.md
        impressions: 184
        subject: one paper
      - post: posts/2026/06-19-vercel-just-bet-your-agent-is-a-directory-not-code-they-open.md
        impressions: 163
        subject: one vendor's agent format
      - post: posts/2026/08-10-humans-catch-13-6-of-dangerous-agent-commands-a-classifier-c.md
        impressions: 163
        subject: one classifier result
        pre_scored: true
      - post: posts/2026/09-08-agents-that-skipped-the-skill-file-wrote-better-code-dan-luu.md
        impressions: 147
        subject: one agent-testing study
      - post: posts/2026/09-16-ubuntu-just-replaced-its-gpl-coreutils-with-mit-licensed-rus.md
        impressions: 107
        subject: the license of coreutils (a t2 tool, a t0 property)
        pre_scored: true
      - post: posts/2026/08-25-windows-paint-bakes-a-server-issued-guid-into-your-pixels-xu.md
        impressions: 78
        subject: one consumer desktop app's internals
        pre_scored: true
# One t0 post landed below the band rather than inside it. n=1, so this is recorded
# and watched, not scored. Twins the numbers in "Below the band".
sub_band_watch:
  confidence: anecdote
  evidence_n: 1
  t0_floor_before: 163
  observed: 78
  post: posts/2026/08-25-windows-paint-bakes-a-server-issued-guid-into-your-pixels-xu.md
  # A second post under this number promotes the hypothesis to a sub-band.
  retest_threshold: 150
  hypothesis: >-
    A t0 subject the audience does not personally operate lands below t0's band, not
    inside it. Windows Paint is universally recognizable and professionally unused.
# A tier is a property of the subject; this is the only thing that modifies one
# after assignment. n=2, so `sequel_discount.confidence` is low on its own terms
# and does not raise the page's. Twins every number in "The sequel discount".
sequel_discount:
  window_days: 7
  cap_reach_ceiling_at: 1
  confidence: low
  evidence_n: 2
  evidence:
    - post: posts/2026/08-21-your-database-has-a-failover-plan-github-doesn-t-on-august-1.md
      subject: GitHub
      subject_tier: 2
      prior_post: posts/2026/08-19-cursor-built-a-github-competitor-that-still-runs-on-github-o.md
      days_after_prior: 2
      prior_impressions: 100588
      published_impressions: 1895
    - post: posts/2026/05-20-yesterday-i-posted-about-teampcp-and-637-malicious-npm-versi.md
      subject: the TeamPCP npm compromise
      subject_tier: 0
      prior_post: null
      days_after_prior: 1
      prior_impressions: null
      published_impressions: 211
# Reusing a *frame* is not the same as reusing a *subject*. Tracked separately so
# sequel_discount's evidence_n stays honest at 2.
frame_reuse_watch:
  confidence: anecdote
  evidence_n: 1
  evidence:
    - post: posts/2026/07-23-openai-s-benchmark-agents-escaped-and-stole-the-answers-open.md
      frame: agent containment failure
      prior_post: posts/2026/07-17-grok-build-uploaded-a-file-it-refused-to-read-cereblab-ran-g.md
      days_after_prior: 6
      prior_impressions: 1380
      published_impressions: 185
# Pre-scored posts whose published number contradicted their score. Retained after
# resolution because promotion_review's counts are derived from them.
disputed:
  - subject: Claude Code auto mode becoming the default
    post: posts/2026/08-10-humans-catch-13-6-of-dangerous-agent-commands-a-classifier-c.md
    scored_at_ideation: 2
    outcome_tier: 0
    published_impressions: 163
    trigger: t2_miss_below
    status: resolved
    resolution: assignment error, not a tier-band error
    resolved_by: 72h retro on the draft slug 2026-08-10-humans-catch-136-of-dangerous-agent-commands
    note: >-
      The brief argued its 2 from how much the topic was being discussed, not from
      how many people already know the subject. Landed inside t0's band. The bands
      held; the procedure for reaching them did not, so "How to assign a tier" gained
      the heat-is-not-size rule rather than the tiers being redefined.
  - subject: Windows Paint's invisible watermark
    post: posts/2026/08-25-windows-paint-bakes-a-server-issued-guid-into-your-pixels-xu.md
    scored_at_ideation: 2
    outcome_tier: 0
    published_impressions: 78
    trigger: t2_miss_below
    status: resolved
    resolution: assignment error, and the first post to land below every band
    resolved_by: 72h retro on the draft slug 2026-08-25-windows-paint-bakes-a-server-issued-guid-into-your-pixels
    note: >-
      The brief argued its 2 from name recognition — everyone can name Microsoft Paint.
      Nobody in this audience uses it. Recognizability is not the test; having used or
      fought with the artifact is. See "Famous is not used".
  - subject: Ubuntu's coreutils license swap (GPL GNU to MIT uutils)
    post: posts/2026/09-16-ubuntu-just-replaced-its-gpl-coreutils-with-mit-licensed-rus.md
    scored_at_ideation: 2
    outcome_tier: 0
    published_impressions: 107
    scrape_age_hours: 41
    trigger: t2_miss_below
    status: resolved
    resolution: assignment error of a third kind — the tier test was applied to the noun, not the argued property
    resolved_by: 72h retro on the draft slug 2026-09-16-ubuntu-just-replaced-its-gpl-coreutils-with-mit
    note: >-
      The brief's case was the right shape — not heat, not recognition, but "every
      developer has typed cp and sort" — and it passes for the tool. The post's argument
      was about the tool's license, which the reader has not fought with. Scraped at 41h,
      so the number is young; it is not young by the 50x the t2 floor would need. The
      classifier reads the post as having no firsthand signal; the body has a runnable
      artifact (blazediff-png). Both readings recorded. See "The noun is not the argument".
# The first news post carrying a runnable firsthand artifact. It was attached to a
# t2-scored subject that landed in t0's band, so it neither promotes nor fails to
# promote a t0 — the open question stays open. n=1, recorded not scored.
runnable_artifact_watch:
  confidence: anecdote
  evidence_n: 1
  post: posts/2026/09-16-ubuntu-just-replaced-its-gpl-coreutils-with-mit-licensed-rus.md
  impressions: 107
  artifact: blazediff-png, a single-thread SIMD reimplementation of libspng
  classifier_has_firsthand_signal: false
  note: the artifact evidences the rewrite claim, not the license claim the post turns on
# t0 subjects that landed above the band's 236 ceiling. Recorded, not scored up:
# each is below the t0_beat_above trigger, so it is counter-evidence to the band's
# crispness, not a redefinition. Twins the impressions number cited in the body.
band_overshoots:
  - subject: Anthropic's self-reported 46% merge rate
    post: posts/2026/08-17-stop-reporting-how-much-code-your-ai-writes-anthropic-let-cl.md
    tier: 0
    published_impressions: 874
    trigger: none — below t0_beat_above 3000
    note: >-
      A t0 vendor metric whose wedge reframed the "AI writes X% of code" argument the
      audience already has. Cleared t0's 236 ceiling but stayed in the t0–t1 gap.
---

# Standing-audience tiers

`reach_ceiling` asks how large the crowd already standing around a topic is, before
the post exists. This page is where that score comes from. Read it, match the
candidate's subject to a tier, name the exemplar it most resembles, and score the
tier's `score`.

**This page is news-lane only.** Its tiers were calibrated on posts reacting to
external events, and every exemplar below is `lane: news`. Experience-lane posts —
the owner's own launches, build logs, and operating numbers — live on [[experience]]
and are never cited here. Mixing them produces a median nobody can recompute.

Catalogued in [[index]]. Revision history in [[log]].

## Why subject, not topic family

`topic_family` does not separate winners from losers in this corpus. In the news lane
`agents` is the largest family (n=15) with a median of 750, and it contains both the
best post (128,280) and the newest miss (107) — a 1199x range inside one label.
`security` (n=11, median 408) contains the #3 post and one of the worst. The
classifier that assigns these labels is a first-match-wins keyword cascade, so
`TypeScript 7 is 11x faster` is filed as `security` because the body says "npm" once.

Subject recognizability does separate them, and the bands do not overlap:

| Tier | n | Median | Range |
|---|---|---|---|
| t2 | 8 | 33509 | 5154 – 128280 |
| t1 | 4 | 2637 | 1380 – 3570 |
| t0 | 11 | 184 | 78 – 236 |

t0's ceiling (236) sits below t1's floor (1380). t1's ceiling (3570) sits below t2's
floor (5154). The gaps are wide enough that the separation survived removing five
experience-lane posts from the pool on 2026-09-02.

## How to assign a tier

The question is not "is this important" or "would a builder find it interesting."
It is: **when you name the subject in five words, has the reader used the thing?**

- **t2** — the subject is a thing the reader has used, fought with, or has an opinion
  about already. Rust, SQLite, TypeScript, Dependabot, the kernel, parameter counts.
  The room is assembled before the post exists.
- **t1** — the subject has a real, namable audience, but not everyone is in it.
  SolidJS. Vercel Zero. A specific vendor's tool that a sub-community actually uses.
- **t0** — one vendor's product nobody else is in, one paper, one benchmark result,
  one configuration. A sharp wedge does not rescue this. Every t0 post in the corpus
  landed between 78 and 236 impressions, several of them with clean craft and a real
  argument.

The three ways this assignment has gone wrong in practice all inflate a t0 into a t2.
They have their own sections below: **heat is not size**, **famous is not used**, and
**the noun is not the argument**.

### On firsthand signal

A firsthand artifact is thought to promote t0 to t1 when the artifact is a real
technical thing another builder could run. **That promotion is still unevidenced** —
there is no post in the corpus where a runnable firsthand artifact lifted a t0
subject out of the band. Only the negative half is evidenced: process-level firsthand
lines do not promote. The 09-08 agents/skill-file post is the third such exemplar —
a t0 study subject carrying a process-level firsthand line ("I keep a repo of my own
skills…") that landed at 147, inside the band.

The first *runnable* artifact in a news post arrived on 09-16 — blazediff-png, a codec
the reader could build and run — and it does not answer the question either way, because
it was attached to a subject scored t2 that landed at 107, inside t0's band
(`runnable_artifact_watch`, n=1). The artifact evidenced "a rewrite is entirely my code";
the post's claim was that a license had been dropped. A receipt for a different claim is
not a receipt. Note the classifier read that post as `hasFirsthandSignal: false`, the
same split the 08-10 post produced; both readings are recorded.

What the lane-scoped corpus does say is the reverse of what this page claimed before
2026-09-02. Under `--lane news`, "news posts without firsthand signal" is a
**validated anti-pattern**: n=27, median 443 against 664 for posts that have it
(0.67x). Unscoped — mixing both lanes — the same flag reads 0.76x across 29 posts and
is reported as discredited. The lane-scoped number is the one that governs a news
draft, and the earlier revision of this page cited the unscoped one.

That said, its absence is not decisive at t2: the SQLite/Tailscale post carried
`experience_hook: none` and published at 7416, the Cursor/GitHub post carried
`experience_hook: none` and published at 100,588. Firsthand work buys a floor under a
small subject. It does not add reach to a subject that already has a room.

### Heat is not size

**How much a topic is being discussed says nothing about how many people already know
the subject.** The two are easy to confuse because the evidence for heat is loud and
quantified — front-page score, comment count, three vendors shipping in one week —
while standing-audience size has no metric attached and has to be judged.

A `2` has to be argued from the subject line, not from the news cycle around it. If the
case for the score cites thread activity, coverage breadth, or how many labs shipped
something adjacent, it is a heat argument and the score is unsupported. "Claude Code auto
mode default" scored a 2 on heat and landed at 163; the tier exemplars would have put it
at 0, next to "one vendor's model release" and "one vendor's agent format".

Heat is a property of the week, tier is a property of the subject. Heat decays in days.
A subject the reader has fought with stays known for years, which is why every t2
exemplar here is a tool, not an event.

### Famous is not used

The second prospective miss failed a different way, and it is the reason t2's label
changed from "a named artifact every working developer already knows" to "a named
artifact the reader has used or fought with."

The 08-25 Windows Paint post was pre-scored `reach_ceiling: 2`, `t2-universal`, and
published at 78 — the lowest post in the news lane. The score was not a heat argument;
the brief's case was name recognition, and on that test it was correct. Every developer
alive can name Microsoft Paint. None of them use it for work.

So recognizability is not the property that builds the room. **Having used the thing
is.** Every t2 exemplar is something the reader has personally fought with — a compiler,
a database, a package bot, a language, a host. A subject can be universally nameable and
still have no standing audience, because nobody has an opinion waiting to be triggered.
When scoring, do not ask "would the reader recognize this name." Ask "has the reader
lost an afternoon to this."

### The noun is not the argument

The third prospective miss passed both tests above and still landed in t0's band. The
09-16 coreutils post was pre-scored `reach_ceiling: 2` on the right kind of argument —
not heat, not recognition, but "every developer has typed cp and sort" — and published
at 107, scraped at 41 hours. The tool is t2. The post's argument was about the tool's
*license*: GPL GNU replaced by MIT uutils, and nobody chose to drop copyleft.

"Has the reader lost an afternoon to this" is true of `cp` and false of copyleft. The
32,731 Rust post argued about rewrites shipping, which is a thing the reader has done or
refused to do; the coreutils post named the same tools and then argued a governance
question a working builder holds an opinion on once a year. The room was measured for
the noun in the first line, and the body was spent in a different one.

So the tier test applies to **the property the post argues**, not the noun in the hook.
A t2 tool lends its room to a behaviour the reader will hit — a flag that changed,
output that diverged, a script that broke. It does not lend it to a property of the
tool the reader has never fought with. The 08-21 GitHub failover post is the boundary
case on the other side: an outage is a property of GitHub the reader has lost an
afternoon to, and it held t1 under the sequel discount.

### Below the band

The Windows Paint post is also the first to land *below* every band: 78, against a
previous news-lane t0 floor of 163. `confidence: anecdote`, `evidence_n: 1` — one post
establishes nothing, and it is recorded in `sub_band_watch` rather than made a rule.

The hypothesis worth testing is that t0 is not one room but two: t0 subjects inside the
audience's working path (a CLI being sunset, an agent format, a coding benchmark) hold
163–236, while a t0 subject outside it has no floor at all. If a second post lands under
150 on a subject the audience does not operate, this becomes a sub-band and t0 gains a
"does the audience touch this category at all" gate. Until then it is one data point.

### The sequel discount

Tier is a property of the subject, with one exception: **the account's own recent coverage
of that same subject.** If a post on subject X published within the last seven days, cap
the next post's `reach_ceiling` at `1`, whatever tier X sits in.

The evidence is a controlled pair, tight because the subject is held constant. On 08-19 the
Cursor/Origin post published at 100,588. On 08-21, two days later, the GitHub-outage failover
post published at 1,895 — 1.9% of it. Both subjects are GitHub. Both were pre-scored
`reach_ceiling: 2`, `t2-universal`. Both scored 11 at ideation, both were labelled
`risk: rehash`, both carried `experience_hook: none`. Every axis the rubric records is
identical; the reach differs 53x. So the separating variable is not on the rubric, and the
only difference between the two briefs is that the second one was second.

The corpus carries one older exemplar: the 05-20 TeamPCP post opened "Yesterday I posted
about TeamPCP" and landed at 211. That one is filed under t0, which is why the discount was
invisible — it read as a t0 subject performing like a t0 subject. The GitHub pair separates
the two effects: a t2 subject took the same discount and landed at 1,895, inside t1's band
(1,380–3,570) rather than t2's (5,154–128,280). The discount lands a tier down, which is why
the rule caps rather than zeroes.

`confidence: low`, `evidence_n: 2`, and two alternatives are not ruled out. The failover post
argues at the reader in the second person and closes on an instruction — but `Your dependency
bot should be three days late` is the same shape at 34,287, so the shape is not the fault.
And 100,588 is an outlier that a single algorithmic pickup could explain, which would make
the ratio meaningless; the failover post performed like an ordinary good post, not like a
failure. What survives both objections is that the second post did not inherit the first
one's room, and nothing in the pipeline expected that: `post-ideator` dedups on *angle*, and
these two angles are genuinely different. The subject was not.

**A reused frame may take a similar discount, on one data point.** The 07-23 OpenAI
benchmark-escape post ran the agent-containment frame six days after the 07-17 Grok Build
post ran it at 1,380, and landed at 185. Different subjects, same shape. This is tracked in
`frame_reuse_watch` at `confidence: anecdote` and deliberately kept out of `sequel_discount`,
whose n=2 depends on subject identity. If a second frame repeat discounts, the seven-day
window generalizes from subject to shape.

**One t0 subject cleared its band (874), and the reason is a trap.** The 08-17
merge-rate post built on Anthropic's self-reported 46% — a textbook t0 vendor metric —
and landed at 874, ~3.7x above t0's 236 ceiling and into the empty gap below t1's floor.
Its wedge reframed the "AI writes X% of our code" argument the audience is already
having, so it rented a room the vendor number does not own alone. This is recorded as a
`counter_post`, not a rule. It sits below the `t0_beat_above: 3000` trigger, so the tier
holds — and "my wedge reframes a discourse people are already having" is **not** a
license to score a t0 subject up, because that reasoning is one short step from the heat
argument this page exists to reject. A t0 subject still scores 0 at ideation; this one
merely overshot its band after the fact, and one post does not move the floor.

**The controlled pair.** Two prospectively-scored posts landed three days apart, and the
rubric could not tell them apart: identical total score of 12, identical `risk` label,
both pre-scored `reach_ceiling: 2`. The SQLite/Tailscale post published at 7416 and the
auto-mode post at 163. A 45x spread with matching scores on every recorded axis.

The subject is the only variable that separates them. SQLite is a thing the reader has
used; "auto mode default" is a setting in one vendor's product. This is the closest the
corpus has to a natural experiment on the tier model, and it is why the model survives a
prospective miss: the miss and the hold came from the same rubric on the same week, and
only the tier assignment predicted the outcome.

**There is no tier above t2.** This page previously left that open at n=1, because the
only six-figure post was Linus Torvalds telling the kernel list to stop sending AI patches
— arguably a cross-cutting moment rather than a known artifact. The Cursor/GitHub post
settles it: 100,588 impressions on an ordinary tool subject, pre-scored `2`, and a hold.
Two of the three largest posts in the corpus are now plain t2 tools, so the 100k band is
t2's top end and not a tier of its own. t2's range is wide (5,154–128,280, a 25x spread)
and the wedge presumably decides where in it a post lands, but that spread lives inside
one tier.

## Confidence and how this page earns more

`confidence: medium`, and the caveat matters: **these tiers were assigned after the
impressions were known.** Clean separation on a post-hoc labelling is a hypothesis, not
a validated model. The pre-scored posts are the actual test, because they get a tier at
ideation time, before publishing.

Raise confidence to `high` only when at least 8 posts have been tier-scored *before*
publishing and the bands still hold. If a pre-scored t2 lands under 1000, or a
pre-scored t0 clears 3000, record it in `disputed` and revise the tier definitions
rather than the post's tier.

`promotion_review` tracks that count: **six scored prospectively, two held, three missed,
one near-miss.** All three misses were pre-scored t2 subjects that were t0, and all three
were assignment errors rather than band errors — each landed inside or below t0's range,
not between bands. A 3-of-6 miss rate on the *procedure* while the *bands* stay intact is
what `medium` describes, and it is also the number to watch: if the next pre-scored t2
misses, the procedure is wrong more often than it is right and `confidence` drops to
`low` whatever the bands say. The three named failure modes above are the fix.

## Disputes

When the ideator or critic believes a subject's tier is wrong, it scores its way and
records the disagreement here rather than silently overriding. Each entry names the
subject, the tier the page assigns, the tier the skill argued for, the reason, and
the source file. `disputed` entries are resolved against the published number once a
retro exists — which is how this page gets calibrated instead of just getting longer.

Three entries, all fired by the page's own `t2_miss_below` trigger rather than by a skill
objecting in advance, and all resolved. Resolved entries stay on the page: they are the
evidence behind `promotion_review.pre_scored_missed`, and deleting them would leave that
count unsupported.

Only 23 of 41 news posts carry a tier: the unambiguous top and bottom. The middle is
unassigned on purpose. Assigning it requires the same judgment call the tiers exist to
make, and doing it in bulk from known outcomes would inflate `evidence_n` without adding
evidence.

## Open questions

Things this page cannot yet answer, which the next retros should settle:

- Does firsthand work promote a t0 subject to t1 at all? Still unshown in the positive
  direction. The negative half has three exemplars: process-level firsthand lines that
  did not promote. The one runnable artifact so far (09-16) was attached to a t2-scored
  subject and evidenced a different claim than the post made, so it tests nothing here.
  `firsthand_promotion` is marked `unevidenced` rather than `true`.
- Does a t2 tool's room transfer to *any* property of the tool, or only to the ones the
  reader has fought with? One miss (the license) and one boundary hold (an outage) say
  only the latter. A coreutils post arguing a behaviour change would settle it.
- Is t0 one room or two? See "Below the band" — one post landed at 78 against a floor of
  163, on a subject the audience does not operate. One more would make it a sub-band.
- Where does a t2 subject with a dull wedge land? Every t2 exemplar here also had a sharp
  take, so the tier's floor is untested.
- Does the seven-day discount apply to a reused *frame* as well as a reused subject? One
  data point in `frame_reuse_watch` says maybe.
