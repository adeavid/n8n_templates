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
Por lote: filas y nulos de LGBM por prediction_datetime en la partición 2025-12-30. Espero: lote de hoy = 28.000 filas, 0 nulos en los 3 modelos; los 28.000 nulos de LGBM concentrados en el lote del 6-oct.
La cadena de is_feasible/coste_estimado: (a) ¿la tabla de DECISIONES que escribió optimize HOY contiene esos campos? DESCRIBE + conteo de no-nulos. (b) ¿De dónde lee el writer del expert los dos valores — del dataframe en memoria o de la tabla de decisiones persistida? fichero:línea. (c) ¿Está disparando el camino de “nulls tipados por fuente sin campos”? Confirma mi hipótesis o mátala: la propagación llega hasta la SALIDA de optimize pero no sobrevive a la PERSISTENCIA entre tareas.
Festivos, bien medido: sobre la tabla de entrenamiento escrita HOY y el lote de predicciones de HOY — conteo de filas con festivo (oficina/local/nacional). El horizonte incluye Año Nuevo y Reyes: nacional ≥ 2 obligatorio. Si de verdad es 0, diff de qué cambió en el camino del calendario entre el run del 9-oct y este (¿naming? ¿start_date wiring?).
Aclárame la nota críptica de E: “task parametrizada con job.parameters.start-date PENDIENTE” — ¿el parámetro llegó al task o no? ¿Con qué start_date efectivo corrió el training?
