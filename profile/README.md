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
<a href="https://t.me/node_maven">
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
| [`nodemaven-python`](https://github.com/nodemaven/nodemaven-python) | [PyPI](https://pypi.org/project/nodemaven/) | Python SDK for building and validating proxy configuration before a request is sent |
| [`nodemaven-rust`](https://github.com/nodemaven/nodemaven-rust) | [crates.io](https://crates.io/crates/nodemaven) | Rust SDK with a builder API, typed errors, provider definitions, and connection checks |

```bash
# Python
pip install nodemaven

# Rust
cargo add nodemaven
```

Both SDKs keep the HTTP client under your control. They build the proxy configuration, validate what can be checked locally, and hand the result to the client or browser you already use.

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

`cURL` · `requests` · `httpx` · `reqwest` · `Playwright` · `Patchright` · `Puppeteer` · Chromium-based automation

The SDKs are optional. Their role is to make that configuration safer and easier to work with in code, while leaving requests, browser lifecycle, connection pooling, retries, and application logic to your existing stack.

For product setup, authentication, targeting options, and account features, use the
[NodeMaven documentation](https://docs.nodemaven.com?utm_source=github&utm_medium=org_profile&utm_campaign=github_org&utm_content=product_docs).

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
[X](https://x.com/NodeMaven) ·
[LinkedIn](https://www.linkedin.com/company/nodemaven) ·
[Telegram](https://t.me/node_maven) ·
[support@nodemaven.com](mailto:support@nodemaven.com)

</div>
