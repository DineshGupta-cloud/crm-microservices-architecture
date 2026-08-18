# Enterprise CRM Microservices Architecture

## Vision
Production-oriented CRM built with Spring Boot microservices, React/Vite, MySQL, JWT/RBAC, Eureka, API Gateway, Config Server and Docker.

## Repository Mapping

Architecture: https://github.com/DineshGupta-cloud/crm-microservices-architecture
Implementation: https://github.com/DineshGupta-cloud/crm-microservices-services

## Services

| Service | Port | Database | Status |
|---|---:|---|---|
| config-server | 8888 | - | Foundation |
| discovery-server | 8761 | - | Foundation |
| api-gateway | 8080 | - | Foundation |
| common-lib | - | - | Foundation |
| auth-service | 8081 | auth_db | Implemented |
| company-service | 8082 | company_db | Implemented |
| branch-service | 8083 | branch_db | Implemented |
| department-service | 8084 | department_db | Implemented |
| designation-service | 8085 | designation_db | Implemented |
| employee-service | 8086 | employee_db | Implemented |
| lead-service | 8087 | lead_db | Implemented |
| customer-service | 8088 | customer_db | Implemented |
| vendor-service | 8089 | vendor_db | Implemented |
| product-service | 8090 | product_db | Implemented |
| task-service | 8091 | task_db | Implemented |
| notification-service | 8092 | notification_db | Implemented |
| audit-service | 8093 | audit_db | Implemented |

## Architecture

```text
React / Vite
     |
     v
API Gateway :8080
     |
     +-- Auth :8081 -------- auth_db
     +-- Company :8082 ----- company_db
     +-- Branch :8083 ------ branch_db
     +-- Department :8084 -- department_db
     +-- Designation :8085 - designation_db
     +-- Employee :8086 ---- employee_db
     +-- Lead :8087 -------- lead_db
     +-- Customer :8088 ---- customer_db
     +-- Vendor :8089 ------ vendor_db
     +-- Product :8090 ----- product_db
     +-- Task :8091 -------- task_db
     +-- Notification :8092 notification_db
     +-- Audit :8093 ------- audit_db

Config Server + Eureka provide shared infrastructure.
```

## Business Domains

```text
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

Cross-service relationships are represented by IDs. Services do not directly access another service's database.

## Implemented APIs

```text
/api/auth/*
/api/v1/companies
/api/v1/branches
/api/v1/departments
/api/v1/designations
/api/v1/employees
/api/v1/leads
/api/v1/customers
/api/v1/vendors
/api/v1/products
/api/v1/tasks
/api/v1/notifications
/api/v1/audits
```

CRUD services expose GET, GET by ID, POST, PUT and DELETE where appropriate. Notification supports user listing and read status; Audit supports global and entity-specific history.

## Architecture Principles

- Database per service
- JWT authentication
- RBAC and permissions
- API Gateway routing
- Centralized configuration
- Eureka service discovery
- DTO/API boundaries
- Validation and consistent errors
- REST for synchronous communication
- Event-driven extension ready
- Docker ready
- OpenAPI/Swagger ready for service documentation

## Technology

- Java 17
- Spring Boot 3.4.x
- Spring Cloud 2024.x
- Spring Security
- JJWT
- Spring Data JPA
- MySQL 8
- Maven
- Docker
- React/Vite

## Build

From the services repository:

```bash
mvn clean install
```

Start infrastructure first, then Auth and business services.

## Important

The source code is committed to the implementation repository. A successful production release still requires running the Maven build, integration tests, database provisioning/migrations, secret configuration and deployment verification in the target environment.
