# SurrealDB GraphQL API

SurrealDB exposes an experimental GraphQL interface that dynamically generates a complete schema from your database's table definitions, field types, custom functions, and access definitions. Enabling GraphQL requires running the server with the `--allow-experimental graphql` flag (pre-1.0 series) or configuring the capability in the server config. Once enabled, each namespace/database pair activates GraphQL by executing a `DEFINE CONFIG GRAPHQL` statement, which controls which tables and user-defined functions are surfaced (`TABLES AUTO`, `TABLES INCLUDE ...`, `TABLES EXCLUDE ...`) along with optional depth and complexity limits and introspection behavior.

The generated schema follows Apollo-style naming conventions: table Object types use PascalCase (e.g., `Person`), query fields use camelCase with automatic English pluralization for list operations (e.g., `person(id)` / `people(filter, order, limit, start)`), and mutation fields are prefixed with the operation name (e.g., `createPerson`, `updatePeople`, `deletePerson`). Subscription fields mirror the query shape and are served over WebSocket. Authentication mutations (`signIn`, `signUp`) are automatically generated from database Record access definitions and accept an `access` name and a `JSON` variables object, returning a JWT string. The schema is regenerated and cached whenever the database configuration changes; per-table `GRAPHQL <alias>` annotations can override the auto-generated names.

Authentication for GraphQL requests uses the same mechanisms as the SurrealDB HTTP API: Basic Auth credentials or a `Bearer` JWT token in the `Authorization` header, plus `NS` and `DB` headers to select the target namespace and database. Both HTTP POST (standard GraphQL JSON body) and WebSocket (`graphql-ws` / `graphql-transport-ws` protocols) transports are supported. Introspection is enabled by default and can be disabled via `DEFINE CONFIG GRAPHQL ... INTROSPECTION FALSE`.

**Endpoint:** `https://<host>/graphql`

**Documentation:** https://surrealdb.com/docs/surrealdb/querying/graphql

**References:**
- Documentation: https://surrealdb.com/docs/surrealdb/querying/graphql
- GettingStarted: https://surrealdb.com/docs/surrealdb/querying/graphql/getting-started
