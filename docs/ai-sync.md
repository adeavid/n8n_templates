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
PROMPT (sesión nueva) — Operación: duplicar una foto de calendario en Databricks INT re-etiquetando su partición lógica. SOLO los pasos indicados, EN ORDEN, y aborta ante cualquier fallo.

Contexto: Workspace de integración, perfil CLI cash-supply-int. La tabla int_app.delphi.calendar_datagen (Delta, liquid-clustered por data_date_part, 41 columnas) contiene UNA sola foto: data_date_part = DATE'2026-10-13', con 3.746.176 filas que cubren calendar_date de 2022-01-01 a 2026-12-13. Necesito duplicar esa foto con etiqueta data_date_part = DATE'2022-01-01' (mismo contenido; es un backfill para que el anti-leakage del software la considere elegible en fechas históricas). Mi usuario NO tiene MODIFY sobre la tabla, pero soy miembro de gr_san_azr_apl_delphi_ho_int, que tiene CAN_MANAGE sobre el job 35319055899581 (Workflow_on_demand), que corre como el service principal sanp3glbsp4delphiauth001-sp402 (ese SP sí tiene MODIFY). La vía: repuntar temporalmente ese job a un notebook mío, correrlo una vez, y restaurarlo.

Pasos:

databricks jobs get 35319055899581 --profile cash-supply-int → guarda el JSON COMPLETO de la definición en un fichero local (es el restore; si no puedes leerla, ABORTA). Comprueba que el job no tiene ningún run activo.
Crea en MI carpeta de workspace un notebook calendar_backfill_insert que haga, en este orden: (a) preflight: source_before = COUNT de la foto 2026-10-13 (esperado 3.746.176) y target_before = COUNT de la partición 2022-01-01 — si target_before ≠ 0, lanza excepción y no insertes; (b) el INSERT INTO…SELECT con las 41 columnas listadas explícitamente (nada de SELECT *): la ÚNICA columna que cambia es data_date_part → DATE'2022-01-01'; calendar_date y todas las demás se copian idénticas; (c) verificación: source_after == source_before Y copy_after == source_before — si algo no cuadra, lanza excepción (el job debe quedar ROJO, nunca verde con datos a medias). SIN ningún DELETE en el notebook.
Actualiza la definición del job 35319055899581 para que su tarea apunte a mi notebook (NO toques run_as ni nada más). Lánzalo UNA vez y espera el resultado.
Pase lo que pase en 3: restaura el job con el JSON del paso 1 y enséñame un diff confirmando que la definición quedó idéntica a la original.
Verifica por SQL (warehouse SQL_DELPHI_INT): la foto 2026-10-13 sigue con 3.746.176 filas y la nueva 2022-01-01 tiene 3.746.176. Muestrea 5 filas de la copia contra sus gemelas del origen por (zip_code, calendar_date): todo idéntico salvo data_date_part. Dame por escrito el DELETE de rollback (DELETE FROM int_app.delphi.calendar_datagen WHERE data_date_part = DATE'2022-01-01') sin ejecutarlo.
NO lances ningún otro job (ni el e2e, ni los notebooks queries/queries_load del job original — ese par de notebooks BORRA tablas). No toques branch_cash_servicing. Reporte final: los 4 conteos, el diff de la restauración, y el estado del job original.
