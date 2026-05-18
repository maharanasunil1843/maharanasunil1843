<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=26&pause=1000&color=4F98A3&center=true&vCenter=true&width=800&lines=Sunil+Maharana+%7C+Senior+GenAI+Engineer;Agentic+Systems+%C2%B7+RAG+%C2%B7+Full-Stack+LLM+Products;~45K+LLM+Queries%2Fmo+%C2%B7+99.5%25+Availability;Solo-Built+%C2%B7+End-to-End+%C2%B7+Production" alt="Typing SVG" />

<br/>

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/maharana-sunil)
[![Email](https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:maharanasunil1843@gmail.com)
[![Hugging Face](https://img.shields.io/badge/HuggingFace-FFD21F?style=for-the-badge&logo=huggingface&logoColor=black)](https://huggingface.co/maharanasunil1843)
[![Twitter](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/maharanasunil18)

</div>

---

## 👤 Profile

I am a **Senior Generative AI Engineer** who entered the field through operations and built a manufacturing enterprise's entire production AI capability **end-to-end** — agents, retrieval, datastores, evaluation, infrastructure, and the user-facing product — as the **sole technical owner**, while completing a CS degree alongside full-time work.

**8+ years** of professional experience, **~4 years** shipping and operating production GenAI single-handedly. I own the whole system: the agentic workflow, the polyglot data layer, the observability, the AWS pipeline, and the chat application on top.

---

## 🏭 Context

> **Sugna Metals Ltd.** — ₹600 Cr steel manufacturing enterprise, Hyderabad
> 
> Sole designer, builder and operator of the company's entire production GenAI capability — with no permanent AI team.

---

## 🚀 Flagship Projects

### Agentic Enterprise Knowledge Platform · `PRODUCTION · SOLO-BUILT`

> **~2,000 queries/day (~45K/month) · 50+ users · 99.5% rolling availability**

Natural-language interface over the enterprise's structured *and* unstructured data — across procurement, operations, and audit.

**Agentic Core:**
Every query is rewritten, decomposed, and intent-classified. A router delegates to:
- 🔍 **Hybrid-Retrieval Agent** — multimodal embeddings + rich metadata, BM25 + dense + metadata-filtered
- 🗄️ **Text-to-SQL Agent** — generates and self-corrects queries against the operational store
- ⚡ **Direct-Answer Path** — multi-hop, with reflection and answer synthesis across hops

**Data Layer:** Polyglot by design — vector store (embeddings + metadata), SQL (structured ERP/operational data), NoSQL (sessions + conversation history)

**Product:** Modern streaming chat client — auth (login/logout), persisted session history with resume + delete, per-message trace surfacing

**Observability:** Per-hop tracing on functional metrics (faithfulness, routing accuracy, SQL execution correctness) and non-functional ones (per-hop latency, token cost, cache hit, error rate), wired into CI eval gates

```
Stack: LangGraph · GPT-5.x · Claude Sonnet 4.6 / Haiku 4.5 · Multimodal Embeddings
       Pinecone · PostgreSQL · DynamoDB · Redis · FastAPI · React/Next.js
       LangSmith · RAGAS · AWS (Lambda/ECS/S3/Cognito) · GitHub Actions
```

| Metric | Value |
|---|---|
| Retrieval p50 / p95 | ~70 ms / ~140 ms |
| Answer p95 | ~3.8 s |
| RAGAS Faithfulness | **0.91** |
| RAGAS Answer-Relevancy | **0.88** |
| Intent-Routing Accuracy | **~95%** |
| Text-to-SQL Execution Accuracy | **~88%** (with self-correction retry) |
| Hallucination Rate (audited) | ~23% → **~6%** |
| Blended Cost | **≈ ₹1.4/query** (~₹70K/month at scale) |
| SOP Retrieval Time | ~12 min → **~80 s** |

---

### Agentic Procurement Negotiator · `IN ACTIVE DEVELOPMENT`

Multi-agent system that ingests vendor offers, scores them against risk and historical pricing, and drafts counter-positions and contracts behind a **human approval gate**.

**Architecture:** Supervisor pattern (`langgraph-supervisor` / `create_supervisor()`)
- An orchestrator with route/finish-only control delegates to **4 specialists**: offer analysis, pricing intelligence (text-to-SQL over historical data), risk, contract drafting
- Tool-based handoffs via `Command(goto, graph=PARENT)`
- Postgres-checkpointed shared state keyed by `thread_id`
- Recursion/handoff guard · routing-accuracy evaluator gating CI · MCP tool layer · human-in-the-loop interrupts · `.astream()` streaming

```
Stack: LangGraph + langgraph-supervisor · Claude Opus 4.7 (planning) + Haiku 4.5 (workers)
       MCP · PostgreSQL + DynamoDB · LangSmith · RAGAS + LLM-as-judge
       FastAPI · React/Next.js · AWS · GitHub Actions
```

| Metric | Value |
|---|---|
| Routing Accuracy | **~95%** |
| Tool-Call Correctness | **~92%** (labelled task set, scored in CI) |
| Cost per Negotiation Session | **≈ ₹22** (Opus for planning only, Haiku workers) |
| Target Cycle Reduction | ~30% (~9 → ~5 days) — validated in eval |

---

## 📊 Impact at a Glance

| Metric | Value |
|---|---|
| LLM Queries Served / Month | **~45K** |
| Text-to-SQL Accuracy | **~88%** |
| Intent-Routing Accuracy | **~95%** |
| Risk + Savings Impact (total) | **₹6.8 Cr** |
| Vendor Fraud Prevented (yr 1) | **₹3.2 Cr** (XGBoost, precision 0.98, ROC-AUC 0.97) |
| Inventory Savings | **₹5.6 Cr** less blocked inventory |
| PO–Invoice Matching | ~3 days → **~2 hours** |
| Manual Reporting Removed | **~30 hrs/week** |

---

## 🛠️ Technical Architecture

| Domain | Technologies |
|---|---|
| **Agentic** | LangGraph, langgraph-supervisor (supervisor/handoff), query rewriting & decomposition, intent routing, multi-hop synthesis, MCP, human-in-the-loop, Postgres checkpointing |
| **Retrieval** | Hybrid BM25 + dense + metadata-filtered, multimodal embeddings, cross-encoder & Cohere re-ranking, parent-document & semantic chunking |
| **Text-to-SQL** | NL→SQL generation with schema grounding, validation and self-correction retry loop over the operational store |
| **Models** | GPT-5.x family · Claude Opus 4.7 / Sonnet 4.6 / Haiku 4.5 · Gemini 3.x · Llama 4 / DeepSeek (routing) · text-embedding-3-large, BGE / E5 |
| **Eval & Quality** | RAGAS (faithfulness, relevancy, context precision/recall), LLM-as-judge, routing-accuracy & SQL-correctness evals, golden sets, CI eval gates |
| **Data Layer** | Pinecone / pgvector (embeddings + metadata) · PostgreSQL (structured / text-to-SQL) · DynamoDB / MongoDB (sessions, history) · Redis (cache, rate limiting) |
| **LLMOps** | Docker · MLflow · DVC · GitHub Actions · LangSmith / Langfuse · OpenTelemetry GenAI · Prometheus · Grafana |
| **Cloud / Product** | AWS (Lambda, ECS/Fargate, S3, IAM, ALB, Cognito, CloudWatch) · FastAPI (async + SSE) · React chat client with auth + session management |
| **Security** | LLM Guard, prompt-injection & PII defenses, RBAC, audit logging, secrets management |
| **Languages** | Python (primary) · SQL · Bash · JavaScript / TypeScript · C++ |

---

## 💼 Experience

**Sugna Metals Ltd.** — ₹600 Cr steel manufacturing enterprise, Hyderabad

| Role | Period |
|---|---|
| **AI Engineer — GenAI & LLMOps** *(titled: AI Architect; sole technical owner)* | Nov 2021 – Present |
| **Procurement Manager — Technology & Analytics Enablement** | Jan 2020 – Oct 2021 |
| **Analytics & Automation Executive — Procurement** | Nov 2017 – Dec 2019 |

---

## 🎓 Education & Certifications

**B.Tech, Computer Science** — Osmania University (affiliated college), Hyderabad · *2018 – 2022*

> Completed full-time while employed at Sugna Metals via a working-professional program. Final-year project: the company's first production RAG system on AWS — the seed of the platform above.

**Certifications (IBM):** Machine Learning with Python · Data Science Methodology · Python for Data Science

---

## 📈 GitHub Stats

<div align="center">

<img src="https://github-readme-stats.vercel.app/api?username=maharanasunil1843&show_icons=true&theme=tokyonight&hide_border=true&count_private=true" height="165" />
<img src="https://github-readme-streak-stats.herokuapp.com/?user=maharanasunil1843&theme=tokyonight&hide_border=true" height="165" />

</div>

---

<div align="center">

*"Ship production AI. Own the architecture. Measure everything."*

![Profile Views](https://komarev.com/ghpvc/?username=maharanasunil1843&color=4f98a3&style=flat-square)

</div>
