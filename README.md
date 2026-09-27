# Polyglot Studio Pro

**Polyglot Studio Pro** is a fully client-side, multi-language code playground in a single HTML file. Three Monaco-powered editor panes (markup, styles, script) render a live iframe preview, while Python runs right in the browser via Pyodide. No backend, no build step, no login — just open it and code.

## What it does

- **Triple editor panes** — markup pane (HTML or Markdown), style pane (CSS or SCSS), script pane (JavaScript, TypeScript, JSX, or Python) — all powered by the Monaco editor (the engine behind VS Code)
- **Live preview** — the iframe updates as you type, with a resizable split layout
- **Python in the browser** — Pyodide (CPython compiled to WebAssembly) executes Python snippets and prints to a built-in console
- **In-browser compilation** — TypeScript and JSX are transpiled with the TypeScript compiler / Babel, Markdown with Marked, SCSS with Sass.js
- **Built-in console + command prompt panel** — run quick commands and inspect output
- **Snippet manager** — save, organize, and reuse code snippets (persisted in `localStorage`)
- **Shareable projects** — share button encodes the project into a URL (LZ-String compressed) so a project can be opened from a link
- **Download** — export your project as a ZIP (JSZip)
- **AI code explanations** — "AI: Explain Code" button calls the Gemini API to explain the selected code *(requires your own API key — see Environment variables)*
- **Dark / light themes** — toggle with `Ctrl+K`, preference saved in `localStorage`
- Keyboard shortcuts: `Ctrl+`` toggles the command prompt, `Ctrl+K` toggles the theme

## Tech stack

All via CDN — nothing to install:

| Library | Purpose |
|---|---|
| Monaco Editor 0.33.0 | Code editing |
| Pyodide 0.25.0 | Python in the browser |
| Babel standalone 7.23.4 | JSX / JS transpiling |
| TypeScript 5.3.3 (CDN) | TS transpiling |
| Marked 4.2.12 | Markdown → HTML |
| Sass.js 0.11.1 | SCSS → CSS |
| JSZip 3.10.1 | Project download as ZIP |
| LZ-String 1.4.4 | URL share-link compression |
| Google Fonts (Inter, Roboto Mono) | Typography |

## Quick start

No dependencies to install. Either:

1. Open `index.html` directly in a browser, **or**
2. Serve it (recommended, some CDN features behave better over HTTP):
   ```bash
   npx serve .
   # or
   python3 -m http.server 8080
   ```

Then open http://localhost:8080 (or 3000).

## Project structure

```
Polyglot-Studio-Enhanced-unread/
└── index.html   # the entire app — markup, styles, and JavaScript
```

## Environment variables

None are needed to run the app itself. The **"AI: Explain Code"** feature calls Google's Gemini API and expects an API key: open `index.html`, find the `apiKey` variable near the Gemini `generateContent` call (line ~701), and paste in your own key:

```js
const apiKey = ""; // Leave empty, will be handled by the environment
```

Without a key, everything else in the app works fine.

## Deployment notes

Pure static single file — deploy `index.html` to any static host (GitHub Pages, Cloudflare Pages, Netlify). Needs internet access at runtime for the CDN libraries and Google Fonts.

---

Built by Girish Lade — https://ladestack.in
