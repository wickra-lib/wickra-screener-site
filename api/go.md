# Go

A cgo wrapper over the C ABI. Construct a `Screener` from a JSON spec, then drive
it with `Command(json) -> json`.

```bash
go get github.com/wickra-lib/wickra-screener-go
```

```go
package main

import (
	"fmt"

	wickra "github.com/wickra-lib/wickra-screener-go"
)

func main() {
	spec := `{"universe":["AAA","BBB"],
	  "condition":{"type":"cmp",
	    "left":{"kind":"indicator","name":"Rsi","params":[14]},
	    "op":"lt","right":{"kind":"const","value":30.0}}}`

	screener, err := wickra.New(spec)
	if err != nil {
		panic(err)
	}
	defer screener.Close()

	report, err := screener.Command(`{"cmd":"scan","data":{}}`)
	if err != nil {
		panic(err)
	}
	fmt.Println("wickra-screener", wickra.Version())
	fmt.Println(report)
}
```

## More

- [Go module (pkg.go.dev)](https://pkg.go.dev/github.com/wickra-lib/wickra-screener-go)
- [Source & examples](https://github.com/wickra-lib/wickra-screener/tree/main/examples/go)
