# pgAdmin service for Kubernetes on Wodby

This repository defines the Wodby pgAdmin service for linked PostgreSQL databases.

Wodby generates a stable pgAdmin administrator password and provides an Administrator email setting that defaults to `user@domain.com`. Changing the setting updates the persisted administrator identity on the next deployment without replacing its password or configuration.

The service registers the linked PostgreSQL host, port, database, and username. The linked PostgreSQL password is supplied through a Kubernetes Secret-backed `.pgpass` file and is never stored in the generated server definition.

The pgAdmin configuration volume is optional. Without it, accounts, sessions, settings, and saved connections are recreated when the pod is replaced.

pgAdmin is included as a disabled component in the managed PostgreSQL stack and can also be referenced from custom stacks.

Validate the manifest with:

```bash
wodby service validate-manifest service.yml --org <org-id>
```
