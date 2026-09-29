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
Objetivo: dejar HOY el despliegue a dev listo. La PR #14 de Agustín no es mergeable (tus 5 findings), así que la sustituimos por una rama mía con lo bueno de la suya, corregido. La PR #14 no la toques — quedará superada y se cierra con un comentario al final.

PASO 1 — Rama limpia con lo aprovechable:
Crea fix/dev-properties desde develop (actualizado, con mi capa de proyección dentro). Trae de la PR #14 SOLO la estructura de properties/config de dev. Explícitamente FUERA: cualquier cambio en lab-adb (lab queda intacto, restaurando lo que su PR tocaba) y cualquier borrado de módulos legacy de cooking_depto (eso será tarea aparte con la suite corriendo).

PASO 2 — Correcciones sobre esa base:
a) source8 duplicado: contrato de claves explícito — cada tabla su clave (denominations y security_stock separadas, source9 si hace falta), en dev Y verificando que el patrón queda coherente.
b) Documenta en un comentario del archivo la correspondencia sources ↔ lo que resuelve DataModelConfig (tu finding 5), para que no convivan dos contratos sin explicar.

PASO 3 — LOS VALORES REALES DE DEV (la clave, con evidencia):
La PR trae valores contradictorios (dev_app.delphi vs pre_app.iadarq vs restos de lab). Para resolverlo SIN adivinar: abre el repo de delphi-models — está desplegado en dev/int de verdad — y localiza sus resources/properties del entorno de dev. Extrae de ahí: catálogo, esquema, patrón de ruta de volumen y policy de dev. Contrasta contra los candidatos de la PR y dime cuál gana CON LA EVIDENCIA (archivo de delphi-models donde lo has visto). PARA AQUÍ y enséñame la tabla de valores propuestos antes de fijarlos — los confirmo yo (y se los paso a Agustín en paralelo).

PASO 4 — Tras mi ok a los valores:
environment correcto en el config de dev (nada de lab-adb), volumen y policy de dev, build local (mvn package) + suite completa. Espero todo verde — si algo rompe, para y me lo enseñas.

PASO 5 — Cierre:
PR de fix/dev-properties a develop con descripción corta ("properties de dev — basada en la #14 de Agustín, con source8 corregido, lab intacto y valores contrastados con delphi-models; la limpieza de cooking_depto se separa a su propia tarea"). Y el comentario para cerrar la #14 agradeciendo y enlazando la nueva.
