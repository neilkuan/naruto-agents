# Skill: Triage

## Purpose
Classify an incoming request and decide how to handle it.

## Steps
1. Parse the request — what is the human asking for?
2. Classify by domain:
   - **code** — features, bugs, refactoring, architecture → Naruto（鳴人 @dev）
   - **ops** — CI/CD, deployment, infra, Docker, monitoring → Yamato（大和 @ops）
   - **writing** — docs, content, email, reports → Jiraiya（自來也 @writer）
   - **research** — analysis, fact-checking, competitive intel → Shikamaru（鹿丸 @researcher）
   - **planning** — project plans, task breakdowns, knowledge org → Tsunade（綱手 @pm）
   - **meta** — about AgentOS itself → handle directly
   - **simple** — quick Q&A, calculations, lookups → handle directly
3. Check complexity: single-domain or multi-domain?
4. Route:
   - Single-domain, clear scope → delegate to one specialist
   - Multi-domain → decompose, delegate parts in parallel when independent, synthesize
   - Ambiguous or high-stakes → ask human for clarification
   - Meta (about AgentOS itself) → handle directly

## Routing Hints
- Code + deployment = Naruto (code) + Yamato (pipeline)
- Research → plan → implement = chain Shikamaru → Tsunade → Naruto
- "幫我整理" without code = Tsunade (knowledge org) or Jiraiya (content), ask if unclear
- Bug in CI → Yamato first. Bug in app code → Naruto first.

## Output
A routing decision: handle directly, delegate to specific agent(s), or ask for clarification.
