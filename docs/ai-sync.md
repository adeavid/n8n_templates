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
El bloqueo de la Fase B revela la pieza que falta: los jobs del PROCESO no están templatizados en resources (en el lab se crearon a mano) — por eso no hay nada que lanzar en dev y intentaste un job temporal. La solución es la tarea ya acordada con plataforma: EL JOB ÚNICO MULTI-TASK. Hazlo ahora:

1. Crea la plantilla job_e2e_cash_supply.json (o nombre según convención): UN job multi-task de punta a punta — tareas encadenadas con depends_on: create-training → create-forecasting → run-predictions → optimize → expert. Mismo patrón que las plantillas existentes: {{JOB_GROUP}}, policy, job cluster como el del seed/integración (identidad SP), parámetros de job (odate, environment, forecast_horizon, seasonality) que las tareas reciben como el del lab.
2. Referencia de las tareas: los jobs del LAB (CASH_SUPPLY_FORECAST_LAB_50 multi-task y CASH_SUPPLY_OPTIMIZE) — mismos entry points y parámetros, pero todo en un solo job y leyendo la config de dev-adb.
3. Mientras lo montas, resuelve también la FASE D que quedó pendiente: el job de siembra limitado a dev (que no se cree en int) — misma condición para este si aplica… no: el job E2E multi-task SÍ debe existir en int y pro (es EL job de producción); solo la siembra es dev-only.
4. PR + merge + redeploy DEV → el install crea el job unificado → lo lanzo con Run Now (como la siembra, que ya demostró que puedo dispararlos) → FASES B y C continúan donde estaban.
NADA de jobs temporales ni run_as: los jobs desplegados ya corren con la identidad correcta.
