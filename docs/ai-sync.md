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
rama feature/limite-175-bloqueo-caja desde el develop actual. NO mergear.

Contexto: los agentes colaboradores tienen bloqueo operativo de caja cuando el saldo alcanza el 175% del encaje (encaje = saldo medio mensual de referencia, viene como dato). Hoy el optimizador solo limita el ENVÍO al 160% del encaje; hay que añadir una restricción sobre el SALDO RESULTANTE.

FASE A — inventario, antes de tocar nada (repórtamelo): (1) dónde se aplica hoy el límite del 160% en las restricciones del algoritmo genético — archivo:línea y fórmula exacta; (2) de dónde sale el valor del encaje y con qué nombre; (3) si en ese punto del optimizador está disponible el saldo/balance del día y los flujos previstos del forecast; (4) si existe algún campo que distinga agentes colaboradores del resto de oficinas en los inputs. No implementes hasta reportar.

FASE B — implementación, commits separados:

Nueva restricción en el GA: saldo_estimado_día_entrega + importe_envío ≤ max_balance_pct × encaje, donde el saldo estimado del día de entrega = último saldo conocido + flujos futuros estimados hasta esa fecha (reutiliza lo que el optimizador ya tenga de flujos; si no existe, repórtalo antes de inventar). La restricción del 160% sobre el envío NO se toca: conviven.
max_balance_pct como parámetro de configuración NUEVO (no renombres ninguna clave existente), default 1.70, con comentario: # margen sobre el 175% real por el decalaje de consumo — pendiente de confirmación funcional. Aplicado a TODAS las oficinas por ahora (decisión funcional abierta: acotarlo a agentes colaboradores si llega el flag).
Tests: (a) oficina cuyo saldo+envío excedería el umbral → el envío se recorta o se omite y la solución sigue siendo factible; (b) oficina holgada → envío idéntico al de antes del cambio; (c) caso frontera exacto en el umbral; (d) la restricción del 160% sigue operando.

Al final: archivos por commit, tests verdes, y la lista de SUPUESTOS FUNCIONALES que hayas tenido que tomar, marcados para validar con Pablo/Álvaro.
