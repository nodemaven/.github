# Contributing

Thanks for taking the time. This applies to every repository under
[github.com/nodemaven](https://github.com/nodemaven).

## Before you write code

For anything larger than a typo, open an issue first. It costs you five minutes and can
save you an afternoon of work we would have to turn down.

Small fixes - typos, broken links, a wrong flag in the docs - go straight to a pull
request, no issue needed.

## Reporting a benchmark result that contradicts ours

This is the most valuable kind of report we get, and it has its own rules:

- include the raw rows, not a summary
- state the time window - target behaviour moves by double digits between two afternoons
  of the same day, so a result measured at a different hour is not comparable
- state whether arms were interleaved or run in sequence. Sequential arms measure the
  hour, not the thing under test
- name the exact engine version and the exact connection parameters

We will re-run it. If you are right, the number changes and you are credited in the
write-up.

## Pull requests

- one logical change per pull request
- keep the diff focused: unrelated formatting changes make review slower for everyone
- add or update tests when behaviour changes
- update the README when the interface changes
- CI has to be green before review

Commit messages: imperative mood, one line summary, body explaining why rather than what.

## Code style

Each repository carries its own linter configuration and a `make lint` target. Run it
before pushing. If the linter and this document disagree, the linter wins.

## What we will not merge

- credentials, tokens or API keys in any form, including in test fixtures
- code that retries a failed request by rotating to a new session in a loop. It degrades
  the exit pool for every other user and makes the original failure worse
- benchmark changes that alter methodology and results in the same commit. Split them, so
  the effect of the methodology change is visible on its own

## Licensing

By contributing you agree that your contribution is licensed under the same license as the
repository it goes into.
