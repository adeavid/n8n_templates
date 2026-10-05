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
Contexto: el run verde de CASH_SUPPLY_E2E_PYTHON (odate=2025-12-31) escribió todo en la partición 2025-12-30: predicciones 56.000 (esperaba 28.000), decisiones 2.000 (ok), tabla final 11 (esperaba 2.000). Antes hubo un run fallido en expert con los mismos parámetros. Necesito forense en SOLO LECTURA: nada de modificar, borrar ni relanzar; en la cosecha solo conteos, agregados y resúmenes de código, nunca filas.

A. Semántica de partición: localiza en el código cómo se deriva data_date_part a partir del odate (¿odate tal cual, odate−1, otra cosa?). Dime fichero y resumen de la lógica. ¿2025-12-30 es el comportamiento esperado para odate=2025-12-31?

B. Predicciones (partición 2025-12-30): total de filas; filas distintas por clave (oficina + fecha objetivo); nº de claves con más de una fila. Si hay columna de timestamp/run que distinga tandas, reparto de filas por tanda (¿dos bloques de 28.000?). Y en el código: ¿el write de predicciones es append o sobrescribe la partición (overwrite/replaceWhere)?

C. Decisiones (2025-12-30): total, oficinas distintas, duplicados por clave, presencia de los canarios 0001-0200, resumen agregado de flags. Y modo de escritura en código (¿por qué aquí 2.000 y no 4.000? ¿sobrescribe?).

D. Tabla final — las 11 filas: qué oficinas son y qué tienen en común (agregado: ¿todas con is_order_recommended_today=1? ¿misma moneda? ¿canarios?). Y en el código de la tarea expert / escritura final: qué filtros se aplican entre las entradas y el insert. Compara con el diff de mi fix de hoy en expert: muéstrame resumen del diff y evalúa si el cambio puede explicar que de ~2.000 filas queden 11.

E. Festivos y nulos sobre 2025-12-30: repite los checks pendientes en esta partición: filas del horizonte en festivo (>0 esperado), nulos en predicción, modelos distintos y reparto.

No arregles nada de lo que encuentres — repórtalo y decido yo. Formato: por bloque, "pregunta | respuesta | evidencia (conteo o fichero:línea)".
