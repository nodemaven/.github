# .github

Organization-level defaults for [github.com/nodemaven](https://github.com/nodemaven).

GitHub reads two things out of this repository automatically:

**`profile/README.md`** renders on the organization landing page at github.com/nodemaven.
Nothing else does. Editing it here is how that page changes.

**Community health files** apply to every repository in the organization that does not
carry its own copy:

| File | Where it shows up |
|---|---|
| `CONTRIBUTING.md` | Linked when someone opens an issue or PR |
| `SECURITY.md` | The "Report a vulnerability" tab |
| `CODE_OF_CONDUCT.md` | Linked in the community profile |
| `.github/ISSUE_TEMPLATE/` | The template picker when opening an issue |
| `.github/PULL_REQUEST_TEMPLATE.md` | Pre-fills the PR description |

A repository with its own version of any of these overrides the default. Nothing here is
inherited into a repo's own files - it is fallback, not merge.

The two paths are not interchangeable, and the difference has no error message. Issue
templates and their `config.yml` are read **only** from `.github/ISSUE_TEMPLATE/`; the
other three files may sit in the root, in `.github/` or in `docs/`. Templates left in a
root-level `ISSUE_TEMPLATE/` are committed, rendered on the file listing, and never
offered to anyone opening an issue. They were in exactly that place here until
2026-08-18.

## What does not live here

Per-repository settings: description, topics, social preview image, branch protection.
Those are set on each repository directly.

Organization settings: avatar, display name, website link, pinned repositories.
Those are set in organization settings and need owner rights.

## Editing

This repository is public. Everything in it is visible, including drafts. There is no
staging area for the org profile - a merge to `main` is a publish.
