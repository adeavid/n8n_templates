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
Último paso de T1: el run canónico desde el artefacto oficial de la pipeline. Por fases:

FASE 1 — Localizar el artefacto oficial.
El merge a develop ya corrió en la pipeline (CloudBees). Localiza dónde publica el build el artefacto Python (¿Artifactory/Nexus? ¿con qué coordenadas y versión quedó el wheel — 1.0.1.dev0 o nomenclatura snapshot?). Dame la ruta/URL exacta de descarga. Si la pipeline no publica el wheel a repositorio y solo lo genera en el workspace del build, dime de dónde lo descargo en CloudBees.

FASE 2 — Verificación de identidad.
Antes de subir nada: compara el wheel oficial descargado con el wheel local 1.0.1.dev0 que usamos en el run validado (checksum/byte a byte, como hicimos la otra vez). Espero que sean idénticos — si difieren en algo más que metadatos de build, PARA y me lo enseñas.

FASE 3 — Despliegue y limpieza previa.
1. Comando CLI para subir el wheel oficial al volumen del lab (misma ruta que la vez anterior, perfil cash-supply-andres).
2. jobs update parcial apuntando las libraries de las 3 tareas al wheel oficial.
3. IMPORTANTE: el job hace append — antes de lanzar, propón cómo dejar la partición para que el run canónico no genere duplicados (¿borro las 700 filas del run anterior y el canónico escribe limpio? Prefiero eso: la evidencia final queda 100% del artefacto oficial). Sentencia exacta y espero mi ok antes de ejecutar.

FASE 4 — Run y sanity exprés.
Lanzo yo el run-now con los mismos parámetros. Después: 3 tareas SUCCESS, 700 filas, 50 oficinas, 14 fechas, 0 nulos, valores no triviales y distintos por modelo, 0 claves duplicadas. Y la línea final para la issue: "run canónico desde el artefacto de la pipeline (run <id>, wheel <versión oficial>): mismos resultados que el run validado — evidencia sin asteriscos".
