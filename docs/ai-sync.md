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
Fase B en feature/limite-175-bloqueo-caja (commits separados, NO mergear):

Nueva restricción de techo duro en el GA: saldo_proyectado ≤ hard_balance_limit_pct × encaje, SIN tolerancia, evaluada en las mismas posiciones que la restricción existente del upper_limit y reparada por el mismo mecanismo (adelantar/crear acción negativa). La restricción actual 1,60+tol NO se toca: conviven, y la nueva solo puede ser más restrictiva.
hard_balance_limit_pct como clave de configuración NUEVA en los YAML de los 4 entornos, valor 70.0 (mismo convenio que upper_limit_pct: porcentaje sobre el encaje), con comentario: # techo absoluto anti-bloqueo de caja (bloqueo físico al 175%; margen de 5 pts acordado en reu 8-oct).
Tests: (a) encaje 20.000 — caso que hoy permite saldo 37.000 (1,85×): con el techo queda ≤34.000 y por debajo del bloqueo de 35.000; (b) encaje 100.000 — el techo no muerde nunca antes que el 1,60+tol… [ojo: 1,60×100k+5k=165k < 170k ✓] el comportamiento actual no cambia; (c) frontera exacta en el techo; (d) la reparación genera retirada cuando el techo se excede; (e) la restricción vieja sigue operando.
NO toques la tolerancia ni el manejo del índice 0: documéntalos en la descripción de la PR como hallazgos pendientes de decisión funcional.
Al final: archivos por commit, tests verdes, y confirma el lot_size de los YAML de int y pro (para recalcular los números del mensaje si difieren de dev).
