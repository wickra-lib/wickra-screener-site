# About Wickra Screener

Wickra Screener scans thousands of symbols in parallel against a single condition
tree over the 514 streaming indicators of the Wickra core. A screen is a JSON
document — **data, not code** — so the exact same scan runs in every one of ten
languages and returns byte-for-byte identical results.

## What makes it different

- **The screen is data.** A serde `ScanSpec` — a `universe`, a `condition` tree of
  indicator / price / constant expressions combined with `all` / `any` / `not`, and
  an optional `rank` and `limit`. Because it is data, it crosses the C ABI and WASM
  unchanged.
- **514 indicators.** Any condition can reference any Wickra indicator (`Rsi`,
  `Ema`, `Macd`, `BollingerBands`, …), evaluated at the latest bar.
- **Parallel and deterministic.** The universe is folded in parallel with rayon, or
  sequentially on the WASM path — both produce a byte-identical ranked report,
  pinned by a golden corpus in CI.
- **Cross-section & breadth.** Rank, percentile and z-score a symbol across the
  whole universe, or gate matches on a market-wide predicate — things a per-symbol
  loop cannot express.

## Why it exists

Screeners are usually one language, one hard-coded rule set. Wickra Screener defines
the scan surface **once**, in Rust, and exposes it as a JSON-over-C-ABI data API to
Rust, Python, Node.js, WASM and — over a C ABI — C, C++, C#, Go, Java and R. The
screen itself is portable JSON, so the same rule set runs anywhere.

## Open source

Released under the **MIT OR Apache-2.0** license — permissive, OSI-approved, free
for any use including commercial. Source, issues and releases on
[GitHub](https://github.com/wickra-lib/wickra-screener).

## Disclaimer

Wickra Screener is a software library, **not** a trading system, and is provided
**as-is with no warranty**. It surfaces conditions over market data; it does not
give financial advice. Use it at your own risk.
