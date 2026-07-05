# Rust

The native crate. Fold a `ScanSpec` over a universe with `scan_batch`, or drive a
`Screener` handle with the JSON command protocol every other binding uses.

```bash
cargo add wickra-screener
```

```rust
use screener_core::{scan_batch, Candle, ScanSpec};
use std::collections::BTreeMap;

let spec = ScanSpec::from_json(SPEC).expect("valid spec");

let mut data: BTreeMap<String, Vec<Candle>> = BTreeMap::new();
// ... fill `data` with each symbol's candle history ...

let report = scan_batch(&data, &spec).expect("scan");
for m in &report.matches {
    println!("matched: {}", m.symbol);
}
```

## More

- [crates.io/crates/wickra-screener](https://crates.io/crates/wickra-screener) · [docs.rs](https://docs.rs/wickra-screener)
- [Source & examples](https://github.com/wickra-lib/wickra-screener/tree/main/examples/rust)
- [Conditions & ScanSpec](https://github.com/wickra-lib/wickra-screener/blob/main/docs/CONDITIONS.md) · [Cross-section & breadth](https://github.com/wickra-lib/wickra-screener/blob/main/docs/CROSS_SECTION.md)
