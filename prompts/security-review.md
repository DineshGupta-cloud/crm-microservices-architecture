# Security Review Prompt

Act as an application security engineer.

Review:
[CODE/DIFF/FEATURE]

Check:
- authentication
- authorization
- JWT handling
- RBAC
- IDOR/broken access control
- input validation
- SQL injection
- XSS
- CSRF where applicable
- CORS
- sensitive data exposure
- secret management
- password handling
- insecure file handling
- logging of secrets/tokens
- service-to-service trust

For every issue provide:
Severity
Problem
Why it matters
Recommended fix
Verification

Prioritize exploitable and production-impacting findings.
