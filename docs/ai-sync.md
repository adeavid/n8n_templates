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
rama fix/cadena-persistencia-y-calendario-dev desde develop. Commit+push tras cada paso. Tres fixes:

A. Persistir is_feasible y coste_estimado en la tabla de decisiones (el principal):

Añade los 2 campos a la proyección de la persistencia de optimize (spark.py) y al esquema de la tabla de decisiones.
Migración guardada 002 en DDL_STRUCTURES: si la tabla de decisiones existe SIN esos campos → ALTER TABLE ADD COLUMNS (aditivo, nada de DROP — esa tabla tiene consumidores futuros); con los campos → no-op. Mismo patrón auto-extinguible que la 001, celda %python PRIMERA línea (la lección de ayer).
El test que faltaba y que es la lección de este bug: test de cadena de persistencia — optimize escribe → se relee la tabla → los 2 campos presentes y con valores del GA. Validar el dato al FINAL del viaje entre tareas, no en memoria.

B. El calendario de dev (festivos a 0):
4. Corrige el tipo de data_date_part en la vista/siembra de calend_lab_nac_50 de dev (STRING → DATE), por la vía que corresponda (ajustar la siembra/DDL de la vista y recrearla con la identidad correcta). Verifica si calend_lab_loc_50 tiene el mismo problema.
5. En la resolución de particiones del calendario: añade una validación de tipo que falle ALTO (error claro) si data_date_part no es DATE — que el “empty or outdated” deje de ser un susurro. No cambies la lógica, solo conviértela en honesta.

C. El drift del template:
6. Alinea el template local del job con la sintaxis desplegada que FUNCIONA (job.parameters.start_date) — verifica contra la doc del formato correcto y deja template y job idénticos.

Suite completa verde. Cosecha: diff por fix, el test de cadena rojo-antes/verde-después, y confirmación de que la migración 002 pasa los tres caminos en seco.
