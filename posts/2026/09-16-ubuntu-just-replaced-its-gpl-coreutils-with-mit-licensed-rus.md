---
urn: 'urn:li:activity:7505974022212382721'
url: 'https://www.linkedin.com/feed/update/urn:li:activity:7505974022212382721/'
posted_at: '2026-09-16T13:01:01.149Z'
impressions: 107
likes: null
comments: null
shares: null
scraped_at: '2026-09-18T06:20:38.858Z'
concept_path: concepts/2026-09-16-ubuntu-just-replaced-its-gpl-coreutils-with-mit/prompt.md
lane: news
---
Ubuntu just replaced its GPL coreutils with MIT-licensed Rust.

Version 26.10 swaps GNU for uutils across ls, cp, mv, rm, the whole set. The pitch is memory safety, and that part is real. Rust catches at compile time what a C compiler waves through.

Nobody mentioned the license. uutils reimplements the same tools, closely enough to be the default now, and ships under MIT. A rewrite is new code. You pick the license. GNU's GPL did not come with it.

I know that firsthand. For BlazeDiff I rewrote libspng myself. blazediff-png decodes the same bytes as spng and rejects the same malformed inputs, just faster, single thread, SIMD. Same output, entirely my code.

The memory safety is worth having. But did anyone actually choose to drop copyleft?

https://lnkd.in/d9ZaA9gt
