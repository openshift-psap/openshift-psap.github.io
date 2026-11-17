# openshift-psap.github.io

Source for the [PSAP team's GitHub Pages site](https://openshift-psap.github.io) — Performance and Scale for AI Platforms.

Built with Jekyll. There is no CI workflow: pushing to `master` triggers a GitHub Pages rebuild (~1 minute). No theme — all markup and CSS are hand-written.

## Local development

```bash
bundle install
bundle exec jekyll serve
# Visit http://localhost:4000
```

All visible content lives in `_data/*.yml`, so the site renders completely without any GitHub token. `JEKYLL_GITHUB_TOKEN` is only useful to avoid GitHub API rate limits locally, and only affects the SEO tags emitted by `jekyll-github-metadata`.

## Adding content

Everything on the home page comes from YAML files in `_data/`. Edit the relevant file, push to `master`, and it goes live.

| File | Content |
|------|---------|
| `_data/blog_posts.yml` | Blog posts, grouped by year with a "Show more" button |
| `_data/talks.yml` | Conference talks (YouTube URLs are auto-embedded, others render as links) |
| `_data/publications.yml` | Academic publications |
| `_data/upstream_projects.yml` | Featured projects maintained by the team |

The sections render in this order on the home page: Blogs, Talks, Publications, Featured Projects — matching the anchor nav in `_layouts/default.html`.

See [AGENTS.md](AGENTS.md) for the full per-file field reference, section ordering, and architecture notes.
