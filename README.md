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
lockup; `main-logo-transparent.svg` is the footer mark; `small-logo.png`
(180x180) is the iOS home-screen icon.

That last one must stay a PNG and must stay opaque — iOS ignores SVG for
`apple-touch-icon` and composites transparency onto black.

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

The live site is <https://penfieldadvisors.com>.

### Custom domain

The site is served from `penfieldadvisors.com`, declared in the `CNAME` file at
the repo root. Because it sits at the web root, `baseurl` is empty and `url` is
the full domain — keep those two in sync with `CNAME` if the domain ever
changes, since canonical tags and the sitemap are generated from `url`.

DNS is managed in Cloudflare. The apex points at GitHub's Pages IPv4 and IPv6
addresses and `www` is a CNAME to `penfield-advisors.github.io`; GitHub
redirects `www` to the apex automatically.

Two Cloudflare settings matter, and both will break the site if set wrong:

- **Proxy status must be DNS only (grey cloud).** With the orange cloud on,
  GitHub cannot complete the certificate challenge and *Enforce HTTPS* stays
  unavailable.
- **If the proxy is ever enabled**, SSL/TLS mode must be **Full** or **Full
  (strict)**. *Flexible* causes an infinite redirect loop against Pages'
  own HTTPS redirect.

All internal links use Jekyll's `relative_url` filter, so a future domain or
`baseurl` change needs no edits to page markup.

## Conventions

- Internal links must use `{{ '/path/' | relative_url }}` so they survive a
  `baseurl` change.
- The accent blue `#9bc6df` fails contrast requirements as text on white — use
  it on navy or as a fill only.
- No external fonts, scripts, or CDNs; the site is fully self-contained.
