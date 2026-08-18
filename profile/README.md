<div align="center">

# NodeMaven

**Next gen web operator.**

Residential and mobile proxy infrastructure, and the open tooling that proves it works.

[Website](https://nodemaven.com?utm_source=github&utm_medium=org_profile&utm_campaign=oss) ·
[Docs](https://docs.nodemaven.com?utm_source=github&utm_medium=org_profile&utm_campaign=oss) ·
[Telegram](https://t.me/node_maven) ·
[support@nodemaven.com](mailto:support@nodemaven.com)

</div>

---

## What is here

Two kinds of repository. **SDKs** wrap the gateway in one language each, so you are not
hand-building proxy usernames or wiring auth into a browser. **Tools** are the things we
built to answer our own questions and had no reason to keep private - chief among them a
benchmark harness that measures block rates against live targets for any provider,
including ours.

| I want to... | Go to |
|---|---|
| Make my first request through a proxy in under 10 minutes | [Quickstart](https://docs.nodemaven.com?utm_source=github&utm_medium=org_profile&utm_campaign=quickstart) |
| Use NodeMaven from my language | [SDKs](#sdks) |
| Work out why a target is blocking me | [Anti-bot detection layers](https://github.com/nodemaven/proxy-benchmark#the-layer-model) |
| Compare providers on my own targets | [proxy-benchmark](https://github.com/nodemaven/proxy-benchmark) |

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

### Tools

| Repository | What it does |
|---|---|
| [proxy-benchmark](https://github.com/nodemaven/proxy-benchmark) | Measures success, captcha and block rates against live targets, for any provider |

---

## We publish our numbers, including the ones we lose on

Most proxy benchmarks are marketing. Ours is a repository you can run: every verdict is
read off the response body rather than the status code, every row lands in JSONL you can
re-read offline, and the runner has never been told which provider it is talking to - it
takes a host, a port and a username out of the environment, so pointing it at a
competitor's gateway is a credentials change rather than a code change.

Each question below is a matrix whose arms are interleaved inside one time window, with a
fresh exit per probe. Two arms run at 10:00 and 14:00 would measure the hour rather than
the thing under test, so the runner goes round-robin across cells and never in sequence.

| What we tested | Result | Sample |
|---|---|---|
| Does a proven exit keep working? | **Yes. 108/109 held queries pass, 99%** | 120 identities, one 1 h 54 window |
| Does warming an exit first help? | **No effect.** 32% vs 30%, Fisher p = 1.0 | same run, both arms interleaved |
| Does pinning `country=us` help? | **No, it costs you.** 13% vs 52% for every other setting, p = 1.5e-05 | 225 attempts over two windows |
| Is the browser the bottleneck on Google? | **No, it is the address.** Of the pages Google served, the script-running engines parsed every one: patchright 309/309, zendriver 168/168 | every run on disk |
| Is there a best anti-detect framework? | **No. It is a diagonal** - the winner changes with the target | every run on disk |

The `country=us` row is about our own product, and it stays in the table. A benchmark that
only shows wins is worth nothing to the person forking it.

Two caveats we would want if we were reading someone else's table. The hold figure is
conditional and censored: every held query follows a probe the target already served, and
a series stops at its first refusal, so later positions are drawn from survivors. And every
rate here is a reading of the hours it was taken in - one target's yield moved 17 points
between two afternoons of the same day, which is why the sample column names the window and
why the repository keeps the claims that did not survive replication next to the ones that
did.

**[Read the methodology and re-run it yourself →](https://github.com/nodemaven/proxy-benchmark)**

---

## What we learned building these

Short version of things that cost us time, so they do not cost you any:

- **A working IP is not a passing IP.** A blocked page usually returns HTTP 200 with a stub
  body. Measure by content, never by status code.
- **Finding an exit a target will serve is the expensive event.** Making a second query on one
  that already worked is nearly free. Never do query, new session, query.
- **Headless Chromium announces itself.** Some targets read one substring in the User-Agent and
  nothing else: 95/95 pass for engines that omit it, 0/50 for engines that send it.
- **The failure mode determines the reaction.** Refused before the page means rotate the exit.
  Served but not parsed means change the config. Confusing the two wastes both.

Full write-ups live in [proxy-benchmark](https://github.com/nodemaven/proxy-benchmark).

---

## Contributing

Issues and pull requests are welcome on every repository here, including ones that tell us our
numbers are wrong. If you can reproduce a result that contradicts ours, open an issue with the
raw rows - that is the most useful thing you can send us.

See [CONTRIBUTING.md](https://github.com/nodemaven/.github/blob/main/CONTRIBUTING.md).

Security reports: [SECURITY.md](https://github.com/nodemaven/.github/blob/main/SECURITY.md).

---

<div align="center">

[nodemaven.com](https://nodemaven.com?utm_source=github&utm_medium=org_profile&utm_campaign=footer) ·
[Docs](https://docs.nodemaven.com?utm_source=github&utm_medium=org_profile&utm_campaign=footer) ·
[X](https://x.com/NodeMaven) ·
[LinkedIn](https://www.linkedin.com/company/nodemaven) ·
[Telegram](https://t.me/node_maven)

</div>
