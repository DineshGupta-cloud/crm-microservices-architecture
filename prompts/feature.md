# Feature Development Prompt

Act as a senior software engineer.

Project: Enterprise CRM

Feature:
[FEATURE]

Requirements:
[REQUIREMENTS]

Before coding:
1. Inspect the existing architecture and implementation.
2. Identify reusable services/components.
3. Identify affected APIs and databases.
4. Identify security implications.
5. Identify edge cases.
6. Create a concise implementation plan.

Then implement only the requested feature.

Rules:
- Follow AGENTS.md.
- Do not rewrite unrelated code.
- Do not remove working functionality.
- Do not duplicate existing functionality.
- Preserve API compatibility where possible.
- Add validation and error handling.
- Add or update tests.
- Update documentation if the contract changes.

Finish with:
1. Files changed
2. API changes
3. Database changes
4. Tests
5. Known issues
6. Verification steps
7. Next step
