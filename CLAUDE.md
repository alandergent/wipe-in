# wipe-in website

Landing page for **WIPE IN**, a surf life experience for entrepreneurs and business leaders in southern Morocco (current edition and format: see Editions). Hosted at **wipe-in.com** via GitHub Pages.

## Editions (as of 2026-11-18)

The `#praktisch` section shows one edition tab:
- The Zeeland weekend (14-17 May 2027) moved to Wipeouts (wipeouts.be / Luma); it is no longer on this site.
- **Founders edition** (single tab): Southern Morocco, Wed 29 Sep to Sun 3 Oct 2027, communicated as 4 days on site/4 nights, max. 8 participants, shared flight Brussels to Agadir (flights not included), early bird €4.500–€4.900 until 31 March 2027, regular €5.000–€5.400.

Accommodation is deliberately kept generic on the page; the actual venues are NOT named on the public site or in this public repo. The `Event` JSON-LD points to the Founders edition (2027-09-29 to 2027-10-03, from €4500); update it when the priced edition changes. Programme details (day structure, rituals) are not on the page yet: pending feedback from the TRD course.

## Repository

- Remote: `git@github.com:alandergent/wipe-in.git`
- Visibility: Public
- Live URL: https://wipe-in.com

## Tech Stack

Single `index.html` file with inline CSS and vanilla JavaScript. No framework, no build step, no package manager.

## Development

Start the local dev server (configured in `.claude/launch.json`):

```bash
npx serve -l 3456 .
```

Preview at `http://localhost:3456`.

## Deployment

Push to `main` → live within ~1 minute via GitHub Pages. Always commit new or changed images together with the updated `index.html`, never one without the other. Full process: `my-business/workflows/workflow_wipe-in-website-deployment_EN.md`.

```bash
git add index.html
git add images/new-image.jpg
git commit -m "Short description"
git push
```

Check deployment status:

```bash
gh api repos/alandergent/wipe-in/pages
# look for "status": "built"
```

## Language

Primary language is **Dutch (nl)**. The **EN/FR language toggle is live**: every translatable element carries `data-nl`, `data-en` and `data-fr` (`switchLang` swaps the content), and the JS `titles` and `descriptions` objects hold nl/en/fr versions. **Whenever copy changes in any language (NL, EN or FR), update the other two in the same edit** so all three stay aligned. For French, follow the "vanuit"/"depuis" rule in `my-business/CLAUDE.md`.

## Images & Assets

Images are locally hosted in `images/`. Only optimised web versions are committed to git. Full-resolution originals are archived in `my-business/files/wipe-in/images/` (not in this repo).

When adding or replacing images, optimise them for web first (see `my-business/workflows/workflow_website-image-optimisation_EN.md`), then place the optimised file in `images/`.

Background audio: `images/ocean.mp3` (plays in hero section).

## Page Structure

One long `index.html`. Sections in order: `#concept`, `#oceaan`, `#traject`, `#themas`, `#praktisch`, `#over`, `#faq` (with `FAQPage` JSON-LD), `#intake`.

### Section-header convention

Every section header uses the same two-part pattern: a short `section-header__eyebrow` label on top, and a longer descriptive `h2` below. Keep this order consistent across all sections. Example: `#traject` uses eyebrow "Het traject" with h2 "Drie stappen, één beweging"; `#themas` uses eyebrow "Het inhoudelijke programma" with h2 "Surfen als metafoor voor ondernemen".

### `#themas` (programme content) layout

`.themes__body` is a **centered column roughly the width of the section title** (`max-width: 49rem; margin: 0 auto`) with **left-aligned text**, so topics line up with the title's left edge, dividers end at its right edge and each topic stays on one line. Do NOT full-width the block and do NOT center-align the text. The lead-in ("Welke thema's aan bod komen ... Enkele voorbeelden:") is a left-aligned `.themes__lead` paragraph inside the column. Each topic gets a gold `>` marker in `var(--accent)` and extra vertical padding. Scoped overrides in the `<style>` block: `#themas .themes__body`, `#themas .themes__lead`, `#themas .themes__list`, `#themas .themes__list li`, `#themas .science__closing`.

## SEO

- Three `schema.org` JSON-LD blocks are embedded directly in `<head>`: `FAQPage`, `Organization`, and `Event` (see Editions above). Keep FAQPage in sync with the visible FAQ.
- Meta tags, Open Graph tags, and Twitter card tags are in `<head>`. The NL meta/`og:description` and the JS `descriptions.nl` string must stay in sync (the language toggle overwrites the meta on switch).
- `sitemap.xml` covers the homepage only. `/en` and `/fr` are intentionally NOT listed (those routes do not exist yet), and no `hreflang` tags are present for the same reason. See `my-business/workflows/workflow_landing-page-seo-and-content-protection_EN.md` for the deferred multilingual-routing plan.
- No em dashes anywhere, including inside JSON-LD (use a colon or the brand middot).

## robots.txt

The `robots.txt` explicitly blocks AI **training** crawlers (ClaudeBot, GPTBot, PerplexityBot, anthropic-ai, CCBot, Bytespider, Google-Extended). **Do not remove or relax these training blocks.** Search engine crawlers (Googlebot, Bingbot) are allowed. `OAI-SearchBot` is intentionally set to `Allow: /` (2026-08-03) because it is ChatGPT search retrieval, not model training, so do NOT change it back to `Disallow`.
