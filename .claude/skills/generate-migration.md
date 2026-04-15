# Skill: Generate Database Migration

## Purpose
Create a new database migration with up/down scripts.

## Usage
`/generate-migration [name] [description]`

## Example
`/generate-migration add_email_to_users Add email column to users table`

## Output
Creates migration files:
- `migrations/[timestamp]_[name].up.sql`
- `migrations/[timestamp]_[name].down.sql`

## Template

### Up Migration
```sql
-- [timestamp]_[name].up.sql
-- Description: [description]

BEGIN;

-- Migration SQL here

COMMIT;
```

### Down Migration
```sql
-- [timestamp]_[name].down.sql
-- Rollback: [description]

BEGIN;

-- Rollback SQL here

COMMIT;
```

## Best Practices
- Always wrap in transaction
- Test rollback works
- No data loss in down migration when possible
- Add indexes in separate migration if large table
