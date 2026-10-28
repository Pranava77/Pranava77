<div align="center">

<h1>Pranava Holla</h1>

<p><b>Agentic AI engineer</b> &nbsp;·&nbsp; co-founder of <a href="https://webfixus.com">WEBFIXUS</a> &nbsp;·&nbsp; Bangalore, India</p>

<p><i>"An agent is only as trustworthy as its boundary: the tools it gets,<br>what needs a person's approval, and what still works when the model doesn't."</i></p>

<p>
  <a href="https://www.linkedin.com/in/pranava-holla/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
  <a href="mailto:pranavarholla@gmail.com"><img src="https://img.shields.io/badge/Email-D14836?style=flat-square&logo=gmail&logoColor=white" alt="Email"></a>
  <a href="https://webfixus.com"><img src="https://img.shields.io/badge/webfixus.com-4F46E5?style=flat-square&logo=googlechrome&logoColor=white" alt="webfixus.com"></a>
  <a href="#project-showcase"><img src="https://img.shields.io/badge/Project_showcase-10B981?style=flat-square&logo=github&logoColor=white" alt="Project showcase"></a>
</p>

</div>

<br>

<table>
<tr>
<td width="58%" valign="top">

### Who I am

I build agents that take real actions: they write records, change calendars, draft reports and run on people's own machines. Most of the work isn't the prompt. It's the boundary around the agent: which tools it gets, which calls need a person's approval, how many steps it may take, what it costs, and what still works when the model is wrong, slow, or missing.

Two of those systems are below in depth, with the rest, including the labs I built to understand what they stand on, in a table after them. I also co-founded WEBFIXUS, a small studio that ships client sites.

</td>
<td width="42%" valign="top">

### At a glance

```yaml
role:     Agentic AI engineer
based:    Bangalore, India
building: Rudra OS · SilverSync · Xotch
focus:    tool-using agents,
          human-in-the-loop approvals,
          local-first AI
models:   Claude · Gemini · Ollama ·
          OpenAI-compatible
agents:   LangChain · CrewAI · Pydantic
code:     Python · TypeScript · Swift
```

</td>
</tr>
</table>

## Project showcase

Click a project to read how it works.

### [Rudra OS](https://github.com/Pranava77/rudra-os): a local-first personal OS with a bounded agent runtime

`Python 3.12` · `FastAPI` · `SQLite + FTS5` · `Pydantic` · `MCP` · `TypeScript` · MIT

Goals, tasks, commitments, decisions, ideas, reading and memory in **one SQLite file on your own machine**, built to answer one question well: *given everything relevant about me, what matters right now, why, and what should I do next?*

<details>
<summary><b>How it works</b></summary>
<br>

```
$ rudra today

PRACTICAL
Today — 110 of 240 minutes
  Answer the vendor email
      why: scores 3.60 — a deadline is close (1.20); someone is expecting
           it (1.10); small enough to finish (0.50)
```

**The agent runtime**
- Every run is bounded in steps, runtime, tool calls and cost.
- 26 tools. Any high-risk action waits for an approval tied to its exact arguments.
- Terminal, local API, a 40-screen desktop Control Center, Telegram and an MCP bridge into your editor all go through **one request layer with 122 typed request kinds**, so no surface can act differently from another.
- The phone deliberately leaves out ten of the thirty write actions: the ones that would weaken a control, or need input a thumb can't give. `/help` says which and why.

**What it refuses to do**
- It can't send email, messages or posts. Drafts are written, checked and never sent.
- Nothing leaves the machine. The API binds to loopback only, and an invariant check names every module allowed to open a socket.
- A reminder with no stated time fails loudly instead of guessing one.
- What you capture is never rewritten. Refining an idea creates a child and keeps the parent.

**Scale:** about 39,700 lines of Python and 5,300 of TypeScript, 67 tables, 21 reversible migrations, 11 automations, checked with `ruff`, `mypy --strict` and eleven architectural invariants. Its [AS_BUILT record](https://github.com/Pranava77/rudra-os/blob/main/docs/AS_BUILT.md) lists what isn't built as plainly as what is.

</details>

---

### [SilverSync](https://github.com/Pranava77/SilverSync): a care-home operations app with a human-in-the-loop agent

`React 18` · `TypeScript` · `FastAPI` · `SQLAlchemy 2` · `Gemini` · `ChromaDB`

Staff see residents, medication, billing, staff and documents in one place, with an assistant that reads the home's own records and drafts changes for a person to confirm.

<details>
<summary><b>How it works</b> (screenshot and agent diagram inside)</summary>
<br>

<img src="https://raw.githubusercontent.com/Pranava77/SilverSync/main/docs/screenshots/dashboard.png" alt="SilverSync's dashboard: the care home drawn as two floors of coloured resident doors" width="100%">

Dementia-friendly care homes paint each resident's door its own colour, so the dashboard draws the home as corridors of those doors.

**The agent**
- A Gemini agent with **18 tools** across retrieval, residents, medical, accounting, HR, documents and reports.
- Responses stream over Server-Sent Events, showing each step, tool call and result, then the records it cited.
- **Writes are proposals.** `create_medical_record`, `record_payment` and `update_leave_status` never write. Each one stores a pending action, and only the person who asked can confirm it. Confirming runs the change through the normal domain service.
- **Role-scoped everything.** Six roles (admin, doctor, nurse, accountant, HR, receptionist). The model is only offered the tools that role may use, and search and the assistant see only what that role can see.
- Every tool call is validated with Pydantic, checked for permission and written to an audit row.

```mermaid
sequenceDiagram
    participant User
    participant Agent as AgentService
    participant LLM as Gemini
    participant Tools as ToolRegistry
    User->>Agent: question + page context
    Agent->>LLM: history + tools this role may use
    LLM-->>Agent: tool call
    Agent->>Tools: permission check + validation
    Tools-->>Agent: data, or a pending action
    Agent-->>User: streamed answer, citations, action card
    User->>Agent: confirm
```

**Around it:** semantic search over records and uploaded documents (ChromaDB), document review that suggests a category, resident and summary (and drops any resident that isn't real), and report drafts. Refill and overdue-invoice alerts are deterministic, with no AI involved. Admins can rotate the API key without a restart, and saved keys are stored encrypted. Without a key, everything except the AI still works. Tested with 49 tests against a scripted fake LLM, so no API key is needed.

</details>

---

### More projects

| Project | What it is | Stack |
|---|---|---|
| **[Xotch](https://github.com/Pranava77/Xotch)** | An AI in the MacBook notch with 20 typed tools. Looking runs at once; anything that shares or changes waits for an **Allow** click. On-device dictation. | Swift 6, SwiftUI, AppKit |
| **[Syncner](https://github.com/Pranava77/syncner-test)** | A learning platform with a Gemini career mentor and separate student, staff and admin surfaces. | React, TypeScript, Redux, Express, MongoDB |
| **[Multi-Agent Planning Studio](https://github.com/Pranava77/Multi_Agent_Planning_Orchestration_Studio)** | A supervisor turns a request into a task graph for specialist agents and an adversarial reviewer, with replanning on failure. No LLM is called, so the orchestration itself is what's on show. | Python, FastAPI, SQLite |
| **[Advanced RAG Studio](https://github.com/Pranava77/Advanced_RAG_Pipelines_Studio_Live_Project)** | Query rewriting, hybrid FAISS + BM25 retrieval, cross-encoder re-ranking and cited answers, with a trace of every stage. The answer step is templated, not an LLM. | Python, FastAPI, FAISS, BM25 |

---

## The guardrails, side by side

| | Rudra OS | SilverSync | Xotch |
|---|---|---|---|
| **Tools** | 26 | 18 | 20 |
| **What needs a person** | High-risk actions, approved with their exact arguments | Every write: it becomes a pending action | Anything that shares or changes your data |
| **Loop limit** | Steps, runtime, tool calls and cost | Final step offers no tools | 5 rounds; no tools on the last |
| **Without a model** | The deterministic half runs fully | Everything but the AI; search falls back to an offline embedder | Everything but the chat |
| **Models** | Any OpenAI-compatible | Gemini, behind provider-neutral types | Claude, OpenAI-compatible, Gemini, Ollama, LM Studio |
| **Data stays** | On your machine, loopback only | In the home's own database | On your Mac unless you chose a cloud model |

---

## Now building

<table>
<tr>
<td width="50%" valign="top">

**Xotch**
- Developer ID signing and notarisation, so installs and updates take one click
- Approving Claude Code's requests straight from the notch
- Talking to the AI by voice, joining dictation and the assistant

</td>
<td width="50%" valign="top">

**Rudra OS**, gaps its own docs list as not built yet
- Feeding the pattern engine, so finished work becomes evidence for its hypotheses
- A bundled transcriber: voice notes are captured today, but labelled as untranscribed

</td>
</tr>
</table>

---

## Under the hood

Labs I built to understand the pieces an agent stands on, rather than just calling them. Each one says plainly which parts are real computation and which are simulated.

| Lab | What's real in it |
|---|---|
| Prompt Studio | Prompt linting, few-shot and chain-of-thought comparisons, and a prompt-injection scanner |
| Tokenizer Studio | BPE and WordPiece trained step by step; WordPiece, byte-level BPE, SentencePiece and tiktoken compared on the same text |
| Embeddings · Transformer · AutoEncoder | GloVe written from scratch in NumPy beside Word2Vec and FastText, a transformer block traced op by op with tensor shapes, PyTorch autoencoders |
| QLoRA & Evaluation | NF4 / INT4 quantization, LoRA adapters on a toy network, ROUGE / BLEU / token F1 |

---

## Toolbox

<p align="center">
  <img src="https://go-skill-icons.vercel.app/api/icons?i=python,ts,swift,fastapi,react,nextjs,tailwind,sqlite,mongodb,express,pytorch,sklearn,langchain,crewai,pydantic&theme=dark&perline=15" alt="Python, TypeScript, Swift, FastAPI, React, Next.js, Tailwind, SQLite, MongoDB, Express, PyTorch, scikit-learn, LangChain, CrewAI, Pydantic">
</p>

| | |
|---|---|
| **Agents & LLMs** | Tool calling, hand-written agent loops, human-in-the-loop approvals, MCP, streaming (SSE), structured output with Pydantic · Claude, Gemini, OpenAI-compatible APIs, Ollama, LM Studio |
| **Agent frameworks** | LangChain, CrewAI, Pydantic |
| **Retrieval** | FAISS, BM25, ChromaDB, sentence-transformers, cross-encoder re-ranking, hybrid search with reciprocal rank fusion |
| **Backend** | Python, FastAPI, Pydantic v2, SQLAlchemy 2, SQLite / FTS5, Express, MongoDB, JWT |
| **Frontend & native** | TypeScript, React, Next.js, Vite, Tailwind, TanStack Query · Swift 6, SwiftUI, AppKit |
| **ML** | PyTorch, NumPy, pandas, scikit-learn, Jupyter |

---

## WEBFIXUS

I co-founded **[WEBFIXUS](https://webfixus.com)** in Bangalore in 2022. It's a small studio built on one idea: good digital work shouldn't need a 50-person agency. AI is how a small team keeps up, both inside our own workflow and in what we build for clients.

It's also where the agent work meets real clients. The habits in the showcase above (scoped tools, typed outputs, a human on anything that matters) are how we approach the AI integration work too.

**What the studio does**

| Service | What it covers |
|---|---|
| **Web design & development** | GSAP-animated, CMS-backed, performance-first sites, from marketing pages to full products |
| **AI integration & automation** | LLM pipelines, AI chat, intelligent dashboards and workflow automation, used where they actually help |
| **Branding & identity** | Logos, type systems, colour palettes, brand guidelines, motion identity |
| **Marketing & growth** | SEO, content, paid campaigns, conversion work, analytics dashboards |
| **Strategy & consulting** | Discovery, user research, information architecture, roadmapping |

**Selected client work**

| Client | What we built | Stack | Code |
|---|---|---|---|
| **Reguru** | Shopify storefront with Razorpay and Cashfree payments | Figma, Shopify, Liquid, JavaScript | [shopify-reguru](https://github.com/Pranava77/shopify-reguru) |
| **Techswamy** | Next.js site with a Payload CMS backend, smooth-scroll motion and Calendly booking | Next.js, Tailwind, Payload CMS, GSAP, Lenis | [techswamy](https://github.com/Pranava77/techswamy) |
| **Digital Mudrana** | Marketing site for a digital printing business | React, Vite, Tailwind, shadcn/ui | [repo](https://github.com/Pranava77/Digital-Mudrana) · [live](https://digital-mudrana.vercel.app) |
| **BGS High** | Animated school website | WordPress, GSAP, JavaScript | private |
| **BGS B-School** | Business school website | React, SCSS, Figma | private |
| **BGS PU** | College website with motion | React, GSAP, Figma | private |

Reusable [WordPress themes and plugins](https://github.com/Pranava77/wp-test) for client sites live in their own repo.

<details>
<summary><b>How a project runs</b></summary>
<br>

| Step | What happens |
|---|---|
| **1. Discover** | Audit, user flows, site map, personas, competitive research |
| **2. Design** | Wireframes, UI kit, prototype, visual system, interaction design |
| **3. Build** | Front end, CMS, GSAP motion, responsive pass, performance, AI features where they fit |
| **4. Launch** | Performance audit, go-live, analytics, post-launch support, iteration |

The studio's own site, [webfixus.com](https://webfixus.com), is a Next.js build on Vercel. The earlier GSAP version is public as [webfixus_final](https://github.com/Pranava77/webfixus_final).

</details>

[![Website](https://img.shields.io/badge/webfixus.com-111111?style=flat-square&logo=googlechrome&logoColor=white)](https://webfixus.com) [![LinkedIn](https://img.shields.io/badge/WEBFIXUS-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/company/webfixus) [![Instagram](https://img.shields.io/badge/@webfixus-E4405F?style=flat-square&logo=instagram&logoColor=white)](https://instagram.com/webfixus)

## Education & certifications

| Programme | Institution | Year |
|---|---|---|
| **Fellowship in Software Development, FullStack AI** | Crio.Do | 2025 |
| **Advanced Certification, Data Science and AI** | Indian Institute of Technology, Madras | 2020 – 2021 |
| **B.E., Electrical, Electronics and Communications Engineering** | Visvesvaraya Technological University | 2014 – 2018 |

## Before this

Before WEBFIXUS I worked in analytics: [credit risk](https://github.com/Pranava77/Banking-credit-risk-analytics), [customer segmentation](https://github.com/Pranava77/Customer-Segmentation-for-one-of-the-leading-credit-card-company) and [spend drivers](https://github.com/Pranava77/Credit-Card-Spend-Identifying-the-key-drivers-of-card-spend-). It's why I'd rather a pipeline be boring than clever.

---

<div align="center">

**Building agents that need to be trusted? Let's talk.**

[LinkedIn](https://www.linkedin.com/in/pranava-holla/) · [Email](mailto:pranavarholla@gmail.com) · [WEBFIXUS](https://webfixus.com) · [GitHub](https://github.com/Pranava77)

</div>
