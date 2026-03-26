# Skill: Code Review

## Purpose
Perform a structured code review and produce actionable feedback.

## Steps
1. Understand context — what does this code do, what problem does it solve?
2. Check correctness — does the logic work? Edge cases handled?
3. Check security — injection, auth, secrets exposure, OWASP top 10
4. Check maintainability — naming, structure, duplication, test coverage
5. Check performance — obvious bottlenecks, unnecessary allocations, N+1 queries
6. Prioritize findings:
   - **Must fix** — bugs, security issues, data loss risks
   - **Should fix** — maintainability, clarity, test gaps
   - **Nit** — style, naming preferences (only mention if few other issues)

## Output
A structured review with findings categorized by priority. Each finding includes: location, issue, suggested fix.
