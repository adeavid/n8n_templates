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
rama feature/vocabulario-contrato-nuevo en WORKTREE desde develop. NO se mergea sin mi OK (entra después de la prueba de rendimiento). Commit+push por paso.

Contexto: tras la Historia 1, la capa de lectura traduce el esquema nuevo a nombres internos del contrato viejo (fecha ← calendar_date, etc.) y el código aguas abajo sigue hablando el idioma antiguo — confuso para cualquiera que audite código contra esquema real.

FASE 1 — Inventario (solo lectura, enséñamelo antes de tocar): localiza TODO el vocabulario del contrato viejo que sobrevive como nombres internos post-Historia 1: fecha y sus hermanos (nombres de columnas de los calendarios viejos, de branch_360 si queda alguno — tipo feclocal, tifestv o los que aparezcan). Tabla: nombre viejo | nombre en el esquema nuevo | dónde se usa (ficheros, nº de apariciones) | clasificación: (a) interno puro renombrable, (b) frontera que NO se toca (claves de config — H5b, columnas de tablas de SALIDA, fixtures que modelan tablas viejas aposta).
FASE 2 — Rename mecánico solo de los clasificados (a): el código pasa a usar los nombres del contrato nuevo de punta a punta; el renombre de la capa de lectura desaparece donde quede redundante (leer calendar_date y llamarlo calendar_date). Cero cambios de comportamiento.
Suite completa verde + paridad re-ejecutada (mismo juez de siempre). Cosecha: inventario, diff, suite, y confirmación de cero claves de config ni esquemas de salida tocados.
