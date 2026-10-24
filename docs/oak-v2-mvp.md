# Oak v2 MVP

Oak v2 is a developer-first, self-hostable CMS built from this Payload CMS fork. The first milestone is a reliable MVP, not a wholesale rewrite of Payload.

## Product decisions

- **Upstream:** `payloadcms/payload`; keep this fork rebased/merged from upstream deliberately.
- **Legacy reference:** `latifiss/oak` (the existing Express/Mongoose publishing backend). Do not copy its app structure into Payload core.
- **Databases:** support MongoDB and PostgreSQL as alternative adapters selected per installation. A single installation uses one adapter at a time; it does not dual-write to both databases.
- **Scope:** get a clean install, admin login, collection configuration, CRUD, REST/local API, access control, and uploads working before expanding features.
- **Compatibility:** preserve upstream license and copyright notices. Keep upstream package names and internal architecture until a working baseline is verified.

## MVP acceptance criteria

- [ ] A clean checkout installs using the Node.js and pnpm versions specified by the repository.
- [ ] Core build and lint/type checks pass, or any baseline failures are recorded with reproducible logs.
- [ ] A minimal example application can boot and render the admin panel.
- [ ] The same minimal collection CRUD and access-control tests run against MongoDB and PostgreSQL.
- [ ] REST and Local API operations work for the example collection on both adapters.
- [ ] Uploads can be configured and tested without coupling them to a specific database.
- [ ] A new developer can follow the Oak v2 quickstart from a clean environment.

## Work sequence

### 1. Establish the baseline
- Record upstream commit and current fork commit.
- Verify toolchain versions and lockfile.
- Run install, core build, lint, type checks, and a minimal dev boot.
- Separate pre-existing upstream failures from Oak changes; do not hide failures by weakening checks.

### 2. Verify database parity
- Use the existing `@payloadcms/db-mongodb` and `@payloadcms/db-postgres` adapters first.
- Add/adjust shared integration coverage for collection create/read/update/delete, relationships, auth/access control, and migrations/schema setup where relevant.
- Use separate test configurations and database services; never assume a test against one adapter proves the other works.

### 3. Build the Oak starter experience
- Provide a minimal documented starter with one example collection and an admin user.
- Document environment variables and adapter selection.
- Keep configuration compatible with normal Payload configuration patterns.

### 4. Map the legacy Oak use cases
- Audit `latifiss/oak` routes, Mongoose models, uploads, and auth before porting anything.
- Translate publishing concepts into collections, fields, access rules, and hooks.
- Keep legacy-specific publishing behavior outside framework internals unless it is genuinely reusable CMS functionality.

### 5. Brand after stability
- Update product naming, docs, package metadata, and visuals only after baseline builds and the dual-adapter test path are green.
- Keep attribution and required upstream notices intact.

## Explicitly out of MVP

Do not start by rewriting the admin UI, replacing the database adapters, removing Payload features, building a new plugin ecosystem, or implementing multi-database dual-write. Advanced localization, custom block builders, extra integrations, and broad rebranding follow after the acceptance criteria pass.

## Current status

- [x] Repository fork exists at `latifiss/oak-v2`.
- [x] Initial working branch created: `oak-v2-mvp`.
- [ ] Baseline install/build/test run recorded.
- [ ] MongoDB/PostgreSQL parity tests verified.
- [ ] Oak starter and quickstart verified end to end.
