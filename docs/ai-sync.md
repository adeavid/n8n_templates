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
osecha E2E dev: certificación de LECTURA DIRECTA + siembra v2 + festivos en forecasting

Run verde en dev sobre la siembra v2. SOLO LECTURA, formato esperado|obtenido|✓/✗, predicciones siempre por el lote de hoy:

A. Run: 5 tareas + duraciones + total (referencia ~45-58 min; la siembra nueva puede mover tiempos — reporta sin alarma).

B. La siembra v2 sembró lo que debía: pre_app.delphi.branch_cash_servicing — ~1.000 particiones (días hábiles 4 años), zip_code presente, 2.000 oficinas, canarios 0001-0200 con sus saldos · calendar_datagen — 48 snapshots mensuales, festivos reales (Año Nuevo/Reyes presentes en la fuente).

C. ⭐ LECTURA DIRECTA en acción (el certificado de la Historia 1): en los logs/planes de las tareas — las lecturas van A PELO contra branch_cash_servicing y calendar_datagen (FileScan/retrieved con esos nombres, SIN _projection por ningún lado) + PartitionFilters activos. Cita las líneas literales (tipo “retrieved N idcents from pre_app.delphi.branch_cash_servicing”) — son el antes/después para plataforma.

D. ⭐ FESTIVOS — la capa 4 en vivo: (1) dataset de forecasting del lote de hoy: flag nacional en Año Nuevo y Reyes — espero ~2.000 filas marcadas por fecha (el 0/2.000 de la semana pasada, curado); local/autonómico según calendario. (2) working_days_to_trip sigue en 6 (no 14) en las oficinas de siempre. (3) Training: conteos de festivos > 0.

E. Los invariantes: 28.000/2.000/14 en el lote de hoy · 0 nulos en los 3 modelos · UN solo lote en la partición (idempotencia) · decisiones 2.000, 0 duplicados, 200 canarios, flags coherentes · cadena is_feasible (0/1 reales) + transport_cost poblados · tabla final 11 filas / 13 columnas / totalamount-is_feasible-coste_estimado sin nulos.

F. LA BASELINE NUEVA: magnitudes min/max/media por modelo vs el lote anterior — espero que CAMBIEN (los modelos ven festivos por primera vez en las features). Reporta el diff por modelo como medida del efecto, y si D y E cuadran, declara este lote como referencia definitiva del proyecto.

G. Logs: lista completa de warnings de las 5 tareas — espero CERO (ni calendario, ni utilities, ni fallback). Cualquier cosa nueva, literal.
