# wipe-in website

Landing page for **WIPE IN**, an 8-day surf life experience for entrepreneurs and business leaders in southern Morocco (26 Sept – 3 Oct 2026, max 7 participants). Hosted at **wipe-in.com** via GitHub Pages.

## Repository

- Remote: `git@github.com:alandergent/wipe-in.git`
- Visibility: Public
- Live URL: https://wipe-in.com

## Tech Stack

Single `index.html` file (~1,848 lines) with inline CSS and vanilla JavaScript. No framework, no build step, no package manager.

## Development

Start the local dev server (configured in `.claude/launch.json`):

```bash
npx serve -l 3456 .
```

Preview at `http://localhost:3456`.

## Deployment

Push to `main` → live within ~1 minute via GitHub Pages.

```bash
git add index.html          # always include index.html
git add images/new-image.jpg  # include any new/changed images in the same commit
git commit -m "Short description"
git push
```

Check deployment status:

```bash
gh api repos/alandergent/wipe-in/pages
# look for "status": "built"
```

## Language

Primary language is **Dutch (nl)**. English content is wired up via `data-lang` attributes on elements and is ready to activate, but the site is currently Dutch-only.

## Images & Assets

Images are locally hosted in `images/`. Only optimised web versions are committed to git. Full-resolution originals are archived in `files/wipe-in/images/` on iCloud Drive (not committed).

When adding or replacing images:
1. Optimise the image for web first (see `workflow_website-image-optimisation_EN.md` in `my-business/workflows/`)
2. Place the optimised file in `images/`
3. Commit the image and the updated `index.html` together — never one without the other

Background audio: `images/ocean.mp3` (plays in hero section).

## Page Structure

The page is one long `index.html`. Key sections (in order):

1. **Hero** — ocean/surfer imagery, headline, primary CTA
2. **Experience** — dates, location, programme, prerequisites
3. **Value proposition** — what makes WIPE IN different
4. **Interviews / testimonials** — quotes from target market and alternative market voices (source files in `interviews/`)
5. **Selection process** — how participants are chosen, intake flow
6. **FAQ** — with schema.org `FAQPage` structured data for SEO

### Section-header convention

Every section header uses the same two-part pattern: a short `section-header__eyebrow` label on top, and a longer descriptive `h2` below. Keep this order consistent across all sections. Example: `#traject` uses eyebrow "Het traject" with h2 "Drie stappen, één beweging"; `#themas` uses eyebrow "Het inhoudelijke programma" with h2 "Surfen als metafoor voor ondernemen".

### `#themas` (programme content) layout

The programme-content body (`.themes__body`) matches the `#traject` section: full container width, left-aligned text, no centered narrow column. This keeps the theme topics on a single line each and improves readability. Do not reintroduce a narrow `max-width` wrapper or center-align the themes list. Scoped overrides live in the `<style>` block: `#themas .themes__body`, `#themas .themes__list`, `#themas .science__closing`. Changed 2026-07-12.

## SEO

- `schema.org FAQPage` structured data is embedded directly in `index.html` — keep it in sync when FAQ content changes
- Meta tags and Open Graph tags are in `<head>`
- `sitemap.xml` covers the homepage only

## robots.txt

The `robots.txt` explicitly blocks AI training crawlers (ClaudeBot, GPTBot, PerplexityBot, and others). **Do not remove or relax these rules.** Search engine crawlers (Googlebot, Bingbot) are allowed.

## Brand

- Always write the brand name as **WIPE IN** (all caps, space) — never "Wipe In" or "Wipe-In".
- **Never let "WIPE IN" break across two lines.** Always use a non-breaking space between the words in copy: `WIPE&nbsp;IN`. This keeps the brand together; if it doesn't fit, the whole "WIPE IN" wraps to the next line as a unit.
- Do not use em dashes (—) in copy. Use a comma or restructure the sentence.

## Interviews

Raw interview files live in `interviews/`. These are the user research recordings and transcripts that feed the testimonials section. Summaries and analysis belong in `my-business/projects/wipe-in/00_user_research/`.

## DNS (Combell)

| Type | Name | Value |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `alandergent.github.io` |

## Related Repositories

- `my-business/` — strategy docs, project files, deployment workflow (`workflows/workflow_wipe-in-website-deployment_EN.md`)
- `alandergent.github.io/` — personal portfolio that links to WIPE IN
