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
Contexto: el código lee branch_360 (vista de la capa de proyección), así que el E2E de int depende de que PROJECTION_VIEWS_SQL cree las vistas en int. Además run-predictions exige 57 observaciones/oficina y create-training fabrica rejilla desde start_date rellenando con y=0. Tres frentes:

Frente 1 — PR feature/arqueos-int-gold (solo valores de int):

Rama desde develop actualizado.
Cambia el valor de la clave de arqueos en la config de int (la que cualificó e4e5c52) a pro_common_canales.oficina_operativa.sanes_arqueos, comentario # FQN definitivo en zona gobernada (confirmado por plataforma 5-oct). Sin TODO de reversión. NO renombres claves.
Revisa los parámetros/plantilla del job PROJECTION_VIEWS_SQL para int: ¿a qué FQN apuntan sus fuentes? Si apuntan a pro gobernada (inexistente), cámbialos a int_app.delphi.branch_cash_servicing y int_app.delphi.calendar_datagen CON el TODO temporal de reversión (como en cash_movements.properties). Si ya apuntan bien, repórtalo y no toques nada.
No toques dev/lab/pro ni código Python. Cosecha: ficheros, valor antiguo → nuevo por cada uno, diff --stat, confirmación dev/lab/pro intactos, y cualquier otra referencia al FQN deducido inexistente (listar, no cambiar).

Frente 2 — start_date (deducción, sin ejecutar): ¿de dónde sale start_date en el flujo (forecasting.yaml, parámetro de job, derivado del odate)? ¿Qué valor efectivo tendría en int con odate=2026-09-15? Calcula la longitud de rejilla resultante y dime: ¿supera las 57 observaciones? Si es parámetro nuestro, ¿qué valor habría que pasarle para asegurar ≥57? Solo deducción con fichero:línea.

Frente 3 — forense del PROJECTION_VIEWS_SQL rojo en int (solo lectura): fecha/hora del último run fallido, mensaje de error literal (truncado si largo) y qué FQN intentó usar. ¿Es anterior o posterior al último despliegue de int?
