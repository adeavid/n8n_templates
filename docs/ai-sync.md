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
Evidencia suficiente por la vía conductual (verde histórico del test contra delphi + DDL de delphi-models con el mismo SP + dobles rojos contra delphi_ho; la ausencia del sink la explica el teardown). ADELANTE con las fases 1 y 2 con dos ajustes:

1. FASE 1 (revert runtime a delphi) tal como estaba — sink, fixtures del test y fuentes de LOS JOBS a pre_app.delphi. Documentación: "delphi = zona de ejecución (SP) · delphi_ho = sandbox humano", con la evidencia conductual citada.

2. AJUSTE A LAS VISTAS EN DEV — simplificación: las fuentes del contrato nuevo (branch_cash_servicing, calendar_datagen) NO van a existir en la zona app de dev de forma natural (nadie con permisos ahí las produce). El ensayo del contrato con tablas reales se hará EN INT, donde esas tablas viven en zona gobernada y el SP las leerá con los permisos de lectura ya previstos. Así que: el job de vistas en dev queda como está (no-bloqueante, fallo controlado "faltan fuentes" documentado como esperado hasta int), y NO perseguimos crear copias del contrato nuevo en dev. Menos piezas, menos identidades, menos permisos.

3. FASE 2 (siembra como job con identidad SP, sembrando en pre_app.delphi) tal como estaba — reglas de siempre, partición anterior del calendario incluida.

4. Luego: PR única y limpia (consolidando y descartando los parches intermedios de las ramas fix/dev-e2e-* que este enfoque deja obsoletos), merge, redeploy DEV, siembra, y fases 3-4 del E2E.
