# AGENTS.md

Shared instructions for coding agents working in this repository (the public GitHub profile of Matteo Dante).

## What this repository is

- `README.md` is the profile page: selected work, the `Writing` list and the badges.
- `articles/*.md` are the blog posts of matteodante.it. The site reads them straight from `main` over the GitHub API
  (`matteodante/portfolio-cockpit`, `lib/blog/source.ts`) and revalidates every five minutes, so a push here is a
  publication. Nothing in the site repository needs to change to publish or fix an article.
- `articles/images/` holds the covers and screenshots. No provenance manifests (Matteo, 23 Oct 2026).

## Articles

- Frontmatter: `title`, `subtitle` (it is the page description and the link preview, so it must stand alone),
  `date`, `cover`, `coverAlt`, `draft` and, only after a substantial revision, `updated` (it becomes
  `dateModified` and the sitemap lastmod). Quote any value that contains a colon. The slug is the file name and
  never changes: shared links point to it, even when the title changes.
- Markdown as the renderer expects: GFM tables, fenced code with a language, ```` ```mermaid ```` for diagrams
  (drawn in the browser), images on consecutive lines to make a gallery, relative links `other-slug.md` for other
  articles. No raw HTML. A leading H1 is dropped; start the body with prose.
- Audience: a recruiter must be able to read every article, and a programmer should come away curious enough to
  write. Tell why the thing exists, what it does for the person using it, what was hard, what was learned, and
  where it stands, in the first person. No sales tone, no feature lists, no call to buy; the closing is an open
  invitation to talk.
- Depth: for a closed-source product (DroneClean, GymTree, Maestro) nothing that would help someone clone it:
  no model names, parameters, pipeline stages, internal limits or infrastructure. Describe what a user sees and
  the decisions behind it. Open-source projects link their repository for the depth; the article still tells
  the story, not the spec. Code blocks only when a line carries the story, and almost never.
- Every number, name and claim comes from the project's repository, its documents or the live product. Feelings
  and motivations only as documented decisions and the author's own words in the notes; no invented biography.
  No invented clients, results or benchmarks. Private footage, creators' clips, tokens, outreach and internal
  business state stay out.
- Voice: first person, plain, candid, with opinions and asides, as in Anthropic's engineering posts. Follow the
  humanizer rules: no em or en dashes, no "not X but Y", no one-line closers that restate the paragraph, no forced
  triads, no bold labels, headings in sentence case that state the point ("The shadow is never where you want
  it"), no "delve/crucial/robust/showcase" filler.
- Every article ends with a `## Links` section: the product site or demo, the repository when public, the App
  Store page, the documents the article rests on, and related articles as relative `slug.md` links. Keep it to
  what a reader would open, with a few words on each.
- Readability: paragraphs of at most about 70 words and sentences of at most about 40, measured with a script, not
  guessed. Screenshots and an occasional blockquote or small table give the eye something to hold; a "What I
  learned" section with two or three plain heuristics closes the story.
- Images: covers are 16:9 (the site also crops them to 3:2 on phones), with no typography. Without an image
  generator, compose the cover from the product's own rights-cleared media. Only a real output may be shown as a
  result. Screenshots of a live product are captured at 1440×1000 with the cookie notice dismissed. Check the
  rights register of the product (for DroneClean, `social/RIGHTS.md`) and record the use there.
- The MMORPG article has its own third-party-rights wording (unnamed game, nothing distributed, private test
  server) and is kept as written unless Matteo asks.

## History

- One commit per article, titled `Publish the <project> article`, containing the article, its images and its
  line in the README. Edits to a published article are folded into that commit
  (`git commit --fixup=<sha>`, then `GIT_SEQUENCE_EDITOR=true git rebase -i --autosquash <base>` with
  `--committer-date-is-author-date`) and pushed with `--force-with-lease`. Only Matteo's own history is rewritten
  here; nobody else works on this repository.
- Commits keep Matteo's author identity and the original publication date.

## Before pushing

- Preview with the site's renderer: in `portfolio-cockpit`, `BLOG_LOCAL_DIR=<this repo>/articles bun run dev`
  (or a script that imports `getArticles`/`getArticle` from `@/lib/blog/source`), and look at each page at 390px
  and 1440px: tables scroll, galleries show whole screenshots, diagrams render.
- Run a link check on every external URL in the article.
- After publishing or renaming: update the README `Writing` line and, in `portfolio-cockpit`, `lib/seo/llms-content.ts`,
  `lib/ai/landing-context.ts` and the public profile in `app/api/chat/route.ts`; update the link text in the
  project's README; re-scrape the URL in LinkedIn's Post Inspector when the title, description or cover changed.
- Check the live page with an HTTP client after the cache window, not with a browser tab.
