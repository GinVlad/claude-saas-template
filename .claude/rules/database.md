# Database Rules

## Migrations
- Location: `migrations/` or `db/migrations/`
- Format: `YYYYMMDDHHMMSS_description.up.sql` / `.down.sql`
- Always provide rollback (down migration)
- Wrap in transactions

## Naming
- Tables: `snake_case`, plural (`users`, `orders`)
- Columns: `snake_case`
- Primary key: `id` (UUID or auto-increment)
- Foreign key: `{table}_id`
- Timestamps: `created_at`, `updated_at`

## Common Tables (SaaS)
```
users           # User accounts
subscriptions   # Plan subscriptions
payments        # Payment history
[your_feature]  # Core feature data
```

## Indexes
- Always index foreign keys
- Index columns used in WHERE clauses
- Index columns used in ORDER BY

## Queries
- Use parameterized queries (never string concat)
- Consider query performance
- Return errors, don't swallow them

## Repository Pattern
```
interface Repository {
  create(entity) → entity
  getByID(id) → entity
  update(entity) → entity
  delete(id) → void
}
```
