# bcm-portal

Static landing page at bcm.thejumpstreet.com that links to the three BCM apps: Dashboard, Mobile, and Plans & Permits.

## Stack

- Plain HTML, one file. No framework, no build step, no dependencies, no `package.json`, no `node_modules`.
- CSS is a single inline `<style>` block in `index.html`.
- No JavaScript, no Supabase client, no env vars. The portal only links out; it reads no data.

## Commands

There are none — no dev server, no build, no typecheck, no lint, no tests. To see a change, open `index.html` in a browser, or push and check the Vercel deploy.

## Layout

- `index.html` — the entire site: `<head>` meta + inline CSS, then a header, a 3-card `.grid`, and a footer.
- `bcm-logo.png` — the logo, also used as the favicon (`/bcm-logo.png`).
- `vercel.json` — `framework: null`, `buildCommand: null`, `outputDirectory: "."`. This pin is required; without it Vercel guesses the framework and the site 404s.
- `.gitignore` — ignores `.DS_Store`, `.vercel`, `.env*`, `node_modules`.
- `.vercel/` — local Vercel project link, gitignored.

## Conventions

- Colors are CSS custom properties on `:root` (`--bg`, `--panel`, `--border`, `--text`, `--text-dim`, `--text-faint`, `--accent`). Use the tokens; do not hardcode hex values in rules.
- Dark theme only — one fixed palette, no light mode and no `prefers-color-scheme` handling.
- Class names are short and flat: `.page`, `.header`, `.logo`, `.tagline`, `.grid`, `.card`, `.icon`, `.url`.
- Each app is one `<a class="card">` containing an inline SVG icon (24x24 viewBox, `stroke="currentColor"`, `stroke-width="2"`), an `<h2>` name, a one-line `<p>` description, and a `<span class="url">` with the bare hostname. Add a new app by copying that block.
- Icons are inline stroke SVGs marked `aria-hidden="true"`; no icon library.
- Mobile-first: the grid is one column, and a single `@media (min-width: 720px)` switches it to three.
- Formatting follows Prettier defaults (2-space indent, double-quoted attributes) even though Prettier is not installed here.
- App links are absolute `https://` URLs to each app's own domain; the apps are separate repos and deploys.
- No migrations here — this repo reads no data.

## Deploy

Push `main` → Vercel project `bcm-portal` → https://bcm.thejumpstreet.com. Files are served as-is from the repo root; there is no build. `main` only moves by shipping staging — see `.claude/rules/cto-workflow.md`.
