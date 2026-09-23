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
Necesito la estructura de la TABLA FINAL del pipeline como documento de una página para una reunión de decisión mañana. La tabla final = donde escribe run_expert_model (el output del criterio experto, lo que consume la aplicación aguas abajo).

1. Localiza en el código dónde escribe el expert model su resultado: nombre físico de la tabla (resuélvelo desde config/defaults — recuerda que los defaults apuntan a PRO) y modo de escritura (append/overwrite, particionado y por qué campo).
2. Esquema completo: lista de columnas con tipo y una línea de significado por columna, deducido del código que las construye (p. ej. cantidad por denominación, fecha de decisión, identificador de oficina...).
3. Marca: (a) qué columnas son la "decisión" que consume la aplicación vs cuáles son metadata/intermedias; (b) si hay campos que se calculan pero NO se persisten (sé que is_feasible se pierde en el entry point — confírmalo y mira si hay más casos); (c) claves de negocio: ¿qué combinación identifica una fila (oficina+fecha+denominación?)?
4. De propina: la tabla de decisiones del optimize (la intermedia previa al experto) — solo nombre y 1 línea, para poder explicar mañana la diferencia entre ambas.
5. Formato de salida: tabla markdown campo|tipo|significado|¿decisión o metadata?, más 3-4 líneas de notas. Es para llevarla impresa/en pantalla, no para publicar.
