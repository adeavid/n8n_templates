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
Cambia de estrategia: nada de jobs reset (reemplazo total). Usa databricks jobs update con new_settings PARCIAL, que solo toca los campos que envías:

Del JSON de respaldo, copia el array tasks EXACTO y cambia únicamente el notebook_path de la tarea al mío (.../calendar_backfill_insert). Primer intento MINIMAL: jobs update --json '{"job_id": 35319055899581, "new_settings": {"tasks": [<la tarea con mi notebook>]}}' — sin tocar clusters ni nada más. Si la tarea referencia el cluster a nivel de job, esto no debería despertar la validación del cluster_log_conf.
Si la validación vuelve a rechazar por el dbfs:/cluster-logs: repite el update quitando SOLO ese campo (cluster_log_conf) del payload — y DÉJAMELO ANOTADO en el reporte, porque entonces la restauración no podrá ser byte-idéntica (ese campo ya no es re-enviable por nadie) y tengo que decírselo a Agustín.
Lanza el run UNA vez. Luego restaura con el mismo método: jobs update parcial devolviendo el notebook_path original (y el cluster_log_conf solo si el paso 2 no lo tocó). Verifica con jobs get + diff contra el respaldo, aceptando como única diferencia legítima la que hayas anotado en el paso 2.
El resto igual: verificación SQL de los 4 conteos + muestreo de 5 filas + rollback por escrito sin ejecutar. Si el update falla también en modo parcial y minimal → PARA y repórtame el error literal: pasaremos al plan C.
