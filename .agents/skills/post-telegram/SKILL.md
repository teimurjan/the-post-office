---
name: post-telegram
description: Write the Russian Telegram version of one finished draft (or a published post) in the owner's own Russian register from tone-samples/ru-*.md. Two shapes, a translation (faithful, reads as if the owner typed it in Russian, nothing added) or a follow-up (when the previous Telegram post had no LinkedIn twin, the new post continues from it instead of repeating it). Use when the user says "telegram version", "translate for telegram", "in Russian for telegram", "на русском для телеграма", "telegram follow-up", or "post-telegram". Writes to channels/telegram/, never to drafts/ or posts/.
---

# post-telegram

The Telegram channel is the Russian-language one (brand wiki, `channels`). This skill writes one post in Russian the way the owner writes Russian. The reference is `tone-samples/ru-*.md`: pieces the owner wrote or rewrote by hand. Read them all first, every time, and match them. Every rule below was read off the samples and loses to them whenever they disagree.

- `ru-1.md` — the Meta-ads post, translated by the owner from `drafts/2026-09-14-368-on-meta-ads-three-sign-ups.md`. The translation register; the two files side by side are the before-and-after of that mode.
- `ru-2.md` — the 2026-09-21 post about stopping those ads, written for Telegram only, no LinkedIn twin.
- `ru-3.md` — the 2026-09-28 follow-up on the first two purchases, the owner's rewrite of this skill's draft. The follow-up register. What the owner cut and added is the lesson (see Follow-up below).

## Input

One file, and a mode:

- **A draft in `drafts/`** — the path the owner gives, or the newest file there when none is given (say which one).
- **A published post in `posts/YYYY/`** — the archive text. Ignore its comments.

Read `lane`, `pillar`, and `experience_hook` from the frontmatter. The body is the text to work from. `experience_hook` holds the owner's own wording of the personal layer; when the body compressed it, the Russian may use the owner's fuller phrasing, because it is theirs.

**Mode.** Look at the newest file in `channels/telegram/`. If its `draft_path` is `null` (it went out on Telegram with no LinkedIn twin) and it is newer than the last experience post in `posts/`, Telegram readers are ahead of LinkedIn readers, and the new post is a **follow-up** that continues from it. Otherwise it is a **translation**. The owner can name the mode outright ("translate", "follow-up"); say which one you used.

## Translation: translate, do not rewrite

Everything in the post is in the Russian, same order, same paragraphs, same closer. The owner adds detail when editing (`ru-1.md` added the Lighthouse score and the podcasts by hand); the skill does not.

Phrase it as Russian, not as English in Russian words. From `ru-1.md`:

- **Drop the subject when the verb carries it.** `Обещал показать цифры в любом случае.` `Разбирал воронку шаг за шагом.` `Починил, Lighthouse дал 97/100.` Keep `я` where it does work: `мне самому продукт был нужен для другого`, `И такой я не один`, `я ушёл слишком широко`.
- **New information goes at the end.** `Регистраций больше не стало.`, not `Регистрации не сдвинулись.`
- **The reader mostly is not addressed.** The English had `the way you would debug a request`; the Russian has `Разбирал воронку шаг за шагом.` A `you` usually goes, or turns impersonal (`можно`, `если`). When one has to stay it is `вы`, lowercase, never `Вы`.
- **Colon for the detail, parentheses for the aside.** `Первая неделя рекламы для Wait, Professor: 42к показов, три регистрации.` `(в этот раз с продуманным ресёрчем)`. The samples have no тире at all; use one only when the sentence cannot be written without it.
- **One деепричастие is fine, a chain is a translation.** `Делая ресёрч, я ушёл слишком широко` is the owner. Three in a row is machine output.
- **Sentence length is mixed and the long ones stay.** `Многим спецам сейчас приходится осваивать кучу нового, а написано всё это незнакомым для них языком.` Do not chop Russian to match English rhythm.
- **Dev vernacular where a native would use it, colloquial where the owner does.** воронка, креатив, флоу, ресёрч, регистрации, спецам, кучу нового. Product names stay Latin: Wait, Professor; Printyard; Meta; Lighthouse; ML, TTS и STT.
- **The closer is flat.** `Посмотрим, что получится.` No summary, no call to action.

## Follow-up: continue, do not recap

Written for the reader who read the last Telegram post. Read that post (the `follows:` file) before writing, and `ru-3.md`, where the owner cut and added exactly this:

- **Open on the outcome with its number.** `Первые две покупки в Printyard. Обе lifetime.` The first line is the news, not the setup.
- **One clause of recap, not a paragraph.** Only what the last post left open (`кампания только прогревалась`), tied to it with `Неделю назад писал, что ...`. Anything the reader already has is cut: the owner deleted the superuser line the draft had carried over.
- **The turn has a cause.** The owner's version says who or what changed the result: `Знакомый посоветовал немного изменить настройки кампании и экспериментировать больше с меньшим бюджетом. Так мой запуск 24-го сентября дал две первые покупки ($83 рекламы на каждую).` The skill does not invent one. When the source post has no cause for the outcome, write the beat with what the post has and add one line to the print, `Нет причины поворота: кто или что изменил результат?`, so the owner adds it by hand as they did in `ru-3.md`.
- **A rough tally in one line.** `Грубо: 300$ с 166$ и эксперимент удался.` Money in against money out, marked as rough, then the verdict in three words.
- **The honest state, in the owner's word, then the stance after `Но`.** `Это всё ещё не стабильность. Но деньги пришли за продукт, собранный под реальную задачу, а не под широкую идею.` Not a dramatic word and not a triumphant one.
- **The closer is the next step, with its number.** `Ещё пару дней погоняю текущую кампанию, слегка подняв бюджет (40$ -> 60$ в сутки), потом буду пытаться скейлить по регионам.` When there is no next step, the closer is flat, as in translation. Never a summary, never a call to action.
- **The owner says more here than on LinkedIn.** `ru-3.md` gives the rough revenue the LinkedIn post left out, and a plain admission (`С каждым днём начинаю "чувствовать" маркетинг чуть лучше.`). The skill adds nothing; the owner adds it by hand. On a re-run, never strip a number or a line the owner put in.

The owner's Russian for this mode: `проитерировали пять версий`, `погоняю кампанию`, `скейлить по регионам`, `знакомый посоветовал`, `запуск 24-го сентября`, `слегка подняв бюджет`. Dev verbs borrowed from English are the register, not a lapse.

## Typography and vocabulary, both modes

Numbers as in the samples: decimal comma (`4,4 секунды`), `42к` for thousands (or `42 000`, never `42,000`), `97/100`, `19%`. `ё` is written. Money keeps the form the post used (`$602`, `$83`); when the owner adds a figure by hand they write it Russian-style, `300$`, `40$ в сутки` (`ru-3.md`), and either is theirs, so keep one form inside a sentence. A change in a value is an ASCII arrow, `40$ -> 60$ в сутки`, never a тире. No emoji, no hashtags, no bold. No quotation marks around a source's words; paraphrase, or «ёлочки» if a quote is unavoidable. Straight quotes around one figurative word (`"чувствовать" маркетинг`) are the owner's own mark, allowed once per post.

Banned, because they are what a translation sounds like: `данный`, `является`, `осуществлять`, `в рамках`, `с помощью` where the instrumental case does the job, `тот факт, что`, `это` opening consecutive sentences, `успешно` as filler. Banned, because they are Russian LinkedIn: `друзья`, `коллеги`, `не секрет, что`, `давайте разберёмся`, `итак`, `подводя итог`, `надеюсь, было полезно`, `лайфхак`, `инсайт`, `ставьте реакции`, `пишите в комментариях`, `подписывайтесь`.

## Platform

- **Text-only by default.** A message is 4,096 characters; as a photo caption, 1,024 (4,096 with Premium). The concept image at `images/<date>-<slug>/prompt.png` has the LinkedIn hook rendered in English, so it does not go under Russian text as-is; say so once if the owner asks for it.
- **The first line is the notification.** Keep the hook first, then a blank line, as in the samples.
- **One link, last.** The draft's `Comment link:` returns to the body as the final line. Write it as a bare URL on its own line (the owner can turn it into a text link in the composer). Do not link the LinkedIn post.
- **Count the saved body, newlines included**, since Telegram counts them:

  ```sh
  awk 'f{print} /^---$/{c++; if(c==2)f=1}' channels/telegram/<date>-<slug>.md | sed '/./,$!d' | wc -m
  ```

## Output file

Save to `channels/telegram/<YYYY-MM-DD>-<slug>.md`, the draft's own filename stem (for `posts/YYYY/MM-DD-<slug>.md`, `YYYY-MM-DD-<slug>`). Create the directory if needed, overwrite on a re-run. `channels/` is gitignored. Never write to `drafts/` or `posts/`.

```yaml
---
draft_path: drafts/2026-09-28-one-superuser-did-what-657-of-ads.md
follows: channels/telegram/2026-09-21-wait-professor-ads-stopped.md   # follow-up only
mode: translation | follow-up
lane: experience
pillar: didnt-teach-me            # experience lane only
language: ru
char_count: 810
fits_caption: true                # char_count <= 1024
generated_at: 2026-09-28T12:00:00.000Z
status: drafted
---
```

The body is the message exactly as it is pasted into Telegram. A post the owner wrote for Telegram only, with no draft, is saved the same way with `draft_path: null`; that file is what tells the next run to write a follow-up.

## Print

Print the message, then `Mode: translation | follow-up`, then `Characters: <n> (fits a photo caption | text-only, over the 1,024 caption limit)`, then the missing-cause line if the follow-up has no cause for its turn, then `Want anything moved, cut, or said differently?` Apply edits, re-count, re-save. Expect a round; the owner reads Russian as a native. **If the owner rewrites it substantially, save their version as the next `tone-samples/ru-N.md` and as the channel file's body.** That is how the register gets better; `ru-3.md` came from exactly that.

## Checklist

- [ ] Read every `tone-samples/ru-*.md` before writing, and the output matches them more than it matches these rules.
- [ ] Mode chosen from the newest `channels/telegram/` file or the owner's word, and printed.
- [ ] Translation: same paragraphs, same order, same numbers as the post. Nothing added.
- [ ] Follow-up: opens on the outcome, one clause of recap, a cause for the turn (or the missing-cause line printed), a rough tally, the honest state then `Но`, the next step with its number as the closer.
- [ ] Subject dropped where the verb carries it; new information last; no `Вы`; тире only where unavoidable, `->` for a changed value.
- [ ] Decimal comma, `42к`, money in one form per sentence, `ё` written. Product names Latin.
- [ ] Nothing from the two banned lists. Read it aloud in Russian: if it sounds translated, it is.
- [ ] No emoji, hashtags, bold, or call to action; at most one figurative word in straight quotes. Link last, if any.
- [ ] Character count printed and `fits_caption` matches it.

## When to use

- "telegram version" / "translate for telegram" / "на русском для телеграма" / "telegram follow-up" / "post-telegram"

## When NOT to use

- Writing the post → `post-writer`. The Substack Note → `post-substack`.
- An English Telegram message: the wiki rejected that (`channels`, alternatives_rejected). Say so once and do it only if the owner confirms.
