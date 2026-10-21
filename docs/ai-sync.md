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
cosecha de LA PRUEBA COMPLETA (int, odate=2026-10-10, SOLO LECTURA):
(1) Wheel y config: el run carga la wheel nueva (post-merge de fix/cruce-zip) — ruta/SHA — y la config con hard_balance_limit_pct=70.0.
(2) Tiempos por tarea y total (referencia: 21:40 el lunes; el fix del zip no debería mover la aguja).
(3) Lote por prediction_datetime: predicciones = oficinas×14, 0 nulos/duplicados en 3 modelos.
(4) Training CON festivos por fin: flags nacionales/locales/autonómicos > 0 sobre el histórico completo (la foto 2022-01-01 las hace elegibles) — reporta conteos.
(5) ⭐ El fix del zip, validado con número: calcula desde la foto los pares oficina-fecha con festivo esperados en el horizonte 10–23/10 (el 12-oct nacional debe marcar TODAS las oficinas; locales los que toque) y compáralo con lo marcado en el dataset de forecast. Esperado vs observado, cero a cero no vale.
(6) ⭐ La cadena COMPLETA por fin: cashflow de la partición 09/10 con filas > 0 → optimize escribe decisiones (is_feasible/transport_cost con valores; fallback 30% operando si security stock sigue vacío) → expert produce la salida de pilotos → tabla final poblada con sus 13 columnas.
(7) El techo del 175 ante encajes reales: ¿cuántas oficinas tienen encaje < 33.333€ y hubo alguna activación/retirada del techo? Primera vez que puede morder de verdad.
(8) Propagación de config (el fix 2): upper/lower_limit_pct del YAML llegan al ProblemConfig — evidencia en logs o valores efectivos.
(9) Warnings de aplicación (los 14 UserWarnings de festivos nulos deben haber DESAPARECIDO o reducirse a las 565 oficinas sin datos recientes), lecturas a pelo, cero referencias viejas.
(10) Magnitudes por modelo (media/min/max) — la base de la comparativa con Pablo/Álvaro.
