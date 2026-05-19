# Stage 4. Databases and data access

**Duration:** 1–2 months.

**Stage goal:** learn to work with data without becoming a bottleneck in production. A junior writes LINQ and hopes EF Core figures it out. A middle reads execution plans and knows why a query takes the time it takes.

## SQL at a confident level

A backend without SQL knowledge is a cargo cult.

- All JOIN types, with an understanding of when each is needed.
- Subqueries, CTEs (`WITH`), recursive CTEs.
- Window functions: `ROW_NUMBER`, `RANK`, `LAG`/`LEAD`, `SUM() OVER (PARTITION BY ...)`.
- Grouping, `HAVING`, `GROUPING SETS`, `ROLLUP`, `CUBE`.
- Transactions and isolation levels: Read Uncommitted, Read Committed, Repeatable Read, Serializable, Snapshot. What phantom read, dirty read, non-repeatable read are.
- Locks: shared, exclusive, update, intent. Deadlock and how to diagnose it.

Resources:

- [Use the Index, Luke](https://use-the-index-luke.com/) — free online, the best material on indexes.
- "SQL Antipatterns" by Bill Karwin.
- "SQL Performance Explained" by Markus Winand.

## Indexes and execution plans

The most common cause of slow queries in production.

- Clustered vs non-clustered indexes.
- Covering index, included columns, filtered indexes.
- When an index doesn't help: leading column violation, functions in WHERE, OR conditions, low selectivity.
- Page splits, fillfactor, fragmentation, index rebuilds.
- Reading the execution plan: seek vs scan, hash join vs nested loop vs merge join, key lookup, RID lookup.
- Statistics and cardinality estimation.

Practice: take a table with a million rows, write 5 typical queries, look at the execution plan, add indexes that change the plan, measure the difference.

## PostgreSQL and SQL Server

Knowing one DBMS well is enough. PostgreSQL shows up more often in new projects, SQL Server in enterprise and legacy.

**PostgreSQL specifics:**

- MVCC and VACUUM. Why a table "bloats" and how to deal with it.
- TOAST for large values.
- JSON and JSONB, GIN indexes over them.
- Extensions: pg_stat_statements, pg_trgm, postgis, pgvector.
- Partitioning, declarative partitioning.

**SQL Server specifics:**

- Query Store for regression analysis.
- Extended Events instead of the deprecated SQL Profiler.
- Columnstore indexes for analytics.
- Always On Availability Groups.
- TempDB and its tuning under load.

## Entity Framework Core

The main data-access tool in .NET. And the main source of problems for people who don't understand what it generates.

- Change tracking: how it works, when to disable via `AsNoTracking()`.
- Lazy, eager (`Include`, `ThenInclude`), explicit loading. When to use what.
- The N+1 problem: how to find it (SQL logging), how to eliminate it.
- Compiled queries for hot paths.
- Split queries vs single queries with `Include`.
- Migrations: `Add-Migration`, `Update-Database`, manual editing, idempotent scripts for production.
- Value converters, owned types, table splitting.
- Global query filters for soft delete and multi-tenancy.
- `ExecuteUpdate` and `ExecuteDelete` (EF Core 7+) for bulk operations without change tracking.
- Interceptors: `SaveChangesInterceptor`, `DbCommandInterceptor`.

Resource: the [official EF Core documentation](https://learn.microsoft.com/en-us/ef/core/), especially the Performance section.

Antipatterns:

- `SaveChanges()` in a loop instead of batch insert.
- Loading an entire table into memory via `.ToList()` before filtering.
- Using `.Include()` where a DTO projection would do.
- Trusting EF to generate complex queries. Past a certain complexity, hand-written SQL is easier.

## Dapper and raw ADO.NET

For hot paths and complex queries EF isn't the right tool. Alternatives:

- **Dapper** — a thin wrapper over ADO.NET. You write the SQL, Dapper maps the result.
- **Raw ADO.NET** through `DbConnection`, `DbCommand`, `DbDataReader`. Maximum control, maximum speed, maximum amount of code.

A good approach in real projects: EF Core for commands (write), Dapper for queries (read). This is a natural path toward CQRS.

## Caching

- **IMemoryCache** for in-process cache. Simple, but doesn't work in multi-instance deployments.
- **IDistributedCache + Redis** for distributed cache.
- Invalidation strategies: TTL, write-through, write-behind, cache-aside.
- Cache stampede and how to prevent it through locks or semaphores.
- HybridCache (new in .NET 9) — a two-level cache with built-in stampede protection.

## NoSQL: when you actually need it

- **MongoDB**, **Cosmos DB**: document databases, convenient for DDD-style aggregates.
- **Redis** isn't just a cache: Pub/Sub, Streams, lock service.
- **Elasticsearch / OpenSearch** for full-text search and log analytics.
- **ClickHouse** for columnar analytics.
- **TimescaleDB / InfluxDB** for time series.

NoSQL isn't "the modern replacement for SQL," it's a different tool with different trade-offs. Default to PostgreSQL and move to NoSQL when there's a concrete reason.

## Readiness checklist for Stage 5

- [ ] I can read any execution plan and explain why a query is slow.
- [ ] I can create a covering index for a specific query and prove the win with measurements.
- [ ] I can explain the difference between Read Committed and Snapshot Isolation.
- [ ] I can find and fix an N+1 in someone else's code and show before/after via SQL logs.
- [ ] I can describe the cache stampede problem and give two ways to solve it.
- [ ] I can write an EF Core migration safe for production (backward-compatible, no locks).
- [ ] I can choose between EF Core, Dapper, and raw ADO.NET for a specific task with justification.

## Stage practical task

Take a learning project with one of the public databases (Northwind or Chinook, for example) and implement:

1. CRUD on EF Core with migrations.
2. One complex report through Dapper with window functions.
3. A two-level cache (memory + Redis) for the heaviest read query.
4. A load test through k6 at 100 RPS. Find an N+1, fix it, measure the difference.
5. A `PERFORMANCE.md` document in the repo: what it was, what it became, which indexes were added, which plans changed.

This task replaces ten EF Core courses.

---

[← All stages](README.md) | [Stage 3 →](03-tooling.md) | [→ Stage 5](05-aspnetcore.md)
