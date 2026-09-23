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
Confirmado, doy H9 por verificado. Aplico yo el cambio: edito el JSON del job añadiendo spark.sql.session.timeZone=UTC dentro de settings.job_clusters[0].new_cluster.spark_conf (fusionando con las claves existentes, sin borrar ninguna) y relanzo con los mismos parámetros. Mientras corre, déjame listo el sanity final para ejecutarlo en cuanto acabe, con un añadido:

- Los 7 checks de siempre (700 filas, 50 oficinas, 14 fechas D+1..D+14, 0 nulos, columnas de los 3 modelos, valores no triviales y distintos entre modelos, conteo de training).
- NUEVO: duplicados. El run malo ya escribió en las tablas de training y predicciones. Verifica si el nuevo run SOBRESCRIBE la partición del odate o AÑADE — si añade, tendríamos las filas a cero conviviendo con las buenas (y sabemos que el pivot de aguas abajo explota con duplicados). Dame: conteo de filas por (idcent, fecha) con más de 1 aparición en la tabla de predicciones, y total de filas de la tabla (si hay residuos del run malo, propón cómo limpiar la partición antes de dar por bueno el sanity — sin ejecutar nada hasta mi ok).
- Cuando todo cuadre: el bloque de evidencia para la issue (fase 3), incluyendo el episodio completo en 3 líneas: run verde con predicciones a cero → sanity lo detectó → causa raíz H9 (join sensible a timezone) → mitigado con timezone fijado en el job y validado.
