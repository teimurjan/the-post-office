---
kind: postmortem
source_post: posts/2026/09-08-agents-that-skipped-the-skill-file-wrote-better-code-dan-luu.md
topic_family: agents
source_type: article
lane: news
hook_type: claim
reach_tier: t0-vendor-paper-or-self
impressions: 164
first_scrape_impressions: 143
likes: null
comments: null
shares: null
cohort: 1 to 4 weeks
cohort_median_at_run: 446
beat_median: false
likely_failure_modes:
  - one study is a t0 subject; the room was 78 to 236 before the post existed
  - the firsthand line is process-level (a repo of skills exists) with no number and nothing another builder could run
decision: modify
summary: A clean claim hook on Dan Luu's 26-condition skill-file study sits at 164 against a 446 cohort median, inside t0's band, and the "I keep a repo of my own skills" line did not lift it because it measured nothing.
# Same claim as the 72h retro on this post (retros/2026-09-08-agents-that-skipped-the-skill-file-wrote-better.md), absorbed into audience on 2026-09-16; marked ingested.
# Refreshed 2026-10-06: 164 on the 09-25 rescrape, cohort median 446, discredited firsthand flag not cited.
wiki_candidate: A process-level firsthand line does not promote a single-study (t0) subject out of the t0 band.
wiki_pages: [audience]
wiki_ingested: true
generated_at: 2026-10-06T10:45:00.000Z
---

The post reported Dan Luu's result that coding agents which never opened a popular Rust testing skill scored better than those that engaged with it closely, and argued that skills matter less with each new model and harness.

It sits at 164 impressions (143 at the 72-hour retro, 164 on the 2026-09-25 rescrape) against a 446 median for its 1-to-4-week scrape cohort (n=40), 37% of cohort, and inside t0's recorded band (78 to 236) on `wiki/audience.md`. The tier model predicted this: one researcher's study, however well run, has no standing crowd.

The finding was real and the hook honest to it. What the post lacks is an artifact. The firsthand paragraph, "I keep a repo of my own skills, mostly for marketing and for connecting to services", is the same shape the 08-10 post showed: a first-person sentence that asserts exposure and measures nothing. No skill count, no before-and-after on a task, nothing the reader could run. The 2026-09-21 version of this file tied that to the "news without firsthand signal" anti-pattern; that flag is discredited in the current lane-scoped report (0.76x), so the lesson stands without it: a process-level line does not promote a t0 subject, and this is the third post in the corpus to show it. The post ends on a takeaway, so the lane's one validated flag (question endings) does not apply.

The change on the agent-study source type: do not run a single study as a news post unless the owner reran a slice of it. One skill, one task, ten runs with and without. That number in the hook is the first chance to answer the tier page's open question (does a runnable artifact promote a t0) in the positive direction instead of the negative one again.
