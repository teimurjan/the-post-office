---
urn: 'urn:li:activity:7509236824347869184'
url: 'https://www.linkedin.com/feed/update/urn:li:activity:7509236824347869184/'
posted_at: '2026-09-25T13:06:13.798Z'
impressions: 2638
likes: null
comments: null
shares: null
scraped_at: '2026-10-06T05:34:58.799Z'
concept_path: concepts/2026-09-25-the-creator-of-rails-put-pencils-down/prompt.md
lane: news
---
The creator of Rails put pencils down at 53%.

DHH told Rails World that writing code by hand is now the exception at 37signals. He compared a manual fix to a bug showing up in Sentry. Two days earlier the official Rails blog published its own agent benchmark. On 20 real feature tickets, GPT-6 Astra passes 53% of runs at max effort. Claude passes 32%.

The rule is about where a failure goes, not about the agent being good enough. At 37signals a failed ticket becomes a change to the agent setup. In most teams you finish the ticket by hand and the workflow stays as broken as it was.

I built blazediff-agent around the same idea. Deterministic CLI steps do the work, and the agent only handles the reasoning. When it gets something wrong, I tighten a command or the plan file instead of fixing the output by hand.

Half the tickets still fail. Did any of your fixes last week make the next run better?
