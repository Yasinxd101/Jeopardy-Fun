# Test boards

## everything-test-board.json

A 6 × 6 board (36 questions) written to exercise every feature and edge case
the app supports at once, so a single play-through covers the lot.

Import it with **Make your own board → ⋮ → Import**, or drop it in the board
maker's import field. It lands in **My Boards**.

### What each category is for

| Category | What it exercises |
|---|---|
| **First Lines** | Plain text questions, long quotations, curly quotes, `note` and `hint` fields |
| **Pictures & Places** | `img` and `aimg` — one embedded data URI that always renders, one real remote URL, and one deliberately broken URL to prove a missing picture fails quietly instead of crashing |
| **Play That Clip** | YouTube `id` clips with `clipStart` / `clipLen` cue points, a clip **with no written question at all** (legal, and easy to break), and one question carrying a clip *and* a picture together |
| **Awkward Characters** | HTML escaping (`& < > " '`), emoji and mixed scripts (日本語, العربية, Русский, Ελληνικά), a very long question, a one-word question, non-breaking spaces, and three unbroken words wider than a phone screen |
| **Screen Time** | Ordinary questions, as a control group |
| **Small Numbers** | Short answers, numeric answers |

### Other things it covers

- **A non-standard grid.** 6 × 6 rather than 5 × 5, so it exercises the
  variable board size rather than the old fixed shape.
- **A custom value ladder** — 150 / 300 / 450 / 600 / 750 / 1000, not the
  default 100–500.
- **Board-level fields**: `name`, `tagline`, `accent`, `icon`, `art` (a cover
  image), `adult: false`.
- **Final Jeopardy** with all three fields filled.

### Worth watching for while you play

- Host **hints** must never appear on the shared screen — only on Host Control.
- **Answers** must not be visible before you tap Reveal.
- **Notes** should appear with the answer, after the reveal.
- The **broken picture** (Pictures & Places, 450) should show a dashed
  placeholder, not a gap or an error.
- The **clip-only question** (Play That Clip, 150) has no text by design.
- The **long-word question** (Awkward Characters, 1000) should wrap rather
  than push the page sideways.

### Verified before shipping

Imported through the app's own validator and played end to end: all 36
questions opened, revealed, scored and closed with no errors; no answer or
host hint leaked early; every note appeared after its reveal; the board
cleared through to Final Jeopardy. The escaping test renders `<b>not bold</b>`
as literal text with zero elements created.

Two things depend on the outside world and are not guaranteed: the remote
Wikimedia picture, and whether YouTube permits embedding that clip in your
region. Everything else is self-contained.
