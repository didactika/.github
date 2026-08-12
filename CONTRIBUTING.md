# Contributing to Didactika projects

Thanks for taking the time to contribute. This file is the default contributing
guide for repositories in the Didactika organization that do not provide their
own. If the repository you are working on has its own `CONTRIBUTING.md`,
follow that one instead — it will have the project-specific commands, branch
names, and test suite this general guide cannot know about.

By contributing, you agree that your contribution is licensed under the terms
of the license in that repository's own `LICENSE` file.

## Before you start

- **Small fix (typo, broken link, obvious bug)**: open a pull request
  directly.
- **Anything larger (new feature, behavior change, refactor)**: open an issue
  first and describe what you want to do. This avoids spending time on a
  pull request built on an approach the maintainers would not take.
- **Security vulnerability**: do not open a public issue. See
  [SECURITY.md](SECURITY.md).

## Code of conduct

Participation in any Didactika repository is governed by our
[Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to
uphold it.

## Making a change

1. Fork the repository (or create a branch, if you have write access).
2. Create a branch named after what it does, for example `fix/broken-link` or
   `feature/schema-validation`.
3. Make your change. Follow the coding style already used in the file you are
   editing — most projects here use an automated linter or formatter; run it
   before committing if the repository has one configured.
4. Add or update tests if the project has a test suite and your change affects
   behavior.
5. Commit following [Conventional Commits](https://www.conventionalcommits.org)
   (see below), and use the body to explain *why* the change is needed, not
   just what it does.
6. Open a pull request against the right branch for that kind of project (see
   below). When in doubt, the repository's default branch is the right target.

## Commit messages

Commits follow [Conventional Commits](https://www.conventionalcommits.org): a
type, an optional scope, and a short imperative summary.

```
feat(query): support case-insensitive search on MySQL
fix: truncate NOW() to milliseconds on MySQL upserts
docs: document the release process
```

Common types are `feat`, `fix`, `docs`, `refactor`, `test`, `ci`, `chore`. A
change that breaks compatibility says so with `BREAKING CHANGE:` in the body,
which is what tells reviewers a major version is involved.

The prefix is a convention, not automation: versions and changelogs are still
written deliberately, not derived from commit history.

## Which branch to open a pull request against

Branching differs by project type, because a library published to a registry
and a Moodle plugin installed into a site are maintained differently. The full
rationale is in [SECURITY.md](SECURITY.md).

- **NPM packages** keep one branch per live major, `vMAJOR.x`. Target the
  highest one — `v3.x` — unless you are backporting a security fix to an older
  major. There is no `develop` branch.
- **Moodle plugins** develop on `main`, with one `MOODLE_XXX_STABLE` branch per
  supported Moodle release. Target `main` unless the fix only applies to a
  specific Moodle release.
- **Services and applications** keep a stable branch and a `develop` branch.
  Target `develop`.

## Pull request review

- Automated checks (if configured) must pass before a maintainer reviews the
  change.
- A maintainer will review, request changes if needed, and merge once
  approved. Response times are best-effort; this is a small team, not a
  company with an SLA.

## How these repositories are configured

Branch protection, merge options, security settings, environments and the rest
are not clicked into each repository by hand. They are declared once, as
policy, and reconciled with
[**octoform**](https://www.npmjs.com/package/@hector21/octoform) — a tool
written for exactly this and released openly:
[hector-ae21/octoform](https://github.com/hector-ae21/octoform).

Two things follow from that, and both affect you as a contributor:

- **The rules are the same everywhere they apply.** If pull requests are
  required on one package's version branches, they are required on all of them.
  A repository that behaves differently is either a different project type — see
  the branch table above — or drift, and drift here is a bug worth reporting.
- **Settings changed by hand get reverted.** Not out of strictness: the whole
  point of declaring them is that the declaration is the truth. If a repository
  genuinely needs to differ, the change belongs in the policy, so ask a
  maintainer rather than changing it in the GitHub UI.

The configuration itself is private, since it names private repositories. The
tool is not, and neither is any of the reasoning behind these conventions.

## Reporting a bug or requesting a feature

Use the issue templates offered when you open a new issue. They ask for the
details that let a maintainer reproduce a bug or evaluate a request without a
back-and-forth first.

## License

Unless the repository states otherwise in its own `LICENSE` file, contributed
code is accepted under that repository's license. Check the `LICENSE` file at
the root of the specific repository before contributing if this matters to
you.
