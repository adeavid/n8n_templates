# Advanced n8n Chatbot Templates (2025-10-29)

## Shortlist

### Build a Smart Chatbot with GPT-5-nano, Web Search & Conversational Memory
- Link: https://n8n.io/workflows/8209-build-a-smart-chatbot-with-gpt-5-nano-web-search-and-conversational-memory
- Why it stands out: Combines chat trigger, AI Agent, conversational memory, live web search, and custom-styled chat UI to deliver grounded answers with running context.
- Key building blocks to reuse: AI Agent node orchestrating GPT-5-nano with memory, web-search tool handoff, ready-to-embed frontend theme.

### Create a Knowledge Base Chatbot with Google Drive & GPT-4o using Vector Search
- Link: https://n8n.io/workflows/6250-create-a-knowledge-base-chatbot-with-google-drive-and-gpt-4o-using-vector-search/
- Why it stands out: Full RAG pipeline—watches Drive for file updates, chunks documents, builds embeddings, serves contextual responses over webhook chat.
- Key building blocks to reuse: Automated ingestion loop, vector store management, context-grounded response pattern ideal for support bots.

### Company Knowledge Base Agent (RAG)
- Link: https://n8n.io/workflows/6538-company-knowledge-base-agent-rag/
- Why it stands out: Multi-modal (voice + text) assistant that leverages Supabase vector search, Google Drive sync, and Telegram interface for distribution.
- Key building blocks to reuse: Voice transcription with Whisper, Supabase embeddings sync workflows, modular chat deployment (Telegram/web widget).

### AI Agent Chat (n8n Team)
- Link: https://n8n.io/workflows/1954-ai-agent-chat/
- Why it stands out: Production-ready chat agent with OpenAI, SerpAPI tool calling, and short-term memory to keep conversations coherent.
- Key building blocks to reuse: Tool-calling pattern, memory buffer configuration, manual chat trigger routing great for demos or live chat.

### Scalable Multi-Agent Chat Using @mentions
- Link: https://n8n.io/workflows/3473-scalable-multi-agent-chat-using-mentions/
- Why it stands out: Orchestrates multiple specialized AI agents in one conversation, routing prompts via @mentions and letting agents run on different OpenRouter models.
- Key building blocks to reuse: JSON-configurable agent registry, mention parser, fan-out/fan-in message handling for collaborative AI teams.

## Next actions
- Pull JSON exports (if available) for top 2 workflows to inspect node wiring.
- Compare knowledge-base workflows for shared primitives we can standardize across lanes.
- Coordinate with other agents so TikTok/LinkedIn/Email research uses similar `research/<lane>.md` structure.
