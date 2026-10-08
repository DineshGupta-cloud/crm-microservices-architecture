# Enterprise CRM AI Development Instructions

## Purpose
This repository is the source of truth for the Enterprise CRM microservices architecture, service boundaries, development workflow, and AI-assisted engineering rules.

## Current Platform
- Java 17
- Spring Boot 3.4.x
- Spring Cloud 2024.x
- Spring Security
- JJWT
- Spring Data JPA
- MySQL 8
- Maven
- React 19 / Vite
- Docker
- Eureka Discovery
- Spring Cloud Gateway
- Spring Cloud Config

## Repositories
- Architecture: DineshGupta-cloud/crm-microservices-architecture
- Backend services: DineshGupta-cloud/crm-microservices-services
- Frontend: DineshGupta-cloud/crm-microservices-frontend

## Source of Truth
Read these files before making architectural changes:
- AGENTS.md
- PROJECT_STATUS.md
- ARCHITECTURE.md
- API.md
- DATABASE.md

For implementation changes, inspect the services/frontend repository before proposing code.

## Architecture Rules
1. Database per service.
2. A service must never directly access another service's database.
3. Cross-service relationships use IDs.
4. DTOs define API boundaries.
5. Business logic belongs in services, not controllers.
6. Validate input before persistence.
7. Use consistent HTTP status codes and error responses.
8. Keep authentication and authorization centralized where appropriate.
9. Use REST for synchronous communication.
10. Keep the platform ready for event-driven workflows.
11. Prefer backward-compatible API changes.
12. Do not introduce a dependency without a concrete reason.

## Feature Workflow
1. Understand the requirement.
2. Inspect existing architecture and code.
3. Identify reusable functionality.
4. Design the API and data changes.
5. Identify security and performance risks.
6. Implement the smallest safe change.
7. Test the change.
8. Review the diff.
9. Perform security review.
10. Update PROJECT_STATUS.md and relevant documentation.

## AI Rules
- Never blindly rewrite working code.
- Never remove functionality unless explicitly requested.
- Never modify unrelated modules.
- Do not duplicate existing services/components/utilities.
- Ask for clarification when a requirement conflicts with the architecture.
- For large changes, provide a plan before implementation.
- Prefer production-ready, maintainable solutions over clever code.
- Do not invent APIs or service capabilities; inspect the repository first.

## Security
Never commit passwords, JWT secrets, API keys, production credentials, or private certificates.
Use environment variables or external configuration.
Review authentication, authorization, input validation, CORS, sensitive data exposure, IDOR, SQL injection, XSS, and logging of secrets for every security-sensitive change.

## Testing
Every feature should consider:
- happy path
- validation failure
- not found
- duplicate data
- unauthorized
- forbidden
- persistence failure
- edge cases
- integration behaviour where services interact

## Git
Preferred commit prefixes:
- feat:
- fix:
- refactor:
- test:
- docs:
- chore:
- security:

Keep commits focused and reviewable.
