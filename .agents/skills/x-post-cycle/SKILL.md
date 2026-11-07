---
name: x-post-cycle
description: The X cycle. Take a build-in-public post the owner wrote for X through the pipeline — the owner's own first line picked from three versions of it, an edit pass that keeps every sentence theirs, critic verdict, and a real screenshot or photo. Use when the user says "x cycle", "x-post-cycle", "tweet this", "post on x", "build in public post", or hands over an X draft about what they built, shipped, measured, or broke this week. Never starts from a LinkedIn post. For LinkedIn use linkedin-post-cycle; for a generic "edit my post" ask which platform.
---

# x-post-cycle

Orchestrates X end-to-end. The input is a post the owner wrote; the output is that post, edited and not rewritten, a critic verdict, and its image. You are the conductor. `x-post-enhancer`, `x-post-critic`, and `post-image` own their logic and each runs standalone. Do not duplicate their rules. Do not skip them.

**What an X post is.** Build in public: the owner's work this week, while it is still moving. A thing shipped, a number moved, a bug, a decision. The brand wiki makes X the growth engine (`channels`) and up to seven posts a week (`content-engine`), so the cadence is frequent and each post is small.

**What it is not.** A take on someone else's news, or anything from LinkedIn. X posts are written separately and share no subject, sentence, or draft with LinkedIn. If the owner hands over a LinkedIn post, say so and ask for an X post.

## Inputs

`args` carries the owner's post, as typed. Empty: ask once, `What did you build, ship, measure, or break this week? Write it the way you'd post it.` A thought rather than a post: ask once, `Write it the way you would post it, rough is fine. I edit from there.` Then wait.

## Human in the loop

Four pauses, each waiting for the owner: the first line (inside the enhancer), the missing specific (inside the enhancer), the edit list, and the image. Never answer any of these for the owner.

## Workflow

### 0. Read the dossier

`bun run --silent --cwd .vendor/teimurjan-llm-wiki wiki view post-writing`. If it fails, stop and tell the owner.

### 1. Edit

Invoke `x-post-enhancer` with the owner's post. It checks scope and LinkedIn overlap, offers three first lines, asks for the missing specific, lists every change for veto, and saves to `channels/x/<date>-<slug>.md` with `author: owner`. Relay the owner's answers verbatim.

### 2. Critique

Invoke `x-post-critic` with the post path. If it rejects, stop and print the rewrite plan.

### 3. Image (only if the critic approved)

Invoke `post-image` with the post path. The owner supplies one to four real screenshots or photos, or `none`. Nothing is generated.

## Output

Print, in order:

1. One status line per step: `pillar: <pillar>`, `author: owner`, `post: <path>`, `characters: <n>`, `edits: N accepted, K vetoed`, `critic: approved | rejected`, `image: artifact (N files) | none`.
2. **X** — the post text, then `Reply link: <url>` if there is one (the first reply).
3. The critic's verdict verbatim.
4. One closing line: on X, reach for a small account comes from replies, not posts; the brand wiki's target is 25 substantive replies a week to the 15 to 25 accounts on the list.

If the critic rejected, stop after the verdict.

## Failure handling

- No post and the owner does not answer: stop. Never invent the owner's work.
- The enhancer fails to save: stop. Do not retry without the user.
- Critic rejects: not a failure. Print the rewrite plan and end.

## What this skill does not do

- It does not write or rewrite a sentence of the post.
- It does not touch `drafts/`, `posts/`, or `wiki/`, which are LinkedIn's.
- It does not publish anywhere.
- It does not reuse, adapt, or cross-post a LinkedIn post.
