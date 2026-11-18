# elliedenmark.com

Static site for Ellie Denmark, singer-songwriter. Cloudflare Worker
(`elliedenmarkmusic`) serving this folder as assets. No build step, no
dependencies, no server code.

Replaces a WordPress site on Hostinger. The WordPress export (files + the
original uploads) is kept **outside** this repo in `../elliedenmark-wordpress`
— it contains `wp-config.php` with database credentials, so it must never be
copied in here.

## Deploying

**Pushing to `main` deploys.** Workers Builds runs `npx wrangler deploy` in
the cloud on push. Treat a push as shipping to production.

- `wrangler.jsonc` must say `name: "elliedenmarkmusic"`. Any other name deploys
  to a phantom Worker with no custom domain: the build goes green and the live
  site never changes.
- `wrangler.jsonc` must stay at the repo root.
- `.assetsignore` keeps repo files (`CLAUDE.md`, `wrangler.jsonc`, `.git`) from
  being served. Add to it when adding non-site files.

Remote: `github.com/RagininW/elliedenmarkmusic`

## Layout

- One folder per page, each with its own `index.html`: `/`, `/shows/`,
  `/collabs/`, `/contact/`. Header and footer are repeated in each file — edit
  all five (including `404.html`) when the nav changes.
- `css/site.css` — the only stylesheet. Colours and fonts are tokens on `:root`.
- `img/` — web-sized images. Originals are in `../elliedenmark-wordpress/wp-content/uploads/`.
- Fonts come from Google Fonts: DM Sans (body, headings) and Forum (serif accents).
- Paths are root-absolute (`/css/site.css`), since pages live in subfolders.

## Old URLs

`_redirects` maps the WordPress paths to the new ones: `/about/` → `/shows/`,
`/services/` → `/collabs/`. Keep those rules; search results and old links
still point there. `not_found_handling: "404-page"` serves `404.html`.

## Copy

All text is Ellie's, carried over verbatim from the old site, in English.
Don't rewrite it without her say.

## Contact

No form. The old WordPress form needed PHP; it was replaced with a `mailto:`
link to `elliedenmarkmusic@gmail.com`.

The domain has no mail of its own. The old `contact@elliedenmark.com` lived on
Hostinger and was dropped with the move — don't put an @elliedenmark.com
address on the site unless mail for the domain is set up again (e.g.
Cloudflare Email Routing).
