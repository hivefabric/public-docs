# Demo Script

Use this for live walkthroughs.

## Setup (before call)

- Run the quickstart steps in `quickstart_current.md`.
- Open Beekeeper UI in a browser.

## Script

1. **Open Honeycomb health endpoint**
   - `http://localhost:8080/health`
   - “Control plane is live.”

2. **Show running combs**
   - `http://localhost:8080/combs`
   - “Two live combs are connected and reporting.”

3. **Open Beekeeper UI**
   - “Here’s the control plane dashboard, updating in real time.”

4. **Point out node telemetry**
   - CPU/RAM, uptime, network.

5. **Explain the near-term roadmap**
   - Tasks and scheduling (next milestone).
   - WASM agent execution (Wax runtime).

## Expected output

- UI shows at least 2 active combs.
- Honeycomb REST returns comb list with reports.
