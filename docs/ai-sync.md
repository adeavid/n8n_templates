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

Diagnóstico convincente, pero necesito clavarlo antes de reportarlo como hallazgo. Tres bloques, NO toques ningún archivo del repo:

A) EVIDENCIA (para el hallazgo):
1. Archivo:línea de: (a) dónde se genera la cuadrícula con timestamps, (b) el join temporal, (c) el fillna(y=0).
2. Confirma spark.sql.session.timeZone del job cluster actual (y si puedes, del cluster interactivo donde corrimos en julio — hipótesis: UTC, por eso entonces funcionó).
3. Prueba de contraste: repite el conteo de matches casteando AMBOS lados a DATE — espero 55.500/55.500. Ese número es la demostración de que el desfase tz es la única causa.

B) WORKAROUND PARA CERRAR T1 (solo configuración, cero código):
Propón añadir spark.sql.session.timeZone=UTC en el spark_conf del new_cluster del JSON del job (ojo: en spark_conf, no spark_env_vars — ya nos pasó que la API ignora lo mal ubicado). Dame el fragmento JSON exacto y dónde va; lo aplico yo y relanzo con los mismos parámetros. Después repetimos el sanity completo (esperado: 700 filas, valores no triviales y distintos por modelo).

C) BORRADOR DE HALLAZGO H9 (mismo formato que H1-H8):
"El join temporal de create_training depende del timezone del cluster: con tz local (Europe/Madrid), 0 matches y el fillna convierte el 100% del target en ceros — silenciosamente, con job verde". Incluye: cuándo muerde (cualquier cluster con tz local = toda la red a cero sin aviso), evidencia archivo:línea + el conteo de contraste, y propuesta (join con semántica DATE en ambos lados como fix robusto; fijar timezone por config es mitigación, no solución). Candidato a test de caracterización.
