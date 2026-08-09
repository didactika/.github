# Security Policy

This is the default security policy for repositories in the Didactika
organization that do not provide their own `SECURITY.md`. If the repository
you found an issue in has its own security policy, follow that one instead —
it may list supported versions or a narrower scope specific to that project.

## Reporting a vulnerability

**Do not open a public issue for a security vulnerability.**

The preferred way to report a vulnerability is through GitHub's private
vulnerability reporting, if the repository has it enabled: go to the
repository's **Security** tab and select **Report a vulnerability**. This
opens a private draft advisory that only you and the maintainers can see,
and keeps a record the fix can be tracked against.

If a repository does not have private vulnerability reporting enabled, or you
would rather not use GitHub, email **security@didactika.org** with:

- The repository and, if relevant, the version or commit affected.
- Steps to reproduce, or a proof of concept.
- What you think the impact is (what an attacker could do with it).

This is a shared inbox for now; if a project grows a dedicated security
contact later, its own `SECURITY.md` will say so.

## Supported versions

Which versions receive security fixes depends on the kind of project. Didactika uses two
maintenance schemes, because a library consumed from a registry and a Moodle plugin
installed into a site do not age the same way.

**NPM packages** keep one branch per live major, named `vMAJOR.x` — starting from `v0.x`
for a brand new package (this is the org's default branch from day one, not something
adopted later), then `v1.x`, `v2.x`, and so on as the API evolves. The highest major is
the default branch and receives features and fixes. The previous major receives
**security fixes only**, never features, and is published on its own when needed. Two
majors back leaves support once the current one is stable: its `vMAJOR.x` branch is
deleted, and someone runs `npm deprecate` for that major, pointing whoever is still on it
at the current one.

**A missing `vMAJOR.x` branch is the signal that a major is unsupported.** There is no
separate list to keep in sync — if the branch for a major is gone, that major is done,
and it is (or should be) marked `deprecated` on npm:

| Signal | Meaning |
|---|---|
| `vMAJOR.x` branch exists, is the default branch | current major — features and fixes |
| `vMAJOR.x` branch exists, is not the default | previous major — security fixes only |
| `vMAJOR.x` branch does not exist | unsupported — `npm deprecate` points elsewhere |

What each position in the version number means, and who is allowed to bump it, is the
same across every project regardless of language or registry:

| Position | Name | Bumped when | Who bumps it |
|---|---|---|---|
| First — `X`.y.z | major | a breaking change ships | whoever ships it, on a new `vX.x` branch |
| Middle — x.`Y`.z | minor | a backward-compatible feature ships | whoever ships it, on the highest `vX.x` |
| Last — x.y.`Z` | patch | a bug or **security** fix ships | always — a security fix is never a major or minor bump, precisely so it can land on an old, otherwise-frozen major without dragging in unrelated features |

The `latest` dist-tag always points at the highest semver published, not at whatever was
published most recently, so a security backport to an older major never pulls `latest`
backwards. Any major that is not the highest gets its own `vNx` dist-tag instead (no dot
— `v2x`, not `v2.x`, since npm's own argument parser would otherwise read a dotted tag as
a semver range and never look at dist-tags at all), so `npm install <package>@v2x` keeps
resolving to that major's newest patch independent of what the current major does.

**Moodle plugins** follow the convention of the Moodle ecosystem rather than ours.
Development happens on `main`, and each supported Moodle release gets its own branch —
`MOODLE_405_STABLE`, `MOODLE_502_STABLE`. The plugin's own version is independent of
those branches: `version.php` carries it in `$plugin->release`, and `$plugin->supported`
declares which Moodle releases that version is tested and supported against. That
declaration is the authoritative answer for any given plugin, and it is what the CI
matrix runs against.

**Services and applications** are deployed rather than distributed. They have no
published versions to support: only what is currently deployed is maintained.

To see which versions of a given project are supported right now, look at the branches
the repository actually has, or at the [Didactika profile](https://github.com/didactika),
which lists them.

## What to expect

- Acknowledgement within a few days.
- We will let you know once a fix is available, or if we assess the report as
  not a vulnerability, with the reasoning.
- Please give us reasonable time to release a fix before disclosing publicly.
  We are a small team maintaining these projects alongside other work, not a
  company with a dedicated security team.

## Scope

This policy covers the code in Didactika-owned repositories. It does not
cover third-party dependencies — please report those upstream — nor does it
cover a Moodle site or other deployment running this software; that is the
operator's responsibility.
