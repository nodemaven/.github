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
<!--
## What is here

Two kinds of repository. **SDKs** wrap the gateway in one language each, so you are not
hand-building proxy usernames or wiring auth into a browser. **Tools** answer questions that
came up internally and had no reason to stay private - chief among them a benchmark harness
that measures block rates against live targets for any provider, NodeMaven included.

| I want to... | Go to |
|---|---|
| Make my first request through a proxy in under 10 minutes | [Quickstart](https://docs.nodemaven.com?utm_source=github&utm_medium=org_profile&utm_campaign=quickstart) |
| Never have seen a terminal before and still get a row of data | [proxy-benchmark quickstart](https://github.com/nodemaven/proxy-benchmark/blob/main/docs/quickstart.md) |
| Use NodeMaven from my language | [SDKs](#sdks) |
| Work out why a target is blocking me | [The three layers](https://github.com/nodemaven/proxy-benchmark#what-it-measures) |
| Measure my own proxies, ours or anybody's | [proxy-benchmark](https://github.com/nodemaven/proxy-benchmark) |
| Check a number we published, offline, without an account | [Reproduce these numbers](https://github.com/nodemaven/proxy-benchmark#reproduce-these-numbers) |
-->
## What a request looks like

The gateway takes its parameters in the username, separated by hyphens, so any HTTP client
in any language can reach it without a library:

```python
import requests

proxy = "http://<login>-country-us-sid-abc123-ttl-10m:<password>@gate.nodemaven.com:8080"
r = requests.get("https://ipinfo.io/json", proxies={"http": proxy, "https": proxy})
print(r.json()["ip"])
```

`sid` holds one exit across requests, `ttl` says for how long. The sticky key is the whole
parameter set rather than `sid` alone - change any parameter and the exit changes with it,
which is the kind of thing probing a gateway tells you and reading its documentation does
not.

Seven malformed inputs produce seven different replies, and none of them names the cause.
One is a 200 with the setting silently dropped, so a run completes while every row claims a
parameter that was never applied. Checking the exit address per request is the only defence,
which is why the harness records one on every row.

---

## Repositories

### SDKs

| Package | Registry | Status |
|---|---|---|
| `nodemaven-python` | PyPI | In development |
| `nodemaven-node` | npm | Planned |
| `nodemaven-go` | Go module | Planned |
| `nodemaven-rust` | crates.io | Planned |

None of these are published yet, so none of them are linked - a name in this table becomes
a link on the day the repository is public, and not before.

Every SDK covers the same ground: typed connection parameters with client-side validation,
browser adapters that handle proxy auth for you, traffic-saving presets, and rotation with a
circuit breaker so a bad run does not make itself worse.
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

## The numbers, including the ones that go against us

Every verdict is read off the response body rather than the status code, every row lands in
JSONL that can be re-read offline, and the runner is never told which provider it is talking
to: it takes a host, a port and a username out of the environment. Pointing it at a
competitor's gateway, or at proxies you already own, is a credentials change and not a code
change.

Each question below is a matrix whose arms are interleaved inside one time window, with a
fresh exit per probe. Two arms run at 10:00 and 14:00 would measure the hour rather than the
thing under test, so the runner goes round-robin across cells and never in sequence.

| Question | Answer | Denominator, and the command that re-derives it |
|---|---|---|
| Does a proven exit keep working? | **Yes. 108 of 109 held queries passed, 99%** | one run, 120 identities, 1 h 54 min: `held.py --run data/runs/probehold_20260813T202606Z.jsonl` |
| Does warming an exit first help? | **No. 32% against 30%**, n = 60 and 60 | same run, arms interleaved, same command |
| Does pinning `country=us` help? | **No, it costs.** 13% served against 44-62% for `de`, `gb`, `any` and `ru`. Pooled, 5/26 against 53/102, Fisher exact **p = 0.0036** | 225 attempts over two windows |
| Is the browser the bottleneck on Google? | **No, the address is.** Of the pages Google served, Patchright parsed **108 of 108** | every run on disk: `report.py --all`, the `google_serp` block |
| Does hardening a browser help on Amazon? | **Not on this evidence.** An unmodified Chromium scored **96%**, the best of the eight engines tried; the most heavily patched one scored 63% | 7627 attempts, 130 h: `report.py data/runs/benchmark_20260819T055927Z.jsonl` |
| Is there a best anti-detect framework? | **No. It is a diagonal** - the winner changes with the target | every run on disk |

Two of those rows are losses. The `country=us` row is about a NodeMaven setting and it stays
in the table. The Amazon row says the anti-detect tooling this harness exists to compare did
not beat a stock browser on that target, which is not the result anyone here wanted, and it
replaced an earlier table that said the opposite - the correction is in the repository next
to the claim it replaced.

Three caveats worth having if this were someone else's table:

- **The hold figure is conditional and censored.** Every held query follows a probe the
  target already served, and a series stops at its first refusal, so later positions are
  drawn from survivors.
- **Every rate is a reading of the hours it was taken in.** One target's yield moved 17
  points between two afternoons of the same day. That is why the denominator column names
  the window, and why claims that did not survive replication are kept beside the ones that
  did.
- **Pooled is the weaker reading.** `--all` merges runs from different weeks into a number
  belonging to neither. Where a row above names a single run, that is deliberate and the
  pooled figure differs.

Every figure above comes out of a command that reads committed rows and sends nothing - no
account, no gateway, no traffic. The repository is internal while the code is reviewed, so
this is what checking one of them will look like rather than something that runs today:

```bash
git clone https://github.com/nodemaven/proxy-benchmark && cd proxy-benchmark
pip install -r requirements-ci.txt
python scripts/analysis/report.py --all
python scripts/analysis/held.py --run data/runs/probehold_20260813T202606Z.jsonl
```

---


## Contributing

Issues and pull requests are welcome on every repository here, including the ones that say a
published number is wrong. A result that contradicts one of these tables, sent with the raw
rows behind it, is the most useful thing this organization can receive - the repository
already keeps several corrections of its own claims, and one more costs nothing.

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
