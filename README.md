# Enterprise CRM Microservices Architecture

## Vision
Production-grade CRM built using Spring Boot Microservices, React, MySQL, JWT, RBAC, Eureka, Gateway, Config Server and Docker.

## Services
- config-server
- discovery-server
- api-gateway
- auth-service
- user-service
- company-service
- branch-service
- department-service
- designation-service
- employee-service
- lead-service
- customer-service
- vendor-service
- product-service
- task-service
- notification-service
- audit-service

## Architecture Principles
- Database per service
- JWT Authentication
- Role Based Access Control
- API Gateway Routing
- Centralized Configuration
- Service Discovery
- OpenAPI Documentation
- Docker Ready
- Event Driven Extension Ready

## Frontend
React + Vite + Material UI + React Query + Zustand

## Service Repository Mapping
Implementation repository: `DineshGupta-cloud/crm-microservices-services`

## Implementation Status
| Service | Status | Port | Database |
|---|---|---:|---|
| Config Server | Implemented | 8888 | - |
| Discovery Server | Implemented | 8761 | - |
| API Gateway | Implemented | 8080 | - |
| Common Library | Implemented | - | - |
| Auth Service | Implemented | 8081 | crm_auth |
| Company Service | Implemented | 8081* | crm_company |
| Branch Service | Implemented | 8082 | crm_branch |
| Department Service | Implemented | 8083 | crm_department |
| Designation Service | Implemented | 8084 | crm_designation |
| Employee Service | Implemented | 8085 | crm_employee |
| Lead Service | Planned | - | crm_lead |
| Customer Service | Planned | - | crm_customer |
| Vendor Service | Planned | - | crm_vendor |
| Product Service | Planned | - | crm_product |
| Task Service | Planned | - | crm_task |
| Notification Service | Planned | - | crm_notification |
| Audit Service | Planned | - | crm_audit |

\* Company Service should use a dedicated port when deployed alongside Auth Service; set `server.port` through environment/configuration before running both locally.

## Organization APIs
- `GET /api/v1/companies`
- `POST /api/v1/companies`
- `GET /api/v1/companies/{id}`
- `PUT /api/v1/companies/{id}`
- `DELETE /api/v1/companies/{id}`
- `GET /api/v1/branches`
- `POST /api/v1/branches`
- `GET /api/v1/departments`
- `POST /api/v1/departments`
- `GET /api/v1/designations`
- `POST /api/v1/designations`
- `GET /api/v1/employees`
- `POST /api/v1/employees`

Organization hierarchy is represented using service-owned IDs rather than cross-database JPA relationships:
`Company -> Branch -> Department -> Employee`, with `Designation` referenced by employee ID.

## Status
Company, Branch, Department, Designation and Employee CRUD foundations are synchronized with the services repository. The next business-services layer is Lead and Customer management.
