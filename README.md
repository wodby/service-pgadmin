# pgAdmin service for Kubernetes on Wodby

This repository defines the Wodby pgAdmin service for linked PostgreSQL databases.

Wodby generates a stable pgAdmin administrator password and registers the linked PostgreSQL host, port, database, and username. The linked PostgreSQL password is supplied through a Kubernetes Secret-backed `.pgpass` file, which the generated server definition references by relative path, and is never stored directly in the server definition.

For persistent pgAdmin configuration volumes created with an older administrator email, the chart loads the linked PostgreSQL server for the sole existing active internal administrator and refreshes that account's `.pgpass` file on every startup. It does not rename or otherwise modify the pgAdmin account.

The pgAdmin configuration volume is optional. Without it, accounts, sessions, settings, and saved connections are recreated when the pod is replaced.

pgAdmin is included as a disabled component in the managed PostgreSQL stack and can also be referenced from custom stacks.

Validate the manifest with:

```bash
wodby service validate-manifest service.yml --org <org-id>
```
