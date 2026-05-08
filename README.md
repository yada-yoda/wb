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
humans.txt        team / cast / awards credits in the humans.txt format
favicon/          full favicon set + web manifest
images/           logo, OG share image (wbog.png), trailer poster,
                  character stamps, promo art (11x17, 8.5x11, 4-up)
promo/            downloadable promo PDFs + a small landing page
```

## Editing

The whole site is a single `index.html` — open it, edit it, push it. No
build step, no dependencies. The version is tracked via a `<meta
name="version">` tag near the top of the file; bump it any time you ship
a visible change and add a matching entry to the changelog below.

## Changelog

### v1.0.7 — 2026-04-28
- **Performance pass.** Five surgical fixes targeting the metrics
  PageSpeed Insights cares about (LCP, CLS, FCP):
  - Added `<link rel="preconnect">` for `fonts.googleapis.com` and
    `fonts.gstatic.com` so the browser opens connections to the font
    CDN in parallel with HTML parsing instead of waiting until it
    encounters the `<link rel="stylesheet">`. Saves ~150ms on first
    font request — directly improves First Contentful Paint.
  - Added `<link rel="dns-prefetch">` for `googletagmanager.com` as a
    backup hint for the GA script.
  - Added `<meta name="color-scheme" content="dark">` so browsers
    paint the page background dark from the very first frame instead
    of flashing white before the CSS applies. Eliminates a jarring
    visual artifact that was both a UX issue and a Lighthouse note.
  - Added `width="720" height="360"` to the hero logo and
    `width="300" height="40"` to the character stamps so the browser
    reserves the right amount of layout space before the images
    decode. Eliminates Cumulative Layout Shift (CLS) from those
    images and gives Lighthouse the aspect ratio it wants.
  - Added `fetchpriority="high"` to the hero logo (it's the LCP
    candidate) and `decoding="async"` to both inline images. The
    browser now knows the logo is the most important asset to render
    and can decode images off the main thread.

### v1.0.6 — 2026-04-28
- **Trivia layout fix.** The first sentence in DID YOU KNOW was
  wrapping mid-sentence with "Second City." orphaned on its own line.
  Bumped the trivia paragraph's max-width from 560px to 680px so the
  whole first sentence fits on one line at desktop widths, added a
  non-breaking space between "Second" and "City" so they always stay
  together as a unit, and applied `text-wrap: pretty` for nicer line
  distribution generally. Also tightened the inter-sentence gap from
  `<br><br>` (blank line) to `<br>` (single line break) so the two
  facts feel like related beats instead of paragraphs.

### v1.0.5 — 2026-04-28
- **Trivia copy break.** Added a paragraph break between the two
  trivia facts in the DID YOU KNOW section so the cast/Second City
  fact and the $500 budget fact read as separate beats instead of one
  run-on sentence.
- **Fixed broken favicon.** The cookie-themed favicon files were
  always in the repo at `favicon/`, but the `<link>` tags in
  `index.html` pointed to root paths (`/favicon.ico`,
  `/apple-touch-icon.png`) which 404'd on the live site — meaning the
  browser tab has been showing the default GitHub Pages icon instead
  of the cookie this whole time. Updated all five favicon link tags
  to point to `/favicon/...`, added the missing 16x16 / 32x32 PNG
  variants, and added the missing `<link rel="manifest">` reference.
- **Fixed `site.webmanifest`.** Same wrong-paths bug
  (`/android-chrome-...png` → `/favicon/android-chrome-...png`), plus
  it had empty `name` / `short_name` and white `theme_color` /
  `background_color`. Now populated with "Waiter Boys" name and the
  site's `#0C0B0F` charcoal background, so PWA install prompts and
  Chrome's address bar style match the site.

### v1.0.4 — 2026-04-28
- **New distribution destination: Relay.** Added Relay
  (`pickrelay.com/t/yrfk-bm3y/waiter-boys`) as a third hero CTA button
  next to YouTube and IMDb, in the footer social row, in the Movie
  schema's `sameAs` array, and in `llms.txt`. Now the page presents
  both a free (YouTube) and a paid-distribution (Relay) watch path.
- **New social channel: TikTok** (`@waiterboysfilm`). Added to the
  footer social row, JSON-LD `sameAs`, and `llms.txt`.
- **Social share buttons** in the SPREAD THE WORD section: X,
  Facebook, Reddit, and Copy Link. Styled to match the existing palette
  (charcoal/cream/pink); copy-link button gives a "COPIED!" flash via
  the gold accent color.
- **GA4 conversion tracking** for outbound links. Two new events fire:
  - `watch_click` (named source: `youtube` or `relay`) — the only
    metric that matters for measuring whether visitors actually go
    watch the film
  - `click_outbound` — generic outbound link tracking for everything
    else (social channels, IMDb, Letterboxd, etc.)
  - `share` (method: `copy_link`) when someone uses the copy-link button
- **Trailer background video performance.** Added `preload="metadata"`
  so the browser only fetches the video header on first paint instead
  of buffering the whole 4.4MB file, and a `poster="images/trailer-poster.jpg"`
  (44KB JPEG, generated from the MP4) so users see a still frame
  instantly while the video loads. Improves Largest Contentful Paint
  (a Google Core Web Vitals signal) and burns a lot less mobile data.
- **Image alt-text upgrade.** The hero logo's alt was just `"Waiter
  Boys"`; promoted to `"Waiter Boys (2025) — short comedy film logo"`
  for richer screen-reader and search-engine context.
- **`humans.txt`** at the root: team, cast, awards, and site
  credits in the standard humanstxt.org format. Small touch — no SEO
  benefit but a nice signal that humans built this.

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
