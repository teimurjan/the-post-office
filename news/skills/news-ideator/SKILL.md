---
name: news-ideator
description: Refresh today's briefing if it is missing, then find news post angles that can reach technical builders right now, but only when the angle is specific, differentiated, defensible, and on a subject the owner has personally touched. Use when the user says "what should I post about", "pitch me ideas", "give me post angles", "find a topic", "ideate a post", "news cycle", or asks for fresh material about current events. Returns 3 to 5 scored idea briefs, each with a one-line gist and the artifact the owner is expected to have, and writes shortlisted ones into ideas/YYYY-MM-DD.md. Capped at one news post a week. A thought about the owner's own work is not news; it belongs to the build-in-public cycles.
---

# news-ideator

Find candidate angles for a **news post**, a reaction to an external event in the briefing, and present them as compact briefs. You do not draft, and your job ends when the ledger is written.

This folder is self-contained. Every path below is relative to `news/`; run every command from there. It needs only the briefing (this folder), the ledger (this folder), and the owner's brand bundle from the personal wiki.

The owner's own work (their apps, numbers, replaced hires, lessons) is not news and is never ideated from a briefing; the owner writes those posts themselves. If the request is really one of those, say so and stop.

## Weekly cap (check first)

At most one news post a week. The ledger is the record: look for an entry approved or drafted in the last seven days.

```sh
since=$(date -v-7d +%Y-%m-%d)
for f in ideas/*.md; do d=$(basename "$f" .md); [ "$d" \> "$since" ] && grep -lE '^status: (approved|drafted)' "$f"; done
```

If anything prints, stop: name the idea, say the cap holds until seven days after it, and end without ideating or fetching a briefing. The only override is the user saying so for this run ("ignore the cap", "anyway", `--force`). The cap is a reach decision: Shield's February 2026 data puts the per-post reach rate at 10% of followers for 9 to 15 posts a month against 16% for 1 to 3, and van der Blom's 2026 report has daily posters down 26% per post.

## Briefing (refresh if missing)

```sh
test -f "briefings/$(date +%Y-%m-%d).md" && echo present || echo missing
```

On `missing`, invoke `topics-briefing` and wait for it to write today's file. Only a same-day file counts. If the briefing fails, report it and stop; every angle depends on it.

## Inputs to read first

1. **Today's briefing** (required): `briefings/$(date +%Y-%m-%d).md`.
2. **The brand bundle** (required): the personal wiki's `post-writing` view (`bun run --silent wiki view post-writing` inside the `teimurjan-llm-wiki` checkout). It says who is posting (a senior engineer building agents for a living who runs consumer apps with zero employees, nights and weekends) and its `assets` page names what the owner actually runs. Use it to find honest entry points; never to invent one. **If it cannot be read, stop and say so.**
3. **The ledger, last 30 days** (dedup): every `ideas/*.md` dated within 30 days. Drop any briefing item whose `source_url` matches an entry, or whose angle overlaps one semantically.

## Selection criterion

**Externally relevant + sharp wedge + defensible + touched by the owner.** A hot topic alone is not enough, and neither is a personal story alone. The post needs a concrete detail, a real opinion wedge, a reason a builder who has never heard of the owner would care, and a thing the owner can show.

**Reach model.** Reach = **size of the standing audience** × a sharp wedge × a front-loaded hook. The first term is the one most often missed: a wedge multiplies the room it lands in; it cannot conjure a room.

## Touched-it gate

A news idea passes only when the owner has personally run, built, migrated, or been bitten by the subject, and can put an artifact in the post: a repo, a config, a benchmark number, a bill, a screenshot. Score `touched_it`:

- `2` — the owner runs or has built with the thing, or it broke under them, per the brand bundle's `assets`. Name the artifact you expect.
- `1` — the owner uses the category but not this thing. Drop it unless the artifact is a direct comparison the owner can actually produce.
- `0` — no plausible contact. Drop.

Only a `2` passes. It is a gate, not an axis. A `2` you guessed wrong costs one question at the pick; a `0` let through costs a post. Platforms now withhold distribution from posts without lived experience (LinkedIn's July 2026 slop enforcement), so a sharp wedge is still required and no longer sufficient.

## External-value gate

Before scoring, ask: **would a builder who has never heard of the owner find this useful or interesting?** Reject outright any idea whose subject is the owner's own content machine: posting performance, this pipeline, streaks, follower counts. A `build_log` source is valid only when the build is a real tool other builders could use, run, or learn from.

## Scoring rubric

Score each candidate `0` to `2` on every axis:

- `heat`: active attention now.
- `specificity`: a concrete number, name, or event.
- `differentiation`: a non-obvious angle, not a recap.
- `builder_fit`: relevant to a stranger builder (senior engineer, tooling builder). Quality of fit, not size of audience.
- `reach_ceiling`: how large the crowd **already standing around this subject** is, before the post exists. Score it from the tiers below, name the tier and the exemplar the candidate most resembles.
- `discussion_potential`: likely to draw real replies from an arguable *technical* stake. Discussion earned by confession or meta-drama scores `0`.

### Reach tiers

Calibrated on the owner's LinkedIn news posts through 2026-10 (impressions per post). The bands are directional, not a forecast.

| Tier | Score | Subject | Exemplars | Observed band |
|---|---|---|---|---|
| `t2-universal` | 2 | A named artifact the reader has used or fought with, not merely one they can name | the kernel, GitHub, Rust, SQLite, TypeScript, Dependabot | 5k to 128k |
| `t1-subcommunity` | 1 | A namable sub-community with an active audience | SolidJS, AI hiring screens, Vercel Zero, Grok Build | 1.4k to 3.6k |
| `t0-vendor-paper-or-self` | 0 | One vendor's product, one paper, one configuration nobody else is in, or a sequel to the owner's own post | a vendor's model release, a product sunset, one paper | 78 to 451 |

A big name carrying a small subject lands in the small subject's tier: DHH and Rails on one company's pencils-down policy was scored `2` and landed in `t1`. If you think a candidate sits between tiers, score the lower one and say why.

### Gates

Pitch only items scoring `>= 8/12`, and drop any candidate with:

- `reach_ceiling` of `0`. A sharp wedge cannot rescue a small room; every `t0` post landed at 451 impressions or under, several with clean craft.
- `builder_fit` of `0` or `1`. A total carried by `heat` and `discussion_potential` on a subject a stranger builder does not care about is the trap.
- `touched_it` under `2`.

## The gist

Every brief carries a `gist`: **one plain sentence, at most 15 words, saying what the post would be about.** No jargon, no wedge. `Paint stamps a server-issued ID into every image it generates.` is a gist. `A privacy-property reframing of on-device inference` is not. The owner reads it first when picking.

Heat from the briefing: HN prefers high `★score` and `comments`; Lobsters the same at lower thresholds; newsletters prefer primary sources over digests; Exa is a freshness tiebreaker. Prefer **Today > Last 3 days > Earlier this week** among candidates that pass.

## Hard rejection rules

- Near-duplicates of any ledger entry from the last 30 days.
- Same-subject sequels without a new artifact (experiment, code, dataset, benchmark).
- Pure recap with no opinion wedge.
- Recap or roundup blogs recirculating an event older than the briefing window: weight the freshness of the event, not of the coverage.
- Anything with `touched_it` under `2`. Never set `experience_hook` to none.

## Output format

Return 3 to 5 numbered briefs:

```md
1.
gist: <one plain sentence, ≤ 15 words>
angle: ...
score: 9/12
source_title: ...
source_url: ...
briefing_date: YYYY-MM-DD
why_now: ...
opinion_wedge: ...
experience_hook: <the owner's honest entry point: what they ran, built, or broke>
touched_it: 2 — <the artifact you expect the owner to have>
reach_ceiling: <0 | 1 | 2> — <tier id> · resembles <exemplar> · <the crowd already watching>
evidence_points:
- ...
risk: generic | rehash | too niche | thin evidence
```

No drafts, no hashtags. Then write the shortlist into `ideas/YYYY-MM-DD.md`, one frontmatter block per idea:

```yaml
---
idea_id: 2026-11-02-01
source_url: ...
source_title: ...
briefing_date: 2026-11-02
source_type: news | article | paper | release | build_log
gist: ...
angle: ...
score: 9
why_now: ...
opinion_wedge: ...
experience_hook: ...
touched_it: 2
expected_artifact: <one line: the thing the owner can show>
reach_ceiling: 2
reach_tier: t2-universal
risk: ...
evidence_points:
  - ...
status: shortlisted
---
```

## Where this skill ends

At the ledger. When the owner picks a brief (by number, idea id, or "do #2"), mark it `status: approved` with Edit and print its `idea_id`, `gist`, and `expected_artifact`, so the owner can say at once whether they have it. If they do not, set it back to `shortlisted`. Drafting, editing, and publishing belong to whatever poster reads the ledger; every field it needs is in the frontmatter.

## If input is ambiguous

On a bare "ideate", pick from the strongest items in the freshest bucket that clear the bar. Do not ask a clarifying question for a default run.
