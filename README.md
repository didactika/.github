# didactika/.github

This repository builds the organisation profile shown at
**[github.com/didactika](https://github.com/didactika)** — the page, its charts
and its numbers.

It is public so anyone can see how that page is produced. It is **not** open
source: the code and content here are proprietary. See
[License and reuse](#license-and-reuse).

## What it does

A GitHub profile README is a static Markdown file. It cannot run JavaScript, and
GitHub publishes no official endpoint for organisation-level statistics. So the
profile is not assembled in the browser — it is rendered ahead of time by a
scheduled job and committed as plain files that GitHub only has to display.

Every run does three things:

1. **Collects.** Queries the GitHub REST API for the organisation's repositories,
   contributors, commit history, releases, stars, licences and language
   breakdown.
2. **Renders.** Draws the charts as SVG and writes the profile pages, in English
   and Spanish, from a single content file.
3. **Commits.** Pushes whatever changed, so the profile page reflects the
   organisation as it is now without anyone editing it by hand.

## What it produces

| Output | What it is |
| --- | --- |
| A KPI strip | Repositories, contributors, commits over 12 months, stars, releases |
| Language and licence charts | How the organisation's code is distributed across both |
| A commit timeline | Activity over the last year |
| Weekday and per-repository charts | Where the commits actually land |
| Contributor avatars | Pulled live from the API, linked to their profiles |
| Per-repository badges | Release, stars, downloads and last commit, live from shields.io |
| Project pages | One page per project group, in both languages |

Everything is produced twice — once for GitHub's light theme, once for dark —
and served through `<picture>` so the page matches the reader's theme. The
charts are single-hue by design: length and height carry the values and every
series is labelled directly, so nothing depends on telling colours apart.

The two-language switch at the top of the profile is the same idea. GitHub
Markdown has no tab widget, so the tabs are two small rendered images that link
to each other's page.

## How it is put together

| Path | Role |
| --- | --- |
| `profile/data/content.json` | All the prose, in English and Spanish. The one hand-written file. |
| `scripts/generate-profile.mjs` | The generator: reads the JSON and the GitHub API, writes the pages and charts. Zero dependencies, Node ≥ 20. |
| `profile/README.md`, `profile/README.es.md` | Generated pages. The English one is what GitHub renders as the org profile. |
| `profile/projects/*.md` | Generated project pages. |
| `profile/assets/*.svg` | Generated charts and language tabs, light and dark. |
| `.github/workflows/update-profile.yml` | Runs the generator on a schedule and commits any change. |

Everything except `content.json`, the generator and the workflow is build
output. It is regenerated end to end on each run, so no wording lives in two
places and no chart can drift out of step with the numbers behind it.

The job runs every 8 hours, on any push that touches the generator or the
content file, and on demand from the Actions tab.

## Running the generator

```bash
GITHUB_TOKEN=$(gh auth token) node scripts/generate-profile.mjs
```

The token is optional but strongly recommended: unauthenticated GitHub API calls
are capped at 60 per hour, which is not enough for a full run. To work on the
layout without spending API calls, `PROFILE_DUMP=<path>` saves a run's data and
`PROFILE_FIXTURE=<path>` replays it.

## License and reuse

**Proprietary — private use only.** See [LICENSE](LICENSE).

This repository is the exception in the Didactika organisation. The
organisation's actual projects are open source under MIT or GPL-3.0; this
profile generator, its charts and its written content are not released for
reuse, and reading the code here does not grant permission to copy or adapt it.

If you want to do something with it, ask: [didactika.org](https://didactika.org).
