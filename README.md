# Password Generator

**[Live Demo →](https://mahtxx.github.io/password-generator/)**

A sleek, dark-themed password generator with a real-time strength meter. Built with pure HTML, CSS, and JavaScript — no dependencies, no backend, runs entirely in your browser.

![Password Generator](https://img.shields.io/badge/HTML-CSS-JS-purple?style=flat-square) ![Live](https://img.shields.io/badge/Live-GitHub%20Pages-brightgreen?style=flat-square) ![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)

---

## Features

- **Adjustable length** — slider from 6 to 64 characters
- **Character type toggles** — Uppercase, Lowercase, Numbers, Symbols
- **Real-time strength meter** — scores Weak / Fair / Good / Strong
- **One-click copy** — copies to clipboard instantly
- **Password history** — keeps your last 5 generated passwords
- **Cryptographically secure** — uses `crypto.getRandomValues()`, not `Math.random()`

---

## How to Use

1. Open `index.html` in any browser — or visit the live GitHub Pages link
2. Adjust the **length slider** to your desired password length
3. Toggle which **character types** to include
4. Click **Generate Password**
5. Click the **copy icon** to copy it to your clipboard

---

## How to Customize

All customization lives inside `index.html`. No build tools needed — just open the file and edit.

### Change the color theme

Find the `:root` block near the top of the `<style>` tag:

```css
:root {
  --bg: #07070f;           /* page background */
  --surface: #0f0f1c;      /* card background */
  --surface2: #181828;     /* input/toggle background */
  --accent: #7c3aed;       /* purple accent (buttons, slider) */
  --accent2: #3b82f6;      /* blue accent */
  --text: #e4e4f0;         /* main text color */
  --muted: #64648a;        /* secondary text color */
}
```

Swap `--accent` and `--accent2` to any colors you like.

### Change the default password length

Find the slider element and change `value="16"`:

```html
<input type="range" id="lenSlider" min="6" max="64" value="16">
```

Set `value` to whatever default length you want. Change `max` to allow longer passwords.

### Add or change the symbol set

In the `<script>` block, find the `CHARS` object:

```js
const CHARS = {
  upper:   'ABCDEFGHIJKLMNOPQRSTUVWXYZ',
  lower:   'abcdefghijklmnopqrstuvwxyz',
  numbers: '0123456789',
  symbols: '!@#$%^&*()_+-=[]{}|;:,.<>?'
};
```

Add, remove, or replace characters in the `symbols` string to match what a specific site allows.

### Change how strength is scored

In the `updateStrength` function, adjust the point values:

```js
if (pw.length >= 8)  score += 10;
if (pw.length >= 12) score += 15;
if (pw.length >= 16) score += 15;
if (pw.length >= 24) score += 10;
if (/[A-Z]/.test(pw))        score += 15;
if (/[a-z]/.test(pw))        score += 10;
if (/[0-9]/.test(pw))        score += 15;
if (/[^A-Za-z0-9]/.test(pw)) score += 20;
```

And the thresholds for the labels:

```js
if (score < 30)      { label = 'Weak';   color = '#ef4444'; }
else if (score < 55) { label = 'Fair';   color = '#f59e0b'; }
else if (score < 80) { label = 'Good';   color = '#3b82f6'; }
else                 { label = 'Strong'; color = '#10b981'; }
```

### Change how many passwords are stored in history

Find this line and change the number:

```js
if (history.length > 5) history.pop();
```

---

## Tech Stack

| Layer | Tech |
|-------|------|
| Structure | HTML5 |
| Styling | CSS3 (custom properties, grid, flexbox) |
| Logic | Vanilla JavaScript |
| Randomness | Web Crypto API (`crypto.getRandomValues`) |
| Font | Inter + JetBrains Mono (Google Fonts) |

---

## License

MIT — free to use, modify, and distribute.
