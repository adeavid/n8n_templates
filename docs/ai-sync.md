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
cosecha E2E dev (certificación del fix festivos-FQN)

Run verde en dev (odate=2025-12-31 → partición 2025-12-30). SOLO LECTURA, formato esperado|obtenido|✓/✗, predicciones SIEMPRE por el lote de hoy:

A. Run: 5 tareas + duraciones (ref 45-49 min).

B. Logs — el síntoma estrella: lista completa de warnings de las 5 tareas. Deben haber DESAPARECIDO: “National holiday table is empty or outdated” y “Local holiday data incomplete” (los dos, en TODAS las tareas — antes salían en OPTIMIZE y EXPERT). Y confirmar que los 5 de utilities/fallback siguen sin aparecer. Lo que quede, listado literal.

C. working_days_to_trip — la materialidad corregida: las 9 oficinas que daban 14 (esperado 6) — ¿ahora dan 6? Muestra 3-4 valores contrastados con el calendario del horizonte (Año Nuevo y Reyes descontando).

D. Flags de festivos en el forecasting: en el dataset/lote de inferencia de hoy — flag nacional en Año Nuevo y Reyes: espero ~2.000 filas marcadas por fecha (antes: 0). Local/autonómico si aplica en el rango.

E. Idempotencia persiste: la partición 2025-12-30 sigue con UN solo lote (28.000) tras este run — el replace pisando al de ayer, sin acumular.

F. Lo de siempre en exprés: 28.000/2.000/14, 0 nulos en los 3 modelos, decisiones 2.000 sin duplicados con canarios, cadena is_feasible/transport_cost poblada, tabla final 11 con sus 13 columnas.

G. El cambio de baseline (documentar, no asustarse): magnitudes min/max/media por modelo del lote de hoy vs el lote anterior — espero que CAMBIEN: los modelos ahora ven los festivos en las features, y predecir distinto es lo correcto. Reporta el diff como medida del efecto del fix, y marca este lote como nueva referencia definitiva para comparativas futuras.
