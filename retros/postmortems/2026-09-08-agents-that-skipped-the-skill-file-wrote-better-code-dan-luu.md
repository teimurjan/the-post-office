---
kind: postmortem
source_post: posts/2026/09-08-agents-that-skipped-the-skill-file-wrote-better-code-dan-luu.md
topic_family: agents
source_type: article
lane: news
hook_type: claim
reach_tier: t0-vendor-paper-or-self
impressions: 147
likes: null
comments: null
shares: null
cohort: 1 to 4 weeks
cohort_median_at_run: 597
beat_median: false
likely_failure_modes:
  - one study is a t0 subject; the room was 78 to 236 before the post existed
  - the firsthand line is process-level (a repo of skills exists) with no number and nothing another builder could run
decision: modify
summary: A clean claim hook on Dan Luu's 26-condition skill-file study landed at 147 against a 597 cohort median, dead centre of t0's band, and the "I keep a repo of my own skills" line did not lift it because it measured nothing.
# Same claim as the 72h retro on this post (retros/2026-09-08-agents-that-skipped-the-skill-file-wrote-better.md),
# which the curator absorbed into audience on 2026-09-16. Marked ingested to avoid a duplicate ingest.
wiki_candidate: A process-level firsthand line does not promote a single-study (t0) subject out of the t0 band.
wiki_pages: [audience]
wiki_ingested: true
generated_at: 2026-09-21T09:42:49.000Z
---

The post reported Dan Luu's result that coding agents which never opened a popular Rust testing skill scored better than the ones that engaged with it closely, and argued from that that skills matter less with each new model and harness.

It landed at 147 impressions (rescraped from 143 at the retro) against a 597 median for its 1-to-4-week scrape cohort — 25% of cohort — and inside t0's observed band of 78 to 236 on `wiki/audience.md`, near its centre. The tier model predicted this: one researcher's study, however well run, has no standing crowd, and the post is now the tenth t0 exemplar on that page.

The finding was real and the hook was honest to it. What the post lacks is an artifact. It carries a firsthand paragraph — "I keep a repo of my own skills, mostly for marketing and for connecting to services" — which is exactly the shape the 08-10 postmortem flagged: a first-person sentence that asserts exposure and measures nothing. No skill count, no before-and-after on a task, nothing the reader could run. The lane's validated anti-pattern (news without firsthand signal, 0.67x) is about that absence, and a process-level line does not fill it; this is the third post in the corpus to show that.

The concrete change on the agent-study source type: do not run a single study as a news post unless the owner reran some slice of it. One skill, one task, ten runs with and without — that is the number the hook would then have carried, and it is the first time the tier page's open question (does a runnable artifact promote a t0) could have been answered in the positive direction instead of the negative one again.
