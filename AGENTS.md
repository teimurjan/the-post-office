# Post pipeline: LinkedIn and X

A content pipeline for the owner's LinkedIn and X, built on a scraped archive of their LinkedIn posts.

- **LinkedIn** (`linkedin-post-cycle`): the owner's own operation. An app they run, a number they measured, a function they built instead of hiring, a lesson the sell side taught them.
- **X** (`x-post-cycle`): build in public. The week's work while it is still moving. No archive or analytics yet.

An X post never reuses, condenses, or adapts a LinkedIn post, and the other way round. When the owner does not say which platform, ask.

Nothing here writes for Telegram or Substack, even though the brand wiki's `channels` and `platforms` pages still cover them.

Reacting to external events is out of scope. `news/` is a self-contained folder that runs from the owner's personal agent: nothing outside it reads it, and nothing in it reads this repo.

## Human in the loop

The owner writes every post. Enhancers stop twice (first line, missing specific), apply only changes the owner can veto, and never write a body. `post-image` files the owner's real screenshots or photos, or `none`; nothing is generated. A skill that cannot reach the owner prints its question and ends. It never guesses.

## Who the owner is

Read these before editing or judging a post:

| Source | Owns |
|---|---|
| `.vendor/teimurjan-agent-config/MY-VOICE.md` | How the owner writes |
| `.vendor/teimurjan-agent-config/MY-BRAIN.md` | Facts about the owner: what they run, current numbers, goals, audience, what is public |
| `bun run --silent --cwd .vendor/teimurjan-llm-wiki wiki view post-writing` | Headcount Zero positioning, pillars, Kill Test, platform notes |

- **If a source is missing or the command fails, stop and tell the owner** (`git submodule update --init` when `.vendor/` is empty). Never reconstruct them from old posts.
- Never invent experience. Use only facts from `MY-BRAIN.md` or the owner, ask about anything it marks unconfirmed, and honour its `Public vs private` section.
- On a fact, `MY-BRAIN.md` beats the older brand wiki. On how the owner sounds, `MY-VOICE.md` beats the wiki's `voice` page. Say so when they disagree.
- Submodules are pinned. If something looks out of date, run `git submodule update --remote <path>` and commit the pointer before assuming the source is wrong.
- Both submodules are private and this repo is public. Read them, never copy them into tracked files. LinkedIn audience findings stay in `wiki/` here and are never mirrored there.

## Where things live

| Path | What it is | Tracked |
|---|---|---|
| `posts/YYYY/MM-DD-<slug>.md` | Scraped LinkedIn archive. Only `concept_path` and `lane` are ever added after the fact. | yes |
| `drafts/` | LinkedIn working drafts, every one `lane: experience`, `author: owner` | no |
| `channels/x/` | X posts and their images | no |
| `concepts/`, `images/` | A LinkedIn draft's artifact list and alt text; the image files | concepts only |
| `retros/`, `retros/postmortems/` | 72-hour reviews and worst-performer reviews | yes |
| `wiki/` | LinkedIn judgment layer | yes |

Never read `.auth/` (browser profile and cookies) or quote from it. Skip `src/` unless the question is about the tooling.

`bun run cleanup` prunes old `drafts/` and `images/` (`--dry-run`, `--days N`).

## The archive

Post frontmatter: `urn`, `url`, `posted_at`, `impressions`, `likes`, `comments`, `shares`, `scraped_at`, plus `concept_path` and `lane` when known. `null` means the number could not be scraped, so exclude it from averages. The body is the post text and a `## Comments` section. Only original posts are collected.

Every post carries `lane: news | experience`. New drafts are always `experience`. `news` marks old posts about external events, a different room with a different median, so LinkedIn reports always run `--lane experience`. A post without a lane counts as `experience`. Correct one with `bun run post-lane <post> <lane>`.

## Analytics

```sh
bun run top-posts --lane experience      # scoreboard
bun run post-patterns --lane experience  # working report; --json for programmatic use
bun run rescrape                         # refresh the most recent posts in place
```

- Respect the `too few to cite` marker. The experience cohort is small, so say so rather than citing a median.
- Cite a fault only from `## Validated anti-patterns`. `## Tested and discredited` lists flags that failed, kept so they are not reintroduced.
- `topic_family` is bookkeeping from a keyword cascade. Never derive a reach judgment from it; use `wiki/experience.md` and the pillars.
- Prefer impressions. Likes, comments, and shares are missing on most posts and count as zero, so engagement rankings partly rank which posts scraped cleanly.
- Impressions freeze at first scrape, so compare a fresh post against its scrape-age cohort, not the pooled median.

## Wiki

- `wiki-curator` is the only writer to `wiki/`. `linkedin-post-retro` and `linkedin-posts-postmortem` emit a `wiki_candidate` with `wiki_ingested: false` for it to absorb.
- The CLI owns counts and the wiki owns causes. Evidence is explicit post paths, and every body number has a frontmatter twin.
- New lessons go to `wiki/experience.md`. `wiki/audience.md` holds the news-lane tier model and is closed to new evidence. X gets a page when it has numbers.
- Run `bun run wiki lint` after touching `wiki/`. It exits non-zero on any error.
