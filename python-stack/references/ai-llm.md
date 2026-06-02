# AI / LLM / Agentic Stack 2026

## LLM Providers
- **Anthropic Claude** — default for quality-critical work
- **OpenAI GPT-4o / o-series** — second default, widest ecosystem
- **Google Gemini 1.5/2.0** — long context use cases
- **Meta Llama 3.x** — self-hosted / open weight needs

## Provider Gateway
- **LiteLLM proxy** — self-hosted gateway, provider-agnostic, rate limiting,
  cost tracking, fallbacks, load balancing. Put this in front of all LLM calls
  in production instead of calling providers directly from app code.

## LLM Client SDKs
- **Anthropic Python SDK** — primary
- **OpenAI Python SDK** — primary + works against any OpenAI-compatible endpoint
  (Llama, Mistral, local models via base_url override)
- **instructor** — structured/typed LLM outputs via Pydantic models, essentially
  standard for any production use case needing typed output from an LLM

## Agent Frameworks
Pick based on use case — do not default to LangChain for new projects:

- **Pydantic AI** — best for greenfield, type-safe, async-first, native Pydantic v2,
  cleanest DX for Python engineers. Preferred default for new projects.
- **LangGraph** — stateful multi-step agents, cyclical workflows, complex control flow.
  Use when agent needs to loop, branch, or maintain state across steps.
- **LlamaIndex** — RAG-heavy pipelines, document ingestion and retrieval. Better default
  than LangChain when core use case is indexing and querying documents.
- **CrewAI** — multi-agent role-based orchestration, simple mental model (agents + tasks
  + crew), good for getting multi-agent systems working fast.
- **AutoGen (Microsoft)** — multi-agent conversation, strong in research/enterprise.
- **LangChain** — do NOT use for new projects. Legacy, over-abstracted. Know it because
  job descriptions mention it; do not build with it.

## MCP (Model Context Protocol)
- MCP is the standard protocol for connecting LLMs to external tools and data sources.
- **FastMCP** — Python library for building MCP servers. Use when exposing your APIs
  as LLM-callable tools.
- Tool calling via provider SDKs directly for simple single-tool cases;
  MCP for anything reusable or composable across agents.

## RAG Stack

### Embeddings
- **voyage-3** — Anthropic-recommended, hosted
- **text-embedding-3-small** — OpenAI, hosted
- **sentence-transformers** — local/self-hosted

### Vector Databases
- **pgvector** — Postgres extension, default if already on Postgres (avoids extra service)
- **Qdrant** — best standalone vector DB for production, Rust-based, fast
- **Weaviate** — more feature-rich, larger teams
- **Pinecone** — managed, easy but expensive
- **ChromaDB** — local dev and prototyping only, not production

### Reranking
- **Cohere Rerank** — hosted reranker
- **cross-encoder models** via sentence-transformers — self-hosted
- Often the single biggest quality improvement in a RAG pipeline after initial retrieval

### Document Ingestion
- **LlamaIndex** document loaders — general purpose
- **Unstructured.io** — PDFs, Word docs, mixed formats into clean text

## Prompt Management
- **Langfuse** — open source, self-hostable, prompt versioning + tracing + evals.
  Default choice for teams avoiding vendor lock-in.
- **LangSmith** — LangChain's platform, use if already in LangChain ecosystem.
- **PromptLayer** — lighter option.

## Evals
Treat prompt changes like code changes. Run evals in CI on every PR touching prompts or agent logic.

- **pytest + custom eval harness** — LLM-as-judge pattern (use Claude/GPT-4 to score outputs)
- **RAGAS** — RAG-specific eval framework (retrieval quality, faithfulness, answer relevance)
- **DeepEval** — broader LLM eval framework, integrates with pytest, good for CI pipelines
- **Braintrust** — hosted eval platform, growing in 2025-2026

## LLM Observability
- **Langfuse** — traces every LLM call, token usage, latency, cost per request.
  Self-hostable. Essentially mandatory for production LLM apps.
- **Helicone** — similar to Langfuse, proxy-based (zero code changes needed)
- **Arize Phoenix** — open source, strong for embedding drift and RAG pipeline debugging
- Token cost tracking: build dashboards on Langfuse data or Datadog custom metrics

## Local Model Serving (dev)
- **Ollama** — run Llama, Mistral, Qwen locally. Standard for local dev to avoid
  burning API credits during development.

## Production Self-Hosted Model Serving
- **vLLM** — PagedAttention, high throughput, production standard for open weight models at scale
- **llama.cpp** — lower level, CPU-capable, when GPU unavailable

## Voice / Multimodal
- **Whisper** (OpenAI) — speech to text, via openai-whisper or API
- **ElevenLabs** or **Cartesia** — TTS
- **LiveKit** — real-time voice agent infrastructure, current standard for voice AI apps

## Data Processing (AI pipelines)
- **Polars** — preferred over Pandas for performance-sensitive data work in pipelines
- **Pandas** — still used, fine for smaller datasets
- **aiokafka** — Kafka async client for event streaming in larger systems
