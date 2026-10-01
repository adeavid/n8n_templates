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
Alto — antes de pedir BROWSE a plataforma, tres verificaciones:

1. EL ORIGEN DEL USE: ¿qué notebook/línea exacta ejecuta `USE pre_app.delphi_ho`? ¿Está en código NUESTRO de esta semana (el notebook de vistas convertido, el de integration testing tocado por la coherencia)? Dame el diff: ¿ese USE existía en el despliegue anterior de dev — el que dio VERDE con el test de integración incluido y SIN permiso BROWSE? Si el USE es nuevo nuestro, el permiso "faltante" lo hemos fabricado nosotros hoy.

2. EL PERÍMETRO REAL: lista TODOS los sitios del repo que ejecutan USE (catalog/schema). ¿Son 1-2 notebooks nuestros o de verdad "notebooks, tests y aplicaciones"? Con números, no con adjetivos.

3. EL FIX SIN PERMISOS: en los notebooks nuestros, sustituye el USE por NOMBRES TOTALMENTE CUALIFICADOS (catalog.schema.tabla vía los widgets que ya tienen) — es el estilo más robusto de todas formas (un notebook que depende de USE es frágil ante el contexto). Si el perímetro del punto 2 confirma que es nuestro y pequeño: aplica el cambio en la rama, mvn validate, y me dices para mergear y relanzar SIN pedir nada a nadie.

Si el punto 1 demostrara que el USE ya estaba y antes funcionaba — entonces algo más cambió (¿identidad del cluster? ¿warehouse vs job?) y quiero ESE diagnóstico antes de aceptar que el permiso es la causa.
