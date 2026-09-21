# Penfield Advisors — Website

The public website for **Penfield Advisors LLC**, an education consulting firm.
Built with [Jekyll](https://jekyllrb.com/) and published with GitHub Pages.

> **Status:** the structure and design are complete; all copy, imagery, and
> contact details are placeholders pending real company information.

## Site structure

```
.
├── _config.yml              # Site settings, company details, navigation
├── _includes/               # Reusable fragments
│   ├── head.html            #   <head> contents, SEO tags, favicons
│   ├── header.html          #   Masthead + primary navigation
│   └── footer.html          #   Footer with contact details
├── _layouts/
│   ├── default.html         #   Base shell: header, <main>, footer
│   └── page.html            #   default + a navy page banner (title/subtitle)
├── assets/
│   ├── css/style.css        #   All site styles
│   ├── js/nav.js            #   Mobile navigation toggle
│   ├── images/              #   Placeholder artwork (swap for real photos)
│   └── logos/               #   Brand logo files (source of truth)
├── index.html               # Home
├── about.html               # About / founder bio        → /about/
├── contact.html             # Contact information        → /contact/
├── 404.html                 # Not-found page
├── robots.txt               # Points crawlers at the sitemap
└── .github/workflows/deploy.yml
```

## Brand

| Token | Hex | Use |
| --- | --- | --- |
| Navy | `#0b254b` | Header, footer, headings, primary buttons |
| Sky | `#9bc6df` | Accents, text on navy, button fills |
| White | `#ffffff` | Page background, text on navy |

Defined as CSS custom properties at the top of `assets/css/style.css`.

**Logo usage:** the `*-transparent.svg` variants render their wordmark in
**white**, so they only work on a dark background — that is why the header and
footer are navy. The non-transparent variants carry their own navy background
and are the ones to use on light surfaces.

`leaf-logo.svg` is the favicon; `main-logo-wide-transparent.svg` is the header
lockup; `main-logo-transparent.svg` is the footer mark.

## Updating content

Most routine edits happen in **`_config.yml`** — email, phone, address, office
hours, founder name and role, and the navigation menu all live there, and every
page reads from those values. Changing `company.email` once updates the footer,
the contact page, and the structured data together.

Page copy lives in `index.html`, `about.html`, and `contact.html`. Placeholder
passages are wrapped in `<em>` tags so they are easy to find and replace.

To swap the placeholder artwork, drop real images into `assets/images/` and
update the `src` attributes. Keep the founder portrait roughly portrait-shaped
(7:8) and the home page tiles at 4:3 so the existing layout holds.

## Local development

Requires Ruby 3.x and Bundler.

```sh
bundle install
bundle exec jekyll serve
```

The site is then available at <http://localhost:4000/github-pages/>. Note the
`/github-pages/` path — it comes from the `baseurl` setting described below.

## Deployment

Pushing to `main` triggers `.github/workflows/deploy.yml`, which builds the site
with Jekyll and publishes it to GitHub Pages.

One-time setup: in **Settings → Pages**, set **Source** to **GitHub Actions**.

The live site is <https://penfield-advisors.github.io/github-pages/>.

### Moving to a custom domain

Because this is a *project* site, `baseurl` is set to `/github-pages` so that
asset and link paths resolve correctly. When a custom domain is ready:

1. Add a `CNAME` file at the repo root containing the domain, e.g.
   `penfieldadvisors.com`.
2. In `_config.yml`, set `url` to `https://penfieldadvisors.com` and change
   `baseurl` to `""`.
3. Configure the domain under **Settings → Pages** and enable
   **Enforce HTTPS**.

All internal links use Jekyll's `relative_url` filter, so nothing else needs to
change.

## Conventions

- Internal links must use `{{ '/path/' | relative_url }}` so they survive a
  `baseurl` change.
- The accent blue `#9bc6df` fails contrast requirements as text on white — use
  it on navy or as a fill only.
- No external fonts, scripts, or CDNs; the site is fully self-contained.
