# Pranava Holla

Agentic AI engineer · Bangalore · [WEBFIXUS](https://webfixus.com) · [email](mailto:pranavarholla@gmail.com)

I build agents that take real actions, and most of the work is the boundary around them: which tools they get, what needs a person's approval, how far they may run, and what still works when the model is wrong, slow, or absent.

`Python` `TypeScript` `Swift` · `FastAPI` `Pydantic` `React` · tool calling · MCP · RAG (`FAISS` `BM25` `ChromaDB`) · Claude · Gemini · OpenAI-compatible · Ollama

---

## Agents I've built

### [Rudra OS](https://github.com/Pranava77/rudra-os): a local-first personal OS with a bounded agent runtime

`Python · FastAPI · SQLite · Pydantic · MCP`

Goals, commitments, decisions and memory in one SQLite file on your own machine, answering one question: what matters right now, and why.

- **Bounded runtime.** Every run has limits on steps, runtime, tool calls and cost. A high-risk action needs an approval bound to its exact arguments, and you can answer it from any surface, including a phone.
- **One request layer, five surfaces.** Terminal, local API, desktop app, Telegram and an MCP bridge into your editor all go through the same 122 typed request kinds, so no surface can act differently.
- **Deterministic first.** Briefings, priorities and reminders need no model call at all. Models sit behind an OpenAI-compatible adapter, so the provider can be swapped, or left out.
- **Removed on purpose.** It cannot send a message on your behalf. It also had a `run_code` tool behind an approval, and I deleted it instead of improving it: the agent doesn't run code it wrote.

### [SilverSync](https://github.com/Pranava77/dua-care-connect): an operations app for a care home, with a tool-using assistant

`React · TypeScript · FastAPI · SQLAlchemy · Gemini · ChromaDB`

Staff see residents, medication, billing, staff and documents in one place. The assistant is a Gemini agent with 18 tools. It streams each step it takes and cites the records it used.

- **Writes are proposals.** New medical records, payments and leave decisions show up as action cards, and nothing changes until the person who asked confirms.
- **Permissions carry through.** Six roles, and each one sees only its own areas, in the app, in search and through the assistant.
- **Works without a key.** With no Gemini key everything except the AI still runs, and semantic search falls back to an offline embedder.

### [Xotch](https://github.com/Pranava77/Xotch): an AI in the MacBook notch that acts only after you click Allow

`Swift · SwiftUI · on-device speech` · private beta

A native macOS app that turns the notch into a control surface for your day. The chat works with Claude, GPT, Gemini or a local model through Ollama or LM Studio, and it can read your calendar, to-dos and timer. It adds an event, starts a focus session or writes a note only after you click **Allow**, and most of those actions can be undone. Push-to-talk dictation runs entirely on the Mac: five seconds of speech in about 30 ms, never saved or sent.

### [Syncner](https://github.com/Pranava77/syncner-test): a learning platform with a Gemini career mentor

`React · TypeScript · Express · MongoDB`

Learning paths, progress tracking and generated portfolios for students, staff and admins. The API handles JWT auth, validation, rate limiting and scheduled jobs. The model key is read from admin settings before the environment, so rotating it is a settings change, not a redeploy.

---

## Under the hood

Labs I built to understand what an agent stands on. Each one says which parts are real and which are simulated.

| Lab | What's real in it |
|---|---|
| [Multi-Agent Planning](https://github.com/Pranava77/Multi_Agent_Planning_Orchestration_Studio) | Supervisor and specialist roles, task decomposition into a DAG, replanning when a step fails, an adversarial fact-checker. It runs without a model, so the orchestration itself is what you see. |
| [Advanced RAG](https://github.com/Pranava77/Advanced_RAG_Pipelines_Studio_Live_Project) | Retrieval: HyDE and multi-query rewriting, FAISS + BM25 fused with reciprocal rank fusion, cross-encoder re-ranking, and grounded answers that cite their sources |
| Prompt Studio | Prompt linting, few-shot and chain-of-thought comparisons, and a prompt-injection scanner |
| Tokenizer · Embeddings · Transformer | BPE and WordPiece trained step by step, GloVe written from scratch in NumPy, a transformer block traced op by op |
| QLoRA & Evaluation | NF4 quantization, LoRA adapters on a toy network, ROUGE / BLEU / token F1 |

---

I also run **[WEBFIXUS](https://webfixus-final.vercel.app)**, a small studio shipping client sites ([Techswamy](https://github.com/Pranava77/techswamy), [Digital Mudrana](https://github.com/Pranava77/Digital-Mudrana), Shopify and WordPress builds). Before that I worked in analytics ([credit risk](https://github.com/Pranava77/Banking-credit-risk-analytics), [segmentation](https://github.com/Pranava77/Customer-Segmentation-for-one-of-the-leading-credit-card-company)), which is why I'd rather a pipeline be boring than clever.
