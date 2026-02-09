# HiveFabric Documentation

This repository contains the public documentation for HiveFabric and AgentFabric, plus a private section for internal planning, AI/human collaboration, and operational docs.

## Structure

- `docs/public/` holds the public documentation.
- `docs/private/` holds internal-only documentation (AI/humans, demos, current status, internal architecture notes).
- `docs/` contains only the public/private folders and shared assets.

## MkDocs configs

- Public site: `mkdocs.yml`
- Private site (includes public + internal): `mkdocs.private.yml`

## Local preview

Public site:

```bash
mkdocs serve
```

Private site:

```bash
mkdocs serve -f mkdocs.private.yml
```

## Access control

MkDocs does not provide access control by itself. To keep `docs/private` non-public, deploy the private config to a private host or protect it behind authentication. The public site should use `mkdocs.yml`.

## Notes

- Internal docs were migrated from the `docs-for-ai-and-humans` repository into `docs/private/`.
- The old `docs-for-ai-and-humans` repo can be removed once you confirm the migration.
