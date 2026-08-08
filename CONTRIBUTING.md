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
5. Commit with a message that explains *why* the change is needed, not just
   what it does.
6. Open a pull request against the repository's default branch, unless its own
   `CONTRIBUTING.md` says otherwise (some projects route pull requests through
   a `develop` branch instead).

## Pull request review

- Automated checks (if configured) must pass before a maintainer reviews the
  change.
- A maintainer will review, request changes if needed, and merge once
  approved. Response times are best-effort; this is a small team, not a
  company with an SLA.

## Reporting a bug or requesting a feature

Use the issue templates offered when you open a new issue. They ask for the
details that let a maintainer reproduce a bug or evaluate a request without a
back-and-forth first.

## License

Unless the repository states otherwise in its own `LICENSE` file, contributed
code is accepted under that repository's license. Check the `LICENSE` file at
the root of the specific repository before contributing if this matters to
you.
