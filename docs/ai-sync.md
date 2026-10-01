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
Hipótesis a probar YA: el esquema de NUESTRA app puede ser pre_app.delphi_ho, no pre_app.delphi (el grupo de jobs es gr_san_azr_apl_delphi_ho_pre y el cluster es delphi_ho). Tres pasos:

1. TEST de permisos (inofensivo): en el workspace de dev, intenta CREATE TABLE pre_app.delphi_ho.__perm_test (x INT) y si funciona, DROP inmediato. También SHOW GRANTS ON SCHEMA pre_app.delphi_ho vs pre_app.delphi si se puede.
2. EVIDENCIA DE IDENTIDAD: ¿dónde más aparece delphi_ho — en la policy, el volumen, las variables de delphi-models o del arquetipo? ¿Hay señales de que delphi_ho es la zona de NUESTRA familia de aplicaciones y "delphi" la de delphi-models? Quiero saber cuál es canónicamente el nuestro.
3. VEREDICTO: (a) si delphi_ho es escribible Y es el nuestro → actualizamos el valor de esquema en las properties de dev (PR de una línea), sembramos ahí, y NO se pide ningún grant; (b) si delphi_ho también deniega o la evidencia dice que no es el nuestro → volvemos al grant sobre delphi, ya con la información completa ("probé ambos").
