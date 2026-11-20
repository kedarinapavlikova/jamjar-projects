# CLAUDE.md: instructions for agents working on jamjar projects

## Purpose

jamjar projects is Keddy's platform for **connecting her ideas with people**, and for **people to reach her easily**. Every change should make one of those two things easier. If a change does neither, question it before building it.

## Who you're working with

- **Keddy (Keds):** Senior PM, barre teacher, app builder. No coding background.
- Never assume she can run a script or use a terminal. Do the technical work yourself, or offer a no-code / GUI route.
- Keep updates short: lead with the ask, use bullets, give multiple-choice options.
- Push back when a request works against accessibility, performance, security, or the site's purpose.

## Repo map

| File | What it is |
| --- | --- |
| `index.html` | The live site. A self-contained bundle exported from the "jamjar website" Claude Design artifact. Fonts and images are packed inside. |
| `README.md` | Public overview of the project. |
| `CLAUDE.md` | This file. |

**Source of truth:** this repo. `index.html` started as an export from the "jamjar website" Claude Design artifact, but it has been edited since (talks, writing card, privacy fixes). **Never re-export from the artifact over `index.html`**; that would wipe those changes. Edit `index.html` directly: its page content lives in the JSON string inside `<script type="__bundler/template">`. Parse it, change only what you need, and re-serialize with `</` escaped as `<\u002F`.

## Non-negotiables

### ♿ Accessible (WCAG 2.2 AA minimum)
- Text contrast at least **4.5:1** (3:1 for large text and UI elements). Keddy loves neon; keep neon for backgrounds and accents, never for small text on white.
- Every interactive element works by keyboard and has a visible focus style.
- Keep the skip link, landmark elements (`header`, `nav`, `main`, `footer`), and one `h1`.
- Every image gets meaningful `alt` text; decorative SVGs get `aria-hidden="true"`.
- Form fields keep visible `<label>`s and correct `autocomplete` values.
- Touch targets at least 44 × 44 px.
- Respect `prefers-reduced-motion` for any animation you add.

### ⚡ Performant
- No frameworks, build tools, or new JS libraries without Keddy's OK.
- Compress images before adding them (WebP or AVIF, under ~200 KB each).
- Keep the total page weight as low as possible; flag it if `index.html` grows past ~1 MB.
- No third-party scripts beyond Google Fonts and Web3Forms. YouTube talks embed via youtube-nocookie with `loading="lazy"`; keep it that way.

### 🔒 Secure and private
- Never commit secrets, API keys, tokens, or `.env` files. (The Web3Forms access key is public by design; that's fine.)
- No analytics, ad pixels, or trackers without Keddy's explicit OK, and update the privacy policy if anything changes.
- External links to other sites open safely (`rel="noopener"` when using `target="_blank"`).
- The privacy policy must match reality. If hosting, forms, or data handling change, update it in the same commit.

### 💖 On brand
- Palette: bubblegum pink, butter yellow, pool teal accents, blackberry ink (`#2A1033`) for text. Minimal dark "grape". No beige or cream.
- Type: Fraunces (WONK off), lowercase upright titles; italic only for subheads and emphasis. Instrument Sans for body.
- Voice: playful, punchy, warm, credible. Short sentences. **No em dashes.** No passive voice. No "utilize" or "leverage".

## How to make a change

1. Read the relevant part of `index.html` before editing.
2. Make the smallest change that does the job.
3. Check it against every non-negotiable above.
4. Commit with a clear, plain message (e.g. `Add new project card for X`).
5. Push to `main`. Tell Keddy what changed in one or two lines.

## Known to-dos

- [x] Privacy policy now says Netlify (was Vercel) and covers YouTube embeds.
- [x] Netlify is linked to this repo: every push to `main` deploys to jamjarprojects.netlify.app automatically. No build command; publishes the repo root.
