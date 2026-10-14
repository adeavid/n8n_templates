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
El fix curó optimize/expert (working_days=6, cero warnings) pero el dataset de forecasting sigue con flags a 0 pese a que el calendario fuente tiene las fechas. SOLO LECTURA, traza quirúrgica:

El camino del forecasting: ¿qué lector/tabla usa add_holiday_features en CREATE_FORECASTING hoy (post-fix)? ¿Es el mismo lector que arreglamos para optimize/expert o uno propio (fichero:línea)? ¿Quedó algún table_path/nombre viejo en sus inputs?
Traza UNA fecha de punta a punta: 2026-01-01 nacional — (a) ¿la fila existe en la fuente? (b) ¿el lector la devuelve? (ejecuta esa lectura suelta y cuenta filas); (c) ¿el JOIN la casa? — claves y TIPOS de ambos lados del join nacional (fecha vs fecha: ¿DATE==DATE, formatos?); (d) ¿dónde se convierte en 0? El punto exacto.
Compara con el training: ¿el dataset de training de HOY marca los festivos (conteos >0)? Si training marca y forecasting no, diff exacto entre los dos caminos de add_holiday.
Veredicto con fichero:línea. No cambies nada aún.

CIERRE PARA PRODUCCIÓN: decisión tomada, la lectura directa entra ANTES de la prueba. Commit+push por paso. El merge sigue necesitando mi OK explícito al final.

1. Rebase sobre develop ACTUAL — develop se ha movido (el fix de lectores de festivos-FQN entre otros). Resuelve conflictos conservando: tus transformaciones + los fixes de develop (resolución de nombres, except honesto, escritura idempotente). Lista los conflictos y cómo los resolviste.

2. La capa 4, verificada DENTRO de la capa nueva: en develop hay un bug abierto — el dataset de forecasting sale con flags de festivos a 0 aunque el calendario fuente los tiene (los lectores viejos; en optimize/expert ya se curó). Tu capa de lectura directa reimplementa esos caminos: verifica con test que el add_holiday del FORECASTING, pasando por tu capa, marca los festivos (fixture con Año Nuevo/Reyes → flags nacionales > 0 en el dataset de inferencia). Si tu capa arrastra el mismo fallo, arréglalo AQUÍ (en la capa nueva, un solo sitio). Este test es condición de merge.

3. Siembra v2 — dev aprende el esquema nuevo (sin esto, dev se queda sin E2E al mergear): adapta e2e_volume_seed.py para generar las tablas con el ESQUEMA DE INT:

branch_cash_servicing sintética: mismas columnas que la de int (zip_code INCLUIDO), data_date_part = transaction_date (un día por partición, días hábiles), mismos 4 años, mismas 2.000 oficinas y los MISMOS canarios de siempre (0001-0200 con sus saldos 0,40/1,60).
calendar_datagen sintética: el esquema del datagen con las columnas que consume el sistema (zip, country, calendar_date, flags de festivo, seno/coseno), particiones mensuales estilo contrato (cada una con su ventana), festivos españoles reales en el rango (Año Nuevo, Reyes incluidos).
Arqueos y security_stock: como están.
La seed sigue siendo JOB con identidad SP, como siempre.

4. Config por entorno: valores de nombres de tabla → las tablas directas (int: las de int_app.delphi que carga plataforma; dev: las nuevas de la siembra v2). Claves intactas (H5b). Las vistas y sus jobs NO se tocan ni se borran — quedan en el install sin consumidores, se jubilan después con calma.

5. Validación final: suite completa + paridad (los 25) + el test nuevo del punto 2. Cosecha: conflictos del rebase, diff de la siembra, el test de festivos-en-forecasting rojo/verde, suite, y confirmación de que las vistas quedan intactas-pero-huérfanas.
