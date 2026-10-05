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
Contexto: en el workspace de INT, Agustín ha cargado int_app.delphi.branch_cash_servicing e int_app.delphi.calendar_datagen con datos reales. Quiero reconocimiento completo en SOLO LECTURA antes de lanzar el E2E de int. Nada de escribir, crear ni modificar; en la cosecha solo conteos, fechas, esquemas y nombres — jamás filas de datos.

A. Particiones (lo más importante): para cada una de las dos tablas: valores distintos de la columna de partición (data_date_part o equivalente), con conteo de filas por partición y min–max. Para calendar_datagen, recuerda que necesito saber si hay partición ESTRICTAMENTE ANTERIOR a la fecha de datos de branch (resolución de calendario).

B. Contrato de esquema: columnas (nombre y tipo) de ambas tablas, comparadas con lo que esperan nuestro código y las vistas de proyección en int. Repórtame cualquier columna que falte, sobre o cambie de tipo — sin corregir nada.

C. Inventario de arqueos: SHOW TABLES en int_app.delphi — lista completa de lo que hay. Después comprueba si existe algo tipo arqueos accesible desde int: ¿existe pro_business_estructurales.cdl_modelos.sanes_arqueos? ¿Alguna tabla con "arqueo" en el nombre en los catálogos/esquemas que podamos listar desde este workspace? Solo existencia y conteo de filas si es legible; si algún catálogo da error de permiso, reporta el error literal y sigue.

D. Piloto: de los 36 idcent de PILOT_BRANCHES, ¿cuántos están presentes en int_app.delphi.branch_cash_servicing? (Conteo, no la lista de códigos.) Esto me predice cuántas filas puede dar la tabla final en int.

E. Volumen: filas totales y oficinas distintas de branch_cash_servicing — para dimensionar la prueba de rendimiento frente a las 2.000 de dev.

Si algo no es consultable por permisos, repórtalo tal cual; no lo sustituyas ni lo deduzcas.
