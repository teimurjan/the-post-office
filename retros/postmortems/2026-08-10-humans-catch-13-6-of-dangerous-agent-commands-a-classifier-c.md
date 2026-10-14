---
kind: postmortem
source_post: posts/2026/08-10-humans-catch-13-6-of-dangerous-agent-commands-a-classifier-c.md
topic_family: security
source_type: news
lane: news
hook_type: result
reach_tier: t0-vendor-paper-or-self
scored_at_ideation: 2
impressions: 163
likes: null
comments: null
shares: null
cohort: 1 to 4 weeks
cohort_median_at_run: 446
beat_median: false
likely_failure_modes:
  - reach_ceiling scored from topical heat rather than standing-audience size (one vendor's self-reported classifier number)
  - the one firsthand line asserts exposure and measures nothing; no subagent count, no blocked command, no configured boundary
decision: modify
summary: A vendor's own classifier benchmark was pre-scored t2 on how loudly the topic was being argued, sits at 163 against a 446 cohort median inside t0's band, and is the case that put the heat-is-not-size rule into the tier model.
# Claim already absorbed into audience ("On firsthand signal": process-level firsthand lines do not promote; the disputed entry was resolved by the 72h retro); marked ingested.
# Refreshed 2026-10-06 against cohort median 446 and rephrased off the discredited "news without firsthand signal" flag.
wiki_candidate: A firsthand line without a number does not lift a t0 subject out of t0's band.
wiki_pages: [audience]
wiki_ingested: true
generated_at: 2026-10-06T10:45:00.000Z
---

The post paired Anthropic's own 13.6%-versus-89% classifier result with LeadDev's 81%/7% agent-write-access split and argued that the permission decision is made once, long before any classifier inspects a command.

It sits at 163 impressions against a 446 median for its 1-to-4-week scrape cohort (n=40), 37% of cohort, inside t0's recorded band (78 to 236) on `wiki/audience.md`, where it is recorded under `disputed` as the first pre-scored miss.

The primary failure is the one the tier model already absorbed: the brief scored `reach_ceiling: 2` because Claude Code auto mode was being argued about everywhere that week, not because a large crowd already stood around the subject. The subject was one vendor's self-reported classifier number, a textbook t0. That is settled, and it produced the heat-is-not-size rule.

The second observation is about the firsthand line, and the 2026-09-21 version of this file framed it through a flag that no longer holds. "News posts without firsthand signal" is discredited in the current lane-scoped report (n=28, median 439 against 578, 0.76x), so the absence of firsthand signal is not a cause here. What the text still shows is narrower. "I run this pipeline on Claude Code subagents. That default just changed under me too" asserts exposure and measures nothing: no count of subagents, no blocked command, no boundary the owner had configured. The 77x security post that broke the family's losing streak carried a prescriptive hook plus one concrete firsthand number. A first-person sentence is not the variable; a number the owner produced is. The hook is honest to the body, and the post ends on a takeaway, so the lane's one validated anti-pattern (question endings) does not apply.

Modify rather than block: agent-permission boundaries remain a live builder subject, but the entry price is the owner's own configuration, measured. Run the classifier against this repo's own agent boundary, report how many of its tool calls would have been stopped, and lead with that number.
