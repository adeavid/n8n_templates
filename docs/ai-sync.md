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
Confirmado: la base contractual es el esquema del registry/código (los 11 campos actuales) MÁS los dos nuevos. El DDL representa el contrato OBJETIVO acordado con el equipo de modelos el 24-sep, no solo lo que el código escribe hoy. Genera los dos artefactos con esto:

1. En el .sql, añade comentario en is_feasible y coste_estimado indicando que se poblarán con un cambio de código pendiente (propagación desde el optimizador) — tarea aparte, para que el DDL sea honesto sobre su estado.
2. Destino parametrizable y nota de CDO como propusiste. Mapas tal cual (coinciden con lo acordado, bien verificado).
3. En la versión legible para Jira, marca los dos campos nuevos como "acordado 24-sep, pendiente de cambio de código".

Y un TERCER entregable, solo análisis, sin tocar código: el plan del cambio mínimo para poblar los campos — (a) dónde deja main.py de eliminar is_feasible y transport_cost, (b) cómo viajan hasta el modelo experto y su escritura final, (c) el mapeo transport_cost → coste_estimado, (d) qué tests hay que ajustar o añadir (incluido el de caracterización que documenta el drop actual), y (e) tamaño estimado del diff. Lo implementaremos después en rama aparte con su propia tarea.
