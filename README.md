# openshift-psap.github.io

Source for the [PSAP team's GitHub Pages site](https://openshift-psap.github.io) — Performance and Scale for AI Platforms.

## Local development

```bash
bundle install
JEKYLL_GITHUB_TOKEN=<your-pat> bundle exec jekyll serve
# Visit http://localhost:4000
```

A GitHub personal access token (`public_repo` scope) is required to populate the Projects section locally via the GitHub Metadata API. Without it, that section will be empty but works automatically on GitHub Pages.

## Adding content

All content is managed through YAML files in `_data/`. Push to `master` and the site redeploys within ~1 minute.

| File | Content |
|------|---------|
| `_data/blog_posts.yml` | Blog posts |
| `_data/talks.yml` | Conference talks (YouTube URLs are auto-embedded) |
| `_data/publications.yml` | Academic publications |
| `_data/upstream_projects.yml` | Upstream open-source projects maintained by the team |

See [CLAUDE.md](CLAUDE.md) for field definitions and examples.
