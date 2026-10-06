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
Diagnóstico diferencial dev-vs-int del ValueError de MLForecast. SOLO LECTURA, nada de editar. Mismos tipos DATE en origen y mismo código, pero dev pasó e int no — encuentra la divergencia:

La tabla de entrenamiento escrita por create-training: esquema en DEV (partición 2025-12-30) vs INT (2026-09-14). Tipo exacto de la columna temporal (¿DATE o TIMESTAMP?). Si es TIMESTAMP en alguno: valores distintos de hora+offset (agregado) en cada entorno.
Config de sesión de los runs: spark.sql.session.timeZone efectivo en el run verde de dev vs el fallido de int (spark confs del clúster del job / metadata del run), y versión de runtime del clúster en ambos.
El camino de la columna temporal en código: dónde se aplica pd.to_datetime(utc=True), dónde el toPandas, y en qué orden respecto al punto donde MLForecast valida freq="D" con intervalos. ¿El utc=True actúa antes o después de lo que ve MLForecast?
Veredicto en una línea: por qué dev pasa e int no, con evidencia (fichero:línea o conteo). Si la causa es config de clúster/entorno, dime exactamente qué clave difiere y dónde se define en nuestros recursos de despliegue.
