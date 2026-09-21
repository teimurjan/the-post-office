---
name: post-telegram
description: Translate one finished draft (or a published post) into Russian for the owner's Telegram channel, in the owner's own Russian register from tone-samples/ru-*.md. A faithful translation that reads as if the owner typed it in Russian, not an adaptation with new material. Use when the user says "telegram version", "translate for telegram", "in Russian for telegram", "на русском для телеграма", or "post-telegram". Writes to channels/telegram/, never to drafts/ or posts/.
---

# post-telegram

The Telegram channel is the Russian-language one (brand wiki, `channels`). This skill translates one post into Russian the way the owner writes Russian. The reference is `tone-samples/ru-*.md`: pieces the owner translated by hand. Read them first, every time, and match them. Every rule below was read off `ru-1.md` and loses to the samples whenever they disagree.

`ru-1.md` is the Meta-ads post. While `drafts/2026-09-14-368-on-meta-ads-three-sign-ups.md` still exists, the two files side by side are the exact before-and-after this skill is asked to reproduce.

## Input

One file:

- **A draft in `drafts/`** — the path the owner gives, or the newest file there when none is given (say which one).
- **A published post in `posts/YYYY/`** — the archive text. Ignore its comments.

Read `lane`, `pillar`, and `experience_hook` from the frontmatter. The body is the text to translate. `experience_hook` holds the owner's own wording of the personal layer; when the body compressed it, the Russian may use the owner's fuller phrasing, because it is theirs. Nothing else is added.

## Translate, do not rewrite

Everything in the post is in the Russian, same order, same paragraphs, same closer. The owner adds detail when editing (`ru-1.md` added the Lighthouse score and the podcasts by hand); the skill does not.

Phrase it as Russian, not as English in Russian words. From `ru-1.md`:

- **Drop the subject when the verb carries it.** `Обещал показать цифры в любом случае.` `Разбирал воронку шаг за шагом.` `Починил, Lighthouse дал 97/100.` Keep `я` where it does work: `мне самому продукт был нужен для другого`, `И такой я не один`, `я ушёл слишком широко`.
- **New information goes at the end.** `Регистраций больше не стало.`, not `Регистрации не сдвинулись.`
- **The reader mostly is not addressed.** The English had `the way you would debug a request`; the Russian has `Разбирал воронку шаг за шагом.` A `you` usually goes, or turns impersonal (`можно`, `если`). When one has to stay it is `вы`, lowercase, never `Вы`.
- **Colon for the detail, parentheses for the aside.** `Первая неделя рекламы для Wait, Professor: 42к показов, три регистрации.` `(в этот раз с продуманным ресёрчем)`. The sample has no тире at all; use one only when the sentence cannot be written without it.
- **One деепричастие is fine, a chain is a translation.** `Делая ресёрч, я ушёл слишком широко` is the owner. Three in a row is machine output.
- **Sentence length is mixed and the long ones stay.** `Многим спецам сейчас приходится осваивать кучу нового, а написано всё это незнакомым для них языком.` Do not chop Russian to match English rhythm.
- **Dev vernacular where a native would use it, colloquial where the owner does.** воронка, креатив, флоу, ресёрч, регистрации, спецам, кучу нового. Product names stay Latin: Wait, Professor; Meta; Lighthouse; ML, TTS и STT.
- **The closer is flat.** `Посмотрим, что получится.` No summary, no call to action.

Numbers and typography, as in the sample: decimal comma (`4,4 секунды`), `42к` for thousands (or `42 000`, never `42,000`), `$368` as the post has it, `97/100`, `19%`. `ё` is written. No emoji, no hashtags, no bold. No quotation marks; paraphrase, or «ёлочки» if a quote is unavoidable.

Banned, because they are what a translation sounds like: `данный`, `является`, `осуществлять`, `в рамках`, `с помощью` where the instrumental case does the job, `тот факт, что`, `это` opening consecutive sentences, `успешно` as filler. Banned, because they are Russian LinkedIn: `друзья`, `коллеги`, `не секрет, что`, `давайте разберёмся`, `итак`, `подводя итог`, `надеюсь, было полезно`, `лайфхак`, `инсайт`, `ставьте реакции`, `пишите в комментариях`, `подписывайтесь`.

## Platform

- **Text-only by default.** A message is 4,096 characters; as a photo caption, 1,024 (4,096 with Premium). The concept image at `images/<date>-<slug>/prompt.png` has the LinkedIn hook rendered in English, so it does not go under Russian text as-is; say so once if the owner asks for it.
- **The first line is the notification.** Keep the hook first, then a blank line, as in the sample.
- **One link, last.** The draft's `Comment link:` returns to the body as the final line. Write it as a bare URL on its own line (the owner can turn it into a text link in the composer). Do not link the LinkedIn post.
- **Count the saved body, newlines included**, since Telegram counts them:

  ```sh
  awk 'f{print} /^---$/{c++; if(c==2)f=1}' channels/telegram/<date>-<slug>.md | sed '/./,$!d' | wc -m
  ```

## Output file

Save to `channels/telegram/<YYYY-MM-DD>-<slug>.md`, the draft's own filename stem (for `posts/YYYY/MM-DD-<slug>.md`, `YYYY-MM-DD-<slug>`). Create the directory if needed, overwrite on a re-run. `channels/` is gitignored. Never write to `drafts/` or `posts/`.

```yaml
---
draft_path: drafts/2026-09-14-368-on-meta-ads-three-sign-ups.md
lane: experience
pillar: didnt-teach-me            # experience lane only
language: ru
char_count: 1064
fits_caption: false               # char_count <= 1024
generated_at: 2026-09-14T12:00:00.000Z
status: drafted
---
```

The body is the message exactly as it is pasted into Telegram.

## Print

Print the message, then `Characters: <n> (fits a photo caption | text-only, over the 1,024 caption limit)`, then `Want anything moved, cut, or said differently?` Apply edits, re-count, re-save. Expect a round; the owner reads Russian as a native. **If the owner rewrites it substantially, offer to save their version as the next `tone-samples/ru-N.md`.** That is how the register gets better.

## Checklist

- [ ] Read `tone-samples/ru-*.md` before writing, and the output matches them more than it matches these rules.
- [ ] Same paragraphs, same order, same numbers as the post. Nothing added.
- [ ] Subject dropped where the verb carries it; new information last; no `Вы`; тире only where unavoidable.
- [ ] Decimal comma, `42к`, `$` as the post had it, `ё` written. Product names Latin.
- [ ] Nothing from the two banned lists. Read it aloud in Russian: if it sounds translated, it is.
- [ ] No emoji, hashtags, bold, quotation marks, or call to action. Link last, if any.
- [ ] Character count printed and `fits_caption` matches it.

## When to use

- "telegram version" / "translate for telegram" / "на русском для телеграма" / "post-telegram"

## When NOT to use

- Writing the post → `post-writer`. The Substack Note → `post-substack`.
- An English Telegram message: the wiki rejected that (`channels`, alternatives_rejected). Say so once and do it only if the owner confirms.
