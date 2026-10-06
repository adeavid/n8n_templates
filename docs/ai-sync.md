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
Contexto: diagnóstico cerrado — ds se persiste como TIMESTAMP y al materializarse en pandas adopta hora local Europe/Madrid (01:00/02:00 según DST); MLForecast valida freq="D" sobre esa secuencia local y lanza el ValueError en los cambios de hora. Fix mínimo en el punto de consumo:

Rama feature/ds-freq-dst desde develop.
En predictions.py, en el flujo que alimenta MLForecast.fit (incluido el camino de intervalos): normaliza la columna temporal a fecha pura sin zona ANTES de la validación — cast a date en Spark antes del toPandas, o tz_localize(None) + normalize justo después; elige el punto más temprano que cubra TODOS los caminos hacia MLForecast, y que sea UNO solo.
NO cambies el esquema persistido de la tabla de entrenamiento ni toques datasets.py, salvo que el punto único de consumo viva ahí — en ese caso justifícamelo en la cosecha.
Test nuevo: una serie que cruce los dos cambios de hora (marzo y octubre) con ds TIMESTAMP en Europe/Madrid, verificando que el flujo ya no lanza el ValueError y produce el horizonte completo. Es el test de caracterización de este bug: tiene que fallar con el código viejo y pasar con el nuevo.
Suite completa verde. Cosecha: diff resumido (ficheros y líneas), resultado de la suite y del test nuevo, y confirmación de que el cambio vive solo en el punto de consumo.
