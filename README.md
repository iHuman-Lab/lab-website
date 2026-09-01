# 🧠 iHuman Lab Website

Home on the internet for the [iHuman Lab](https://github.com/iHuman-Lab) —
humans, machines, and the occasional exploding gaze-tracker. Built with
[Quarto](https://quarto.org), held together with Python scripts and vibes.

## 🛠️ Prerequisites

- [Quarto](https://quarto.org/docs/get-started/) (CLI) — the engine
- Python 3 — for the robots that write pages for us (stdlib only, no `pip install` required)

## 🚀 Development

Spin it up and watch it live-reload as you type:

```sh
quarto preview
```

Build the real, deployable, static site (lands in `_site/`):

```sh
quarto render
```

Both commands quietly summon two little robots first (via `_quarto.yml`'s
`pre-render` hook), so you never have to update these pages by hand:

- 🤖 `scripts/fetch_github_repos.py` — raids the `iHuman-Lab` GitHub org for
  public repos and writes a `software/repos/<name>/index.qmd` for each one.
  Don't want a repo showing up? Add it to `EXCLUDE_NAMES` in the script.
- 🖼️ `scripts/update_gallery.py` — scans `images/work/` and
  `images/outreach/` and redraws the gallery grid (`gallery/index.qmd`) and
  homepage slideshow (`index.qmd`) between their `..._START`/`..._END`
  markers. Want a photo on the site? Just drop it in one of those folders
  and re-render — no code required.

Either robot can also be summoned solo:

```sh
python scripts/update_gallery.py
```

## 🗺️ Structure

| Path            | Contents                                                                     |
| --------------- | ---------------------------------------------------------------------------- |
| `index.qmd`     | Homepage                                                                     |
| `research/`     | Research area pages                                                          |
| `publications/` | Publications (`publications.bib` + Lua filter does the formatting)           |
| `people/`       | PI, PhD & Master's students, and the illustrious alumni                      |
| `news/`         | News posts                                                                   |
| `software/`     | Software/repos listing ✨ auto-generated, see above                           |
| `gallery/`      | Photo gallery ✨ auto-generated, see above                                    |
| `outreach/`     | Outreach events — slides, workshops, and the rest                            |
| `contact/`      | Join us / contact page                                                       |
| `images/`       | Site images, incl. `images/work/` & `images/outreach/` for the gallery robot |
| `scripts/`      | The robots (pre-render Python scripts)                                       |
| `_extensions/`  | Quarto extensions (e.g. academicons)                                         |
| `custom.scss`   | Theme tweaks on top of the `cosmo` base                                      |
| `_quarto.yml`   | Site/project configuration — mission control                                 |

## 📦 Deployment

Every push to `main` triggers [`.github/workflows/publish.yml`](.github/workflows/publish.yml),
which renders the site and publishes it to the `gh-pages` branch automatically —
no manual step needed. You can also trigger it by hand from the
Actions tab (`workflow_dispatch`).

To publish from your machine instead, one command, no drama:

```sh
quarto publish gh-pages
```
