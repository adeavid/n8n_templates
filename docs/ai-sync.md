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
E2E DE VOLUMEN REAL EN DEV — el pack completo, por fases con parada al final de cada una. Cosecha siempre: conteos, tiempos, errores — nunca filas de datos.

FASE 1 — SIEMBRA (puede arrancar ya, en paralelo al despliegue):
Genera en pre_app.delphi el juego sintético de volumen real: 2.000 oficinas × histórico desde 2022-01-01 (~4 años). Reglas aprendidas (no negociables):
- ~10% de oficinas canario (fuera de banda en ambas direcciones) + festivos DENTRO de la ventana del horizonte.
- Denominaciones que SUMAN el balance; disponibilidad por fecha (no repetida del día 0).
- CALENDARIOS CON UNA PARTICIÓN ANTERIOR adicional (lección H10 — sin esto los festivos salen a cero en silencio).
- Nombres de tablas: los que esperan las properties de dev (contrato viejo — el proceso lee eso; las espejo del contrato nuevo NO hacen falta para esta prueba).
COSECHA 1: tabla de conteos por tabla sembrada (filas, oficinas, rango de fechas, particiones), % canarios, verificación denominaciones-balance (gap %), y confirmación de la partición anterior del calendario. PARA.

FASE 2 — PRECONDICIONES DE RUN (tras el verde del despliegue de dev):
Confirma: jobs actualizados por el install (IDs y nombres), wheel nuevo en el volumen, y el estado del job de vistas (se espera fallo controlado "faltan fuentes" — anótalo tal cual). Propón los parámetros de los runs: odate con ~4 años por detrás (p.ej. el último día del histórico), environment dev-adb, horizonte 14. PARA y me enseñas los parámetros antes de lanzar.

FASE 3 — EJECUCIÓN (tras mi ok):
Lanza en orden: forecasting (las 3 tareas) → optimize → expert. Si algo sale rojo, PARA en ese punto con el error exacto.
COSECHA 3 por etapa: estado, duración, y comparación contra mis tiempos de agosto (referencia: 2.000 oficinas ≈ 22 min total con 1 worker; statsforecast ~12-13 min; optimize ~5-6 min con params de producción). Desviación >50% en cualquier etapa = señálala.

FASE 4 — SANITY COMPLETO:
1. Predicciones: 2.000 oficinas × 14 días = 28.000 filas; 0 nulos; valores no triviales y DISTINTOS entre los 3 modelos; festivos presentes en la ventana (¡que H10 no reaparezca!).
2. Decisiones: 2.000 filas; los CANARIOS ACTÚAN (retiradas/pedidos en las fuera-de-banda — nada de "todo en calma"); % is_feasible y distribución de acciones.
3. Tabla final: escrita con el NOMBRE NUEVO (sanes_modelo_predictivo, sin _u — verifica que el rename desplegado se aplicó); una fila por oficina; mapas de denominaciones poblados y coherentes (suma del mapa = total).
4. Cero claves duplicadas en las tres salidas.
COSECHA 4: todo en formato esperado-vs-obtenido con ✓/✗, más el bloque de evidencia en español listo para la issue de Jira: "prueba de volumen real en dev — software validado con 4 años × 2.000 oficinas, tiempos en línea con el baseline de agosto".
