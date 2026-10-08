# Enterprise CRM API Standards

## Gateway
Base URL during local development:
`http://localhost:8080`

The frontend should normally call the gateway rather than individual business-service ports.

## Authentication

```
POST /api/auth/register
POST /api/auth/login
POST /api/auth/refresh
```

Authentication responses should not expose passwords or secrets.

## Business APIs

```
GET    /api/v1/companies
GET    /api/v1/companies/{id}
POST   /api/v1/companies
PUT    /api/v1/companies/{id}
DELETE /api/v1/companies/{id}

GET    /api/v1/branches
GET    /api/v1/departments
GET    /api/v1/designations
GET    /api/v1/employees
GET    /api/v1/leads
GET    /api/v1/customers
GET    /api/v1/vendors
GET    /api/v1/products
GET    /api/v1/tasks
GET    /api/v1/notifications
GET    /api/v1/audits
```

## API Design Rules

### List endpoints
Support pagination where the dataset can grow.

Recommended query parameters:
```
page=0
size=20
sort=name,asc
search=abc
```

### Create
Use POST and return the created resource or a documented creation response.

### Update
Use PUT for full replacement semantics. Use PATCH only when partial update semantics are explicitly required.

### Delete
Use soft delete for business data when retention/audit requirements require recovery.

### Validation
Return 400 for invalid request data.

### Authentication
Return 401 when the caller is unauthenticated.

### Authorization
Return 403 when the caller is authenticated but lacks permission.

### Not Found
Return 404 when the requested resource does not exist or is not visible to the caller.

### Conflict
Return 409 for business conflicts such as duplicate unique values.

### Server Error
Return 500 for unexpected server-side failures without exposing internal stack traces.

## Error Response

Use a consistent shape similar to:

```json
{
  "timestamp": "2026-10-08T10:00:00Z",
  "status": 400,
  "error": "VALIDATION_ERROR",
  "message": "Request validation failed",
  "path": "/api/v1/employees",
  "fieldErrors": {
    "email": "Invalid email"
  }
}
```

Do not expose SQL statements, stack traces, credentials, tokens, or internal infrastructure details.

## API Compatibility

When changing an API:
1. Identify existing consumers.
2. Prefer additive changes.
3. Deprecate before removing where practical.
4. Update API documentation and frontend integration.
5. Add regression tests.
