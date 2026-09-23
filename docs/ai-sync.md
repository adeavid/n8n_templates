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

La serie que llegó a los modelos era de ceros (el SeasonalNaive copia valores, no puede producir 0 si recibió la serie real). El target se pierde entre branch_360_50 y el modelo. Bisecta la cadena, en orden, y para en cuanto encuentres el punto donde el target muere:

1. TABLA DE TRAINING (salida de la tarea create-training, la df_training_..._50):
   - nombre exacto de la columna target y sus stats: nº de no-nulos, nº de valores distintos, mín/máx, % de ceros.
   - Si aquí ya es todo ceros o nulos → el problema está en create_training: sigue al paso 2.
   - Si aquí está viva → el problema está en la preparación de run_predictions: salta al paso 3.

2. SI EL TARGET MUERE EN CREATE_TRAINING:
   - ¿Qué tabla origen leyó exactamente? (resuelve el nombre desde el config del entorno lab-adb y confirma que es la _50 poblada, no otra vacía o mal apuntada).
   - Los JOIN de la construcción de la cuadrícula: compara los TIPOS y el FORMATO de las claves a ambos lados — idcent (¿string con ceros a la izquierda tipo "0001" vs int?) y fecha (¿date vs timestamp? ¿mismo formato?).
   - Dame el conteo de filas que MATCHEAN en ese join contra el total de la cuadrícula (espero encontrar 0 o casi 0 matches).

3. SI EL TARGET LLEGA VIVO AL TRAINING:
   - Repite el mismo análisis sobre la preparación de datos dentro de run_predictions (el df que se pasa a los modelos): stats del target justo antes del fit, y cualquier join/filtro intermedio con sus claves.

4. En ambos casos: ¿cuántas oficinas pasaron el filtro de observaciones mínimas (~57)? Con 3 años de histórico deberían ser 50/50 — si son 50 pese a target cero, anótalo: el filtro cuenta filas, no valores útiles.

Cosecha: solo conteos, tipos, nombres de columnas y stats — nada de filas de datos.
