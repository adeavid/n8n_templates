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
Forense del ValueError de MLForecast en int, SOLO LECTURA, solo agregados. Series afectadas: 0094, 0097, 0100, 0107, 0108, 0109.

En int_app.delphi.branch_cash_servicing: filas por cada idcent afectado (¿sigue siendo 1?) y su(s) zip_code. Compara con 2-3 oficinas sanas.
En int_app.delphi.calendar_datagen: para esos zips, ¿cuántas filas por calendar_date? ¿Cuántos country_name distintos tiene cada uno de esos zips? Haz lo mismo para los zips de las oficinas sanas.
En la tabla de entrenamiento que escribió create-training en int: para los idcents afectados, conteo de filas por fecha (¿duplicadas?) y nº de fechas ausentes en el rango; lo mismo para una oficina sana.
En el código: el join entre branch y calendario — ¿por qué claves cruza (solo zip+fecha, o también country)? Fichero:línea.
Además: ¿cómo escribe create-training su tabla de salida — sobrescribe partición o append? (Necesito saber si relanzar el E2E es limpio o acumula.)
Veredicto en una línea: duplicación por join de calendario / duplicado de origen / huecos reales / otra cosa. No corrijas nada.
