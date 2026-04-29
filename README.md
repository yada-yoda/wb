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
llms.txt          Markdown-formatted summary for AI/LLM consumption
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

### v1.0.3 — 2026-04-28
- **Fixed two SEO errors flagged by Bing Webmaster Tools** during the
  initial Bing crawl after sitemap submission:
  - **H1 tag missing.** The page had three H2s but no H1, so search
    engines had no anchor for the page's primary topic. Promoted the
    `<div class="logo-wrap">` in the hero to an `<h1>` so the existing
    logo image now sits semantically as the page title. Added a
    visually-hidden `<span>` inside the H1 with the full text
    "Waiter Boys (2025) — Award-Winning Short Comedy Film" so screen
    readers and search engines get strong text content (the visible
    layout is unchanged).
  - **Meta description too long.** Was 251 characters, well past
    Google/Bing's ~155-character SERP truncation point. Trimmed to 152
    chars while keeping the brand keyword first, the hook, and the
    call-to-action.

### v1.0.2 — 2026-04-28
- **Added standalone `VideoObject` JSON-LD for the full short film.**
  The trailer was already nested inside the Movie schema, but a
  top-level VideoObject is what triggers Google's video rich results
  (thumbnail, duration, watch action right in the SERP). Includes
  contentUrl, embedUrl, both YouTube thumbnail sizes, and a
  `WatchAction` so AI assistants know where to send viewers.
- **Added standalone `Person` JSON-LD for Skylar Kendall and Frank
  Rizzo.** They were nested as director/writer/producer/actor inside
  the Movie schema; as standalone Person entities with `sameAs` IMDb
  links and `worksFor` production companies, they help search engines
  build knowledge-panel entries for the creators independently of the
  film page.
- Skipped FAQ schema — Google deprecated FAQ rich results for non-
  authoritative sites in August 2023, so the SEO upside is gone for
  a film site.

### v1.0.1 — 2026-04-27
- **Made the site LLM-friendly so it can actually surface in AI answer
  engines.** The previous robots.txt explicitly blocked GPTBot, CCBot,
  anthropic-ai, Claude-Web, and Google-Extended — which protected the
  content from training scrapes but also prevented Perplexity, ChatGPT
  search, Google AI Overviews, and Claude with web search from citing
  the film. For a marketing site whose whole job is to drive viewers
  to the YouTube release, that tradeoff was upside down. Removed the
  blocks; all bots are welcome.
- Added `llms.txt` at the root: a clean Markdown-formatted summary
  with the synopsis, facts, full cast and roles, awards, trivia, and
  watch links. LLMs prefer this over scraping a styled HTML page.

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
