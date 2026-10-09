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
Contexto: CDO validó el CREATE definitivo de la tabla final (te lo adjunto — es el contrato oficial; la tabla ya existe en pro con ese esquema exacto). En la validación un campo quedó como totalamount (sin guion bajo) mientras nuestro código y DDL dicen total_amount. Hay que alinear NUESTRO lado al contrato, no al revés. Rama feature/contrato-cdo-tabla-final desde develop actualizado:

Diff de contrato completo: compara columna a columna (nombre, tipo, orden) nuestro DDL de resources (sanes_modelo_predictivo.sql) contra el CREATE validado adjunto. Lista TODAS las diferencias, no solo totalamount — si CDO cambió algo más en la validación, quiero verlo ahora y no en el primer insert de pro.
Alinear el DDL de resources al contrato validado, exacto.
Alinear la escritura: en el código del expert que escribe la tabla final, ajusta el mapeo de columnas de salida a los nombres validados. OJO: solo los nombres de SALIDA de esta tabla — ni claves de config (H5b), ni columnas de entrada, ni otras tablas.
Tests: actualiza cualquier test que referencie los nombres viejos de salida; si hay test de esquema de la tabla final, que valide contra el contrato nuevo.
Las tablas ya creadas en dev e int (pre_app.delphi e int_app.delphi) tienen el esquema viejo: propón el plan de migración — recomiendo DROP + CREATE con el DDL nuevo vía el mecanismo de DDL del despliegue (los datos son de prueba, 11 filas, desechables), pero dime si hay razón para ALTER RENAME en su lugar. NO lo ejecutes: plan solamente.
Suite completa verde.

Cosecha: el diff de contrato del punto 1 (tabla: columna | nuestro | CDO | acción), ficheros tocados, resultado de suite, y el plan de migración del punto 5.
