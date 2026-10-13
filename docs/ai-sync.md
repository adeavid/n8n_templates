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
SOLO LECTURA, formato esperado|obtenido|✓/✗. Contexto: run de mecánica/contrato — forecast de juguete esperado; los warnings de utilities/fallback y de festivos son CONOCIDOS (H14, fix en vuelo): lístalos pero márcalos “esperado”, no como fallo.

A. Run: 5 tareas + duraciones + total (referencia: ~18 min del run mecánico anterior).

B. La migración en int (estreno): DESCRIBE de int_app.delphi.sanes_modelo_predictivo — ¿recreada con 13 columnas del contrato (totalamount, is_feasible INT, coste_estimado DECIMAL)? ¿Y decisiones con is_feasible + transport_cost (migración 002)? ¿La de security_stock intacta?

C. La cadena en su segundo entorno: en las decisiones de hoy: filas (~2.210), duplicados (0), is_feasible con 0/1, transport_cost con valores. En la tabla final: filas, is_feasible/coste_estimado/totalamount poblados (valores de juguete, pero NO nulos).

D. ⭐ LA LECTURA DE GOLD (el pendiente de dos semanas): en los logs/plan de la tarea expert — ¿ejecutó la lectura de pro_common_canales.oficina_operativa.sanes_arqueos? Tres desenlaces posibles, dime cuál: (1) leyó con éxito → cuántas filas trajo y cuántas oficinas del piloto casaron en el join; (2) PERMISSION_DENIED → el error LITERAL completo con la identidad que lo recibió; (3) ni llegó a intentarlo → en qué línea retornó antes y por qué.

E. Predicciones del lote de hoy: 2.210 × 14 = 30.940 filas, 0 nulos en los 3 modelos, magnitudes (juguete: mayoría ~0 con ecos del día real).

F. El zip en acción: ¿las vistas sirvieron sin error y algún camino usa ya el zip_code (el cruce oficina-calendario)? Evidencia breve.

G. Logs de las 5 tareas: lista completa de warnings/errores, separando “esperados” (utilities/fallback/festivos — H14) de cualquier cosa NUEVA.

Si algo inesperado sale ✗, repórtalo y para.
