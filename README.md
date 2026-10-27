# MDotion website

The public page for [MDotion](https://github.com/MDotion/mdotion), the visual Markdown editor for VS Code and Cursor.

A static [Astro](https://astro.build) site with no client framework: the only JavaScript is the small script behind the interactive editor demo in the hero and the copy button.

## Development

Requires Node.js 22 (see `.nvmrc`).

```sh
npm install
npm run dev      # http://localhost:4321
npm run build    # static output in dist/
npm run preview
```

## Structure

| Path | What |
|---|---|
| `src/pages/index.astro` | The page, assembled from the sections below |
| `src/components/EditorDemo.astro` | Live mock of the editor: Visual / Markdown toggle, to-dos that rewrite the source |
| `src/components/*.astro` | Header, hero, diff, features, install, FAQ, footer |
| `src/styles/global.css` | Tokens (colour, type, easing), base styles, buttons |
| `src/links.ts` | Store, repository and install links |
| `public/` | Favicons, Open Graph image, robots.txt |
| `scripts/og.html` | Source of `public/og.png` |

The editor mock uses the product's own palette (copied from `webview/src/styles/notion.css` in the extension repo); the rest of the page uses the brand ink `#0F1419`. Brand assets come from `assets/` in the extension repo.

### Motion

Motion follows Emil Kowalski's [design engineering skills](https://github.com/emilkowalski/skills): strong custom ease-out / ease-in-out curves, only `transform`, `opacity`, `filter` and `clip-path` animated, UI transitions under 300 ms, `:active` press feedback, hover effects gated behind `(hover: hover) and (pointer: fine)`, and a gentler variant under `prefers-reduced-motion`.

### Open Graph image

`public/og.png` is a 1200×630 screenshot of `scripts/og.html`:

```sh
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --hide-scrollbars \
  --force-device-scale-factor=1 --window-size=1200,630 \
  --screenshot=public/og.png "file://$PWD/scripts/og.html"
```

## Deployment

Every push to `main` builds the site and publishes it to GitHub Pages (`.github/workflows/deploy.yml`). `SITE` and `BASE_PATH` come from the Pages configuration, so the same build works under `mdotion.github.io/<repo>` and on a custom domain. Enable it once in **Settings → Pages → Source: GitHub Actions**.

## License

The code of this site is released under the MIT License. The MDotion name and logo identify the project and are not covered by it.
