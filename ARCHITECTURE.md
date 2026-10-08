# Enterprise CRM Architecture

## High-Level Architecture

```
React 19 / Vite
       |
       v
API Gateway :8080
       |
       +--> Auth Service :8081 -------- auth_db
       +--> Company Service :8082 ----- company_db
       +--> Branch Service :8083 ------ branch_db
       +--> Department Service :8084 -- department_db
       +--> Designation Service :8085 - designation_db
       +--> Employee Service :8086 ---- employee_db
       +--> Lead Service :8087 -------- lead_db
       +--> Customer Service :8088 ---- customer_db
       +--> Vendor Service :8089 ------- vendor_db
       +--> Product Service :8090 ------ product_db
       +--> Task Service :8091 -------- task_db
       +--> Notification :8092 -------- notification_db
       +--> Audit Service :8093 ------- audit_db

Config Server + Eureka provide shared infrastructure.
```

## Service Responsibilities

| Service | Responsibility |
|---|---|
| config-server | Centralized configuration |
| discovery-server | Eureka service discovery |
| api-gateway | Routing and edge concerns |
| common-lib | Shared non-business platform utilities |
| auth-service | Authentication, JWT, roles, permissions |
| company-service | Company master |
| branch-service | Branch master |
| department-service | Department master |
| designation-service | Designation master |
| employee-service | Employee management |
| lead-service | Lead management |
| customer-service | Customer management |
| vendor-service | Vendor management |
| product-service | Product management |
| task-service | Tasks and activities |
| notification-service | User notifications |
| audit-service | Audit history |

## Domain Relationships

```
Company
  -> Branch
      -> Department
          -> Employee
              -> Designation

Lead -> Customer
Customer -> Product / Task
Task -> Notification
All business services -> Audit
```

These are logical relationships. A service does not create JPA relationships to entities owned by another service.

## Communication

### Synchronous
Use REST for request/response workflows where the caller needs an immediate result.

### Asynchronous
Use events for future workflows such as:
- notification delivery
- audit propagation
- long-running processing
- integration with external systems

Do not add a message broker merely for CRUD.

## Security Boundary

```
Client
  |
  v
API Gateway
  |
  +--> JWT validation / propagation
  |
  v
Service authorization
  |
  v
Service database
```

Authentication identifies the caller. Authorization determines whether the caller may perform the requested operation.

## Data Ownership

Each service owns its schema/database and is responsible for:
- persistence
- validation relevant to its domain
- migrations
- repository queries
- domain rules

Never solve a cross-service query by reading another service's database.

## Scalability Rules

- Paginate large collections.
- Index search/filter columns.
- Avoid N+1 database access.
- Avoid unbounded result sets.
- Use timeouts for service-to-service calls.
- Use idempotency where retryable operations can duplicate work.
- Cache only after measuring a real performance need.

## Change Rules

For a new service:
1. Define business responsibility.
2. Define owned data.
3. Define API contract.
4. Define authentication/authorization.
5. Define failure behaviour.
6. Add tests.
7. Add gateway route.
8. Add service discovery/configuration.
9. Update documentation.

