# Oak v2 database baseline validation

This repository already includes Payload's MongoDB and PostgreSQL adapters. Oak v2 should verify both adapters before introducing product-specific abstractions.

## Automated baseline

The `.github/workflows/oak-v2-database-baseline.yml` workflow installs from the committed lockfile and builds:

1. Payload core packages
2. `@payloadcms/db-mongodb`
3. `@payloadcms/db-postgres`

Run it from GitHub Actions using **Run workflow**, or let it run on a pull request that changes the core, adapter, workspace, or lockfile inputs.

## Local commands

Use the versions in `.tool-versions` and run from the repository root:

```sh
pnpm install --frozen-lockfile
pnpm run build:core
pnpm run build:db-mongodb
pnpm run build:db-postgres
```

A successful package build is necessary but does not prove runtime database parity.

## Runtime parity still required

The next test milestone must run the same minimal collection scenarios against separate MongoDB and PostgreSQL instances:

- initialize the adapter and schema
- create, read, update, and delete a document
- verify access control with allowed and denied requests
- verify a relationship field
- verify REST and Local API behavior
- verify upload metadata and file storage
- verify migrations/schema setup for PostgreSQL and collection setup for MongoDB

Record the database versions, exact test commands, and CI result for each adapter. Do not report parity until both suites pass.
