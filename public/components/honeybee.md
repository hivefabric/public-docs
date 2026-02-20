# Honeycomb UI

The current user-facing UI is `honeycomb/ui` (legacy docs may refer to Honeybee).

## What it does

- IAM login/session bootstrap through Honeycomb service.
- Dashboard for nodes/tasks/status.
- Message input routed by role (`admin` -> Queen Bee, `user` -> Worker Bee).
- Embedded node controls exposed through backend APIs.

## Run locally

```bash
cd honeycomb/ui
npm install
npm run dev
```

Set backend URL with `VITE_HONEYCOMB_API_BASE_URL` when needed.
