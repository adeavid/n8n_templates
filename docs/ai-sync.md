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
Contexto: el job CASH_SUPPLY_E2E_PYTHON ha terminado en verde en dev (parámetros: odate=2025-12-31, environment=dev, forecast_horizon=14, seasonality=7, sobre la siembra de pre_app.delphi). Necesito la cosecha de sanity ANTES de dar por validado el run. Todo en modo SOLO LECTURA: consultas de conteo y agregación, nada de modificar tablas ni relanzar nada. En la cosecha solo números, esquemas y resúmenes — nunca filas de datos.

A. El run en sí:

Estado final y duración de cada una de las 5 tareas (create-training, create-forecasting, run-predictions, optimize, expert) y duración total del job.

B. Tabla de predicciones:
2. Conteo total de filas para odate=2025-12-31 (espero 28.000 = 2.000 oficinas × 14 días).
3. Oficinas distintas (espero 2.000) y fechas objetivo distintas (espero 14), con el rango min–max de fechas.
4. Conteo de nulos en la columna de predicción (espero 0).
5. Modelos distintos usados (espero 3) y reparto de filas por modelo.
6. Conteo de filas del horizonte que caen en festivo según el calendario (espero > 0 — el horizonte incluye fin de año; si sale 0, repórtalo como ANOMALÍA, no lo justifiques).

C. Tabla de decisiones:
7. Conteo de filas para el odate (espero 2.000, una por oficina) y duplicados por clave (espero 0).
8. Las oficinas canario de la siembra: confirma que aparecen y dame un resumen agregado de sus decisiones (sin datos fila a fila).

D. Tabla final sanes_modelo_predictivo:
9. Conteo de filas para el odate y duplicados por clave (espero 0 duplicados).
10. Esquema real: número de columnas y sus nombres. En particular: ¿existen is_feasible y coste_estimado? Si existen, % de nulos en cada una (el cambio de código que las alimenta aún no está hecho, así que repórtame lo que haya SIN arreglar nada).
11. Conteo de nulos por columna en el resto de campos.

Restricciones: no modifiques nada, no relances nada, no "corrijas" ninguna anomalía que encuentres — repórtala y paro yo. Si alguna consulta no se puede hacer, di cuál y por qué, no la sustituyas por otra cosa.

Formato de salida: tabla por bloque (A/B/C/D) con columna "esperado | obtenido | ✓/✗", para que me sirva directamente como evidencia de Jira.
