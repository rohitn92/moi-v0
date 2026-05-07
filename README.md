# Musicology of India

A digital edition of Pandit Vishnu Narayan Bhatkhande's foundational work on Hindustani classical music theory, published as a static GitHub Pages site at [musicologyofindia.com](https://www.musicologyofindia.com).

---

## Project Structure

```
/
├── index.html              # Single-page app — all CSS and JS lives here
├── books/
│   └── part1/
│       ├── chapters.json   # Chapter index for Part I
│       ├── chapters/       # Markdown files (chapter1.md … chapter20.md)
│       └── images/         # Images referenced by chapters
└── README.md
```

Additional parts (`part2/`, `part3/`, `part4/`) follow the same structure under `books/`.

---

## Adding Content

### Images

Place image files in `books/partN/images/` and reference them in markdown using a root-absolute path:

```markdown
![Alt text](/books/part1/images/filename.png)
```

Do **not** use relative paths — the browser resolves paths against `index.html`, not the markdown file.

---

## Notation Formatting

All notation rendering is handled by a post-processor in `index.html`. Markdown files use plain-text conventions only — no HTML in `.md` files.

### Note Modifiers

Applied to individual notes (`Sa Re Ga Ma Pa Dha Ni`):

| Markdown | Meaning | Renders as |
|---|---|---|
| `Re_` | Komal (flat) | underline below the note |
| `Sa.` | Mandra (lower octave) | dot below the note |
| `'Sa` | Tara (upper octave) | dot above the note |
| `Ma'` | Teevra (sharp) | vertical line above the note |

> Note: The Tara (`'Sa`) and Teevra (`Ma'`) conventions use single quotes. The post-processor uses lookahead/lookbehind guards to distinguish these from prose quotation marks.

### Phrase Notations

Applied to groups of notes to indicate ornamentation or rhythmic grouping:

| Syntax | Class | Renders as |
|---|---|---|
| `{Ga Ma Pa}` | `.meend` | arc above |
| `{v:Ga Ma Pa}` | `.soot` | arc below |
| `{vv:Ga Ma Pa}` | `.soot-double` | double arc below |
| `{-:Ga Ma Pa}` | `.toda` | dashed bracket below |
| `[Ma]Pa` | `.kan` | Ma as small superscript grace note before Pa |

These can contain any note text, including modifiers. Curly braces have no special meaning in Markdown so they pass through `marked.js` untouched.

**Meaning of each:**
- **Meend** — graceful glide between notes without breaking continuity of sound (arc above)
- **Soot / Ghaseet** — smooth glide over notes in one bow or finger action (arc below)
- **Soot Double** — double-arc variant indicating a specific ornamental stroke
- **Toda grouping** — dashed bracket marking a rhythmic cluster played as one unit

---

## Tech Stack

- Pure HTML + vanilla JS
- [marked.js](https://marked.js.org/) via CDN for Markdown parsing
- [Tailwind CSS](https://tailwindcss.com/) via CDN for layout
- No build step — GitHub Pages serves the `gh-pages` branch directly
