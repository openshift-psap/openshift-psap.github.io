# AGENTS.md

Guidance for AI coding agents (Claude Code, OpenCode, and others) working in this repository.

> `CLAUDE.md` is a symlink to this file — edit `AGENTS.md` only.

## Repository purpose

GitHub Pages site for the [PSAP](https://github.com/openshift-psap) team (Performance and Scale for AI Platforms), served at <https://openshift-psap.github.io>.

Built with Jekyll. There is no CI workflow — GitHub Pages rebuilds automatically on every push to `master` (~1 minute).

## Local development

```bash
bundle install
bundle exec jekyll serve
# Visit http://localhost:4000
```

`JEKYLL_GITHUB_TOKEN` is only needed if you hit GitHub API rate limits locally; it is used by `jekyll-github-metadata` for repository metadata in the SEO tags, not for page content. All visible content comes from `_data/*.yml`, so the site renders fully without a token.

## Architecture

Static Jekyll site, no theme — all HTML and CSS are custom.

- `_config.yml` — site title/description/url, `master` as the source branch, and the `jekyll-github-metadata` + `jekyll-seo-tag` plugins
- `_layouts/default.html` — the single base layout: header with anchor nav (`#blog`, `#talks`, `#publications`, `#upstream`), `{{ content }}`, footer, `{% seo %}`
- `_includes/*.html` — one partial per section, each a `<section class="section">` with an id matching the nav anchors
- `_data/*.yml` — the content itself (see below); no Markdown pages hold content
- `assets/css/style.css` — all styles; Red Hat brand colors as CSS variables on `:root` (`--red: #EE0000`, `--dark`, `--gray`, `--max-width: 1140px`)
- `index.md` — home page, just includes the four section partials in display order: `blog_posts`, `talks`, `publications`, `upstream_projects`

### Sections and their includes

| Include | Section id | Heading | Ordering |
|---|---|---|---|
| `blog_posts.html` | `#blog` | Blogs | `date` descending, grouped by year, 10 at a time behind a "Show more" button |
| `talks.html` | `#talks` | Talks | `date` descending |
| `publications.html` | `#publications` | Publications | `year` descending |
| `upstream_projects.html` | `#upstream` | Featured Projects | file order (not sorted) |

Each section header shows a live count of its entries.

Behaviour worth knowing:

- **Blogs** renders a compact list (title link, authors, date) with the year-grouping and "Show more" pagination implemented in an inline script, driven by `data-blog-index` and `data-year-start` attributes. Adding entries needs no JS changes.
- **Talks** embeds an iframe only when the URL matches `youtube.com/watch?v=` or `youtu.be/`; every other URL (FINOS, ACM, conference sites) renders as a plain linked card.
- **Featured Projects** renders in the order given in the YAML file, so reorder the file to reorder the cards.

## Adding content

Edit the relevant `_data/` YAML file and push to `master`. Keep list entries newest-first where the include sorts, and quoted `YYYY-MM-DD` dates.

### `_data/blog_posts.yml`

```yaml
- title: "Post Title"
  url: https://link-to-post
  date: "2026-11-02"       # YYYY-MM-DD, controls sort and year grouping
  authors: "Name, Name (Org)"
  summary: "One sentence." # optional; not currently rendered
```

### `_data/talks.yml`

```yaml
- title: "Talk Title"
  url: https://www.youtube.com/watch?v=VIDEO_ID   # or any non-YouTube URL
  speakers: "Name (Org), Name (Org)"
  event: "Conference Name Year"
  date: "2026-11-04"
```

### `_data/publications.yml`

```yaml
- title: "Paper Title"
  url: https://doi.org/...
  authors: "Name, Name"
  venue: "Conference Name Year"
  year: 2026               # integer, controls sort
  doi: "10.1145/..."       # optional; not currently rendered
  abstract: "One sentence." # optional; rendered as the card body
```

### `_data/upstream_projects.yml`

```yaml
- name: "ProjectName"
  url: https://github.com/org/repo
  org: "org-name"          # shown as the small label above the title
  description: "One sentence."
  role: "Creator"          # or Maintainer, Contributor, etc.
```
