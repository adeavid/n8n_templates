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
edactar comentario de cierre para la historia de Jira del límite 175% (SOLO LECTURA, no toques código):

Estás en la rama feature/limite-175-bloqueo-caja (commits c91aadf y 3df23ea). Redacta un comentario para Jira en español, dirigido al equipo de modelos (perfil funcional/data scientist, no ingeniería de plataforma), AUTOCONTENIDO: quien lo lea no debe necesitar preguntar nada más. Usa exactamente esta estructura y estos datos, y TU trabajo es añadir las referencias exactas archivo.py:línea (verificándolas en el código, no de memoria) donde indico [REF]:

1. Qué se revisó (lo que pedía la historia). La restricción actual del algoritmo genético ya limita el SALDO PROYECTADO, no solo el importe del envío: construye el saldo futuro día a día (saldo actual + flujos previstos acumulados + impacto de envíos/retiradas propuestos) [REF: construcción del baseline] y lo capa en encaje × (1 + upper_limit_pct/100) con upper_limit_pct: 60.0 en configuración [REF: cálculo del upper_limit + REF: clave en el YAML]. Cuando detecta exceso, repara adelantando o creando una retirada (envío negativo, redondeado al lote) [REF: lógica de reparación].

2. El hallazgo: por qué se bloqueaban cajas pese a ese límite. La comprobación lleva una tolerancia implícita: si balance_tolerance no se configura, vale lot_size / 2 [REF]; con lot_size: 10000.0 (igual en los 4 entornos [REF a un YAML]), son 5.000€ fijos. El tope real era 1,60 × encaje + 5.000€. Para encajes pequeños eso es material: con encaje de 20.000€ el tope efectivo era 1,85 × encaje — POR ENCIMA del bloqueo físico del 175%. Para todo encaje inferior a ~33.333€, el optimizador podía recomendar envíos que cruzan el umbral de bloqueo sin violar ninguna restricción. Este perfil (encaje pequeño) coincide con los agentes colaboradores donde se reportaron bloqueos.

3. Lo implementado. Un techo duro adicional: saldo proyectado ≤ encaje × (1 + hard_balance_limit_pct/100) con hard_balance_limit_pct: 70.0, SIN tolerancia, aplicado a todas las oficinas, conviviendo con la regla del 160% (que no se toca) [REF: restricción nueva + REF: clave nueva en YAML]. Hereda el mismo mecanismo de reparación por retirada. Para oficinas grandes no cambia nada (el 1,60+5.000 muerde antes); para las pequeñas cierra el agujero. Validación: 174 tests en verde; caso de regresión clave: oficina con encaje 20.000 que antes podía alcanzar saldo 37.000 ahora queda capada en 34.000, por debajo del bloqueo de 35.000 [REF: test].

4. Decisión que os pedimos confirmar. El valor 170 (= 5 puntos de margen sobre el bloqueo del 175, como se comentó en la reunión del 8-oct por el decalaje y porque los flujos son estimados) es PARAMETRIZABLE: cambiarlo a otro umbral, o en el futuro acotarlo a agentes colaboradores si llega un flag de tipo de oficina, es editar un valor de configuración. Si os cuadra el 170, con un comentario aquí basta; si queréis otro, decidlo y se cambia antes del corte de la release.

5. Hallazgos fichados que NO se tocaron (decisión funcional pendiente, no bloquean): (a) la tolerancia fija de 5.000€ de la regla del 160% queda inofensiva bajo el techo nuevo, pero está mal dimensionada para encajes pequeños — si se quiere, se puede hacer proporcional al encaje; (b) el primer día del horizonte queda excluido de la comprobación [REF: la máscara/índice 0] — con inconsistencia entre el comentario del código (“hoy”) y el contrato de estado (D+1..D+H); (c) pregunta abierta: el límite se aplica sobre la columna encaje de branch_cash_servicing [REF: lectura del campo] — en el código no hay evidencia de que equivalga al saldo medio mensual que definió negocio (existe una fuente separada, pro_common_canales.oficina_operativa.hl_encaje.iencaje, que usa la ruta de alertas [REF]) — ¿podéis confirmar qué contiene exactamente esa columna?

Reglas: cada [REF] verificado abriendo el archivo (archivo:línea reales de la rama); no cambies ninguno de los números que te he dado; tono natural, sin jerga de plataforma innecesaria; longitud máxima ~1 página de Jira. Devuélveme el texto listo para pegar.
