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

**NPM packages** keep one branch per live major, named `vMAJOR.x` — `v3.x`, `v2.x`. The
highest major is the default branch and receives features and fixes. The previous major
receives **security fixes only**, never features, and is published on its own when
needed. Two majors back leaves support once the current one is stable. The `latest`
dist-tag always points at the highest semver published, not at whatever was published
most recently, so a security backport to an older major never pulls `latest` backwards.

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
