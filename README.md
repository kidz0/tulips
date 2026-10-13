# Virtual Love Letter

A six-stage romantic experience: tulip puzzle → "Do you want to continue?" → tulip bloom → mystery scroll → love letter, with gentle background music.

## Project structure

```
love-letter/
├── index.html      Page structure (all six stages)
├── style.css       Design, animations, responsive rules
├── script.js       Config, state machine, puzzle, scroll, letter, music
└── assets/
    ├── images/tulip-reference.svg   Optional: same tulip as in script.js (for editing or reuse)
    └── audio/romantic-piano.mp3     YOU ADD THIS (see below)
```

The puzzle picture (the pink tulip bouquet) is embedded inside `script.js`, so the game never depends on an image file loading. `tulip-puzzle.jpg` is the same picture as a normal file. To use a different picture, make it square, then replace `TULIP_URL` in `script.js`.

## 1. Personalize it (only `script.js`, top of the file)

Edit the `CONFIG` block:

| Setting | What it does |
|---|---|
| `girlfriendName` | Used in the letter greeting ("Dear HER NAME,") |
| `myName` | Page title and fallback signature |
| `greeting`, `introText`, `howToPlay` | Texts on the puzzle screen |
| `puzzleCompleteMessage` | Message shown when the puzzle is finished |
| `questionText`, `yesLabel`, `noLabel` | The "Do you want to continue?" screen |
| `letterSalutation` | Greeting line, `{name}` becomes her name |
| `loveLetter` | **Your letter.** Replace `[INSERT MY PERSONAL LOVE LETTER HERE]` between the backticks |
| `closing`, `signature` | Closing line and signature (replace `[INSERT MY NAME OR NICKNAME HERE]`) |
| `finalMessage` | Optional P.S. under the signature (empty = hidden) |
| `musicPath`, `musicVolume` | Audio file location and loudness |

Writing the letter: blank line = new paragraph, single line break = line break. Don't use the backtick character (`) or `${` inside the letter.

## 2. Add the music

1. Find a gentle instrumental piano or music-box track you are **allowed to use** (royalty-free or Creative Commons libraries, or music you licensed or made yourself).
2. Name it exactly `romantic-piano.mp3`.
3. Put it in `assets/audio/`.

Or use another name/format and change `musicPath` in `CONFIG`. If the file is missing, everything else still works and the music button explains why.

Phones and browsers block sound until the user taps something, so the music tries to start when the letter appears. If blocked, the music button pulses softly and she can tap it.

## 3. Run it on your computer

- Easiest: double-click `index.html` (opens in your browser).
- Or from the folder: `python3 -m http.server 8000`, then open `http://localhost:8000`.

## 4. Open it on a phone

- **Best way (gift-ready):** upload the whole `love-letter` folder to a free static host such as Netlify Drop, GitHub Pages or Cloudflare Pages, and send her the link. Test the link on your own phone first.
- **Testing on your own phone:** run `python3 -m http.server 8000` on your computer, connect both devices to the same Wi-Fi, and open `http://YOUR-COMPUTER-IP:8000` on the phone.
- Keep the `assets` folder next to `index.html` wherever you upload it.

## 5. Testing guide

1. **Puzzle:** pieces are shuffled. Tap one (it lifts with a pink ring), tap another to swap. A correct piece shows a check mark and locks. Progress text and bar update. Finishing triggers sparkles, the message, then the next stage.
2. **Question:** Yes and No are visible. Tapping No makes it jump to a new spot inside the screen, every time. Rotate the phone: it stays on screen. Tap Yes once: both buttons disable and the scene fades.
3. **Bloom:** stem grows, leaves unfold, bud opens, more tulips bloom, petals drift. It ends by itself (about 7 seconds) and the scroll appears.
4. **Scroll:** the wax seal shimmers and pulses. Tap it (or swipe on the scroll). The seal breaks, the paper unrolls, then the letter appears. After about 7 seconds without interaction a soft hint fades in.
5. **Letter:** greeting, paragraphs, closing and signature fade in one after another. Tap the letter to show everything at once. "Read it again ♡" replays only the reveal.
6. **Music:** button top-right; animated bars = playing, slash = off. Test with the mp3 present, and once with it removed (nothing should break).
7. **Responsive:** try 320, 375, 390, 430 px widths, tablet, desktop, portrait and landscape. There must be no sideways scrolling.
8. **Reduced motion:** turn on "Reduce motion" in your device settings: animations shorten and everything still works.

## Notes

- Stages can only happen in order: Puzzle → Question → Tulip Reveal → Closed Scroll → Opening Scroll → Letter. This is enforced in `script.js` by `goTo()`.
- Google Fonts are optional. Offline, Georgia and system fonts are used instead.
- Colours live at the top of `style.css` under `:root`.
