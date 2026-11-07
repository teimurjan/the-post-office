A content pipeline for two platforms, LinkedIn and X, built on top of a personal LinkedIn
post archive.

Two **directions**, written separately and sharing nothing but the voice:

- **LinkedIn** — posts about the owner's own operation (apps, numbers, functions built
  instead of hired, lessons from the sell side). A **loop** takes a draft the owner wrote
  through an edit pass, a critic, and a real screenshot, and a **wiki** accumulates what
  the archive has taught, so the loop stops rediscovering it on every run.
- **X** — build in public: the week's work while it is still moving.

News posts (reactions to external events) left on 2026-11-02. The fetchers, briefings,
and the ideator live in [`news/`](news/), a self-contained folder meant to run from a
personal agent. The brand wiki in `.vendor/teimurjan-llm-wiki/` defines the positioning of
both platforms, read with `bun run --silent --cwd .vendor/teimurjan-llm-wiki wiki view post-writing`.
`.vendor/teimurjan-agent-config/` holds the owner's voice (`MY-VOICE.md`) and facts (`MY-BRAIN.md`).

https://github.com/user-attachments/assets/f478ba31-8091-411e-b672-80c22c7735ee

## Setup

```sh
bun install
git submodule update --init      # brand wiki and agent config (private repos, .vendor/)
```

CloakBrowser (stealth Chromium under Playwright) downloads on first scrape (~200 MB, cached).

## The wiki layer

Modeled on [Karpathy's LLM wiki pattern](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f):
instead of re-deriving conclusions from raw documents at query time, the model
incrementally builds and maintains a persistent, interlinked set of markdown pages that
sit between the sources and the consumer. Three layers:

| Layer | Contents | Who writes it |
|---|---|---|
| Raw sources | `posts/`, `concepts/` | scraper, immutable afterward |
| Derived counts | `bun run post-patterns --lane <lane>`, `bun run top-posts --lane <lane>` | recomputed every run, never stored |
| The wiki | `wiki/` | `wiki-curator` skill, nothing else |
| The brand context | `.vendor/teimurjan-llm-wiki/` (`wiki view post-writing`) | a pinned submodule; read here, never copied |
| The schema | `AGENTS.md` (`CLAUDE.md` symlinks to it) | co-evolved by hand |

**The CLI owns counts, the wiki owns causes.** `post-patterns` recomputes arithmetic from
`posts/` and is never stale. `wiki/` holds the conclusions those counts support, each page
carrying the corpus fingerprint it was written against (`posts_covered`,
`corpus_median_at_revision`, `last_revised`) so drift is detectable by subtraction rather
than by memory.

Rules, all enforced by `bun run wiki lint`:

- Evidence is cited as explicit post paths, never as a query. A query-based claim inherits
  the classifier's errors and cannot be recomputed.
- `confidence` is bounded by `evidence_n`: `high` needs 8+, `medium` 4+, `low` 2+, a single
  post is `anecdote`. An `anecdote` may not be cited.
- Every number in a page body needs a frontmatter twin, or it drifts unnoticed.
- Pages cross-link with `[[slug]]`. A page nothing links to is flagged.
- Lanes stay apart: `audience` holds the old news posts' evidence and is closed;
  `experience` holds every new lesson. A page that mixes them has a
  number nobody can recompute.
- `wiki/log.md` is append-only, `## [YYYY-MM-DD] <op> | <title>`, and every entry states
  what it contradicted even when the answer is `none`.

```sh
bun run wiki lint     # check every page against the corpus, non-zero exit on error
bun run wiki index    # regenerate the catalog table in wiki/brand/index.md
```

Lessons reach the wiki through a queue, not a direct write. `linkedin-post-retro` and
`linkedin-posts-postmortem` emit `wiki_candidate` with `wiki_ingested: false`; `wiki-curator`
absorbs them one at a time, reconciles each against the existing pages, and appends to the
log. Writing from the retro skills would race the postmortem sweep, which produces several
files per run.

Current pages: `experience.md` (LinkedIn), `audience.md` (the news posts' standing-audience
tier model, closed), plus `index.md` and `log.md`.

## Reading the numbers honestly

Three things about this corpus that cost real posts to learn.

**An anti-pattern has to earn the name.** Counting traits inside the bottom quartile
reports any trait that shows up twice, including traits every post shares. Each candidate
flag is now tested against the whole corpus and only counts when flagged posts median
below 0.7x the unflagged ones on at least 4 posts. On 50 posts (median 439 impressions),
three of the four previously-reported anti-patterns do not survive:

```
## Validated anti-patterns
- question endings                       n=4,  median 297 vs 506 (0.59x)

## Tested and discredited
- news posts without firsthand signal    n=25, median 435 vs 569 (0.76x)
- announcement hooks that read like recaps  n=7, median 578 vs 435 (1.33x)
- posts with no concrete numbers        n=12, median 618 vs 425 (1.45x)
```

Two of them are inverted: posts carrying the "fault" do better. The discredited list stays
printed so nothing reintroduces it as a rule.

**`topic_family` is bookkeeping, not signal.** `detectTopicFamily` is a first-match-wins
keyword cascade over the whole body, so a post about the TypeScript 7 compiler is filed as
`security` because the body says "npm" once. `agents` is the largest family (n=18, median
310 against a corpus median of 439) and spans 163 to 128,280 impressions. `other` is the
residue bucket rather than a family, and holds two of the top six posts.

**The two lanes are different rooms.** After the one-time backfill, the archive splits into
38 news posts (median 664) and 18 experience posts (median 362). Every report takes
`--lane`, and the unscoped one prints a `## Lanes` table so the split is never invisible.
An experience post judged against the news median is being judged in the wrong room.

**What separates reach in the news lane is subject recognizability.** Hand-labelling the
unambiguous top and bottom 24 posts gives three non-overlapping bands, which is what
`wiki/audience.md` encodes and what `news/skills/news-ideator` scores `reach_ceiling` from:

| Tier | Subject | n | Median | Range |
|---|---|---|---|---|
| t2 | a named artifact every working dev knows (Rust, SQLite, TypeScript, the kernel) | 7 | 32731 | 5144 to 128280 |
| t1 | a namable sub-community, or the author's own shipped work | 5 | 2192 | 1271 to 3570 |
| t0 | one vendor's product, one paper, or the author's own metrics | 12 | 192 | 76 to 236 |

t0's ceiling sits below t1's floor, and t1's ceiling below t2's floor. The page ships at
`confidence: medium` and says why: the tiers were assigned knowing the impressions, so
clean separation on 24 post-hoc labels is a hypothesis. It earns `high` only once 8 posts
have been tier-scored before publishing and the bands still hold.

Two more caveats worth knowing before trusting any number here. Impressions freeze at
first scrape and are never refreshed, so compare a post against its scrape-age cohort
rather than the pooled median. And engagement coverage is thin (likes on 30/50 posts,
comments 17/50, shares 7/50, missing values counting as zero), which makes any
`likes + 3*comments + 5*shares` ranking partly a ranking of which posts scraped cleanly.

## Content pipeline

Runs inside Claude Code or Codex as a set of skills in `.agents/skills/`. Each skill runs
standalone and hands off through files; only the two cycles chain them. The pipeline is an
edit engine, not a draft engine and not a publish engine: the owner writes every post, and
each enhancer stops for the owner's first-line pick, the one missing specific in their own
words, and a change list they veto line by line.

| Skill | What it does | Writes |
|---|---|---|
| `linkedin-post-cycle` | LinkedIn conductor: retro sweep, experience-lane context, enhancer, critic, image. | — |
| `linkedin-post-enhancer` | Edits the owner's LinkedIn draft without writing a sentence of it. Tags a `pillar`; moves body links to a `Comment link:` line. | `drafts/YYYY-MM-DD-<slug>.md` |
| `linkedin-post-critic` | Scores seven categories against the experience-lane report. Approves at `>= 10/14` with no zero; five hard-zero rules. | verdict |
| `linkedin-post-retro` | 72h after publishing: compares against the experience scrape-age cohort, emits one falsifiable `wiki_candidate`. | `retros/YYYY-MM-DD-<slug>.md` |
| `linkedin-posts-postmortem` | The same analysis over the lane's bottom performers. | `retros/postmortems/` |
| `linkedin-post-comments` | Drafts replies to comments on a published post. | — |
| `wiki-curator` | Absorbs `wiki_candidate` lessons one at a time, answers questions, health-checks. | `wiki/` |
| `x-post-cycle` | X conductor: enhancer, critic, image. | — |
| `x-post-enhancer` | Edits the owner's build-in-public post to 400–600 characters with a setup, a turn, and an outcome. Refuses news takes and anything shared with LinkedIn. | `channels/x/YYYY-MM-DD-<slug>.md` |
| `x-post-critic` | Scores six categories on brand rules and craft (no X cohort yet). Approves at `>= 9/12` with no zero. | verdict |
| `post-image` | Both platforms: one to four real screenshots or photos the owner supplies, leak-checked, with alt text. Nothing is generated. | `images/` + `concepts/` (LinkedIn), `channels/x/` (X) |

```sh
/linkedin-post-cycle "one paying user on Wait Professor, 14 months in"
/x-post-cycle "shipped offline mode in Printyard tonight, 212 lines"
/wiki-curator ingest
```

## Engagement analyzer

```sh
bun run top-posts                        # markdown report, whole archive
bun run top-posts --n 20 --lane experience  # bigger N, one lane
bun run top-posts --json                 # programmatic
bun run post-patterns --lane experience  # archive pattern report, one lane
bun run post-patterns --json             # includes laneStats and postIndex, one row per post
bun run post-lane <post> <lane>          # correct a post's lane by hand
```

`top-posts` reports raw winners and losers. `post-patterns` adds the classification layer
used by the LinkedIn enhancer, critic, and retros. Both take `--lane news|experience`; the
unscoped patterns report prints a `## Lanes` table so the split stays visible. Its `--json`
output carries `postIndex` (with each post's `lane`), which is what lets `wiki lint`
recompute a page's cited statistics instead of trusting them.

## Scraper

```sh
bun run scrape
```

A browser window opens. On first run, sign in manually. Cookies persist in `.auth/` for
subsequent runs.

How it works:

1. Pass 1 scrolls your Posts tab and collects new URNs (stops on the first
   already-saved post or when posts get older than 3 years).
2. Pass 2 opens up to 5 tabs in parallel, expands each post fully (body +
   comments + replies), writes `posts/YYYY/MM-DD-<slug>.md`.

Failed fetches are saved as `posts/YYYY/MM-DD-failed-<id>.md` and retried
automatically on the next run.

On save, each post is auto-linked to the draft it was published from.
The scraper matches the post to a same-date draft by text similarity, copies
that draft's `concept_path` and `lane` onto the post, and back-links the post
into the concept's `prompt.md` (`post_url`, `post_path`). Matching needs the
local draft present (`drafts/` is gitignored), so a fresh clone links nothing;
`rescrape` keeps links already on the file when the draft has been pruned.

### Refreshing frozen metrics

```sh
bun run rescrape             # new posts + refresh the 5 most recent in place
bun run rescrape --limit 20  # go further back
```

`scrape` only appends new posts, so a post's numbers stay frozen at whatever they were on
first capture. Since scrape age varies widely across the archive, the pooled median mixes
72-hour numbers with mature ones, which is why `post-patterns` reports a per-cohort median
and why retros compare against their own cohort. `rescrape` is the direct remedy: it runs
the same two passes as `scrape` — so anything new lands too — and additionally refetches
impressions, likes, comments, shares, and threaded replies for the N most recent saved
posts. It is a superset of `scrape`; running it periodically shrinks the cohort spread the
reports have to work around. A post discovered during the run is saved once as new, never
double-scraped as a refresh target.

Selector accuracy is anchored to HTML dumps under `debug/`. When LinkedIn ships a DOM
change, update `src/scraper/selectors.ts` against a fresh dump.

## Output layout

```
posts/YYYY/MM-DD-<slug>.md         # scraped LinkedIn corpus, immutable
wiki/                              # accumulated judgment, written only by wiki-curator
wiki/brand/index.md                      # catalog, table regenerated by `bun run wiki index`
wiki/log.md                        # append-only change record
wiki/audience.md                   # standing-audience tiers behind reach_ceiling
drafts/YYYY-MM-DD-<slug>.md        # LinkedIn working drafts (gitignored)
concepts/YYYY-MM-DD-<slug>/        # prompt.md: the LinkedIn draft's artifact list and alt text
images/YYYY-MM-DD-<slug>/          # the owner's screenshots, mirrors concepts/ 1:1 (gitignored)
channels/x/                        # X posts and their images (gitignored)
news/                              # portable news folder: skills, briefing CLI, briefings, ideas
.vendor/teimurjan-llm-wiki/        # git submodule: the private brand wiki, pinned to a commit
.vendor/teimurjan-agent-config/    # git submodule: the owner's voice and facts, pinned to a commit
retros/YYYY-MM-DD-<slug>.md        # 72-hour reviews
retros/postmortems/                # same shape for the worst performers, kind: postmortem
```

Tracked: `posts/`, `concepts/`, `wiki/`, `retros/`, `src/`, `news/` (except `news/ideas/`).
Working files (`drafts/`, `images/`, `channels/`) stay local.

Each post file has YAML frontmatter (`urn`, `url`, `posted_at`, `impressions`, `likes`,
`comments`, `shares`, `scraped_at`, `lane`, and `concept_path` when a concept was matched)
followed by the post body and a `## Comments` section with author and threaded replies.
`AGENTS.md` holds the agent-facing repo guide and the wiki conventions.
