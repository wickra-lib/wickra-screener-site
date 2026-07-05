# R

A `.Call` binding over the C ABI. Construct a screener from a JSON spec, then drive
it with `wkscreen_command(screener, json) -> json`.

```r
install.packages("wickrascreener", repos = "https://wickra-lib.r-universe.dev")
```

```r
library(wickrascreener)

spec <- '{"universe":["AAA","BBB"],
  "condition":{"type":"cmp",
    "left":{"kind":"indicator","name":"Rsi","params":[14]},
    "op":"lt","right":{"kind":"const","value":30.0}}}'

screener <- wkscreen_new(spec)
response <- wkscreen_command(screener, '{"cmd":"scan","data":{}}')
cat("wickra-screener", wkscreen_version(), "\n")
cat(response, "\n")
```

## More

- [r-universe](https://wickra-lib.r-universe.dev)
- [Source & examples](https://github.com/wickra-lib/wickra-screener/tree/main/examples/r)
