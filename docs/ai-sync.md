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
rama fix/lectores-festivos-fqn desde develop. Commit+push por paso.

Causa confirmada: los lectores de festivos (optimize/expert y las features de forecasting) consultan calend_lab_nac_50/calend_lab_loc_50 por nombre corto sin resolver, y un except Exception amplio traga el error y lo convierte en “empty or outdated”.

Resolución de nombres: esos lectores pasan a resolver la tabla por la MISMA vía que el resto del código (resolve_table_name()/la config de PersistenceConfig) — nada de nombres cortos sueltos. Verifica los TRES consumidores: working_days del optimize, el expert, y las holiday-features del dataset de forecasting.
El except mentiroso, fuera: sustituye el except Exception amplio por manejo honesto — el error real se loguea COMPLETO y la lectura de festivos irresoluble FALLA ALTO (o como mínimo warning con la excepción literal). Un calendario que no se encuentra no es “vacío”: es un error. Revisa si el mismo patrón de except-ancho existe en los lectores hermanos y lístalos (sin cambiarlos si no toca).
Tests: (a) el lector devuelve festivos con fixture (Año Nuevo y Reyes presentes → working_days los descuenta); (b) nombre irresoluble → excepción visible, no vacío silencioso; (c) suite completa verde.
Cosecha: diff, fichero:línea del resolve aplicado en cada consumidor, los tests rojo-antes/verde-después, y la lista de otros except-anchos detectados.
