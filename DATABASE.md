# Enterprise CRM Database Standards

## Database-per-Service

```
auth_db
company_db
branch_db
department_db
designation_db
employee_db
lead_db
customer_db
vendor_db
product_db
task_db
notification_db
audit_db
```

Each service owns its database/schema.

## Rules

1. No cross-service database queries.
2. No cross-service JPA relationships.
3. Store external entity IDs rather than foreign keys to another service.
4. Use migrations for schema changes.
5. Add indexes based on actual query patterns.
6. Avoid storing secrets in plain text.
7. Use UTC timestamps where practical.
8. Use soft delete when recovery/audit requirements apply.

## Recommended Audit Fields

For business entities where appropriate:

```
createdAt
createdBy
updatedAt
updatedBy
deletedAt
deletedBy
isDeleted
```

## Query Performance

For large datasets:
- paginate
- index search/filter columns
- select only required columns for heavy read paths
- avoid N+1 queries
- avoid loading large collections into memory
- use database-side filtering/sorting

## Migrations

Every schema change must:
1. Have a versioned migration.
2. Be backward-aware when deployed across versions.
3. Be tested against a clean database.
4. Be tested against an existing database where applicable.

## Production

Use environment/external configuration for:
- database URL
- username
- password
- connection pool settings
- encryption keys

Never commit production credentials.
