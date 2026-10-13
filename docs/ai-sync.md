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
Run verde en dev (odate=2025-12-31 → partición 2025-12-30). SOLO LECTURA, formato esperado|obtenido|✓/✗. REGLAS FIJAS: en predicciones, TODO medido sobre el lote de HOY por prediction_datetime; e incluye al final la sección de logs.

A. Run: 5 tareas + duraciones (referencia 45-49 min).

B. Jobs del install: DDL_STRUCTURES — ¿la migración 002 disparó (ALTER ADD COLUMNS en decisiones) y la 001 quedó en no-op (la tabla final ya tiene el esquema nuevo)? Evidencia del log de cada guarda.

C. La cadena, certificada en la tabla de DECISIONES (el fix principal): DESCRIBE de cash_supply_optimization: ¿existen ya is_feasible y coste_estimado? En las 2.000 filas de hoy: distribución de is_feasible (0/1, espero mayoría 1), coste_estimado min/max/media (>0 donde hay movimiento), % nulos (~0).

D. Tabla final: 13 columnas contrato CDO · en las ~11 filas: is_feasible con 0/1 REALES (ya no 11/11 nulos), coste_estimado con valores, totalamount poblado.

E. Festivos (el fix B — el otro estreno): en el training de hoy: conteos oficina/local/nacional — todos > 0 (referencia sana: ~6.000/4.000/2+). En el lote de forecasting de hoy: flag nacional en Año Nuevo y Reyes — espero ~2.000 filas marcadas por cada fecha (todas las oficinas). Si algo sigue a 0 → ✗ y para.

F. Predicciones del lote de HOY: 28.000 filas, 0 nulos en los 3 modelos, min/max/media por modelo. OJO — AVISO IMPORTANTE: los valores YA NO deben coincidir con el lote de referencia del 5-oct — con los festivos por fin presentes en las features, los modelos predicen distinto, y eso es lo CORRECTO. No reportes la divergencia como fallo: repórtala como magnitud (diff agregado por modelo) para documentar el efecto del fix de festivos.

G. Decisiones — lo de siempre: 2.000, 0 duplicados, 200 canarios, flags (espero 0, canarios en rango).

H. Logs de las 5 tareas (la regla nueva): lista TODOS los warnings/errores. En particular: “National holiday table is empty or outdated” y “Local holiday data incomplete” deben haber DESAPARECIDO; la validación de tipo nueva no debe haber saltado. Cualquier warning nuevo, lístalo tal cual.

I. start_date: valor efectivo del run (espero default 2022-01-01) y confirmación de que template y job desplegado ya dicen lo mismo.

Si algo sale ✗, repórtalo y para — no corrijas nada.
Suite completa verde. Cosecha: diff por fix, el test de cadena rojo-antes/verde-después, y confirmación de que la migración 002 pasa los tres caminos en seco.
