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
Contexto: en integración, el equipo de datos aún no ha publicado las tablas origen en la zona gobernada de pro. Como puente temporal, Agustín las ha cargado en la zona privada de la aplicación en int. Hay que cambiar el apuntamiento de los sources del entorno de int para leer de ahí. Es un cambio SOLO de valores de configuración, SOLO del entorno de int.

Tarea:

Crea una rama feature/sources-int-zona-privada desde develop actualizado.
Localiza en la configuración del entorno de int (integration-adb / properties de int) los sources que hoy apuntan a los FQN de la zona gobernada de pro para estas dos tablas: la de branch cash servicing y pro_business_estructurales.cdl_modelos.calendar_datagen.
Cambia ÚNICAMENTE los valores de esos sources a estos FQN exactos (me los pasó por escrito el dueño de las tablas):
int_app.delphi.branch_cash_servicing
int_app.delphi.calendar_datagen
Junto a cada valor cambiado, añade un comentario # TODO: temporal — revertir a FQN de pro gobernada cuando el equipo de datos publique las tablas (los FQN definitivos quedan aquí en el comentario), conservando en ese comentario el FQN antiguo para que la reversión sea copy-paste.

Restricciones estrictas:

NO renombres ninguna clave de configuración, solo valores (el config loader ignora claves desconocidas en silencio).
NO toques la configuración de dev, lab ni pro, ni código Python, ni jobs, ni el DDL.
NO inventes ni deduzcas ningún otro valor: si encuentras más sources que creas relacionados, NO los cambies — repórtamelos y decido yo.
Si te desvías en algo de estas instrucciones, decláralo explícitamente.

Cosecha (sin volcar datos ni contenido de ficheros, solo resumen):

Lista de ficheros tocados y, por cada uno, la clave modificada con valor antiguo → valor nuevo.
Confirmación explícita de que ningún fichero de dev/lab/pro cambió (ej. salida de un git diff --stat contra develop).
Cualquier source adicional que apunte a esas dos tablas y que NO hayas tocado.
