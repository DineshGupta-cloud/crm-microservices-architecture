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

Current implemented foundation:
- Config Server
- Eureka Discovery Server
- API Gateway
- Common Library
- Auth Service

Auth Service provides:
- User, Role and Permission persistence
- BCrypt password hashing
- JWT access and refresh tokens
- Stateless Spring Security authentication
- Role and permission authorities
- Registration, login and token refresh APIs
- Default USER and ADMIN roles plus CRM permissions
- Docker image definition
- JWT unit tests

## Core Runtime Ports
| Service | Port |
|---|---:|
| Discovery Server | 8761 |
| API Gateway | 8080 |
| Auth Service | 8081 |

## Auth API
- `POST /api/auth/register`
- `POST /api/auth/login`
- `POST /api/auth/refresh`

## Status
Foundation implementation is synchronized with the services repository. Business services will be added in the order defined above, starting with Company and Organization management.
