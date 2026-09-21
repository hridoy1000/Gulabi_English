# Gulabi English 🌸

A free, offline-friendly English learning website for a Class 8 student in the Bangla-medium curriculum.
Everything is explained in Bangla, with English examples — built for someone who can read English but is
afraid to use it.

**One file, no server, no account.** Open `index.html` in any browser and it works. All progress is kept in
the browser's own storage.

---

## What's inside

| Section | What it has |
|---|---|
| **গ্রামার (Grammar)** | 52 chapters in 8 parts, arranged like a textbook — rules, tables, examples, common-mistake lists and practice after every chapter |
| **প্র্যাকটিস (Practice)** | 778 questions — multiple choice, fill in the blank, and drag-the-words-into-order |
| **লেখা (Writing)** | 11 writing chapters + 30 topics (paragraph, letter, application, email, dialogue, story, 300-word composition). She writes, the app marks every mistake, explains it in Bangla, offers a one-click fix and links back to the chapter that covers it |
| **কথা বলা (Speaking)** | 7 technique chapters (pronunciation, stress, intonation, fluency, conversation, viva) + 102 practice items. Speak into the microphone and it scores each word, marks the ones it couldn't hear, and rates pace |
| **পরীক্ষা (Exams)** | 16 timed exams — mock tests, chapter tests, skill tests and two grand finals, with grade, GPA and a full explanation of every mistake |
| **খেলা (Games)** | 6 games — word match, scramble, spelling hunt, 60-second speed quiz, odd one out, sentence builder |
| **শব্দ (Words)** | 1000 words in 25 themes, each with Bangla meaning, part of speech, an example sentence and its translation |
| **বাক্যাংশ (Phrases)** | 500 everyday sentences, idioms and proverbs |

Plus a daily lesson, a mistake book that collects everything she got wrong, a progress page, stars and levels,
day/night mode, and a Bangla/English interface toggle.

### The writing checker

`src/writing.js` is a rule-based English proofreader written from scratch — no network, no API. It checks
spelling against a 69,000-word dictionary, subject–verb agreement, tense consistency, articles, prepositions,
capitalisation, punctuation, run-on sentences and common Bangla-speaker mistakes. Every issue carries a Bangla
explanation and a suggested fix.

There is also an **optional** "ask Claude" button in the writing studio. It only appears when the page is
opened as a Claude Artifact; on GitHub Pages or a local file it stays hidden and everything else still works.

---

## Running it

Just open `index.html`. Nothing to install.

To host it for free, turn on **GitHub Pages** (Settings → Pages → Deploy from branch → `main` / root).

## Building from source

The single-file `index.html` is generated from the pieces in `src/`.

```bash
cd src
./build.sh
```

This runs the data validator, concatenates every module into `bundle.js`, then writes:

- `page.html` — an HTML fragment (used when publishing as a Claude Artifact)
- `preview.html` — the full standalone document (copy this over `../index.html`)

### Source layout

```
src/
  data_lessons*.js  data_new*.js  data_patch*.js  data_g*.js   grammar chapters
  data_exams*.js                                               the 16 exams
  data_vocab*.js    data_phrases*.js                           1000 words, 500 phrases
  data_writing*.js                                             writing chapters, prompts, model answers
  data_speak.js                                                speaking chapters and drills
  data_dict.js                                                 spell-check dictionary
  writing.js                                                   the proofreading engine
  app1.js                                                      state, helpers, book structure
  app_ui.js                                                    theme + language toggles
  app_fx.js                                                    animations and celebrations
  app2.js                                                      home, grammar, practice, quiz engine
  appw.js                                                      writing studio, more, progress
  app_speak.js                                                 spoken English + microphone scoring
  app_games.js                                                 the six games
  app3.js                                                      exams, words, phrases, router, events
  head.html  body.html                                         styles and page shell
  build.sh   validate.js                                       build and content checks
```

## Tests

```bash
python3 tests/smoke3.py
```

A Playwright pass that walks every route, plays through the games, scores a simulated speech result,
submits a piece of writing, flips both toggles and checks that nothing throws.

---

## Notes and limits

- The microphone check needs Chrome and permission to use the mic. Where it isn't available, the app falls
  back to listen-and-repeat with self-marking. Even when it works, it sometimes mishears — background noise
  especially.
- The writing checker follows rules, not understanding. It can miss a mistake or flag a correct sentence.
  There's an "this word is fine" button for names and unusual words.
- The exam questions are original, written in the style of the Bangladesh board exams. They are not past papers.
- The interface toggle switches menus, buttons and headings. Grammar explanations stay in Bangla on purpose.
- Progress lives in one browser on one device. Opening it elsewhere starts fresh.

## Credits

Content written against the NCTB Class 8 *English Grammar and Composition* syllabus.
Fonts: Baloo Da 2 and Nunito, loaded from Google Fonts.
