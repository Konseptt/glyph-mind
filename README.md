# GLYPHMIND

**GLYPHMIND** is a browser-based **3D corridor** task that combines a **visual N-back** memory challenge with **Egyptian hieroglyph** stimuli. It is styled for **cognitive training and research** (including study metadata fields such as **tDCS condition** and **session phase**).

The entire experience ships as a **single `index.html` file** (HTML, CSS, and JavaScript) with **Three.js** loaded from a CDN—no build step or package install required.

---

## What you do in the game

1. **Walk** down a torch-lit corridor. **Paintings** on the walls stay blank until you get close; then each reveals **one hieroglyph** at a time, in order.
2. The first **N** paintings are **warm-up** (observe only). After that, you decide whether the **current** glyph matches the glyph **N steps back** in the sequence (classic N-back comparison).
3. This build uses a **single-target (“one-shot”) rule per run**: there is **exactly one** true N-back match among the scored paintings. **Shoot that painting** (click while aiming, or **Space** / **F**) to **win** the run; **shoot a non-match** to lose; if you reveal all paintings and **do not shoot** within the grace period, the run ends as **no response**.
4. **Win** → **N** increases for the next run. **Lose or timeout** → you can retry at the same **N** (or adjust **N** from the pause menu).

Corridor length scales with **N + 6** paintings per run, with **one** controlled match position per sequence.

---

## Running locally

1. Clone or download this repository.
2. Open **`index.html`** in a **modern desktop browser** (Chrome, Firefox, Safari, Edge).

For the most reliable **pointer lock** and font loading, serving the folder over **HTTP** is recommended:

```bash
# Example: Python 3
python3 -m http.server 8080
# Then visit http://localhost:8080
```

On **mobile**, the page can request fullscreen / landscape where supported; touch controls are provided for movement and shooting.

---

## Controls

| Action | Desktop | Notes |
|--------|---------|--------|
| Move | **W A S D** or arrow keys | **Shift** = sprint |
| Look | **Mouse** (after pointer lock) | Click the canvas or use the on-screen hint to lock |
| Shoot | **Left click** (when locked) or **Space** / **F** | Raycast must hit a **revealed** painting |
| Pause | **Esc** | Opens pause menu; Esc again cycles accessibility submenu / resume where applicable |

**Touch:** joystick for movement, drag to look, tap to shoot (see in-game tutorial).

---

## Research metadata and data export

On the **title screen** you can set:

- **Participant ID** and **Session ID**
- **Condition:** tDCS, Sham, or Control  
- **Phase:** Pre, During (stored as `during_stimulation`), or Post  

During a session, **Pause → Export CSV** downloads a UTF-8 CSV containing:

- One **trial row per completed run** (outcomes, reaction time when applicable, stimulus/target IDs, block index, timestamps, etc.)
- A trailing **commented summary** section (counts, task accuracy, session duration, paradigm notes)

**Session vs blocks:** Starting from the title screen or using **Restart (N=1)** begins a **new session** (trials cleared). **Run Again** and **Start at this N** advance the **block** counter while **keeping accumulated trial rows** so one export can cover multiple runs.

---

## Stimuli

Glyphs are drawn from the Unicode **Egyptian Hieroglyphs** block and rendered with **Noto Sans Egyptian Hieroglyphs** (Google Fonts). The task uses **12** fixed signs. In **CSV exports**, `stimulus` / `target` use the **Gardiner list IDs** below (`D010`, `D021`, …); `stimulus_unicode_hex` / `target_unicode_hex` give the code points.

### Symbols used in the game

| # | Glyph | Unicode | Gardiner ID | Description |
|---|:-----:|---------|-------------|-------------|
| 1 | 𓂀 | U+13080 | D010 | Eye (D10) |
| 2 | 𓂋 | U+1308B | D021 | Mouth (D21) |
| 3 | 𓂝 | U+1309D | D036 | Hand (D36) |
| 4 | 𓅓 | U+13153 | G017 | Owl (G17) |
| 5 | 𓆄 | U+13184 | H006 | Feather (H6) |
| 6 | 𓆑 | U+13191 | I009 | Horned viper (I9) |
| 7 | 𓆓 | U+13193 | I010 | Cobra (I10) |
| 8 | 𓈖 | U+13216 | N035 | Water (N35) |
| 9 | 𓇼 | U+131FC | N014 | Star (N14) |
| 10 | 𓏏 | U+133CF | X001 | Loaf (X1) |
| 11 | 𓇳 | U+131F3 | N005 | Sun (N5) |
| 12 | 𓊽 | U+132BD | R011 | Djed pillar (R11) |

If the **Glyph** column appears as empty boxes, install a font that covers Egyptian Hieroglyphs or view this file on GitHub (which bundles suitable fonts for many viewers).

---

## Accessibility (Pause → Accessibility)

- High contrast  
- HUD glyph labels (Gardiner IDs)  
- Larger crosshair  
- Lower mouse sensitivity  
- Mute sounds  
- Longer post-reveal glow on paintings  

---

## Tech stack

- **Three.js r128** (WebGL), loaded from CDN  
- **Web Audio API** — synthesized UI/shoot feedback (no audio files)  
- **Pointer Lock API** — first-person look on desktop  
- Procedural **canvas-generated** textures (stone, wood, metal, bump maps) for the corridor and weapon  

---

## File layout

| File | Role |
|------|------|
| `index.html` | Full application: markup, styles, game logic, research export |

---

## Credits and use

GLYPHMIND is presented as **DLPFC-oriented N-back cognitive training** in the UI copy. Hieroglyph identities follow standard Egyptological **Gardiner** numbering; font coverage depends on **Noto Sans Egyptian Hieroglyphs** loading correctly.

If you use this task in a publication, cite your study protocol, stimulus set version, and any changes you make to `index.html`.

---

## License

No license file is included in this repository by default. Add a `LICENSE` file if you intend to distribute or modify the project under explicit terms.
