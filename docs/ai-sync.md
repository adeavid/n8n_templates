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
ejecutar la re-publicación del calendario y relanzar el e2e. Ejecuta los pasos EN ORDEN y DETENTE ante cualquier condición de aborto:

Preflight: COUNT de la foto origen (data_date_part='2026-10-13') → source_before. COUNT de la partición destino (data_date_part='2022-01-01') → target_before. Si target_before ≠ 0 → ABORTA y repórtame, no insertes nada.
INSERT: las 41 columnas explícitas. La ÚNICA columna que cambia es data_date_part → DATE’2022-01-01'. calendar_date y todas las demás se copian IDÉNTICAS. Confírmamelo en el reporte citando el SELECT.
Verificación: (a) source_after == source_before (la foto del 13/10 intacta); (b) copy_after == source_before (la copia completa); (c) muestrea 5 filas de la copia y compáralas con sus gemelas del origen por (zip, calendar_date): TODAS las columnas idénticas salvo data_date_part. Si cualquiera falla → ejecuta el DELETE de rollback, verifica que target vuelve a 0, y ABORTA reportando qué no cuadró.
Solo si TODO lo anterior pasó: lanza el e2e con odate=2026-09-15 (el jobs run-now de siempre con ese job_parameter) y dame el run_id y el link.
Reporte final: los 4 conteos, la confirmación de la comparación de filas, y el run lanzado. NO toques branch_cash_servicing, NO toques código, NO relances nada más si el run falla — solo repórtame el error.
