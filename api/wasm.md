# WASM

A `wasm-bindgen` build for the browser and other WebAssembly runtimes. The same
`Screener` handle and JSON command protocol as the native bindings — this is the
sequential path that produces byte-identical output to the parallel scan.

```bash
npm install wickra-screener-wasm
```

```javascript
import init, { Screener } from 'wickra-screener-wasm'

await init()

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
for (const match of report.matches) console.log('matched:', match.symbol)
```

## More

- [npm (wickra-screener-wasm)](https://www.npmjs.com/package/wickra-screener-wasm)
- [Source & bindings](https://github.com/wickra-lib/wickra-screener/tree/main/bindings/wasm)
