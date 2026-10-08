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
Contexto: contrato de ingesta cerrado con el equipo de datos. Calendario (calendar_datagen): ingesta MENSUAL solo-hacia-adelante (cada partición trae ~2 meses desde su fecha de ingesta; las particiones históricas hasta 2022 las están reprocesando igual, mes a mes). Branch: diaria, data_date_part = transaction_date, un día por partición sin repetir. Rama feature/lecturas-contrato-ingesta desde develop, con DOS subtareas:

A. Calendario en training (la crítica): sustituir la lectura por última-partición por lectura por rango de particiones: data_date_part entre start_date y reference_date. Como las particiones mensuales se solapan (~1 mes repetido entre consecutivas), hay que deduplicar siendo conscientes del leakage: para cada (zip, country, calendar_date), quedarse con la fila de la partición más reciente que sea ≤ esa calendar_date (la foto que se conocía en ese momento — acordado con negocio). La INFERENCIA no se toca: sigue con la última partición.

B. Branch: añadir filtro de partición en las lecturas de training y forecasting: data_date_part en [start_date, odate] además del filtro actual de transaction_date (cinturón y tirantes, acordado con plataforma). También en get_all_branches, que hoy lee la tabla entera sin filtro.

Tests: caracterización de A con un mini-escenario de 3 particiones mensuales solapadas verificando (1) que el histórico completo se reconstruye, (2) que ante un festivo que CAMBIA entre particiones se usa la foto anterior a la fecha (anti-leakage), (3) que no hay duplicados tras el dedup. Para B, test de que las particiones fuera de rango no se leen. Suite completa verde. H5b: ni una clave de config renombrada.

Cosecha: diff por fichero, resultado de tests nuevos y suite, y lista de cualquier OTRO lector de calendario o branch que NO hayas tocado (el ad-hoc de festivos, holidays.py con su fallback MAX, security_stock.py) — listar, no cambiar.
