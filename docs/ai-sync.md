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
Rename de la tabla final: fuera el sufijo _u (regla del banco: _u es exclusivo de tablas publicadas por analistas — confirmado por plataforma y modelos). Nombre nuevo: sanes_modelo_predictivo. Alcance:

1. EL DDL del repo (el CREATE en resources): renombra la tabla a sanes_modelo_predictivo. Actualiza también el comentario de cabecera (nota de CDO/casita) si menciona el nombre viejo.
2. REFERENCIAS — barrido completo del nombre viejo en el repo y clasifica cada aparición:
   - Properties/config por entorno (el VALOR de cash_denominations_service_table_name): en dev-adb e integration-adb → nombre NUEVO (allí la tabla aún no existe, empezamos limpios). En lab-adb → DÉJALO como está (_u): la tabla del lab ya existe con ese nombre y funciona; renombrarla es churn sin beneficio — anótalo como divergencia documentada del lab.
   - El DEFAULT del código (que apunta a la paramétrica _u de pro): NO LO TOQUES — la paramétrica real sigue llamándose así y ese default es tema aparte (H5).
   - Docs: el .md del esquema en Jira, evidence.md y el doc de linaje → nombre nuevo con una línea de nota ("renombrada desde _u por convención de zona gobernada").
3. CLAVES: ninguna clave de config se renombra — solo valores. (Regla de siempre.)
4. PR pequeña con título claro ("Rename tabla final sin sufijo _u — convención de publicación") y me dices cuándo mergear.
