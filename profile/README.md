<div align="center">

<a href="https://nodemaven.com/?utm_source=github&utm_medium=org_profile&utm_campaign=github_org&utm_content=banner">
  <img src="./assets/banner.png" alt="NodeMaven">
</a>

# NodeMaven

**Residential and mobile proxy infrastructure with open-source SDKs, benchmarks, and tooling for scraping and browser automation.**

<a href="https://nodemaven.com/?utm_source=github&utm_medium=org_profile&utm_campaign=github_org&utm_content=website_badge">
  <img src="./assets/website-badge.svg" alt="Website">
</a>
<a href="https://docs.nodemaven.com?utm_source=github&utm_medium=org_profile&utm_campaign=github_org&utm_content=docs_badge">
  <img src="./assets/docs-badge.svg" alt="Docs">
</a>
<a href="https://t.me/NodeMavenTG">
  <img src="./assets/telegram-badge.svg" alt="Telegram">
</a>
<a href="https://x.com/NodeMaven">
  <img src="./assets/x-badge.svg" alt="X">
</a>
<a href="https://www.linkedin.com/company/nodemaven">
  <img src="./assets/linkedin-badge.svg" alt="LinkedIn">
</a>

</div>

---

## Open source

### SDKs

| Repository | Registry | What it does |
|---|---|---|
| [`nodemaven-python`](https://github.com/nodemaven/nodemaven-python) | [PyPI](https://pypi.org/project/nodemaven/) | Python SDK: builds and validates the gateway username, checks a proxy, and calls the account API |
| [`nodemaven-rust`](https://github.com/nodemaven/nodemaven-rust) | [crates.io](https://crates.io/crates/nodemaven) | Rust SDK: a builder with typed errors, provider definitions, connection checks, and an account API client |
| [`nodemaven-go`](https://github.com/nodemaven/nodemaven-go) | [pkg.go.dev](https://pkg.go.dev/github.com/nodemaven/nodemaven-go) | Go SDK: builds and validates the gateway username, checks a proxy, and calls the account API |

```bash
# Python
pip install nodemaven

# Rust
cargo add nodemaven

# Go
go get github.com/nodemaven/nodemaven-go
```

The SDKs keep the HTTP client under your control. They build the proxy configuration, validate what can be checked locally, and hand the result to the client or browser you already use. Each also has a client for the account API: sub-users, IP whitelist, usage statistics, and the location catalogue.

### AI agents

[`nodemaven-mcp`](https://github.com/nodemaven/nodemaven-mcp) is an MCP server that connects Claude, Cursor and other MCP clients to a NodeMaven account: geo-targeted proxy strings with sticky sessions, connection checks, a site check through the proxy, locations, traffic usage, sub-users and whitelisted IPs. Read-only by default; the tools that change the account are switched on explicitly. On [PyPI](https://pypi.org/project/nodemaven-mcp/) and the official MCP Registry.

```bash
uvx nodemaven-mcp   # with NODEMAVEN_APIKEY set
```

[`skills`](https://github.com/nodemaven/skills) is a Claude Code plugin: skills for proxy setup in code, the SDKs, the account API, Google scraping, proxy benchmarking and troubleshooting, with the MCP server included.

```text
/plugin marketplace add nodemaven/skills
/plugin install nodemaven@nodemaven
```

### Google Browser Scraper

[`google-browser-scraper`](https://github.com/nodemaven/google-browser-scraper) is a self-hosted SERP API alternative: Google search results from a real browser through your own sticky proxy, from any provider.

It warms the proxy session with ordinary browsing, opens Google's results page, and checks whether Google served results or refused before parsing. Captchas and blocks are reported as such, never as an empty result. It runs as a CLI, a Python library, a local HTTP API, an MCP server, or a Docker image.

```bash
pip install google-browser-scraper
patchright install chromium

# or
docker run --rm ghcr.io/nodemaven/google-browser-scraper doctor
```

### Proxy Benchmark

[`proxy-benchmark`](https://github.com/nodemaven/proxy-benchmark) is a reproducible benchmark harness for separating proxy, browser, host, handshake, and target-side failures.

It compares controlled combinations of:

- proxy providers, gateways, countries, and sticky sessions;
- plain HTTP clients, Chromium, patched browsers, CDP drivers, and anti-detect frameworks;
- target-side verdicts such as `ok`, `captcha`, `block`, `empty`, and harness-level `error`;
- browser fingerprints, TLS behavior, exit reputation, and host-level effects.

The raw JSONL rows are the source of truth. Result tables, denominators, confidence intervals, run IDs, and research notes are kept alongside the data rather than reduced to a single success-rate number.

[![gate](https://img.shields.io/github/actions/workflow/status/nodemaven/proxy-benchmark/ci.yml?style=flat-square&label=gate)](https://github.com/nodemaven/proxy-benchmark/actions/workflows/ci.yml)
[![license](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](https://github.com/nodemaven/proxy-benchmark/blob/main/LICENSE)
[![python](https://img.shields.io/badge/python-3.11%20%7C%203.13-blue?style=flat-square)](https://github.com/nodemaven/proxy-benchmark)

**Start here:**  
[README](https://github.com/nodemaven/proxy-benchmark) ·
[Full results](https://github.com/nodemaven/proxy-benchmark/blob/main/RESULTS.md) ·
[Research notebook](https://github.com/nodemaven/proxy-benchmark/blob/main/NOTEBOOK.md) ·
[Quickstart](https://github.com/nodemaven/proxy-benchmark/blob/main/docs/quickstart.md)

---

## How NodeMaven fits into your stack

NodeMaven exposes residential and mobile proxies through a standard proxy gateway.

Targeting and session configuration are encoded in the proxy username, so the gateway can be used directly from tools and clients such as:

`cURL` · `requests` · `httpx` · `reqwest` · Go `net/http` · `Playwright` · `Patchright` · `Puppeteer` · Chromium-based automation

The SDKs are optional. Their role is to make that configuration safer and easier to work with in code, while leaving requests, browser lifecycle, connection pooling, retries, and application logic to your existing stack.

For product setup, authentication, targeting options, and account features, use the
[NodeMaven documentation](https://docs.nodemaven.com?utm_source=github&utm_medium=org_profile&utm_campaign=github_org&utm_content=product_docs).

No account yet? [Sign up](https://dashboard.nodemaven.com/accounts/signup/?utm_source=github&utm_medium=org_profile&utm_campaign=github_org&utm_content=signup_promo) and enter the code **GITHUB** for 2 GB of free traffic, once per account.

---

## Engineering principles

The repositories here are built around a few simple rules:

- **Measure before attributing.** A failed request alone does not tell you whether the proxy, browser, host, handshake, or target caused it.
- **Keep evidence reproducible.** Benchmark conclusions should trace back to raw rows, parameters, and run IDs.
- **Fail locally when possible.** Configuration mistakes that can be identified before opening a socket should not become ambiguous gateway failures.
- **Keep the transport yours.** SDKs should integrate with existing HTTP clients and browser frameworks rather than replacing them.
- **Corrections are part of the record.** If a later experiment contradicts an earlier conclusion, the correction belongs beside the original evidence.

---

## Contributing

Issues and pull requests are welcome across the public repositories.

For benchmark findings, a contradiction backed by raw rows or a reproducible test case is especially useful. The goal is not to preserve a conclusion; it is to preserve enough evidence to check it.

See [CONTRIBUTING.md](https://github.com/nodemaven/.github/blob/main/CONTRIBUTING.md).

Security reports: [SECURITY.md](https://github.com/nodemaven/.github/blob/main/SECURITY.md).

---

<div align="center">

[Website](https://nodemaven.com/?utm_source=github&utm_medium=org_profile&utm_campaign=github_org&utm_content=footer) ·
[Documentation](https://docs.nodemaven.com?utm_source=github&utm_medium=org_profile&utm_campaign=github_org&utm_content=footer) ·
[PyPI](https://pypi.org/project/nodemaven/) ·
[crates.io](https://crates.io/crates/nodemaven) ·
[pkg.go.dev](https://pkg.go.dev/github.com/nodemaven/nodemaven-go) ·
[X](https://x.com/NodeMaven) ·
[LinkedIn](https://www.linkedin.com/company/nodemaven) ·
[Telegram](https://t.me/NodeMavenTG) ·
[support@nodemaven.com](mailto:support@nodemaven.com)

</div>
