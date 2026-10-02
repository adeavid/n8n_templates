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
CONTEXTO (sesión nueva — resumen del estado): Proyecto cash-movements (gestión de efectivo), entorno DEV de Databricks desplegado en verde vía CloudBees. Doctrina de zonas establecida: pre_app.delphi = zona de EJECUCIÓN (los jobs corren con el service principal y operan ahí) · pre_app.delphi_ho = sandbox humano (no lo usa el proyecto). El runtime de dev está alineado a pre_app.delphi (rama fix/dev-delphi-runtime-volume-seed, ya mergeada y desplegada). Existe un job de siembra e2e_volume_seed (identidad SP) que genera el juego sintético de volumen real: 2.000 oficinas × 4 años (2022-01-01..2025-12-31), ~2,9M filas, con canarios (~10%), denominaciones que suman el balance, y calendarios CON partición anterior (lección H10: sin partición previa, los festivos salen a cero en silencio). El job de vistas PROJECTION_VIEWS_SQL falla controlado en dev (fuentes del contrato nuevo no existen aquí — se validará en INT contra zona gobernada); es esperado y no bloquea. Referencias de rendimiento (benchmark agosto, 2.000 oficinas, 1 worker): total ≈ 22 min · statsforecast ≈ 12-13 min · optimize ≈ 5-6 min con params de producción (pop60/maxiter7500/retries10).

TAREA — completar el E2E de volumen en DEV:

FASE A — SIEMBRA: lanza el job e2e_volume_seed (Run Now). Al terminar, sanity de siembra: conteos por tabla (espero ~2.922.000 en las principales), % canarios, gap denominaciones-balance (<1%), particiones del calendario (la anterior DEBE existir). PARA y enséñame.

FASE B — RUNS: propón parámetros (odate=2025-12-31, environment=dev-adb, horizonte 14, seasonality 7) y tras mi ok lanza en orden: forecasting (3 tareas) → optimize → expert. Si algo sale rojo, PARA con el error literal. Reporta duración por etapa vs las referencias de agosto (desviación >50% = señalarla y buscar causa: params reducidos del GA, cluster, particionado).

FASE C — SANITY DE SALIDAS:
1. Predicciones: 28.000 filas (2.000×14) · 0 nulos · 3 modelos con valores no triviales y DISTINTOS entre sí · festivos PRESENTES en la ventana (verificar sum de flags > 0 — que H10 no reaparezca).
2. Decisiones: 2.000 filas · canarios ACTUANDO (las fuera-de-banda con retiradas/pedidos — nada de "todo en calma") · % is_feasible y distribución de acciones.
3. Tabla final: nombre NUEVO sin _u (sanes_modelo_predictivo) · una fila por oficina · mapas de denominaciones poblados y suma del mapa = total · (is_feasible/coste_estimado aún NO están — cambio de código pendiente, no es fallo).
4. Cero claves duplicadas en las tres salidas.
COSECHA: esperado-vs-obtenido con ✓/✗ + tiempos + bloque de evidencia EN ESPAÑOL listo para Jira: "prueba de volumen real en dev completada — 2.000 oficinas × 4 años, identidades correctas (siembra y ejecución como SP en zona de runtime), tiempos en línea con baseline de agosto".

FASE D — FLECO PARA EL REDEPLOY DE INT: verifica si la plantilla del job de siembra se crearía también en int al desplegar — si es así, proponme cómo limitarla a dev (condición tipo la del auto-test del install, o plantilla solo en dev-adb). Int no debe tener job de siembra.
