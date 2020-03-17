# wasm-barnes-hut
Barnes-hut algorithm implemented in Rust and compiled to WASM / WASI, for publication on WAPM &amp; execution in many programming languages


## Misc comments

* rand library only supports Entropy via WASI from version >= 0.7, which in turn requires an updated nightly environment


## Workflow

### Creating environment

### Building rust -> wasm

* Example from `rust-wasm-simd128-example` repository (uses cargo config)
```bash
RUSTFLAGS='-C target-feature=+simd128' cargo +<nightly-2019-05-20> build --release --target=wasm32-wasi
```


### executing

* The first time we execute (there is some compilation going on..?)
```bash
wasmer --backend=llvm --enable-simd <target>.wasm
```

* On repeated runs, we don't need to specify the --enable-simd option anymore (although it doesn't hurt, since no further compilation is performed)
```bash
wasmer --backend=llvm <target>.wasm
```
