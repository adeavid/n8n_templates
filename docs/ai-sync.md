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
rama fix/cruce-zip-festivos-y-config desde develop, commits separados:
Commit 1 — el cruce zip (H16): en la capa de lectura directa, conserva zip_code en la proyección del branch (la tabla lo trae; la vista vieja lo proyectaba y la lectura directa lo perdió). En forecasting, cruza los calendarios LOCAL/AUTONÓMICO por zip_code+fecha (el nacional sigue por fecha/país). Espejo del training, que sí cruza bien — iguala los dos caminos. Test de aceptación con el caso real: una foto con festivos locales en horizonte + oficinas con zip → flags >0 (y un test que falle si alguien vuelve a comparar branch_id con zip_code: cero matches = error, no silencio).
Commit 2 — propagación de config: en el path RunOptimizeTask→ProblemConfig, pasa también upper_limit_pct y lower_limit_pct desde la config (hoy solo viaja hard_balance_limit_pct y los otros caen a defaults). Test: los tres valores del YAML llegan al ProblemConfig reconstruido.
Commit 3 — fichaje, no fix: el filtro de rol deja pasar filas ‘F’ que el builder ignora — documentado en la PR como decisión pendiente.
Tests completos en verde. NO mergear sin mi OK.
