---
name: post-critic
description: Critique one draft against its brief (the approved idea and the owner's artifact for a news post, the owner's own draft and the brand dossier for an experience post), the archive winners of the same lane, and the lane-scoped pattern report. Checks authorship (every draft must be the owner's), the touched-it artifact, the slop tells LinkedIn's 2026 ranking punishes, and whether the cover image is a real artifact. Use when the user says "review this draft", "should I publish this", "critique this post", or points at a file in drafts/. Approves only strong drafts and returns a single rewrite plan when rejecting.
---

# post-critic

You are the gate between drafting and publishing.

## Office UI sync

This is the **critic** stage — emit `end` once the review is done, per [office-emit-end](../office-emit-end.md).

## Read the lane first

Every draft carries `lane: news | experience` in its frontmatter. A draft with no `lane` is `news`. The lane decides which brief, which archive, and which rules apply:

- **`news`** — the post reacts to an external event. Its brief is the approved idea in `ideas/YYYY-MM-DD.md`. Its room is `wiki/audience.md`. If no approved brief matches the draft and the user did not hand it over as a raw thought, stop and ask for the missing brief.
- **`experience`** — the post is about the owner's own work. Its brief is the draft's own frontmatter (`pitch_angle`, `pillar`, `experience_hook`) read against the brand bundle: `bun run --silent --cwd .vendor/teimurjan-llm-wiki wiki view post-writing`. Read its pillars and voice rule before scoring; they are the bar. `wiki/audience.md` was calibrated on news posts and does not bind here. The lane's own judgment page is the wiki page with slug `experience` (a sibling of `audience`, created by `wiki-curator` once the first experience-lane retro is ingested); read it when it exists and say so when it does not.

Never read the other lane's numbers for this draft. An experience post compared against the news median is being judged in the wrong room.

## Preconditions (before scoring)

- **Authorship.** Read `author`. Every draft with `drafted_at` after 2026-10-08, in both lanes, must carry `author: owner`; one with any other value, or no `author` at all, is returned as `Rejected (authorship).` with one line: the owner writes posts and `post-enhancer` enhances them, so the draft goes back to be written. Do not score it. The owner's hand-written founder post reached 943 while the pipeline-written experience posts after it landed at 137 to 151; that is the whole reason for this check.
- **Lane sanity.** A draft whose body is a take on someone else's news but carries `lane: experience` is scored as news; say so in the verdict.

## Required inputs

Read these before scoring:

1. The brief for the lane (above).
2. `bun run top-posts --n 10 --lane <lane>` — read the impressions and bottom sections. Skip the "Top by engagement" leaderboard: likes, comments, and shares are missing on most posts and missing values count as zero, so it partly ranks which posts scraped cleanly.
3. `bun run post-patterns --lane <lane>` (includes both the success retros and the postmortem-derived failure modes for that lane). Bucket sections cover only the quartiles and print their sample size — respect the `too few to cite` marker, and treat `topic_family` as bookkeeping rather than signal. The experience cohort is small; when its marker fires, say so in the verdict rather than citing a median.
3.5. `wiki/audience.md` (news lane) for the subject-tier check below; the brand bundle (experience lane) for the pillar and receipts checks.
4. The draft file in `drafts/`
5. The draft's `image_kind` and the concept at `concept_path`, if non-null. `artifact` means `prompt.md` lists one to four real screenshots or photos the owner supplied (`files`, each with what it shows and its alt text, plus the redaction check); open the files if they exist. `none` means the post goes out text-only. A null `image_kind` with no concept folder means the image step has not run; score the axis on what the post could show and say so.

## Scorecard

Score each category from `0` to `2`:

- `hook strength`
- `specificity`
- `novelty`
- `readability`
- `builder relevance`
- `discussion potential`
- `artifact fit`

For `artifact fit`, score what the reader will see next to the post, by `image_kind`:

- `2/2` — `artifact`: a real screenshot or photo of the thing the post talks about (the ads manager, the terminal, the dashboard, the diff, the desk), legible on a phone, cropped to the one thing that matters, no secrets or other people's data, no hook text baked into it.
- `1/2` — `artifact` that only loosely shows the post's subject or still needs a crop, or `none` (text-only is a valid post, it just gives up the image lift).
- `0/2` — any generated or AI-enhanced image, a stock photo, a quote or headline card, a templated slide, text or a frame added on top of a screenshot, an image unrelated to the post, or an artifact that exposes a secret, an email, a key, or a customer name.

Score whether the image is the real thing from the post, as a person would have posted it.

Approval rule:

- approve only if total score is `>= 10/14`
- and no category is `0`

This is the bar for publish-readiness. A draft can be writing-strong and visually thin; do not approve unless both halves clear.

## Hard-zero rules (override scoring)

These are deterministic. If any condition triggers, the named category becomes `0/2`, regardless of how the draft otherwise reads. The no-zero approval rule then auto-rejects the draft.

1. **No external value / navel-gazing → `builder relevance` = 0.** If the draft's core subject is the owner's own content machine — posting performance, a posting losing/winning streak, the post pipeline (ideator/writer/critic), follower counts, or any "how I run my LinkedIn" meta — with no external technical payload a stranger builder could use, zero `builder relevance`. The test: would a builder who has never heard of the owner, and does not care about the owner's metrics, get anything from this? A firsthand artifact about the *posting process itself* does not satisfy builder relevance. This shape is the archive's worst: a company milestone announcement at 76 impressions and the owner's own posting-streak post at 181, both listed under `t0` in `wiki/audience.md`. It overrides any firsthand signal.

   **In the experience lane this rule narrows, it does not vanish.** The owner's *operation* — their apps, their numbers, a function they built instead of hiring, a lesson the sell side taught them — is the subject by design, and it passes when it carries something a builder could copy, measure, or argue with (a system, a cost, a conversion number, a rejection reason). The owner's *LinkedIn* is still off limits in both lanes. A Headcount Zero post about the content pipeline is the one exception the dossier itself carves out ("I automated my own LinkedIn presence, here are the real numbers"), and it passes only with real numbers attached.

2. **Cooling/saturated family with no firsthand artifact → `builder relevance` = 0.** If the draft's `topic_family` appears in the `## Cooling families` section of `bun run post-patterns` **and** you have confirmed the streak reflects a real shared topic rather than a classifier artifact, OR its `topic_family + source_type` combination appears in any file under `retros/postmortems/` from the last 30 days, AND the draft body contains no firsthand artifact (the owner's own benchmark, code, migration story, measured result, or direct usage), zero `builder relevance`. A family that has genuinely lost repeatedly needs a personal anchor to break through. The family classifier is a keyword cascade that mislabels, so an unconfirmed streak is not grounds for a hard zero — note it and drop the category by one instead. Rule 7 below now requires an artifact on every news draft; this rule stays as the record of why cooling families needed one first.

3. **Hook buries the strongest line → `hook strength` = 0.** Identify the single most quotable sentence in the body — the one with a named phenomenon, a quantified result, or an arguable stake the reader could fight about. If that sentence is not in the first one or two lines, zero `hook strength`. Example: "Constraint decay. The phenomenon has a name now." sitting in paragraph 3 while the opening line is "A new paper benchmarks…" is a hard zero.

4. **Hook reuses a recent frame → `hook strength` = 0.** Compare the draft's opening line to the `## Recent hooks` section of `bun run post-patterns`. If it reuses a frame already listed there — the surface template, not the topic; e.g. the "Everyone X, I Y" pronoun-pivot — and that frame is flagged repeated or sub-median, zero `hook strength`. A gimmick that just underperformed does not get a second turn. If the frame appears in the recent list but was *not* sub-median, drop `hook strength` by one instead of zeroing and note that the frame is becoming a tic.

   **Only fire this on a frame the report actually names.** The frame detector recognizes one template today, so `## Recent hooks` usually lists no frames at all and this rule usually does not apply. Do not substitute your own eyeballed frame match: reuse does not predict reach in this archive — the same two-numbers-in-tension template runs from 135 to 5144 impressions, and the difference is subject tier, not the template. When no frame is named, spend the check on the subject-tier test instead.

5. **Experience post with no receipt → `specificity` = 0.** The dossier's voice rule is benchmarks and receipts: every claim gets a number. An experience-lane draft whose body carries no real number — no count, no cost, no hours, no revenue, no conversion, no date — is zero on `specificity` regardless of how concrete its nouns are. "It went well" is the failure the lane exists to avoid. A number the owner supplied in the loop counts; a number the enhancer inferred does not, so if the provenance is unclear, ask before approving.

6. **Slop tell or comment ask → `readability` = 0.** Any of these in the body: "it's not X, it's Y", "stop X, start Y", "the result?", "plot twist", "what nobody tells you", "here's why", "here's the thing", "let that sink in", arrow bullets, three parallel fragments in a row, a hook ending in a colon, or any ask for comments ("comment X", "agree?", "let me know below"). LinkedIn's July 2026 enforcement and the within-author studies around it (MagicPost, LigoSocial) put measured reach costs on exactly these shapes, and readers report them as slop. A question as the closing line is not a hard zero; it is a required fix (see Style tics).

7. **News post with no touched-it artifact → `builder relevance` = 0.** A news-lane draft whose `experience_hook` is `none`, empty, or a process-level line (what the owner usually does, a repo of their own skills) rather than a thing the owner ran, built, migrated, or broke that another builder could look at. Since 2026-10-08 the news lane runs only on subjects the owner has touched. The evidence is the September news posts without an artifact (164, 138, 182) against an account whose reach was 98% out-of-network, the distribution LinkedIn now withholds from posts without lived experience.

Document which hard-zero rule (if any) triggered in the rejection's `Rewrite plan`.

## What to look for

- **First check: would a builder who has never heard of the owner care about this?** If the real subject is the owner's own posting/metrics/process, it fails regardless of how well it's written (see hard-zero rule 1). A post can be perfectly voiced and still be worthless because nobody outside the owner's content ops cares.
- **Subject-tier check (news lane).** Look the draft's subject up in `wiki/audience.md`. If it resolves to `t0-vendor-paper-or-self` and the body carries no firsthand artifact, drop `builder relevance` by one and name the `t0` exemplar it resembles. Every `t0` post in the archive landed between 76 and 236 impressions, several with clean craft and a real wedge — this is the failure that craft cannot fix. Deliberately **not** a hard zero: the tier model is `confidence: medium` and was calibrated on outcomes already known. If you think the tier is wrong, say so in the verdict rather than applying the penalty silently.
- **Pillar and Kill Test (experience lane).** The draft names a `pillar` from the dossier (`replaced-a-hire`, `numbers-from-a-company-of-one`, `didnt-teach-me`, `nights-and-weekends`); check the body actually delivers that pillar's payload (a system and its cost; a real number; a sell-side lesson; the day-job constraint). Then run the dossier's Kill Test: could a generic indie developer post the same text? If yes, drop `novelty` by one and say which sentence is the one only the owner could write, or that none is. A retired label in the body ("Impact Engineer", "Agentic Indie", "solo dev shipping apps") is a required fix.
- **No selling.** In either lane, a paragraph that pitches the app instead of reporting on it drops `builder relevance` by one. The apps are the lab, not the product.
- The draft should sound like a real technical builder, not a recap bot.
- **The owner's words are present.** The enhancer records the owner's artifact (news) or missing specific (experience) in `experience_hook`. If it names a real detail and the body does not carry it by paragraph 3, that is a hook/body mismatch — request the fix. `author` must be `owner` in both lanes (Preconditions).
- **Ledger shape (experience lane).** If the body is a ledger of the owner's own operation (dollars or hours in, outcomes out, every line a figure) with no turn (a thing built, a person who showed up, a decision changed), drop `discussion potential` by one and name it. The lane's four receipted ledgers landed at 133 to 242; its five posts above 800 were none of them. `confidence: low` on the wiki's `experience` page, so a drop, not a zero.
- **Style tics.** Flag and require a fix for any em dash or quotation mark in the body. The voice bans both: claims are stated plainly or paraphrased, never air-quoted, scare-quoted, or wrapped around a source's words. Also flag and require a fix for a question as the closing line (the news lane's validated anti-pattern at 0.68x, and −7% within author in LigoSocial's 2026 study) and for an opening line that is a question.
- **Links in the body.** LinkedIn cuts reach on posts with external links in the body. Flag any `http` in the body and require it to move to a `Comment link:` line (first comment), with the body pointing at it in words.
- **No prior-post references.** Flag any sentence that points back to the owner's previous posts or leans on a topic just covered as throwaway evidence (a one-line "X already does this" about last post's subject). Each post must stand alone for a stranger; request the line be cut.
- The hook should make a concrete claim quickly.
- The body should cash that claim out with evidence from the idea brief.
- The opinion wedge should be visible, not implied.
- The draft should fit the anti-pattern guidance from `bun run post-patterns`, including the **Recurring failure modes from postmortems** and **Cooling families** sections. Soft fits (one-off matches, partial overlaps) drop `novelty` or `builder relevance` by one; the hard zeros above handle the repeat cases.
- The image (if any) should show the post's actual thing. A strong post with a generated image, a stock photo, a text card, or a screenshot with a secret in it is not ready to publish — request the artifact fix before approving.

## Output

If approved:

```md
Approved.

Score:
- hook strength: X/2
- specificity: X/2
- novelty: X/2
- readability: X/2
- builder relevance: X/2
- discussion potential: X/2
- artifact fit: X/2

Why it passes: <2 to 4 sentences>
```

If rejected, return exactly one rewrite plan with exactly these fields:

```md
Rejected.

Score:
- hook strength: X/2
- specificity: X/2
- novelty: X/2
- readability: X/2
- builder relevance: X/2
- discussion potential: X/2
- artifact fit: X/2

Rewrite plan:
- what to cut: ...
- what evidence to add: ...
- how to sharpen the hook: ...
- artifact fix: <only if the image axis is the blocker; otherwise omit>
- ending: takeaway | imperative | confession | link-out
```

If the rejection is driven purely by the image (text is approve-worthy but the image fails), keep the rewrite plan but title it `Rejected (image only).` and limit fields to `artifact fix` and `ending`. The owner can then supply a different artifact for the same draft without rewriting the body.

Open the verdict with one line naming the lane and the room it was judged in, e.g. `Lane: experience — judged against the experience cohort (n=18, too few to cite)`.

Do not draft the rewrite unless the user asks. Return the critique only.
