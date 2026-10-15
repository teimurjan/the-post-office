---
urn: 'urn:li:activity:7513222579550289920'
url: 'https://www.linkedin.com/feed/update/urn:li:activity:7513222579550289920/'
posted_at: '2026-10-06T13:04:11.890Z'
impressions: 255
likes: null
comments: null
shares: null
scraped_at: '2026-10-15T09:07:51.958Z'
concept_path: concepts/2026-10-06-node-will-run-your-typescript-but-not-your/prompt.md
lane: news
---
Node will run your TypeScript, but not your dependencies'. On purpose.

David Bushell moved his site generator from Deno back to Node 26 over the weekend. Two API swaps, 15% faster builds, Deno uninstalled. Then the one Deno feature Node will not copy: a .ts file inside node_modules does not run. The docs say why: to discourage publishing packages written in TypeScript.

Right call. Let Node run your dependencies' TypeScript and TS becomes the ecosystem's publishing format, every package tied to one compiler's version, an enum or a decorator breaking at first run. Deno let you publish TypeScript straight to its registry. Node said no.

My approach was always to bundle. Webpack and Gulp were hard to understand on my first day in JavaScript, and I bundled anyway. Avatune is 52 packages built with Rslib, TypeScript never leaves the repo, and the configs took five commits in six months, all for new themes. Delivering raw TS feels like imperfectionism to me, an extra on top of native JS.

Compile once when you publish, and ship the types beside it.
