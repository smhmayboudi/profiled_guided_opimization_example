# profiled_guided_opimization_example


## rustc

```bash
$ rustc -Cprofile-generate=./pgo-data ./src/main.rs
$ ./main
$ llvm-profdata merge -o ./pgo-data/merged.profdata ./pgo-data
$ rustc -Cprofile-use=./pgo-data/merged.profdata -O ./src/main.rs
```

## cargo

```bash
$ rm -rf /tmp/pgo-data
$ RUSTFLAGS="-Cprofile-generate=/tmp/pgo-data" \
    cargo build --release --target=x86_64-unknown-linux-musl
$ llvm-profdata merge -o /tmp/pgo-data/merged.profdata /tmp/pgo-data
$ RUSTFLAGS="-Cprofile-use=/tmp/pgo-data/merged.profdata" \
    cargo build --release --target=x86_64-unknown-linux-musl
```
