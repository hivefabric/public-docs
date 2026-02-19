# API Reference (Public)

This page documents the Honeycomb REST endpoints used by Stinger and Beekeeper. The API is intentionally small and focused.

## Base URL

Default: `http://localhost:8080`

## Endpoints

### `GET /health`

Returns `200 OK` if the service is running.

### `POST /combs/register`

Registers a comb and stores its initial report.

**Request body** (example):

```json
{
  "id": "comb-123",
  "metadata": {
    "owner_id": "local",
    "device_type": "container",
    "os": "linux",
    "arch": "amd64",
    "runtime_version": "0.1.0"
  },
  "cpu": {"cores": 2, "threads": 2, "model": "container-cpu", "freq_mhz": 2400},
  "memory": {"total_mb": 2048, "available_mb": 1024},
  "gpu": {"present": false, "model": "", "vram_mb": 0, "compute_capability": ""},
  "storage": {"total_gb": 10, "free_gb": 5},
  "power": {"source": "ac", "battery_percent": 100, "thermal_state": "normal"},
  "network": {"type": "ethernet", "uplink_mbps": 100.0, "downlink_mbps": 100.0, "latency_ms": 5},
  "availability": {"uptime_seconds": 120, "cpu_percent": 5.0, "mem_percent": 20.0, "capacity_score": 0.8},
  "location": {"country": "US", "region": "CA", "city": "San Francisco", "timezone": "America/Los_Angeles", "region_hint": "us-west"},
  "local_models": []
}
```

### `POST /combs/heartbeat`

Sends a heartbeat for a comb. The report payload is optional.

**Request body** (example):

```json
{
  "id": "comb-123",
  "report": null
}
```

### `GET /combs`

Lists active combs and their most recent report.

**Response** (example):

```json
{
  "combs": [
    {
      "id": "comb-123",
      "last_heartbeat": "2026-02-09T22:10:00Z",
      "status": "active",
      "report": {"id": "comb-123", "metadata": {"owner_id": "local", "device_type": "container", "os": "linux", "arch": "amd64", "runtime_version": "0.1.0"}}
    }
  ]
}
```

### `GET /tasks`

Lists pending tasks in the queue.

**Response** (example):

```json
{
  "tasks": [
    {"id": "task-1", "payload": "do something", "status": "pending"}
  ]
}
```

## Versioning

This API is currently unversioned and intended for local/dev usage. Public versioning will be added once the control plane stabilizes.
