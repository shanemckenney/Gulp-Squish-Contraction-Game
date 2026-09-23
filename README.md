# Gulp & Squish

**Feed the monsters. Squish the words.**

A tablet-friendly game that helps first graders learn contractions. Every contraction is a monster. Kids feed it two words, watch some letters go *poof*, and drop the apostrophe into the gap: **we + will → we'll**.

It's one HTML file with no accounts, no ads, no tracking, and no build step.

> Built for a first grader, by his dad.

---

## Play it

**Live:** `https://<your-username>.github.io/<repo-name>/`

Open it on a tablet, then **Share → Add to Home Screen** and it launches like an app.

---

## How it plays

Three mini-games, each teaching a different piece of the skill:

| Game | What the child does | Skill |
|---|---|---|
| **Gulp it** | Drags (or taps) two words into the monster in order, watches the extra letters float away, then places the apostrophe in the gap. | Building a contraction, and seeing what the apostrophe replaces |
| **Split it** | Sees *we'll* and picks which two words made it from four choices. | Taking a contraction apart |
| **Spot it** | Sees *we + will* and picks the correct spelling from three (*well*, *we'll*, *wel'l*). | Spelling and apostrophe placement |

**Play** on the home screen mixes all three. A round is 5 questions and ends with confetti and a look at the new stars.

### Rewards

- Each of the **28 contractions has its own monster**, generated in code, so there are no image files.
- A monster earns **one star per game** (Gulp, Split, Spot). Three stars means it's fully awake.
- A **My monsters** screen shows the collection. Tapping a monster revisits its lesson.

### Gentle by design

- No timers and no losing.
- A wrong answer gets a soft "try again." After two misses the right answer pulses.
- Every question finishes on the correct answer, spoken aloud in a full sentence.

---

## The word list

The game starts small and opens new worlds as the child masters words. A world unlocks when **4 monsters in the previous world have all 3 stars**.

| World | Focus | Contractions |
|---|---|---|
| 1 | is & am | I'm, it's, he's, she's, that's, what's |
| 2 | not | isn't, don't, didn't, doesn't, can't, aren't |
| 3 | will, are & have | I'll, we'll, you'll, we're, they're, you're, I've, we've |
| 4 | tricky ones | let's, won't, wasn't, weren't, couldn't, I'd, they'll, you've |

Every contraction comes with a short, first-grade-level example sentence that is read aloud after a correct answer.

---

## How it adapts

- **Spaced practice:** Words a child misses are chosen more often, and each first-try success cools them down.
- **Coverage:** Questions favor words that are still missing a star for the game being played.
- **New-word intro:** The first time a word appears in Split or Spot, a short "Meet we'll" card shows the letters that drop and where the apostrophe goes.
- **Shuffled everything:** Word order, answer order, and question order all use Fisher-Yates shuffles.

---

## Built for small hands and eyes

- **Big touch targets:** Everything is tap or drag. Nobody has to type an apostrophe on a tablet keyboard.
- **Readable letters:** Andika is the default font because it's designed for early readers, with single-story *a* and *g* that match handwriting lessons. **OpenDyslexic** is one switch away.
- **Read aloud:** The tablet's built-in voice reads prompts and answers, with a replay button and a mute toggle.
- **Contrast:** The palette was checked against WCAG AA. The main text pairs are well above 7:1.
- **Motion:** `prefers-reduced-motion` is respected, and confetti is skipped when it's on.
- **Keyboard:** Buttons and drag targets also work with Enter and Space.

---

## Grown-ups panel

**Press and hold the gear icon for about a second** (or Shift-click on a desktop).

- Read aloud: on or off
- Sound effects: on or off
- Letters: Andika or OpenDyslexic
- Open all worlds
- Per-word progress (G, S, P for each game's star, with misses in brackets)
- Reset progress (asks twice)

---

## Privacy

Everything stays on the device.

- No accounts, analytics, ads, or network requests
- Progress is saved in the browser's `localStorage` under `gulpsquish:v1:state`
- Clearing site data or switching browsers or devices starts fresh

---

## Deploy it yourself

1. Put `index.html` (and this README) in a GitHub repo.
2. **Settings → Pages →** deploy from the main branch, root folder.
3. Open the Pages URL on the tablet and add it to the home screen.

There is nothing to build or install.

---

## Under the hood

| Piece | How |
|---|---|
| App | Vanilla JavaScript in a single file, with no frameworks and no CDN |
| Monsters | Seeded procedural SVG. Each contraction always gets the same monster |
| Fonts | Andika and OpenDyslexic (both SIL Open Font License), embedded as base64 WOFF2 |
| Voice | Web Speech API (`speechSynthesis`) |
| Sound | Web Audio oscillators, so there are no audio files |
| Drag and drop | Pointer Events, with tap and keyboard fallbacks |
| Storage | `localStorage`, namespaced and wrapped in `try/catch` |

### Add or change contractions

The whole word list is the `RAW` array near the top of the script:

```js
// [world, first word, second word, contraction, example sentence]
[3, 'we', 'will', "we'll", "We'll have fun."],
```

The letters that drop, the apostrophe position, the hints, the wrong-answer choices, and the monster are all derived from that one row. Irregular forms like *won't* get a note instead of a letter breakdown.

To add a world, add a row to `TIERS` and use the new number in `RAW`.

---

## Roadmap ideas

- Installable offline mode (web manifest and service worker)
- More worlds: *there's*, *here's*, *they'd*, *should've*
- Read-aloud pace control
- A printable "monster certificate" when a world is complete

---

## Credits

- Fonts: [Andika](https://software.sil.org/andika/) and [OpenDyslexic](https://opendyslexic.org/), via Fontsource
- Everything else was made with love, for one very good monster feeder
