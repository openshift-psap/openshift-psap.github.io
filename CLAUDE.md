# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is the GitHub Pages site for the [PSAP](https://github.com/openshift-psap) team (Performance and Scale for AI Platforms). Served at `https://openshift-psap.github.io`. Built with Jekyll; GitHub auto-deploys on push to `master`.

## Local Development

```bash
bundle install
bundle exec jekyll serve
# Visit http://localhost:4000
```

Set `JEKYLL_GITHUB_TOKEN` to a GitHub personal access token to populate the Projects section locally (it uses the GitHub Metadata API). Without it, that section will be empty locally but works on GitHub Pages automatically.

## Architecture

Static Jekyll site with no theme — all HTML/CSS is custom. Structure:

- `_layouts/default.html` — single base layout used by all pages
- `_includes/*.html` — one partial per section (projects, blog_posts, talks, conferences, upstream_projects)
- `_data/*.yml` — maintainer-edited content files (see below)
- `assets/css/style.css` — all styles; uses CSS variables for Red Hat brand colors (`--red: #EE0000`)
- `index.md` — home page; just pulls in all the includes in order

The Projects section (`_includes/projects.html`) is fully dynamic: it iterates `site.github.public_repositories` via the `jekyll-github-metadata` plugin, skipping archived and forked repos.

## Adding Content

Edit the relevant `_data/` YAML file and push to `master`. The site redeploys within ~1 minute.

### `_data/blog_posts.yml`
```yaml
- title: "Post Title"
  url: https://link-to-post
  date: "2025-01-15"       # YYYY-MM-DD
  summary: "One sentence." # optional
```

### `_data/talks.yml`
YouTube URLs are auto-detected and embedded; all other URLs render as linked cards.
```yaml
- title: "Talk Title"
  url: https://www.youtube.com/watch?v=VIDEO_ID   # or any URL
  speakers: "Name (Org), Name (Org)"
  event: "Conference Name Year"
  date: "2025-11-11"
```

### `_data/conferences.yml`
```yaml
- name: "Conference Name"
  url: https://conference-url
  location: "City, Country"
  date: "2025-11-11"
  talks:                   # optional
    - "Talk A"
    - "Talk B"
```

### `_data/upstream_projects.yml`
```yaml
- name: "ProjectName"
  url: https://github.com/org/repo
  org: "org-name"
  description: "One sentence."
  role: "Contributor"      # or Maintainer, Co-creator, etc.
```
