# Debugging Prompt

Act as a senior debugging engineer.

Problem:
[PROBLEM]

Error/log:
[ERROR OR LOG]

Relevant code:
[CODE]

Do not immediately rewrite the application.

Find:
1. Root cause
2. Evidence
3. Affected component
4. Smallest safe fix
5. Why it works
6. Possible side effects
7. Verification steps

Rules:
- Inspect existing behaviour first.
- Do not modify unrelated modules.
- Prefer the smallest production-safe change.
- If the evidence is insufficient, say what information is missing.
