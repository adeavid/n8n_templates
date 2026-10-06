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
Contexto: el ValueError de MLForecast viene de que las fechas llegan como TIMESTAMP con zona (medianoches UTC → 01:00+01/02:00+02 Madrid) y la validación freq="D" se rompe en los cambios de hora. Hipótesis: la vista de proyección sirve transaction_date como TIMESTAMP mientras el contrato original (y la tabla física de dev) es DATE.

Confirma tipos (solo lectura): tipo de transaction_date, month_date y data_date_part en (a) int_app.delphi.branch_cash_servicing, (b) la vista branch_360_50_projection, (c) la tabla física pre_app.delphi.branch_360_50 de dev (el contrato de referencia); y calendar_date en la vista de calendario vs su físico de dev. Tabla comparativa.
Si se confirma: rama feature/vistas-cast-date — en el SQL de las vistas de proyección, CAST a DATE de todas las columnas de fecha que el contrato original define como DATE (las que salgan del punto 1, no solo transaction_date — no quiero jugar otra ronda de este juego con month_date). SOLO el SQL de vistas: ni Python, ni configs, ni otros entornos.
Cosecha: tipos antes → después por columna, diff --stat contra develop, confirmación de que no hay más cambios.
