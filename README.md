# alexandrepd.github.io

Personal portfolio with a **hacker / Matrix** aesthetic.

Live: https://alexandrepd.github.io

Pure HTML + CSS + JavaScript. **No build step, no dependencies, no framework.** Just open `index.html` in a browser.

---

## Highlights

- Matrix rain background on a full-screen `<canvas>`
- CRT effect: scanlines, subtle flicker, vignette
- Glitch title with RGB split (pure CSS)
- Typewriter tagline that loops through phrases
- Live UTC clock and session uptime
- **Interactive terminal** with command history (↑/↓), `Ctrl+L` to clear, and a small set of real commands
- Konami code easter egg (`↑ ↑ ↓ ↓ ← → ← → B A`)
- Fully responsive, mobile-friendly
- Only external resource is Google Fonts

---

## Project structure

```
alexandrepd.github.io/
├── index.html      # everything: HTML, CSS, JS in one file
└── README.md
```

Yes, a single file. That's deliberate — the site is small, has no build pipeline, and GitHub Pages can serve it as-is.

---

## How it's built

### 1. Layout & theme

The page is divided into:

- **Top bar** — status line with a pulsing dot, "connection" string, live UTC clock and uptime
- **Hero** — ASCII-art name, glitch heading, typewriter tagline, meta chips, CTA buttons
- **`whoami`** — short bio
- **`cat stack.json`** — tech stack as grouped badge cards
- **`tail -f experience.log`** — vertical timeline of roles
- **`ls certifications/`** — grid of certifications
- **`./contact.sh`** — interactive terminal

All sections share a common card style (`<section>`): green border, dark translucent background, soft inner glow.

Colors are defined as CSS custom properties at the top of the `<style>` block — change them in one place to re-theme:

```css
:root{
  --bg:#000;
  --green:#00ff66;
  --green-dim:#0a8a3a;
  --amber:#ffb000;
  --magenta:#ff2bd6;
  --cyan:#00e0ff;
  /* ... */
}
```

### 2. Matrix rain (`<canvas>`)

A fixed full-screen `<canvas id="matrix">` sits behind everything at z-index 0.

The algorithm is the classic one:

1. On each frame, paint a slightly transparent black rectangle over the whole canvas (`rgba(0,0,0,0.08)`). This creates the **trail / fade** effect without clearing the previous frame.
2. For every column, pick a random katakana / digit / symbol and draw it at the current `drops[i]` Y position.
3. The first character is drawn brighter (almost white) — that's the **head** of the trail. The previous one is repainted in classic Matrix green.
4. Increment `drops[i]` by a fraction of the font size. When the drop goes past the bottom, randomly reset to 0 so columns desync.

It uses `requestAnimationFrame` and is sized with `devicePixelRatio` so it stays crisp on retina screens.

### 3. CRT + glitch effects (pure CSS)

- **Scanlines** — a `body::before` with `repeating-linear-gradient` overlaid using `mix-blend-mode: overlay`.
- **Vignette** — `body::after` with a radial gradient darkening the corners.
- **Flicker** — a low-amplitude `opacity` keyframe animation on `<main>`.
- **Glitch title** — the `h1.glitch` has its text duplicated via `::before` and `::after` pseudo-elements (using `content: attr(data-text)`). Each pseudo is offset a few pixels in magenta and cyan, clipped to a horizontal slice with `clip-path`, and animated independently. The result is the chromatic-aberration / glitch look.

### 4. Typewriter tagline

A tiny state machine with two phases (`deleting = false / true`), an array of phrases, and `setTimeout` to schedule the next character. Pauses 1.8 s at the end of each phrase before starting to delete.

### 5. Live clock and uptime

`setInterval(tick, 1000)` updates two spans: current UTC time and elapsed time since page load (`Date.now() - start`).

### 6. Interactive terminal

The terminal is a `<div class="term-body">` with a single `<input>` at the bottom. The shell logic:

- A `commands` object maps command names to functions returning an array of output lines.
- On `Enter`, the input is echoed as a fake prompt line, then the command function is invoked with the parsed `args`.
- `↑ / ↓` walk through a `history` array. `Ctrl+L` runs `clear`.
- `escapeHtml` sanitizes any text echoed back from user input to prevent injecting markup.
- Clicking anywhere inside the terminal re-focuses the input.

Available commands:

```
help · about · skills · experience · education · languages
contact · social · repos · whoami · date · echo <txt>
ls · cat <name> · matrix · sudo · clear · exit
```

### 7. Konami code easter egg

A keyboard listener tracks the canonical sequence (`↑ ↑ ↓ ↓ ← → ← → B A`). On match: full-screen green flash + a random `hue-rotate()` on the whole body.

### 8. Scroll behavior

A small script at the top of the body runs before the rest:

```html
<script>
  if ('scrollRestoration' in history) history.scrollRestoration = 'manual';
  window.addEventListener('load', () => window.scrollTo(0, 0));
</script>
```

This disables the browser's automatic scroll restoration and forces the page to start at the top on every load. (Originally the terminal `<input>` had `autofocus`, which caused the browser to scroll directly to it on load — that was removed.)

### 9. Accessibility & responsiveness

- All images are SVG / CSS art or `aria-hidden` ASCII blocks.
- The terminal input has `aria-label="terminal input"`.
- A `@media (max-width:640px)` block adjusts ASCII size, hides the right side of the top bar, and tightens hero padding.

---

## Local preview

No build needed. Any static server works:

```powershell
# Python
python -m http.server 8080

# Node
npx serve .

# or just open the file directly
start index.html
```

Then visit http://localhost:8080.

---

## Deployment

The repo `alexandrepd/alexandrepd.github.io` is a **GitHub Pages user site** — every push to `main` is published automatically at https://alexandrepd.github.io. No Actions workflow needed.

Workflow used while building this:

1. `git checkout -b feature/matrix-portfolio`
2. Commit changes
3. Open a Pull Request into `main`
4. Merge → GitHub Pages auto-deploys

---

## Credits

- Fonts: [JetBrains Mono](https://www.jetbrains.com/lp/mono/) + [VT323](https://fonts.google.com/specimen/VT323) via Google Fonts
- Inspiration: every "Matrix code rain" tutorial ever, plus `cmatrix`
- Built with `<3` and a lot of `console.log`

---

## License

MIT — feel free to fork and remix.
