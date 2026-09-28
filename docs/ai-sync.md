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
Arrancamos la capa de proyección (aprobada por modelos el jueves): vistas SQL que exponen el CONTRATO VIEJO sobre las tablas del contrato NUEVO, para que el código no se toque. Te adjunto los CREATEs del equipo de datos y el análisis de diferencias (renombres, tipos, calendario único). Trabaja por fases y PARA al final de cada una con la cosecha (conteos/resúmenes, nunca datos).

FASE 1 — Tablas nuevas en el lab con datos espejo.
Crea en lab_app.iadarq las tablas del contrato NUEVO (desde los CREATEs de Juan, con sufijo _50) y puéblalas TRANSFORMANDO las tablas sintéticas viejas existentes con el mapeo inverso (idcent→branch_id, daily_net_cashflow→daily_customer_cashflow, tipos casteados, los 3 calendarios fundidos en calendar_datagen con sus flags y zip_code, etc.). Así el CONTENIDO es idéntico y solo cambia la forma — condición para la paridad de la fase 3. Cosecha: conteos por tabla nueva vs vieja (deben cuadrar).

FASE 2 — Las vistas.
Escribe las vistas que reconstruyen el contrato viejo sobre las tablas nuevas: renombres con AS, CASTs de tipos, y los 3 calendarios lógicos derivados de calendar_datagen con filtros. Como archivo SQL en los resources del proyecto (el mecanismo del install), no ejecutado a mano suelta. Enséñame el SQL completo antes de crearlas.

FASE 3 — Paridad.
Corre el pipeline completo (forecast → optimize → experto) leyendo DE LAS VISTAS, y compara la salida contra la ejecución de referencia sobre las tablas viejas: mismas filas, mismos valores, diff = 0. Es el mismo listón de paridad de siempre.

FASE 4 — Empaquetado.
Integra el SQL de vistas en los resources por entorno + nota de documentación + PR en feature/capa-proyeccion.

CASO A DOCUMENTAR (no resolver ahora): las tablas reales solo tienen filas de días laborables y las sintéticas viejas tienen todos los días — la vista no puede inventar fines de semana. Déjalo escrito como diferencia conocida a validar con las particiones reales de integración.
