# didactika/.github

Source of the Didactika organisation profile shown at
**[github.com/didactika](https://github.com/didactika)**.

## Layout

| Path | Role |
| --- | --- |
| `profile/data/content.json` | **The only file to edit.** Every word of the profile, in English and Spanish. |
| `scripts/generate-profile.mjs` | Reads the JSON and the GitHub API, renders the charts and both READMEs. No dependencies. |
| `profile/README.md` | Generated — English. This is what GitHub renders as the org profile. |
| `profile/README.es.md` | Generated — Spanish. |
| `profile/assets/*.svg` | Generated — charts and language tabs, in light and dark variants. |
| `.github/workflows/update-profile.yml` | Runs the generator daily and commits any change. |

The two READMEs and everything under `profile/assets/` are build output. Editing
them by hand is pointless: the next scheduled run overwrites the change. Edit
`content.json` instead.

## Running it locally

```bash
GITHUB_TOKEN=$(gh auth token) node scripts/generate-profile.mjs
```

The token is optional but strongly recommended — unauthenticated GitHub API
calls are rate-limited to 60/hour, which is not enough for a full run.

## Why some charts are committed files

A GitHub profile README cannot execute JavaScript, and GitHub publishes no
official statistics-image endpoint. Per-repo facts (release, stars, downloads,
last commit) come live from shields.io on every page load. Organisation-wide
aggregates — language distribution, licensing, the commit timeline, contributor
avatars — have no equivalent working service, so the scheduled job recomputes
them and commits the result.

## License

**Proprietary — private use only.** See [LICENSE](LICENSE).

This repository is the exception in the Didactika organisation: the profile
generator and its content are our own work and are not released for reuse. The
organisation's actual projects are open source under MIT or GPL-3.0.
