# qianntong.github.io

Personal academic site for Qianqian Tong, built with [Jekyll](https://jekyllrb.com/)
and the [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes) remote
theme, deployed via GitHub Pages.

## Structure

| Path | Purpose |
| --- | --- |
| `_config.yml` | Site config. Navigation lives in `_data/navigation.yml`. |
| `index.html` | Home / About page (`/`). |
| `_pages/research.md` | Research page (`/research/`) — renders the timeline from `_data/research.yml`. |
| `_pages/meet.md` | Weekly schedule (`/meet/`). |
| `_data/research.yml` | Source of truth for research projects (year, order, summary, skills, methods, visual). |
| `_data/navigation.yml` | Top navigation. |
| `_includes/head/custom.html` | Loads `assets/css/custom.css` (overrides the theme's head include). |
| `assets/css/custom.css` | All custom styling: the research timeline + author avatar. |

## Local preview

The pinned `github-pages` gem needs Ruby 3.1.x (Jekyll 3.9 / Liquid 4.0.3 do not
run on Ruby 3.2+):

```sh
bundle install
bundle exec jekyll serve
```

GitHub Pages builds the live site remotely, so a local build is only for preview.
