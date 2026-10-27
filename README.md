# Pranava Holla

Full-stack AI engineer · Bangalore · [WEBFIXUS](https://webfixus.com) · [email](mailto:pranavarholla@gmail.com)

I build systems where the model is load-bearing, and spend most of my time on the boundaries: what the system may do, what it refuses, and how it behaves when the model is wrong, slow, or absent.

`Python` `TypeScript` `Swift` · `FastAPI` `React` `Next.js` `Express` · `SQLite` `MongoDB` · `PyTorch` `FAISS` · `GSAP` `Shopify` `WordPress`

---

## What I'm building

### Xotch — the MacBook notch, as a place to get work done

`Swift · SwiftUI · on-device speech` · private beta

A native macOS app that turns the notch (or a drawn one on any display) into a control surface for the things you do fifty times a day: calendar, to-dos, focus timer, now playing.

Two parts I care about most. An AI chat (Claude, GPT, Gemini, or a local model through Ollama or LM Studio) that can act on your day, but changes nothing until you click **Allow**, and most actions can be undone from the card. And push-to-talk dictation into any app that runs entirely on the Mac: five seconds of speech transcribed in about 30 ms, and your voice is never saved or sent.

### Rudra OS — a local-first personal operating system

`Python · FastAPI · SQLite · Pydantic` · private repo

Goals, commitments, decisions and memory in one SQLite file on your own machine, reachable from a terminal, a browser, a phone or an editor, answering one question: what matters right now, and why.

Models sit behind an OpenAI-compatible adapter, so the provider is swappable and the deterministic half runs with no model configured at all. It cannot send a message on your behalf. That wasn't hard to build; an assistant that can speak as you is a different product with a different risk, and this one declines to be it.

### [Syncner](https://github.com/Pranava77/syncner-test) — a learning platform with a Gemini-backed mentor

`React · TypeScript · Redux · Express · MongoDB`

Structured learning paths, progress tracking and generated student portfolios, across separate student, staff and admin surfaces.

The interesting half is the API: JWT auth, request validation, rate limiting, scheduled jobs. The model key resolves from admin settings before falling back to the environment, so rotating a key is a settings change rather than a redeploy.

---

## Learning the stack from the bottom

A set of interactive labs I built to understand the pieces under an LLM rather than just call it. Each one says plainly which parts are real computation and which are simulated.

| Lab | What it covers |
|---|---|
| Tokenizer Studio | BPE and WordPiece trained step by step; WordPiece, byte-level BPE, SentencePiece and tiktoken compared side by side |
| Word Embeddings | Word2Vec, GloVe (written from scratch in NumPy) and FastText trained side by side, including how each handles typos and unseen words |
| Transformer Studio | A sentence traced through a transformer block op by op, with tensor shapes, plus attention masks compared across BERT, GPT and T5 |
| AutoEncoder Studio | PyTorch autoencoders: latent space, denoising, anomaly detection |
| QLoRA & Evaluation | NF4 / INT4 quantization, LoRA adapters on a toy network, ROUGE / BLEU / token F1 |
| Advanced RAG | HyDE, multi-query rewriting, FAISS + BM25 fused with reciprocal rank fusion, cross-encoder re-ranking |
| Multi-Agent Planning | Supervisor agent, task decomposition into a DAG, replanning on failure, adversarial fact-checking |

---

## The studio

**[WEBFIXUS](https://webfixus-final.vercel.app)** is where client work ships, end to end: animated marketing sites with GSAP, React / Vite builds like [Techswamy](https://github.com/Pranava77/techswamy) and [Digital Mudrana](https://github.com/Pranava77/Digital-Mudrana), [WordPress themes and plugins](https://github.com/Pranava77/wp-test), and [Shopify storefronts](https://github.com/Pranava77/shopify-reguru).

---

Before web, I worked in analytics: [credit risk](https://github.com/Pranava77/Banking-credit-risk-analytics), [customer segmentation](https://github.com/Pranava77/Customer-Segmentation-for-one-of-the-leading-credit-card-company), [spend drivers](https://github.com/Pranava77/Credit-Card-Spend-Identifying-the-key-drivers-of-card-spend-). It's why I'd rather a pipeline be boring than clever.
