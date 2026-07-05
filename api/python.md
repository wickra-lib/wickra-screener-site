# Python

Native PyO3 bindings over the Rust core. Construct a `Screener` from a JSON spec,
then drive it with `command(json) -> json`.

```bash
pip install wickra-screener
```

```python
import json
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
    print("matched:", match["symbol"])
```

## More

- [PyPI](https://pypi.org/project/wickra-screener/)
- [Source & examples](https://github.com/wickra-lib/wickra-screener/tree/main/examples/python)
