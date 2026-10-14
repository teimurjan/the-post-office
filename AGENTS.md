# LinkedIn Post Collector

A content-generation pipeline for the owner's LinkedIn presence, built on top of a personal post archive.

The repo has two halves: an **archive** (scraped corpus of the owner's past posts) and a **workflow** (briefings, ideas, drafts, critique, retros) that optimizes for reach with technical builders. The workflow runs in two **lanes** with separate cycles, separate analytics, and a shared brand dossier.

## Lanes

Every post, draft, idea, and retro carries `lane: news | experience`.

- **`news`** — the post reacts to an external event. It comes out of the briefing → ideator → the owner writes → enhancer → critic → image path, conducted by `news-post-cycle`.
- **`experience`** — the post is about the owner's own operation: an app they run, a number they measured, a function they built instead of hiring, a lesson the sell side taught them. It comes from a draft the owner wrote and goes enhancer → critic → image, conducted by `experience-post-cycle`. No briefing, no ideator.

The two lanes are **analyzed separately**. `bun run post-patterns --lane <lane>` and `bun run top-posts --lane <lane>` scope every number to one lane; the unscoped report adds a `## Lanes` table so both cohorts stay visible. A news post's reach says nothing about an experience post's, and `wiki/audience.md` (the standing-audience tier model) was calibrated on news posts only. Never compare a post against the other lane. Posts without a `lane` in their frontmatter predate the axis and count as `news`.

## Brand context — the personal wiki (`.vendor/teimurjan-llm-wiki`)

**This repo does not own the brand positioning.** It lives in the personal wiki, vendored here as the `.vendor/teimurjan-llm-wiki/` submodule, and is read with:

```bash
bun run --silent --cwd .vendor/teimurjan-llm-wiki wiki view post-writing
```

That bundle defines the owner (a ten-year senior engineer building agents for a living, running consumer apps with zero employees, nights and weekends, from Bishkek), the **Headcount Zero** framing, its four pillars (`replaced-a-hire`, `numbers-from-a-company-of-one`, `didnt-teach-me`, `nights-and-weekends`), the voice rule (benchmarks and receipts — every claim gets a number), the Kill Test, the LinkedIn platform notes (links in the body cut reach; AI-generic text is suppressed), and the citable numbers. `post-enhancer`, `post-critic`, `post-ideator`, and `experience-post-cycle` read it. It is context for both lanes and the definition of the experience lane.

Never invent experience from it: it names what the owner runs, not stories about any of it. **If the command fails, stop and tell the owner** — a cycle without brand context should not run, and reconstructing positioning from old posts is how a brand drifts.

### Layout

| Path | What it is |
|---|---|
| `.vendor/teimurjan-llm-wiki/` | git submodule of the private brand wiki, tracking its `main`. `.vendor/` is where vendored repos live, named `<owner>-<repo>`. |
| `.vendor/teimurjan-llm-wiki/wiki/brand/index.md` | the wiki's router — page list with each page's kind, freshness and which view reads it |
| `.vendor/teimurjan-llm-wiki/wiki/facts/`, `claims/`, `decisions/` | the pages themselves, e.g. `.vendor/teimurjan-llm-wiki/wiki/facts/proof.md` for the citable numbers |

**There is no brand file at this repo's root any more.** The dossier that used to live at `headcount-zero-positioning.md` is gone; read the bundle command above, or the vendor path directly. Links inside the router are relative to the wiki directory, so resolve them against `.vendor/teimurjan-llm-wiki/wiki/`.

### Keeping it current

```bash
git submodule update --init                            # after cloning
git submodule update --remote .vendor/teimurjan-llm-wiki   # pull brand changes
```

**The submodule is pinned to a commit, so it lags the wiki by design.** Editing a page in the brand wiki changes nothing here until that change is pushed there and pulled with the command above, then committed here. If a number in the bundle looks out of date, run that before assuming the wiki is wrong.

That repo is private and this one is public. A public clone gets a submodule it cannot fetch and two dangling symlinks; that is expected, and no part of the positioning is stored in this repo.

### Which repo owns what

| Subject | Owner | The other repo |
|---|---|---|
| Brand positioning, voice, pillars, the owner's numbers | `.vendor/teimurjan-llm-wiki/` | reads it, never copies it |
| Audience findings, tier model, lane behaviour | **this repo** (`wiki/audience.md`, `wiki/experience.md`) | points at it, never copies it |

The direction does not reverse. Never mirror audience numbers into the personal wiki, and never mirror brand positioning into this one. A number with two owners drifts silently in both.

## Human in the loop

The pipeline is an **edit engine, not a draft engine and not a publish engine**: since 2026-10-08 the owner writes every post and `post-enhancer` enhances it. The enhancer stops twice before it touches a body — the owner picks one of three versions of their own first line, then supplies the one missing specific (news: the artifact they ran, built, or broke, mandatory; experience: the number or the moment) in their own words — and it applies only the cuts and fixes it lists for veto. It never writes a body. `post-image` asks the owner for one to four real screenshots or photos (or `none` for text-only); nothing is generated. Both cycles pause at those points and wait. A skill that cannot reach the owner prints its question and ends; it does not guess.

## Archive — `posts/YYYY/MM-DD-<slug>.md`

One file per original post. Newest dates have the most recent posts.
Read these to answer questions about content, topics, performance.

YAML frontmatter:

```yaml
urn: urn:li:activity:...          # stable LinkedIn ID
url: https://www.linkedin.com/... # canonical post URL
posted_at: 2026-05-13T14:22:00.000Z
impressions: 1234 | null          # null = couldn't be scraped
likes: 42 | null
comments: 7 | null
shares: 3 | null
scraped_at: 2026-05-13T15:00:00.000Z
concept_path: concepts/.../prompt.md  # present when scrape matched a draft's concept
lane: news | experience           # inherited from the matched draft, or stamped by hand
```

Body below the frontmatter is the post text plus a `## Comments` section
with threaded replies.

On scrape, each post is auto-linked to the local draft it was published from:
the scraper matches the post to a same-date draft by text similarity, copies
that draft's `concept_path` and `lane` onto the post, and back-links the post
into the concept's `prompt.md` (`post_url`, `post_path`). Matching needs the
local draft present (`drafts/` is gitignored), so a fresh clone links nothing.
`rescrape` keeps an existing `concept_path` and `lane` when the draft has since
been pruned. A post published without a local draft gets its lane by hand:

```sh
bun run post-lane posts/2026/09-01-<slug>.md experience
```

The archive that predates the lane axis was backfilled once: the owner's own
launches, build logs, experiments, and founder updates are `experience`; every
post about an external event is `news`.

A concept is a real artifact. `post-image` files one to four screenshots or photos
the owner supplies at `images/<date>-<slug>/artifact-N.<ext>` (gitignored, mirrors
`concepts/` 1:1), after checking size, legibility, and leaks, and writes
`concepts/<date>-<slug>/prompt.md` with `kind: artifact`, the file list, what each
shows, and alt text; the draft records `image_kind: artifact | none`. Nothing is
generated: since 2026-10-08 there are no AI illustrations, sketches, carousels, or
flowcharts in the pipeline, and the feed is meant to look like a person's. The
`generate-image` and `select-variant` CLIs under `src/images/` are unused and kept
only until deleted.

## Workflow

News lane, conducted by `news-post-cycle`:

0. Hold if a news post went out in the last 7 days: the lane runs one post a week.
1. Refresh `briefings/` (only if today's is missing).
2. Sweep pending 72-hour retros (both lanes) and ingest their lessons into the wiki.
3. Run `bun run top-posts --lane news` and `bun run post-patterns --lane news`.
4. Produce 3 to 5 scored idea briefs with `post-ideator`, each with a one-line `gist` and an `expected_artifact`, gated on subjects the owner has personally touched; save shortlisted ideas in `ideas/YYYY-MM-DD.md`.
5. The owner picks an idea (the pick shows each idea's gist and expected artifact first) and confirms they have the artifact.
6. The owner writes the post from the brief. `post-enhancer` enhances it (three versions of their first line, the artifact if the draft lacks it, a fact-check against the source, a change list they veto); no artifact, no post.
7. Gate the draft through `post-critic`.
8. `post-image` files the owner's screenshot or photo, or marks the post text-only.

Experience lane, conducted by `experience-post-cycle`:

1. Read the brand bundle: `bun run --silent --cwd .vendor/teimurjan-llm-wiki wiki view post-writing`.
2. Sweep pending retros for experience drafts and ingest them.
3. Run `bun run top-posts --lane experience` and `bun run post-patterns --lane experience`.
4. The owner writes the draft. `post-enhancer` enhances it with the owner in the loop (three versions of their own first line, the one missing specific, a change list they veto line by line), tagging the draft with a `pillar` and `author: owner`. It never writes the body.
5. Gate through `post-critic` (experience rules: `author: owner` or rejected before scoring, receipts required, a ledger with no turn marked down, navel-gazing narrowed to the owner's LinkedIn).
6. `post-image` files the owner's screenshot or photo, or marks the post text-only.

After publishing in either lane, the owner replies to every comment within two hours in their own words (no skill does this), and `post-retro` saves the 72-hour review against the lane's own cohort, folding in the owner's pasted post analytics (in-network share, saves, sends, members reached) when they are available.

Key directories:

1. **`briefings/YYYY-MM-DD.md`** — dated source briefings written by the
   `topics-briefing` skill. Each one merges HN + Lobsters + RSS (last 7
   days only) plus an appended Exa fresh-news section, bucketed into
   Today / Last 3 days / Earlier this week. The newest file is the current-news context. News lane only.
2. **`ideas/YYYY-MM-DD.md`** — the working ledger of shortlisted and approved news-lane ideas. Each entry has YAML frontmatter with `idea_id`, `source_url`, `source_title`, `briefing_date`, `topic_family`, `source_type`, `lane`, `gist`, `angle`, `score`, `why_now`, `opinion_wedge`, `experience_hook`, `reach_ceiling`, `reach_tier`, `touched_it`, `expected_artifact`, `wiki_rev`, `evidence_points`, `risk`, and `status`.
3. **`drafts/YYYY-MM-DD-<slug>.md`** (gitignored) — local working drafts, written by the owner and saved by `post-enhancer`. Every draft carries `lane` and `author: owner` (the critic rejects anything else); experience drafts also carry `pillar`, and the image step sets `image_kind` (`artifact` | `none`). Backward-compatible frontmatter is still accepted, but new drafts should also include `topic_family`, `source_type`, `hook_type`, `why_now`, `opinion_wedge`, `experience_hook`, and `status`. Published drafts later add `published_url`, `published_at`, `impressions_24h`, `impressions_72h`, `likes_72h`, `comments_72h`, and `shares_72h`.
4. **`retros/YYYY-MM-DD-<slug>.md`** — one post-publish review per draft, written 72 hours after publishing. Retros carry `lane`, compare against the lane's scrape-age cohort, answer whether the post beat that cohort, validated the intended discussion angle, matched hook to body, and whether the pattern should be repeated, modified, or blocked. `retros/postmortems/` holds the same shape for the worst performers of one lane, marked `kind: postmortem`.
5. **`wiki/`** — the accumulated judgment layer. See `## Wiki` below.
6. **`tone-samples/`** (gitignored) — pieces the owner wrote by hand, the canonical voice reference. Samples 1 to 4 are rough drafts; sample 5 is the published founder post that opened the experience lane and is that lane's register. `ru-N.md` are pieces the owner wrote in Russian by hand, the register for `post-telegram`: `ru-1.md` is the Meta-ads post translated, `ru-2.md` and `ru-3.md` are Telegram-only follow-ups.
7. **Skills in `.agents/skills/`**. Each skill runs standalone and hands off through files, never by invoking another skill; only the two cycles compose them.
   - `news-post-cycle`, `experience-post-cycle` — the two conductors.
   - `topics-hn`, `topics-lobsters`, `topics-rss`, `topics-briefing` — source fetchers (news lane).
   - `post-ideator` — news lane only. Scores angles 0-2 on six axes (`heat`, `specificity`, `differentiation`, `builder_fit`, `reach_ceiling`, `discussion_potential`) and pitches only those clearing 8/12, each with a plain-language `gist`. `reach_ceiling`, `builder_fit`, and `touched_it` (the owner has personally run, built, or been bitten by the subject; each brief names the `expected_artifact`) are hard gates, and the lane is capped at one post a week. Requires `bun run post-patterns --lane news` plus `wiki/audience.md`, reads the dossier for what the owner actually runs, and ends at the ledger.
   - `post-enhancer` — enhances a post the owner wrote, in either lane, never writing the body: three versions of their first line, the one missing specific (the artifact for news, the number or the moment for experience), a fact-check against the source for news, and a change list the owner vetoes line by line. Grounds in the dossier, `tone-samples/`, the lane-scoped pattern report, and recent posts of the same lane. Moves body links to a `Comment link:` line.
   - `post-critic` — reads the lane first, then scores 0-2 across seven categories (hook strength, specificity, novelty, readability, builder relevance, discussion potential, artifact fit) against the lane's report. Approves only at `>= 10/14` with no zero-scored category. Seven hard-zero rules: the fifth zeros `specificity` on an experience post with no number, the sixth zeros `readability` on a slop tell or a comment ask, the seventh zeros `builder relevance` on a news post with no touched-it artifact. An experience draft not written by the owner is rejected before scoring.
   - `post-image` — native only: one to four real screenshots or photos the owner supplies, checked for leaks and filed with alt text; `none` for text-only. Nothing is generated.
   - `post-retro` — saves the 72-hour review. Requires only `impressions`, read from the published post, and folds in the owner's pasted post analytics (in-network share, saves, sends, members reached) plus the draft's `author` and `image_kind`; compares against the lane's scrape-age cohort and emits the lesson as a `wiki_candidate` claim routed to `audience` (news) or `experience` (experience).
   - `posts-postmortem` — the same analysis for the bottom performers of one lane (`--lane`, default `news`).
   - `wiki-curator` — owns `wiki/`. Absorbs `wiki_candidate` lessons into pages (`ingest`), keeps the lanes apart (`audience` for news, `experience` for the experience lane, created on first ingest), answers questions (`query`), and health-checks (`lint`). Nothing else writes to `wiki/`.
   - `post-comments` — drafts replies to comments on a published post.
   - `post-substack`, `post-telegram` — take one finished draft (or a published post) to another channel, per the brand wiki's `channels` decision. `post-substack` writes a Substack Note: tweet-length, the hook and one number, link last, concept image attached. `post-telegram` translates the post into Russian in the owner's own register, read from `tone-samples/ru-*.md`; nothing is added, and Russian typography applies (decimal comma, `42к`, тире only when unavoidable). Both save to `channels/<channel>/<date>-<slug>.md` (gitignored, not pruned by `cleanup`) and never touch `drafts/` or `posts/`.

### Housekeeping

```sh
bun run cleanup              # prune cycle working files, keep the last 3 days
bun run cleanup --dry-run    # print the plan, delete nothing
bun run cleanup --days 7     # widen the retention window
```

Prunes dated entries in `ideas/`, `drafts/`, and `images/` only. `briefings/`,
`posts/`, `concepts/`, `retros/`, and `wiki/` are durable and never touched, and
a draft whose published post has no retro yet is held back so the retro sweep at
the top of either cycle can still read it.

## Analytics

```sh
bun run top-posts                       # markdown report, whole archive
bun run top-posts --lane experience     # one lane
bun run post-patterns --lane news       # classification and anti-pattern report, one lane
bun run post-patterns --json            # programmatic, includes laneStats and postIndex
bun run wiki lint                       # check every wiki page against the corpus
bun run wiki index                      # regenerate the wiki/brand/index.md catalog
bun run post-lane <post> <lane>         # stamp a lane on a post published without a draft
```

`top-posts` is the simple scoreboard. `post-patterns` is the working-context report and adds:

- a `## Lanes` table (n, median, p25, p75, range per lane over the whole archive), and a `lane` field on the report when scoped
- deterministic classification of each post into `topic_family`, `source_type`, `hook_type`, `contains_numbers`, `has_firsthand_signal`, and `ending_type`
- full-corpus per-family distribution (`n`, median, p25, p75, range)
- grouped top and bottom performers, each bucket carrying its sample size
- impressions grouped by scrape-age cohort
- top-quartile median length and hook-length range
- repeated anti-patterns from the bottom quartile
- retro and postmortem conclusions when `retros/` exists, filtered to the lane when scoped

### Reading the numbers honestly

- **Scope to the lane you are judging.** The experience cohort is small and its `too few to cite` marker will fire; say so rather than citing a median. The news cohort is not a baseline for an experience post, and vice versa.
- **Respect the `too few to cite` marker.** The top and bottom bucket sections cover only the quartiles, so a family there can be `n=2`. A 2-post median is an anecdote.
- **Cite a fault only from `## Validated anti-patterns`.** Each candidate flag is tested against the whole (lane-scoped) corpus and only counts when flagged posts median below 0.7x the unflagged ones on at least 4 posts. The `## Tested and discredited` list is the flags that failed that test, kept visible so they are not reintroduced.
- **`topic_family` is bookkeeping, not signal.** `detectTopicFamily` is a first-match-wins keyword cascade over the whole body, so `TypeScript 7 is 11x faster` is filed as `security` because the body mentions npm once, and `other` is the residue bucket rather than a family. Never derive a reach judgment from a family label. Use `wiki/audience.md` (news) or the dossier's pillars (experience).
- **Engagement rankings are unreliable.** Impressions are present on every post, but likes, comments, and shares are missing on most, and missing values count as zero. The `likes + 3·comments + 5·shares` leaderboard partly ranks which posts scraped cleanly. Prefer impressions.
- **Compare a fresh post against its own cohort.** Impressions are frozen at first scrape and never refreshed, and scrape age varies widely, so the pooled median mixes 72-hour numbers with mature ones.

## Wiki

`wiki/` is the accumulated judgment layer, written by the model and read by the skills.
**The CLI owns counts, the wiki owns causes.** `post-patterns` recomputes arithmetic from
`posts/` on every run and is never stale; the wiki holds the conclusions those counts
support, each page carrying the corpus fingerprint it was written against
(`posts_covered`, `corpus_median_at_revision`, `last_revised`) so drift is detectable.

Rules that hold across every page:

- Evidence is cited as explicit post paths, never as a family query. That makes each claim recomputable and immune to the classifier.
- `confidence` is bounded by `evidence_n`: `high` needs 8+, `medium` 4+, `low` 2+, a single post is `anecdote`. Never cite an `anecdote`.
- Every numeric claim in a page body needs a frontmatter twin, so it can be rechecked rather than trusted.
- `wiki/log.md` is append-only, one entry per change, each stating what it contradicted.
- Pages cross-link with `[[slug]]` wikilinks. A page nothing links to is flagged — the connections carry as much of the knowledge as the pages.
- **Lanes stay apart.** `audience` holds news-lane evidence only. Experience-lane lessons go to `experience`, a sibling page the curator creates on the first experience ingest. A page that mixes them has a number nobody can recompute.
- **Only `wiki-curator` writes to `wiki/`.** `post-retro` and `posts-postmortem` emit a `wiki_candidate` claim with `wiki_ingested: false`; the curator absorbs them one at a time. Writing from the retro skills directly would race the postmortem sweep, which produces several files per run.

`bun run wiki lint` enforces all of this and exits non-zero on any error. Run it after
touching anything under `wiki/`. Beyond the schema checks it reports unabsorbed retro
lessons and lessons routed at pages that do not exist yet — both are prompts to run the
curator. Current pages: `audience.md` (the news-lane standing-audience tier model that grounds
`reach_ceiling`), plus `index.md` and `log.md`.

## Where NOT to read

- `.auth/` — browser profile + cookies. Never read, never quote. Gitignored.
- `node_modules/` — dependencies.
- `src/` — scraper + CLI implementation; only relevant if the user asks
  about the tooling itself, not the post corpus.

## Typical questions this repo can answer

- "Which of my posts got the most impressions?" → `bun run top-posts`.
- "How do my founder posts do?" → `bun run top-posts --lane experience`.
- "What topics get the most engagement?" → rank by impressions; the engagement formula is unusable at current metric coverage (see Analytics). For *why* something reached, read `wiki/audience.md`.
- "How has my post frequency changed?" → count files per month under `posts/`.
- "What did I post about in May 2026?" → list `posts/2026/05-*.md`.
- "What should I post about this week?" → `news-post-cycle`, or `post-ideator` on its own.
- "Edit my post" / "Turn this draft into a post" → `experience-post-cycle`, or `post-enhancer` on its own.
- "Should this draft be published?" → invoke `post-critic`.
- "What patterns should I stop repeating?" → run `bun run post-patterns --lane <lane>`.

## Caveats

- Archive analytics are frozen at first-scrape time. The scraper only adds new posts; it never refreshes old ones, so posts scraped at different ages carry numbers from different points on the growth curve. `bun run rescrape` refreshes the most recent N in place.
- Posts with unparseable numbers have `null` for that field — exclude them from averages.
- Only original posts are collected. Reshares, comments, and articles are out of scope.
- There is no `cv.md` in this project. The dossier names what the owner runs; it is not a source of stories. Do not invent personal experience for the owner — the enhancer asks them.
- `posts/` is scrape output. The only fields ever added to it after the fact are `concept_path` and `lane`. Draft lifecycle data belongs in `ideas/`, `drafts/`, and `retros/`; durable conclusions belong in `wiki/`.
- `drafts/`, `ideas/`, `images/`, `channels/`, and `tone-samples/` are gitignored working files; `wiki/`, `retros/`, `posts/`, `briefings/`, and `concepts/` are tracked, as is the `.vendor/` submodule pointer.
