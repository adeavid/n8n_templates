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
cosecha del e2e de dev del FLUJO FINAL (lectura directa + renombres + preparación-release + techo 175). SOLO LECTURA:
A. Identifica el run: run_id, fecha, resultado por tarea y DURACIÓN por tarea y total (compara con los ~45-49 min históricos de dev).
B. El lote: todo medido por el prediction_datetime del lote de ese run (la partición de dev acumula lotes viejos — regla de siempre).
C. Conteos: oficinas de la siembra × 14 días en predicciones, 0 nulos en los 3 modelos; decisiones y tabla final pobladas (13 columnas, is_feasible/coste con valores).
D. Renombres vivos: en los logs de las 5 tareas, CERO referencias a la columna vieja fecha y cero AnalysisException de columnas; las lecturas usan calendar_date.
E. Festivos: flags > 0 (la siembra tiene 48 fotos mensuales); working_days del horizonte verificado CONTANDO con el calendario sembrado (no asumas el número).
F. El techo nuevo: hard_balance_limit_pct=70.0 cargado en el run (config/parámetros); reporta si hubo activaciones/retiradas por el techo o “cargado sin activaciones” (legítimo con la siembra).
G. Warnings de aplicación: CERO (los de utilities deben seguir muertos); ruido de infra listado aparte.
H. Veredicto: compara los conteos contra la última cosecha certificada de dev — iguales = los tres merges no alteraron el comportamiento; cualquier diferencia, explicada o fichada.
