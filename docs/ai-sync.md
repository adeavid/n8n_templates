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
Run verde de CASH_SUPPLY_E2E_PYTHON en int (odate=2026-09-15 → partición 2026-09-14). Verifica contra esperado, formato "esperado | obtenido | ✓/✗":

A. El run: estado y duración de cada una de las 5 tareas + total. (Referencia dev: ~52 min con 2.000 oficinas × 4 años; aquí hay menos historia real pero rejilla similar.)

B. Predicciones (partición 2026-09-14): total de filas (espero ~30.940 = 2.210 × 14) · oficinas distintas (2.210) · fechas distintas (14, rango 2026-09-15 a 2026-09-28) · nulos en los 3 modelos (0) · magnitud de los valores (espero cercanos a 0 — forecast de juguete por la historia de un día; repórtame min/max/media por modelo, sin filas).

C. Decisiones: total (espero 2.210) · duplicados por clave (0) · límite inferior aplicado: confirmo que todas usan el fallback del 30% configurado (la tabla de security stock está vacía a propósito) · resumen de flags.

D. Tabla final sanes_modelo_predictivo: filas (espero ≤34 — los pilotos presentes tras el join con arqueos; dime cuántas exactamente) · duplicados (0) · columnas (11) · todas las filas son oficinas piloto.

E. La lectura de gold: confirma en los logs/plan de la tarea expert que leyó pro_common_canales.oficina_operativa.sanes_arqueos con éxito (la prueba empírica del acceso del SP, para la evidencia).

No corrijas ni relances nada; esto es el acta.
