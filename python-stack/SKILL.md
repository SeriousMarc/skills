---
name: python-stack
description: >
  Reference skill for the current (2026) Python backend and AI/LLM/Agentic technology stack.
  Use this skill whenever starting a new project, planning architecture, choosing libraries,
  scaffolding a repo, writing a README, setting up CI/CD, or making any technology selection
  decision for a Python application. Also triggers when the user asks what to use for any
  layer of the stack (framework, ORM, testing, observability, LLM orchestration, RAG, evals,
  vector DB, agent framework, etc). In plan mode or at project start, always consult this
  skill first before suggesting any technology. Applies to both pure backend projects and
  AI/LLM/agentic projects.
disable-model-invocation: true
---

# Python Stack 2026

This skill defines the canonical technology choices for Python projects in 2026.
Consult it at project start, during architecture planning, and whenever a technology
selection needs to be made. Two reference files cover the full stack:

- `references/backend.md` — core Python backend stack (framework, DB, testing, CI/CD, observability)
- `references/ai-llm.md` — AI/LLM/agentic stack (providers, orchestration, RAG, evals, observability)

## When to read which file

- Pure backend API / service → read `references/backend.md`
- AI / LLM / agentic app → read both files; backend.md for infra layer, ai-llm.md for AI layer
- Full stack project → read both

## Key principles

- Prefer the listed technology unless the user has an explicit reason to deviate
- When suggesting alternatives, note which listed tool it replaces and why the deviation is justified
- Do not suggest deprecated or legacy tools (Flask as primary framework, pip/poetry over uv,
  black/flake8/isort over Ruff, requests over httpx in async contexts)
- Always default to async-first patterns (FastAPI, asyncpg, asyncio, httpx, arq)
- uv is the package manager — do not suggest pip install or poetry unless asked
