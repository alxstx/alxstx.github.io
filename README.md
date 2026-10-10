# alexanderstepanov.cv

Personal site built on the [al-folio](https://github.com/alshedivat/al-folio) v1 Jekyll starter
(runtime comes from the `al_folio_*` gems pinned in `Gemfile`).

Prompts used to write the site text (and for the fields still empty, like the SEO description) live in [PROMPTS.md](PROMPTS.md).

## Where content lives

| What                   | File                       |
| ---------------------- | -------------------------- |
| Name, description, SEO | `_config.yml`              |
| Intro (home page)      | `_pages/about.md`          |
| Experience, education  | `_data/experience.yml`     |
| Interests              | `_pages/interests.md`      |
| Publications           | `_bibliography/papers.bib` |
| Social links           | `_data/socials.yml`        |
| Photo                  | `assets/img/prof_pic.jpg`  |

## Run locally

```bash
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll serve   # http://localhost:4000
```

Or with Docker: `docker compose up`.

## Deploy

Pushing to `master` builds with Jekyll and deploys to GitHub Pages via `.github/workflows/deploy.yml`.
