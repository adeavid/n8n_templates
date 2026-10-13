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
rama fix/eliminar-dependencia-utilities desde develop. Commit+push por paso.

Contexto: utilities.spark_utils nunca se instala (pip en runtime contra ruta inaccesible) y todo corre en fallbacks — incluido el fallback de escritura que causa el append (H11). Para la V1, eliminamos la dependencia rota y hacemos oficiales los caminos propios:

0. Materialidad primero (solo lectura): ¿optimize usa festivos (vía holidays.py) para working_days_to_trip? Compara working_days de 2-3 oficinas del run de hoy contra el calendario real del horizonte (hay Año Nuevo y Reyes). Repórtalo ANTES de tocar nada — necesito saber si las decisiones actuales están contando festivos como hábiles.

1. Inventario: todos los usos de utilities.spark_utils (f_df_ultima_particion_anterior, f_guarda_df, f_guarda_particion, f_existe_df) y los tres bloques de pip-en-runtime (forecasting/_utils.py, holidays.py, send_email_notification.py).

2. Resolución de particiones: los lectores de holidays.py (y cualquier otro) pasan a usar la misma lógica de resolución que ya tiene el repo (la de la rama de lecturas) — extráela a un helper compartido si no lo está. Fuera el fallback “reference_date as partition”.

3. Escritura — aquí matamos H11 a propósito: implementa los equivalentes nativos explícitos: escribir partición = replaceWhere sobre la partición (idempotente), existencia = chequeo nativo. Elimina el fallback append. OJO: esto CAMBIA la semántica en dev (antes acumulaba lotes) — es deliberado y deseado; el próximo run limpiará la partición de fósiles él solo.

4. Fuera los pip de runtime: elimina los tres bloques de instalación en caliente. Ningún código instala paquetes en ejecución.

5. Tests: (a) idempotencia de escritura — dos escrituras a la misma partición dejan UN lote (el test que H11 siempre mereció); (b) resolución de festivos de holidays.py con fixture multi-partición (el mismo estilo que los de lecturas); (c) suite completa.

6. Cosecha: materialidad del punto 0, inventario, diff, tests rojo-antes/verde-después donde aplique, y la lista de warnings que deben DESAPARECER en el próximo run (“utilities not available”, “fallback partition”, festivos empty).
