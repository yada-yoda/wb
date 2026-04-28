# Waiter Boys — Official Site

Static one-page site for **Waiter Boys (2025)**, an award-winning short
comedy film about underdog FBI agents going undercover to investigate a
mysterious orange substance.

- **Live:** [waiterboys.com](https://waiterboys.com/)
- **Hosting:** GitHub Pages (CNAME → `waiterboys.com`)
- **Trailer:** [YouTube](https://www.youtube.com/watch?v=zS43lgYXDrA)

## Layout

```
index.html        single-page site (everything inline: HTML, CSS, JS)
404.html          retro DOS-style "page not found"
trailer_bg.mp4    hero background video
sitemap.xml       lists site URLs + video/image entries for Google
robots.txt        allows search crawlers, blocks AI training bots
CNAME             custom domain pointer
favicon/          full favicon set + web manifest
images/           logo, OG share image (wbog.png), character stamps,
                  promo art (11x17, 8.5x11, 4-up)
promo/            downloadable promo PDFs + a small landing page
```

## Editing

The whole site is a single `index.html` — open it, edit it, push it. No
build step, no dependencies. The version is tracked via a `<meta
name="version">` tag near the top of the file; bump it any time you ship
a visible change and add a matching entry to the changelog below.

## Changelog

### v1.0.0 — 2026-04-27
- First tagged release. Cleaned up the repo so it's readable from a
  cold start: removed the leftover Nicepage scaffolding (`nicepage.css`,
  `nicepage.js`, `jquery.js`, `12345.css`, `index.old`, `robots.txt.old`)
  that the new design no longer references.
- Fixed the social-share image: meta tags pointed at a non-existent
  `og-poster.jpg`; corrected to the actual `images/wbog.png` so link
  previews on Facebook, LinkedIn, iMessage, Slack, Discord, and X
  render the poster instead of plain text.
- Added this README and a `<meta name="version">` tag so future edits
  have a clear baseline to bump from.

### Pre-v1.0.0 (web-Claude work, ended 2026-04-16)
- Full redesign away from the original Nicepage build into a cinematic
  single-page experience with hero video, cast roster, awards row,
  promo downloads, and footer.
- Added comprehensive SEO: meta description, 25+ keyword set, canonical
  link, Open Graph + Twitter Card tags, Schema.org Movie JSON-LD with
  cast/crew/awards, and a `WebSite` JSON-LD block.
- Wrote `sitemap.xml` (with video and image entries) and `robots.txt`
  (allows search engines, blocks AI training crawlers).
- Wired in Google Analytics (`G-Q5JD7JNPCV`).
- Populated the four real festival wins: Paris Film Awards, London
  Movie Awards (Best Actress: Shelby Henderson), Best Shorts
  Competition (Ensemble Cast), Florence Film Awards.
