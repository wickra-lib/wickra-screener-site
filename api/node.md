# Node.js

Native napi-rs bindings over the Rust core. Construct a `Screener` from a JSON
spec, then drive it with `command(json) -> json`.

```bash
npm install wickra-screener
```

```javascript
import { Screener } from 'wickra-screener'

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

- [npm](https://www.npmjs.com/package/wickra-screener)
- [Source & examples](https://github.com/wickra-lib/wickra-screener/tree/main/examples/node)
