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
Plan de resolución del E2E sin peticiones a nadie. Hipótesis de trabajo: delphi = zona de EJECUCIÓN (el SP de los jobs opera ahí) y delphi_ho = zona de trabajo HUMANO; el choque de la semana era de identidades, no de permisos faltantes. Por fases:

FASE 0 — EVIDENCIA (solo queries de metadatos, nada de ejecutar jobs):
a) DESCRIBE SCHEMA EXTENDED pre_app.delphi y pre_app.delphi_ho → campo Owner de cada uno.
b) ¿Existe pre_app.delphi.cdp_bigdata_users_with_department (el sink del cooking del primer deploy verde)? Si existe: DESCRIBE EXTENDED → owner y fecha de creación (¿la creó el SP el día del verde?).
c) Diagnóstico del último run rojo de la pipeline: confirma que el fallo es la misma familia (identidad SP sin acceso a delphi_ho) y no algo nuevo.
PARA y enséñame la evidencia. Si los owners/creaciones confirman la hipótesis (SP opera en delphi), seguimos; si la contradicen, replanteamos ANTES de tocar config otra vez — no hacemos un tercer flip de esquema sin evidencia.

FASE 1 — REVERT DE RUNTIME A delphi (tras mi ok):
En dev-adb: las referencias que usan LOS JOBS (sink del flujo, fuentes que leen los jobs, destino de las vistas, fixtures del test de integración) vuelven a pre_app.delphi. delphi_ho queda SOLO como zona de trabajo humano (documentado así: "delphi = runtime/SP · delphi_ho = sandbox humano del área"). Rama corta sobre develop limpio — y cuidado de no arrastrar los parches intermedios que queden obsoletos con este enfoque (revisa qué quedó de fix/dev-e2e-no-browse y fix/dev-e2e-reuse-sink: lo que ya no aplique, fuera).

FASE 2 — LA SIEMBRA COMO JOB (identidad SP):
Convierte e2e_volume_seed.py en un job desplegable por la maquinaria del proyecto (plantilla tipo job_python, mismo patrón que el test de integración), parametrizado, que siembre en pre_app.delphi. Mismas reglas de siempre: 2.000 oficinas × 4 años, canarios, denominaciones que suman, partición anterior del calendario (H10). Documentado como utilidad de dev (se retira o desactiva de cara a pro).

FASE 3 — MERGE + REDEPLOY DEV:
PR, merge, Build with Parameters DEV. Esperado: install verde + lanzar el job de siembra → siembra en delphi con identidad SP.

FASE 4 — E2E:
Con la siembra SP en delphi: los runs (forecast → optimize → expert) + el sanity completo del plan original (28.000 predicciones, canarios actuando, festivos presentes, tabla final sin _u, sin duplicados, tiempos vs agosto). Yo verifico leyendo con mi SELECT sobre delphi.

En cada fase: cosecha corta y parada si algo no cuadra con la hipótesis.
