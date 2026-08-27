<div align="center">

<!-- The logo asset is committed and rendering. Checked against the live page on
     2026-08-25: the relative src resolves to
     /nodemaven/.github/raw/main/profile/assets/nodemaven-head.png and serves 200.
     Keep the src relative - it survives a fork, an absolute raw.githubusercontent
     URL does not. The wordmark and the slogan are pixels inside this file, so
     changing either means re-cutting the asset and updating alt in the same commit. -->

<a href="https://nodemaven.com/?utm_term=github&utm_content=nodemaven_readme"><img src="./assets/nodemaven-head.png" alt="NodeMaven"></a>

# NodeMaven

Residential and mobile proxy infrastructure. Open tooling that proves it works.

<a href="https://nodemaven.com/?utm_term=github&utm_content=nodemaven_readme"><img src="./assets/website-badge.svg" alt="Website"></a>
<a href="https://docs.nodemaven.com?utm_source=github&utm_medium=org_profile&utm_campaign=badge"><img src="./assets/docs-badge.svg" alt="Docs"></a>
<a href="https://t.me/node_maven"><img src="./assets/telegram-badge.svg" alt="Telegram"></a>
<a href="https://x.com/NodeMaven"><img src="./assets/x-badge.svg" alt="X"></a>
<a href="https://www.linkedin.com/company/nodemaven"><img src="./assets/linkedin-badge.svg" alt="LinkedIn"></a>

</div>

<!-- One badge style per row, and repository-status badges are deliberately not up
     here: a CI gate, a licence and a row count belong to proxy-benchmark rather
     than to the organization, so they sit beside that repository in Tools below.
     Five social badges in one style is the shape an org landing page reads best in. -->

---

## What this is

NodeMaven runs a residential and mobile proxy gateway. Country, city, ISP, the sticky
session and how long it holds are set in the username rather than through an API, so any
HTTP client in any language reaches it without a library.

This organization is the code side of that: an SDK per language, each going to that
language's own registry as it ships. Product documentation and sign-up are on
[nodemaven.com](https://nodemaven.com/?utm_term=github&utm_content=nodemaven_readme) - what
is here is source, and none of it needs an account to read.

<!-- This section used to open with a request in Python and three paragraphs on how the
     gateway answers a malformed username. Both are true and both belong in the docs and in
     the SDK README, not on a landing page: a reader arriving here is deciding whether this
     organization is worth their time, and a code block is an answer to a question they have
     not asked yet.
     The same call removed a results table that stood below Repositories - six questions with
     their denominators and the commands that re-derive them. Nothing was lost: every one of
     those numbers, its denominator and the command that re-derives it is in the README of
     the repository that produced it, which is where a figure can sit next to the rows behind
     it. Do not paste the table back here; if the front page should carry those numbers, it
     carries one link to them, and only once that repository is public. -->

---

## Repositories

### SDKs

<!-- The column is the name you install, not the name of the repository - those differ
     for Python (`nodemaven` on PyPI, `nodemaven-python` on GitHub) and getting it
     wrong sends a reader to a `pip install` that fails.
     Status is read off the registry, not off intent. Checked 2026-08-25:
     pypi.org/project/nodemaven answers 200 with 0.1.1, and `pip install nodemaven`
     into a clean venv succeeded, so "not published yet" - which this table said
     until today - was false for the Python row.
     The repository behind it is still internal and answers 404 anonymously, so the
     link goes to PyPI, which is public, rather than to GitHub, which is not. -->

| Install | Registry | Status |
|---|---|---|
| [`nodemaven`](https://pypi.org/project/nodemaven/) | PyPI | **0.1.1, published** |
| `nodemaven-node` | npm | Not started |
| `nodemaven-go` | Go module | Not started |
| `nodemaven-rust` | crates.io | Not started |

Only the Python one exists. Its source is not public yet, so the row links to the package
rather than to a repository; the three below it are names, not work in progress.

<!-- This paragraph used to promise "browser adapters that handle proxy auth for you,
     traffic-saving presets, and rotation with a circuit breaker". The shipped Python
     SDK does none of those, and refuses the last one on purpose: its README documents
     that past six consecutive failures the next attempt succeeds 0.5% of the time,
     measured over 1464 attempts, so automatic retry spends a user's pool on their
     behalf. An org page promising retry above a library whose headline is that it
     does not retry is the first thing a hostile reader would catch. -->

What ships today builds the gateway username and validates it before anything is sent:
an unknown parameter name is answered `200` with the setting silently dropped, so the
only place that mistake can be caught is client-side. It opens no socket, holds no
session and retries nothing - the HTTP client stays yours.
<!--
### Tools

| Repository | What it does | Language |
|---|---|---|
| [proxy-benchmark](https://github.com/nodemaven/proxy-benchmark) | Measures pass, captcha and block rates against live targets, for any provider and eleven browser engines | Python |

[![gate](https://img.shields.io/github/actions/workflow/status/nodemaven/proxy-benchmark/ci.yml?style=flat-square&label=gate)](https://github.com/nodemaven/proxy-benchmark/actions/workflows/ci.yml)
[![license](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](https://github.com/nodemaven/proxy-benchmark/blob/main/LICENSE)
[![python](https://img.shields.io/badge/python-3.11%20%7C%203.13-blue?style=flat-square)](https://github.com/nodemaven/proxy-benchmark)
[![rows](https://img.shields.io/badge/rows-12%2C173%20published-blue?style=flat-square)](https://github.com/nodemaven/proxy-benchmark/tree/main/data/runs)
-->

<!-- Uncomment the two blocks above on the day proxy-benchmark becomes public, and not
     before. Measured anonymously on 2026-08-25, github.com/nodemaven/proxy-benchmark
     answers 404 to a logged-out visitor because the repository is internal - the same 404
     it gave when the repository did not exist at all. Creating it did not make these links
     work. The row count in the badge above was re-counted on 2026-08-25: 12,173 rows
     across data/runs/, where the badge previously said 3,701. -->
---

## Contributing

Issues and pull requests are welcome on every repository here, including the ones that say a
number we published is wrong. A result that contradicts one of ours, sent with the raw rows
behind it, is the most useful thing this organization can receive - our repositories already
keep several corrections of our own claims, and one more costs nothing.

See [CONTRIBUTING.md](https://github.com/nodemaven/.github/blob/main/CONTRIBUTING.md).

Security reports: [SECURITY.md](https://github.com/nodemaven/.github/blob/main/SECURITY.md).

---

<div align="center">

[nodemaven.com](https://nodemaven.com/?utm_term=github&utm_content=nodemaven_readme) ·
[Docs](https://docs.nodemaven.com?utm_source=github&utm_medium=org_profile&utm_campaign=footer) ·
[X](https://x.com/NodeMaven) ·
[LinkedIn](https://www.linkedin.com/company/nodemaven) ·
[Telegram](https://t.me/node_maven) ·
[support@nodemaven.com](mailto:support@nodemaven.com)

</div>
