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
Antes de mergear la #21, revisión con evidencia:

1. BASE: la PR está contra fix/dev-properties, que ya está en develop. Cámbiale la base a develop y confirma que el diff sigue siendo solo la carpeta nueva de int (sin arrastrar nada raro).
2. NOMBRE DE CARPETA: ¿qué nombre de carpeta de resources espera la pipeline/install cuando el targetEnvironment es INT? Evidencia: cómo mapea el Jenkinsfile/install.sh el parámetro a la carpeta, y qué nombre usa delphi-models para su entorno de int. Si lo esperado es "int-adb" y creaste "integration-adb" (o viceversa), corrígelo al que la evidencia diga.
3. MINERVA: aparece "minerva" en la PR — ¿qué es y de dónde sale? Archivo:línea. ¿Es algo del entorno int real (evidenciado en delphi-models) o un arrastre de sus plantillas que no nos aplica?
4. CORREOS: hay direcciones de correo en la PR — ¿de quién son y dónde están (¿email_notifications de los jobs?)? Si son del equipo de delphi-models, sustitúyelas por las nuestras o déjalas vacías — que sus buzones no reciban las alertas de nuestros jobs.
5. HOME_WSPACE de int: el UUID que has puesto — ¿corresponde al home de NUESTRO service principal EN INT? Que no repitamos lo de ayer (el home copiado de otra identidad).
6. FQN de branch_cash_servicing en pro: dijiste pro_business_estructurales.cdl_modelos para ambas fuentes — ¿el de branch_cash_servicing está EVIDENCIADO en algún sitio o es extrapolación del calendar_datagen? Si es extrapolación, márcalo como "a confirmar con el equipo de datos".
7. Checklist de siempre: claves sin renombrar, dev-adb y lab-adb intactos, contrato de sources completo.
Veredicto y luego decido merge.
