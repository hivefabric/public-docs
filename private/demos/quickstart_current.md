# Quickstart (Current)

This is the fastest path to a working demo **today**.

## 1) Start Honeycomb + NATS

```bash
cd hive/crates/ms-honeycomb
docker compose up -d --build
```

Health check:

```bash
curl -fsS http://localhost:8080/health
```

## 2) Start two Stinger clients

```bash
cd hive/crates/sdk-stinger
docker compose up -d --scale sdk-stinger=2
```

## 3) Start Beekeeper UI

```bash
cd ui-beekeeper
npm install
npm run dev -- --host 127.0.0.1 --port 5173
```

Open `http://127.0.0.1:5173`.

## 4) Optional: Honeybee UI (experimental)

```bash
cd ui-honeybee
npm install --registry=https://registry.npmjs.org --no-fund --no-audit
npm run dev -- --host 127.0.0.1 --port 5174
```

Open `http://127.0.0.1:5174`.
