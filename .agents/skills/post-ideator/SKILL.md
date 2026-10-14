---
name: post-ideator
description: Find news-lane LinkedIn post angles that can reach technical builders right now, but only when the angle is specific, differentiated, and defensible. Use when the user says "what should I post about", "pitch me ideas", "give me post angles", "find a topic", "ideate a post", or asks for fresh material without supplying a thought. Returns 3 to 5 scored idea briefs, each with a one-line gist and the artifact the owner is expected to have, and writes shortlisted ones into ideas/YYYY-MM-DD.md with lane news. Gated on a subject the owner has personally touched and capped at one news post a week. A thought about the owner's own work is not ideated; the owner writes it and `post-enhancer` edits it as an experience post.
---

# post-ideator

Your job is to find candidate angles for a **news-lane** LinkedIn post — a reaction to an external event in the briefing — and present them as compact briefs. You are not drafting yet, and your job ends when the ledger is written.

The owner's own work (their apps, numbers, replaced hires, lessons) is the **experience lane** and is never ideated from a briefing; the owner types those thoughts themselves. If the user's request is really one of those, say so and stop.

## Office UI sync

This is the **ideator** stage — emit `end` once `ideas/<YYYY-MM-DD>.md` is written, per [office-emit-end](../office-emit-end.md).

## Weekly cap (check first)

The news lane publishes at most one post a week. Before reading the briefing, look for a news post published or drafted in the last seven days:

```sh
since=$(date -v-7d +%Y-%m-%d)
for f in posts/$(date +%Y)/*.md; do d="$(date +%Y)-$(basename "$f" | cut -c1-5)"; [ "$d" \> "$since" ] && ! grep -q '^lane: experience' "$f" && echo "published: $f"; done
for f in drafts/*.md; do d=$(basename "$f" | cut -c1-10); [ "$d" \> "$since" ] && grep -q '^lane: news' "$f" && echo "drafted: $f"; done
```

If anything prints, stop: name the post, say the cap holds until seven days after it, and end without ideating. The only override is the user saying so for this run ("ignore the cap", "anyway", `--force`). The cap is a reach decision, not a style rule: Shield's February 2026 data puts the per-post reach rate at 10% of followers for 9 to 15 posts a month against 16% for 1 to 3, van der Blom's 2026 report has daily posters down 26% per post, and this account's own September at 2.4 posts a week produced its lowest month. The slot the cap frees goes to the owner's own experience post and to commenting on other people's posts, which is where followers now come from.

The selection criterion is **externally relevant + sharp wedge + defensible + touched by the owner**. A hot topic alone is not enough, and neither is a personal story alone. The post needs a concrete detail, a real opinion wedge, a reason a builder who has never heard of the owner would care, and a thing the owner can show.

**Reach model.** Reach = **size of the standing audience** × a sharp differentiated wedge × a front-loaded hook × a non-saturated topic. The first term is the one most often missed. "A stranger builder *would* care if they read it" is not the same as "a crowd is already standing around this topic." A wedge multiplies the room it lands in; it cannot conjure a room. The sharpest take on a topic only a few thousand people will ever touch still lands in a near-empty room.

The standing-audience model lives in `wiki/audience.md`: three tiers keyed on **subject
recognizability**, each with its observed impression band and its exemplar posts. Read that
page rather than reasoning about reach from intuition. Do not restate its contents here — it
gets revised as posts accumulate, and a copy in this file would go stale silently.

If `wiki/` is absent (fresh clone), fall back to the top and bottom bucket sections of
`bun run post-patterns` and say so explicitly in your output, so the user knows the reach
scores are ungrounded that run.

## Inputs to read first

1. **Latest briefing** (required): `ls briefings/*.md | sort | tail -1` and read it. This is the canonical signal for this week.
2. **`bun run post-patterns --lane news`** (required): the mechanical ground truth over the news-lane archive — medians, sample sizes, anti-patterns, cooling streaks. The `--lane news` scope keeps the owner's own launches and build logs (the experience lane, a different room) out of the medians. Two cautions when reading it. The top/bottom bucket sections cover only the quartiles, so a family there can show `n=2`; every bucket prints its sample size and marks thin ones `too few to cite`. Respect that marker. And `topic_family` labels come from a keyword cascade that mislabels, so treat the family axis as bookkeeping, not signal.
2.5. **`wiki/audience.md`** (required when `wiki/` exists): the accumulated judgment layer. `post-patterns` gives you counts; the wiki gives you the conclusions those counts support, each carrying its own `confidence` and `evidence_n`. Never cite a claim whose `confidence` is `anecdote`.
2.7. **The brand bundle** — `bun run --silent --cwd .vendor/teimurjan-llm-wiki wiki view post-writing`. It tells you who is posting — a senior engineer building agents for a living who runs consumer apps with zero employees, nights and weekends — and therefore which news items the owner has an honest entry point into (agent tooling, app-store mechanics, indie economics, the sell side). Use it to ground `experience_hook`; never to invent one.
3. **Drafts dedup** (required): list files in `drafts/` whose `<YYYY-MM-DD>` prefix is within the last 30 days, then read each one's YAML frontmatter. Collect every `source_url` and `pitch_angle`. Drop any briefing item whose URL matches, or whose angle overlaps semantically with a recent draft.
4. **Recent published posts** (dedup): `ls posts/$(date +%Y)/*.md | sort | tail -10` and skim titles plus opening lines. Reject near-duplicates of any published post from the last 7 days.
5. **`bun run top-posts --n 10 --lane news`**: this is the quick scoreboard for what already earned reach in this lane.

There is **no `cv.md`** in this project. Do not look for one.

## The owner's real experience

The published corpus and the dossier (its `assets` page names what the owner runs: the apps, Rslib and the Avatune packages, BlazeDiff, the Speechify translation and video pipelines, Meta ads, the App Store, Claude Code and the agent toolchain) are the only records of what the owner has genuinely touched. Read them to learn the owner's real domains, and never invent a first-hand story.

**Touched-it gate.** Since 2026-10-08 a news idea passes only when the owner has personally run, built, migrated, or been bitten by the subject, and can put an artifact in the post: a repo, a config, a benchmark number, a bill, a screenshot. Score `touched_it` for every candidate:

- `2` — the owner runs or has built with the thing, or it broke under them, per the dossier or the corpus. Name the artifact you expect them to have.
- `1` — the owner uses the category but not this thing (a different runtime, a rival tool). Drop the candidate unless the artifact is a direct comparison the owner can actually produce.
- `0` — no plausible contact. Drop.

Record it in the brief as `touched_it: <0|1|2> — <the artifact you expect the owner to have>` and name the honest entry point in `experience_hook`. The owner confirms or denies the artifact at the pick, and the enhancer asks for it when the owner's draft does not carry it; a `2` you guessed wrong costs one question, a `0` you let through costs a post. The archive's biggest posts carried no firsthand layer, and that shape stopped travelling after LinkedIn's July 2026 slop enforcement, which withholds out-of-network distribution from posts without lived experience; this account's reach was 98% out-of-network. A sharp wedge is still required. It is no longer sufficient.

## External-value gate (pre-filter, runs before scoring)

Before scoring any candidate, ask one question: **would a builder who has never heard of the owner, and does not care about the owner's LinkedIn metrics, find this useful or interesting?**

Reject outright — do not score, do not shortlist — any idea whose primary subject is the owner's own content machine: posting performance, the posting/critic/ideator pipeline, a posting losing or winning streak, follower counts, or any "here's how I run my LinkedIn" meta. This is navel-gazing. It reads as firsthand and scores well on discussion potential, but the audience is technical builders, not the owner's content ops. Three of the twelve `t0` posts in `wiki/audience.md` are exactly this shape, including the owner's posting-streak post at 181 impressions.

`source_type: build_log` is valid **only** when the build is a real technical product or tool other builders could use, run, or learn from (BlazeDiff, Avatune, GEPA-on-Qwen, a benchmark, a migration). A build log about the post pipeline itself fails this gate.

## Scoring rubric

Score each candidate angle from `0` to `2` on every axis:

- `heat`: active attention now
- `specificity`: concrete number, name, or event
- `differentiation`: non-obvious angle, not a recap
- `builder_fit`: relevant to a stranger builder (senior engineer or tooling builder) who does not know the owner — measures *quality* of fit, not size of audience
- `reach_ceiling`: how large is the crowd *already standing around this topic*, independent of how good the wedge is. This is not "would one builder care" (that's `builder_fit`) — it is "how many are watching before the post exists." **Do not score this from intuition.** Look the subject up in `wiki/audience.md`, name the matching `tiers[].id`, name the single exemplar the candidate most resembles, and take that tier's `score`. Put the tier id and the exemplar in the brief's `reach_ceiling` line so the reasoning is auditable.
  - If you think the page assigns the wrong tier for this subject, score it your way **and** record the disagreement in the `reach_ceiling` line as `disputed: <page tier> -> <your tier>, because <reason>`. Never silently override a tier. Disputes get resolved against the post's actual number at retro time, which is how the tier model gets calibrated instead of just getting longer.
- `discussion_potential`: likely to trigger real replies, not passive agreement

Only pitch items scoring `>= 8/12`, with these gates:

- **`reach_ceiling` is a gate.** If `reach_ceiling` is `0`, drop the candidate regardless of the total. A sharp wedge cannot rescue a small room. Every `t0` post in the archive landed between 76 and 236 impressions, several of them with clean craft and a real argument. **`topic_family` carries no reach signal** — never adjust `reach_ceiling` on family grounds. `other` in particular is the classifier's residue bucket, not a family, and it contains two of the archive's top six posts.
- **`builder_fit` is a gate.** If `builder_fit` is `0` or `1`, drop the candidate regardless of the total. A high total carried by `heat` and `discussion_potential` on a topic a stranger builder doesn't care about is the trap that shipped the worst posts in the archive — a company milestone announcement (76) and the owner's own posting-streak post (181).
- **`touched_it` is a gate.** Only a `2` passes (see The owner's real experience). It is not an axis and does not change the 12-point total.
- **Discussion bait doesn't count.** `discussion_potential` earned by personal vulnerability, confession, or meta-drama ("I failed N times", "here's what's wrong with my process") scores `0` on that axis. Count only discussion that comes from an arguable *technical* stake.

Carry the computed total (out of 12) through to the output — print it in the numbered brief and store it in the idea's frontmatter as `score: <n>`. Anything that later reads the ledger uses it rather than recomputing it.

## The gist

Every brief carries a `gist`: **one plain sentence, at most 15 words, saying what the post would be about.** No jargon, no wedge, no scoring — the sentence a friend would use to tell the owner what they would be posting. `Paint stamps a server-issued ID into every image it generates.` is a gist. `A privacy-property reframing of on-device inference` is not. The owner reads the gist first when picking an idea, so if it does not land in one glance the brief is not ready.

Use the briefing for heat:

- **HN items**: prefer high `★score` and high `comments`.
- **Lobsters items**: use lower thresholds, but same logic.
- **Newsletters and blogs**: prefer primary sources over digest-style summaries.
- **Exa fresh news**: treat as a freshness tiebreaker, not the whole case.

## Hard rejection rules

- Reject near-duplicates of any draft from the last 30 days.
- Reject near-duplicates of any published post from the last 7 days.
- Reject same-topic sequel posts unless there is a new artifact: experiment, code, dataset, benchmark, or strong prediction.
- Reject pure news recap angles with no opinion wedge — a flat summary that adds nothing.
- Reject any item the owner has not touched (`touched_it` under 2), however sharp the wedge. The `t2` exemplars in `wiki/audience.md` won without a firsthand layer before July 2026; the tier still sets the ceiling, and the artifact is now what gets the post past the owner's own network. Never set `experience_hook` to none.
- **Cooldown rule.** `## Cooling families` in `bun run post-patterns` is a **trigger for review, not a gate.** The report flags a family when 3 of its last 4 posts fall below its own p25, on at least 6 posts of record — but the family classifier mislabels, so confirm the streak is about a real shared topic before acting on it. When it is real, any new idea in that family needs a firsthand artifact in `experience_hook`: the owner's own benchmark, code, migration story, measured result, or direct usage. When the streak is a classifier artifact, say so in your output and ignore it. An unreviewed streak must not block an idea.

## Recency preference

The briefing is bucketed by recency. When multiple candidates pass the rubric and the rejection rules, prefer fresher ones: **Today > Last 3 days > Earlier this week**.

## Output format

Return 3 to 5 numbered idea briefs. Each item should be compact, but include all of these fields:

```md
1.
gist: <one plain sentence, ≤ 15 words, what the post is about>
angle: ...
score: 9/12
source_title: ...
source_url: ...
briefing_date: YYYY-MM-DD
why_now: ...
opinion_wedge: ...
experience_hook: <the owner's genuine first-hand entry point: what they ran, built, or broke>
touched_it: <0 | 1 | 2> — <the artifact you expect the owner to have>
reach_ceiling: <0 | 1 | 2> — <tier id from wiki/audience.md> · resembles <exemplar subject> · <one line naming the crowd already watching>. Append "disputed: <page tier> -> <your tier>, because ..." only when you disagree with the page.
evidence_points:
- ...
- ...
risk: generic | rehash | too niche | thin evidence
```

Do not draft the posts. Do not propose hashtags.

After presenting the list, write the shortlisted ideas into `ideas/YYYY-MM-DD.md` with YAML frontmatter entries:

```yaml
---
idea_id: 2026-05-21-01
source_url: ...
source_title: ...
briefing_date: 2026-05-21
topic_family: security
source_type: news
lane: news
gist: <one plain sentence, ≤ 15 words>
angle: ...
score: 9
why_now: ...
opinion_wedge: ...
experience_hook: ...
reach_ceiling: 2
reach_tier: t2-universal
touched_it: 2
expected_artifact: <one line: the thing the owner can show>
wiki_rev: 2026-08-17
risk: generic | rehash | too niche | thin evidence
evidence_points:
  - ...
  - ...
status: shortlisted
---
```

`reach_tier` is the tier id from `wiki/audience.md`; `wiki_rev` is that page's
`last_revised`. Together they record which version of the reach model scored this idea, so
a later retro can tell whether a miss came from the model or from the pick. `lane` is always
`news` here — this skill only ideates from the briefing.

## Where this skill ends

At the ledger. You do not draft, and you do not invoke anything else. When the user picks a brief (by number, idea id, or "do #2"), mark that entry `status: approved` in `ideas/YYYY-MM-DD.md` via Edit and print its `idea_id`, `gist`, and `expected_artifact`, so the owner can say at once whether they have it. The owner writes from the brief and `post-enhancer` reads it from the ledger — every field it needs (`angle`, `gist`, `source_url`, `source_title`, `briefing_date`, `topic_family`, `source_type`, `lane`, `format`, `why_now`, `opinion_wedge`, `experience_hook`, `touched_it`, `expected_artifact`, `evidence_points`) is in the frontmatter you wrote, so the file is the handoff.

## If input is ambiguous

If the user said "ideate" with no further direction, pick from the strongest items in the freshest bucket that still clear the defensibility bar. Do not ask a clarifying question for a default ideation run.
