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
Tarea: convertir projection_views.sql de "SQL validado en lab" a "recurso desplegable por entorno". Hoy tiene nombres _50 cableados y placeholders ${target_catalog}/${target_schema} sin mecanismo de sustitución, y nada lo ejecuta. Por fases:

FASE 1 — EL MECANISMO (descubrir antes de decidir):
¿Cómo se ejecutan los SQL en este arquetipo durante el install? Evidencia: cómo llegan a ejecutarse notebook.sql / python_integration_testing.sql (¿convención de cloudutils? ¿plantilla de job?), qué sistema de variables usa cada cosa ({{ }} de las plantillas vs ${ } del SQL — ¿quién renderiza cada uno?), y cómo ejecuta delphi-models sus SQL de instalación si lo hace. Con eso, PROPÓN el mecanismo para las vistas (¿se suman al flujo del install? ¿tarea SQL propia en el job? ¿notebook?) y espera mi ok.

FASE 2 — PARAMETRIZACIÓN por entorno (tras mi ok):
- Las FUENTES de las vistas salen del contrato de sources de cada entorno: en lab, las espejo _50; en dev, pre_app.delphi.branch_cash_servicing y calendar_datagen; en int, los FQN de producción que ya están en las properties. Nada cableado en el SQL — todo resuelto por el mecanismo de la fase 1.
- El DESTINO (donde se crean las vistas): el catálogo/esquema privado de cada entorno.
- Lab queda funcionando igual (es la referencia de la paridad) — verifica que con los valores de lab el SQL renderizado es equivalente al actual.

FASE 3 — EL ORDEN Y LA TOLERANCIA:
Las vistas se crean SOBRE las tablas del contrato nuevo — que en dev/int pueden no existir aún (las de Marcos están pendientes). Decide y justifica: ¿el paso de vistas falla y tumba el install si faltan las bases (estricto), o se hace tolerante/condicional con aviso claro? Mi inclinación: que NO tumbe el install (el deploy de software no debe depender de tablas de datos), pero con señal visible — dime opciones.

FASE 4 — CIERRE:
Build + suite + PR en rama feature/vistas-por-entorno con descripción corta. Tras el merge toca el REDESPLIEGUE EN LOTE (rename + vistas): primero dev, verde, luego int — recuérdamelo en el resumen.
