# AI Collaboration Log (Local Only)

## Worktree Map
- Codex A: ~/Desktop/n8n_workspaces/codexA (branch feature/codexA)
- Codex B: ~/Desktop/n8n_workspaces/codexB (branch feature/codexB)
- Claude A: ~/Desktop/n8n_workspaces/claudeA (branch feature/claudeA)
- Claude B: ~/Desktop/n8n_workspaces/claudeB (branch feature/claudeB)

## Usage Guidelines
- At the start of a session, add a timestamped note with your task, owner initials, and expected deliverable.
- Before handing off, record status, blockers, remaining work, and links/references gathered.
- When opening PRs, copy the relevant summary from here into the PR description so GitHub sees only final updates.

## Current Mission (2025-10-29)
Goal: compile the most advanced n8n templates we can find for **chatbots**, **TikTok**, **LinkedIn**, and **email automation**. Each agent owns one lane.

### Deliverables
- Curated list per lane (3-5 top templates) with short description, source link, why it is advanced.
- Note any reusable building blocks or ideas worth porting into our project.
- Capture findings in each agent's worktree under `research/<lane>.md`; commit to your branch.

### Search workflow
1. Log your intent here before starting.
2. Use available search tools (browser, CLI, MCP). If you need new access (e.g. Exa, SerpAPI), note it here so we can request/enable.
3. Store raw notes locally (scratchpad) but summarize into the research markdown before committing.
4. When done, mark the lane as ✅ and handoff context.

### Lane assignments
- Codex A (this terminal) → Planner + Chatbots lane. Responsible for collecting meta-status and reviewing outputs before PR.
- Codex B → TikTok automation templates.
- Claude A → LinkedIn outreach/nurture templates.
- Claude B → Email drip/newsletter templates.

### Sync cadence
- Every ~30 minutes or after major finding, drop a status line in Activity Log.
- When a lane is complete, open a draft PR from your branch so others can comment.

### Interaction shorthand
- "continua" / "ok sigue" / "continue workflow": reread this doc, check your lane's open TODOs, and advance the next actionable task without additional prompting.
- "sync" / "status": post a quick update in the Activity Log, then summarize blockers if any.
- "handoff to <agent>": document pending work, commit current progress, and ping the named agent via Activity Log entry.
- If a command is unclear, ask once in Activity Log before proceeding.

## Activity Log
- *[2025-10-29 20:01]* Codex A: Planning + starting chatbot template research; need external search results to shortlist.
- *[2025-10-29 20:03]* Codex A: Logged five advanced chatbot templates in `research/chatbots.md`; ready for other agents to mirror structure.
La policy cierra la vía de configuración: vamos al fix en código. Prepáralo SIN tocar develop — todo en una rama fix, y no hagas commit hasta mi ok:

1. EL FIX (quirúrgico, en datasets.py): normaliza el join temporal a semántica DATE en ambos lados (cuadrícula y transaction_date). Elige la variante de menor huella: o generar la cuadrícula ya como date (quitar utc=True y truncar), o castear ambos lados a date justo en el join. Justifícame cuál eliges y por qué. El fillna(target=0) NO lo toques — es otro debate (H9 lo documenta, pero cambiarlo es decisión aparte).
2. TEST DE REGRESIÓN: caso con origen DATE + sesión con timezone Europe/Madrid → con el código actual el target sale a cero, con el fix sale con valores. Que quede nombrado con referencia H9.
3. PARIDAD: verifica que con timezone UTC el fix produce EXACTAMENTE los mismos matches y el mismo training que el código actual (55.500/55.500, mismos valores) — el fix debe ser invisible donde hoy funciona.
4. SUITE: corre la batería completa del paquete de forecasting en local y dime el resultado (espero verde + el test nuevo).
5. Cuando todo esté verde, dame el plan de redespliegue al lab: bump de versión del wheel, mvn package, subida del wheel al volumen, y qué hay que tocar en el job (¿basta relanzar o hay que recrear el job apuntando al wheel nuevo?). No ejecutes el despliegue: me das los pasos y lo hago yo.
