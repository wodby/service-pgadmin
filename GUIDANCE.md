# pgAdmin on Wodby

A database administration interface for the PostgreSQL service of the environment, from the official pgAdmin 4 image.

## Login to pgAdmin

pgAdmin has its own login: the administrator email fixed in the manifest (`admin.email` under `helm.values`) and a password generated once per environment (token `admin_password`). These are not database credentials.

## Pre-configured server

The required `db` link points to one PostgreSQL service and registers it in pgAdmin as a server named `PostgreSQL`:

- host, port and user name of the environment's database user, with the environment's database as the maintenance database;
- the user's password, passed to the container as `PGADMIN_DB_PASSWORD` and used through a password file, so opening the server asks for no password.

The server definition is written again on every start: a change made to this server inside pgAdmin does not last. The connection is made as the environment's database user, not as the administrator `postgres`.

The interface listens on port `8080`.

## Data

The optional `data` volume holds pgAdmin's own data (`/var/lib/pgadmin`), such as preferences and servers added by hand. Without it they are lost when the container is replaced.
