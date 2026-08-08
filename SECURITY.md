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
