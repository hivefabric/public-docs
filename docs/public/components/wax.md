# Wax (Runtime)

Wax is the WASM runtime for executing sandboxed modules. It is designed to be embedded by Honeybee or other host applications.

## Current status

- Rust crate lives at `hive/crates/runtime-wax`
- Intended to run WASM tasks in isolation
- Integration with Honeybee is in progress

## Build

```bash
cd hive
cargo build -p runtime-wax
```

As Wax evolves, this section will include runtime APIs and module packaging guidance.
