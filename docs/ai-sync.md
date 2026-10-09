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
Run verde en dev (odate=2025-12-31 → partición 2025-12-30). SOLO LECTURA, formato esperado|obtenido|✓/✗:

A. Run: 5 tareas + duración total (referencia 45:19 del run anterior).
B. Migración (el estreno): ¿sanes_modelo_predictivo fue DROPEADA por DDL_STRUCTURES y RECREADA por el writer? DESCRIBE: 13 columnas, con totalamount (no total_amount), is_feasible INT, coste_estimado DECIMAL(17,2), tipos y orden del contrato CDO.
C. Las columnas nuevas (el otro estreno): en las filas escritas hoy — is_feasible: distribución de 0/1 (espero mayoría 1, coherente con el GA); coste_estimado: min/max/media, > 0 donde hay movimiento, coherente con los importes. % de nulos en ambas (espero 0 en filas con decisión).
D. Lo de siempre: predicciones del lote nuevo (28.000, 0 nulos en los 3 modelos — que el batch no haya roto el fix), decisiones (2.000, canarios, flags 0), filas de la final (11), festivos > 0.
E. start_date: confirma en los logs/parámetros del run que usó el default 2022-01-01 y la ventana es IDÉNTICA a la del run anterior (el “default no cambia comportamiento” verificado en producción de verdad).

Si algo sale ✗, repórtalo y para.
