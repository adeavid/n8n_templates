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
Rama feature/historia1-datagen-directo en WORKTREE AISLADO desde develop. Commit+push tras cada fase. ⚠️ Esta rama NO se mergea sin autorización explícita — convive semanas con develop; rebase periódico.

FASE 0 — El mapa (entregable propio): genera el doc “Mapeo de adaptación al contrato nuevo”: por cada lectura del contrato viejo (branch_360 y los 3 calendarios), tabla: columna consumida | de qué columna real viene (según projection_views.sql) | transformación que aplica la vista (rename/cast/lógica — literal) | punto del código que la consume (fichero:línea). Las vistas son la spec: todo lo que hacen, lo tendrá que hacer el código. Enséñame este doc ANTES de seguir — es mi punto de control.

FASE 1 — La adaptación:

Los lectores pasan a consumir branch_cash_servicing y calendar_datagen directamente. Las transformaciones de las vistas se mudan a UNA capa de lectura en código (un módulo/funciones, no esparcido): renames, casts de tipos (los DOUBLE/INT), la conversión de denominations_balance, y la derivación de los 3 calendarios desde el datagen (filtro nacional, filtro local/autonómico, oficina vía zip_code→idofic) — cada una implementada UNA vez.
Config: los VALORES de nombres de tabla pasan a las tablas reales por entorno (int: las de int_app; dev: pendiente de siembra v2 — en dev esta rama puede apuntar a las mismas que int o documentar la limitación; dímelo como decisión abierta, no la tomes solo). Claves intactas (H5b).
Los filtros existentes (rango de particiones, dedup anti-leakage, transaction_date) se CONSERVAN tal cual — solo cambia de dónde se lee, no cómo se filtra.
NO toques en esta rama: projection_views.sql ni el job de vistas (se jubilan en el cleanup posterior al merge, no antes), ni DDL_STRUCTURES, ni nada de escrituras.

FASE 2 — El juez:
5. Suite completa + tests adaptados (los ~que referencien el contrato viejo).
6. Test de paridad nuevo: con el mismo fixture de entrada, la salida de la lectura directa == la salida vía vistas, columna a columna (el mismo método con el que las vistas se ganaron su puesto, ahora en reversa).
7. Cosecha por fase: el doc de fase 0, diff de fase 1 con la decisión abierta de dev señalada, resultados de fase 2 con la paridad en el centro.
