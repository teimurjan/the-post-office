---
urn: 'urn:li:activity:7507785972504219650'
url: 'https://www.linkedin.com/feed/update/urn:li:activity:7507785972504219650/'
posted_at: '2026-09-21T13:01:03.763Z'
impressions: 449
likes: null
comments: null
shares: null
scraped_at: '2026-10-06T05:35:05.244Z'
concept_path: concepts/2026-09-21-jev-will-not-replace-your-model-it-goes-in-front/prompt.md
lane: news
---
Jev will not replace your model. It goes in front of it.

TypeSafe sells it as a new frontier. Its own benchmark says 67.8%, tied with GPT-5.6 Terra, under Opus 5 at 73.1%. Nobody swaps Opus for that.

It answers typed questions in one pass: yes or no, pick one, score it, each with a probability. 70 to 500 ms, $0.042 per million input tokens, output free. An if-statement with calibrated doubt, and most calls in an agent pipeline have that shape. Run it first. Pay frontier prices only when it is not sure.

Jev is not changing AI, but it adds multiple new angles. Mine is on-device. I have run tiny models on a Raspberry Pi for smart home management and voice control in an old Toyota, and every one of them generated text just to make a decision. A parallel decision head is the right shape for that box. Jared Palmer's Kev already ships it open on Qwen3.5, from 0.8B.

Which of your calls actually need a sentence back?

---

## Comments

**Alexander Talavera Karslake**

> The issue is that jev might be 90% confident while still being wrong. And then the system is broken. So I wouldn't use it for critical stuff, it's tricky though.

**Anurag Parepally**

> This is the architecture I have been running since early access, and the typed output is what makes the whole thing operational. With text you are parsing a paragraph to decide whether to escalate; with a probability you set a threshold and routing becomes automatic. The 70-500ms figure matters more than it looks: it means the escalation decision lives inside the request loop, not in a review queue the next morning. The open question is drift. Calibrated today does not mean calibrated next quarter
> … more

