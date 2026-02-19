# Stinger (SDK)

Stinger is a lightweight SDK/CLI that registers combs with Honeycomb and sends periodic heartbeat reports.

## Usage modes

- `register`: send an initial comb report
- `heartbeat`: send periodic updates
- `both`: register + heartbeat

## Run from source

```bash
cd hive
cargo run -p sdk-stinger -- --base-url http://localhost:8080 --id comb-123 --mode both
```

Looping heartbeats:

```bash
cargo run -p sdk-stinger -- --base-url http://localhost:8080 --id comb-123 --mode heartbeat --loop --interval 15s
```

## Run with Docker

```bash
cd hive/crates/sdk-stinger
docker build -t sdk-stinger:local .

docker run --rm -e STINGER_BASE_URL=http://host.docker.internal:8080 sdk-stinger:local --id comb-1 --mode both
```

## Scale combs with Compose

```bash
cd hive/crates/sdk-stinger
./scripts/run.sh -s 5
```

## Related docs

See `hive/crates/sdk-stinger/README.md` for full CLI flags and environment variables.
