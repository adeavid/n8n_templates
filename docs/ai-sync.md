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
Sobre la rama feature/naming-hardcodes: en el diff, ¿se modificó algún literal de string “branch_id”/”idcent” usado como nombre de columna (en select, withColumn, join, rename, esquemas de DataFrames intermedios, o el mapeo a unique_id de MLForecast)? Lista cada literal tocado con fichero:línea y clasifícalo: (a) columna interna creada y consumida dentro del código — renombrada consistentemente en TODOS sus puntos de uso, o (b) columna de contrato externo (tablas, vistas, salidas) — que NO debe haberse tocado. Si todo son identificadores Python puros sin literales, dilo y listo.

Run verde de CASH_SUPPLY_E2E_PYTHON en dev (odate=2025-12-31 → partición 2025-12-30). SOLO LECTURA, solo agregados, formato “esperado | obtenido | ✓/✗”:

A. El run: estado y duración de las 5 tareas + total (referencia: ~49-52 min).

B. Predicciones (partición 2025-12-30) — el certificado del fix:

Lotes por prediction_datetime (espero 4 — los 3 históricos + el de hoy) con filas por lote.
EN EL LOTE DE HOY: nulos por modelo — espero 0 en los TRES, LGBM incluido (el síntoma estrella; si LGBM trae un solo nulo, el fix no certificó).
En el lote de hoy: min/max/media por modelo (valores reales), 2.000 oficinas, 14 fechas, rango 2026-01-01 a 2026-01-14.
Comparativa con el lote del 5-oct (el último sano pre-bug): ¿los valores de hoy son equivalentes a los de aquel lote (misma siembra, mismos modelos)? Diff agregado por modelo. Esto verifica que las lecturas nuevas no alteraron los DATOS de entrada — espero diferencias ~0.

C. Decisiones: 2.000 filas, 0 duplicados, 200 canarios presentes, flags (espero 0 — canarios en rango), límite inferior aplicado (espero el 30% de siempre).

D. Tabla final: 11 filas (piloto∩arqueos), 11 columnas, 0 duplicados.

E. Las lecturas nuevas en acción — el certificado de la rama:

¿El calendario del training se leyó por RANGO? Confirma en logs/plan que entraron las DOS particiones de la siembra (2025-12-30 y 31) con su dedup, no solo la última.
¿Los filtros de partición de branch actuaron? Evidencia de partition pruning en el plan de lectura o conteo de particiones leídas vs totales.
Festivos del horizonte presentes (>0 — el check H10 de rigor).

No modifiques ni relances nada. Si algo sale ✗, repórtalo tal cual y paro yo.
