---
layout: home
title: Wickra Screener — scan thousands of symbols, one condition tree
titleTemplate: false

hero:
  name: "Wickra Screener"
  text: "Scan thousands. One condition tree."
  tagline: "Parallel multi-symbol screening over 514 streaming indicators. A screen is a JSON condition tree — data, not code — deterministic and byte-identical across ten languages."
  image:
    src: /wickra-mark.svg
    alt: Wickra Screener
  actions:
    - theme: brand
      text: View on GitHub
      link: https://github.com/wickra-lib/wickra-screener
    - theme: alt
      text: Conditions & ScanSpec
      link: https://github.com/wickra-lib/wickra-screener/blob/main/docs/CONDITIONS.md
    - theme: alt
      text: API
      link: /api/rust

features:
  - icon: 🌲
    title: The screen is JSON, not code
    details: A scan is a serde ScanSpec — a condition tree of indicator, price and constant expressions combined with all/any/not. Because it is data, the exact same screen crosses the C ABI and WASM unchanged.
  - icon: 📈
    title: 514 indicators
    details: "Every condition can reference any of the 514 O(1) streaming indicators from the Wickra core — Rsi, Ema, Macd, BollingerBands and the rest — evaluated at the latest bar."
  - icon: ⚡
    title: Parallel over the universe
    details: Thousands of symbols are folded and evaluated in parallel with rayon, or sequentially on the WASM fallback path. Both produce a byte-for-byte identical ranked report.
  - icon: 🌐
    title: Ten languages, one screen
    details: "The core is a JSON-over-C-ABI data API (Screener::command) in Rust, Python, Node.js, WASM, C, C++, C#, Go, Java and R. A developer in any language runs the same screen."
  - icon: 🔀
    title: Cross-section & breadth
    details: "Rank, percentile and z-score a symbol's metric across the whole universe, or gate matches on a market-wide predicate (\"60% of the universe above its Sma(200)\") — the thing a per-symbol loop cannot express."
  - icon: 🧪
    title: Deterministic, proven
    details: The parallel and sequential paths are byte-identical, pinned by a golden corpus replayed through all ten bindings in CI. No RNG, stable sort, ties broken by symbol key.
---

<script setup>
const installTabs = [
  { label: 'Python', lang: 'bash', code: 'pip install wickra-screener' },
  { label: 'Node',   lang: 'bash', code: 'npm install wickra-screener' },
  { label: 'Rust',   lang: 'bash', code: 'cargo add wickra-screener' },
  { label: 'WASM',   lang: 'bash', code: 'npm install wickra-screener-wasm' },
  { label: 'C',      lang: 'bash', code: '# prebuilt header + library from GitHub releases:\n# github.com/wickra-lib/wickra-screener/releases' },
  { label: 'C#',     lang: 'bash', code: 'dotnet add package WickraScreener' },
  { label: 'Go',     lang: 'bash', code: 'go get github.com/wickra-lib/wickra-screener-go' },
  { label: 'Java',   lang: 'xml',  code: '<!-- Maven Central -->\n<dependency>\n  <groupId>org.wickra</groupId>\n  <artifactId>wickra-screener</artifactId>\n  <version>0.1.0</version>\n</dependency>' },
  { label: 'R',      lang: 'r',    code: 'install.packages("wickrascreener", repos = "https://wickra-lib.r-universe.dev")' },
]

const pyCode = `import json
from wickra_screener import Screener

spec = json.dumps({
    "universe": ["AAA", "BBB"],
    "condition": {
        "type": "cmp",
        "left": {"kind": "indicator", "name": "Rsi", "params": [14]},
        "op": "lt",
        "right": {"kind": "const", "value": 30.0},
    },
})

screener = Screener(spec)
response = screener.command(json.dumps({"cmd": "scan", "data": data}))
report = json.loads(response)
for match in report["matches"]:
    print("matched:", match["symbol"])`

const nodeCode = `import { Screener } from 'wickra-screener'

const spec = JSON.stringify({
  universe: ['AAA', 'BBB'],
  condition: {
    type: 'cmp',
    left: { kind: 'indicator', name: 'Rsi', params: [14] },
    op: 'lt',
    right: { kind: 'const', value: 30.0 },
  },
})

const screener = new Screener(spec)
const report = JSON.parse(screener.command(JSON.stringify({ cmd: 'scan', data })))
for (const match of report.matches) console.log('matched:', match.symbol)`

const cliCode = `# Scan a directory of <SYMBOL>.csv candle files against a spec:
wickra-screener --spec golden/specs/momentum.json --data golden/data

# Raw ScanReport JSON — the same bytes every binding returns:
wickra-screener --spec golden/specs/momentum.json --data golden/data --format json`

const snippetTabs = [
  { label: 'Python', lang: 'python',     code: pyCode },
  { label: 'Node',   lang: 'javascript', code: nodeCode },
  { label: 'CLI',    lang: 'bash',       code: cliCode },
]
</script>

## The screen is JSON, not code

A scan is a `ScanSpec`: a `universe`, a `condition` tree, and an optional `rank`
and `limit`. Expressions are constants, price fields or indicators; conditions
compare, cross or aggregate them.

```json
{
  "universe": ["AAA", "BBB", "CCC"],
  "condition": {
    "type": "all",
    "conditions": [
      { "type": "cmp",
        "left":  { "kind": "indicator", "name": "Rsi", "params": [14] },
        "op":    "lt",
        "right": { "kind": "const", "value": 30.0 } },
      { "type": "cmp",
        "left":  { "kind": "indicator", "name": "Ema", "params": [7] },
        "op":    "crosses_above",
        "right": { "kind": "indicator", "name": "Ema", "params": [19] } }
    ]
  },
  "rank": { "by": { "kind": "indicator", "name": "Roc", "params": [10] }, "desc": true },
  "limit": 25
}
```

## Install

The same screen from every language — native Rust, Python, Node.js and WASM, plus
a C ABI for C, C++, C#, Go, Java and R.

<InstallTabs :tabs="installTabs" />

## Run it from any language

Construct a `Screener` from the JSON spec, then drive it with
`command(json) -> json`. Every binding returns the same bytes.

<InstallTabs :tabs="snippetTabs" />

## Built on the Wickra core

Wickra Screener is part of the [Wickra](https://wickra.org) ecosystem. Every
condition draws on the 514 O(1) streaming indicators of
[`wickra-core`](https://github.com/wickra-lib/wickra), so a screen sees exactly
the same numbers a backtest or a live chart would.

> Wickra Screener is a software library, not a trading system, and comes with no
> warranty — use at your own risk.
