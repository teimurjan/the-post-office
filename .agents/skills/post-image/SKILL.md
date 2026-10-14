---
name: post-image
description: Attach the image for a LinkedIn post the way a person would, native to the feed. One to four real screenshots or phone photos the owner supplies, checked for size, legibility and leaks, filed under images/<date>-<slug>/, described with alt text in concepts/<date>-<slug>/prompt.md, and linked from the draft's concept_path and image_kind. No artifact means a text-only post. Nothing is generated, no AI illustrations, sketches, stock photos, or text cards. Use when the user says "image for this post", "cover image", "attach the screenshot", "post-image", or picks a draft to illustrate.
---

# post-image

Attach the image for one LinkedIn post. Two outcomes, nothing else:

1. **Artifact**: one to four real screenshots or photos of the thing the post talks about, supplied by the owner.
2. **None**: a text-only post.

Nothing is generated. Since 2026-10-08 the pipeline makes no images: no AI illustrations, no sketches, no carousels, no flowcharts, no stock, no quote or headline cards. The drawn sketch sat on every one of the account's five viral posts and on every post of the collapse that followed, so it never bought reach, and it never showed a reader anything the first line had not said. LinkedIn's slop reporting now covers images, readers unfollow over AI-looking visuals, and every growing technical creator sampled in October 2026 posts text or one real artifact. The feed is meant to look like a person's.

## What native looks like

- **A screenshot of the actual window**, cropped to the part that matters: the ads manager results table, App Store Connect, the terminal with the benchmark line, the diff, the dashboard, the plan file. Operating-system chrome, light or dark mode, and the owner's own cursor are fine. No added arrows, circles, captions, headline text, brand bars, device frames, mockups, or "cleaned-up" re-renders.
- **A phone photo**, unstaged: the desk, the screen, a whiteboard, a notebook page. No filters.
- **Real output**: a terminal, a log, a spreadsheet, a chart from the real tool, with the one number visible.
- **Never**: an AI-generated or AI-enhanced image, a stock photo, a quote or headline card, a templated slide, a logo on a gradient, a composed collage with labels.
- **Up to four images per post.** The first is the thumbnail and the one that matters. AuthoredUp's 3M-post set put multi-image posts near 1.3x a text post's reach and single images near 1.1x; four weak images are not better than one strong one.

## Office UI sync

This is the **illustrator** stage — emit `end` once `concepts/<date>-<slug>/prompt.md` exists or the draft is marked `image_kind: none`, per [office-emit-end](../office-emit-end.md).

## Inputs

A **draft path** like `drafts/2026-09-01-10-years-as-an-engineer.md`, required, since the artifact is filed against the draft. Read the file in full; the body tells you which artifact fits it. The skill does not accept `posts/...` paths; images are for new drafts only.

Sizes are in [linkedin-image-specs](../linkedin-image-specs.md). An artifact keeps its own shape as long as it sits between 1.91:1 landscape and 4:5 portrait; a screenshot forced into a square is a cropped screenshot.

## Step 1: ask for the artifact

Read the draft, name the two most specific things in it that could be on a screen, then ask once, in plain text, and wait:

`What real thing from this post can go on screen? For this one I'd expect <candidate A> or <candidate B>. Give me the file path (up to four), or say none for text-only.`

Never pick for the owner, never generate an artifact, never fake a screenshot. If no interactive channel is available, print the question and end with the draft untouched.

## Checks, per file

1. **The file exists.** Read its dimensions:
   ```sh
   sips -g pixelWidth -g pixelHeight <file>
   ```
   If the aspect is wider than 1.91:1 or taller than 4:5, say so and offer the crop. On the owner's yes, crop with `sips --cropToHeightWidth <h> <w> <file> --out images/<date>-<slug>/artifact-<N>.<ext>`; otherwise the owner crops by hand.
2. **Look at it** (Read renders PNG and JPEG). The one number or line that makes the post has to be readable at phone width. A full-page screenshot with the number in a corner needs a crop to that region; ask for it.
3. **Leak check.** Scan for emails, API keys, tokens, session cookies, account IDs, customer or user names, private repository names, other people's faces, and anything the owner's apps show about their users. List what you find and ask the owner to redact before filing. Never file an image with a visible secret, and never redact by hand; the owner does it and sends the file again.
4. **Native check.** No overlay text, no mockup frame, no generated or stock image. If the owner sends a composed card, ask for the raw screenshot instead.

## Filing

- Copy each accepted file to `images/<YYYY-MM-DD>-<slug>/artifact-<N>.<ext>`, numbered in the order the owner wants them shown (gitignored, mirrors `concepts/`).
- Write `concepts/<YYYY-MM-DD>-<slug>/prompt.md`:

```yaml
---
draft_file: drafts/<YYYY-MM-DD>-<slug>.md
kind: artifact
files:
  - path: images/<YYYY-MM-DD>-<slug>/artifact-1.<ext>
    size_pixels: <w>x<h>
    shows: <one line: what the reader sees, and the number or line that matters>
    alt: <one or two lines of alt text for LinkedIn's image description>
redaction_checked: true
generated_at: <ISO timestamp>
---
<the first image's alt text, repeated as the body>
```

The body is alt text, not a prompt. The scraper may later append `post_url` and `post_path` to this file when it matches the published post back to the concept; do not author those by hand.

- Update the draft frontmatter with Edit, preserving everything else:

```yaml
concept_path: concepts/<YYYY-MM-DD>-<slug>/prompt.md
image_kind: artifact
```

Print exactly this, nothing else:

```
Image: artifact (<N> files)
Files:
  1. images/<YYYY-MM-DD>-<slug>/artifact-1.<ext> (<w>x<h>) — <shows>
  2. ...
Leak check: clean | redacted by owner
Alt text: <alt text of the first image>
Saved to: concepts/<YYYY-MM-DD>-<slug>/prompt.md
Linked from: drafts/<YYYY-MM-DD>-<slug>.md
```

## None mode

Set `image_kind: none` on the draft with Edit and leave `concept_path: null`. Create no concept folder. Print `Image: none (text-only)` and the draft path. That is the whole mode.

## Workflow

1. Read the draft in full.
2. Name two candidate artifacts from the post's own materials and ask the owner for the files or `none`. Wait.
3. Artifact: run the four checks on each file; crop on the owner's yes; copy to `images/`; write the concept with alt text; set `concept_path` and `image_kind: artifact`; print the block.
4. None: set `image_kind: none`; print the one line.

## Hard rules

- The owner supplies every image. Never generate, compose, enhance, or fake a screenshot or photo, and never substitute a stock image.
- Never file an image with a visible secret.
- No text in any image beyond what the real screen already shows. The hook lives in the post.
- Always read the whole draft before naming candidate artifacts.
- One to four files, in the order the owner wants; the first one is the one that matters.

## When NOT to use

- The user wants a drawing, an illustration, or any generated image. The pipeline no longer makes them; say so and offer the artifact path or text-only.
- The user wants an image for an already-published post in `posts/`. Out of scope.
