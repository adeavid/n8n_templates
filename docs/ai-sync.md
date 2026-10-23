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
generar los lotes de octubre para la comparativa (secuencial, con puertas):
Vas a lanzar el job e2e de int (el de siempre, perfil cash-supply-int) una vez por cada odate de esta lista, EN ORDEN: 2026-10-01, 2026-10-02, 2026-10-03, 2026-10-06, 2026-10-07, 2026-10-08, 2026-10-09, 2026-10-10 — saltándote el 10/10 si ya existe su lote (lo generamos el 21).
Para cada odate: (1) preflight: COUNT del cashflow en branch_cash_servicing para transaction_date = odate−1 — si es 0, SÁLTATE ese odate y repórtalo (no lances un run que sabemos vacío); (2) lanza el run con ese odate como job_parameter y espera el verde (~26 min); (3) verificación del lote: nuevo prediction_datetime en predicciones con filas = oficinas×14 y 0 nulos; decisiones en la partición odate−1 con filas >0; tabla final con filas nuevas del lote; (4) si un run falla o la verificación no cuadra: PARA la secuencia, no relances, repórtame cuál y el error.
Al final: tabla resumen — odate, run_id, duración, nº predicciones, nº decisiones (factibles/no), nº filas en la final. Nada de código ni DDL; solo run-now y SELECTs.
