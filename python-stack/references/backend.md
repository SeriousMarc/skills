# Python Backend Stack 2026

## Dependency Management
- **uv** — replaces pip, poetry, virtualenv. Use pyproject.toml. setup.py is dead.

## Framework
- **FastAPI** — default for all API work, async-first, OpenAPI auto-generated
- **Pydantic v2** — validation + settings management (pydantic-settings replaces dotenv)
- Django only for monoliths needing admin panel; not the default

## Async & Task Queue
- **asyncio** natively in FastAPI
- **Arq** — async task queue, Redis-backed, preferred for new projects
- **Celery** — still dominant in existing codebases, use if team already on it
- **Dramatiq** — cleaner alternative to Celery if starting fresh
- **Redis / Valkey** — broker in all cases (Valkey = Redis fork post-license change)

## Database
- **PostgreSQL** — default relational DB, no contest
- **SQLAlchemy 2.0** + **asyncpg** — ORM + async driver, standard
- **SQLModel** — wraps SQLAlchemy + Pydantic, good for greenfield FastAPI projects
- **Alembic** — migrations, no real alternative
- **DuckDB** — embedded OLAP, analytical queries without a separate service
- **ClickHouse** — heavier analytical pipelines with real traffic

## Caching
- **Redis** via redis-py async client
- **Valkey** for new infra setups (Redis fork)

## Auth
- **FastAPI-Users** — managed auth for FastAPI
- **PyJWT / python-jose** — roll your own JWT
- **Authlib** — OAuth / SSO flows
- Managed: Supabase Auth (simple projects) or Cognito (AWS teams)

## HTTP Client
- **httpx** — replaces requests in async contexts, standard for 2026
- aiohttp still around but httpx is cleaner

## Code Quality
- **Ruff** — replaces flake8 + isort + black entirely, 10-100x faster
- **mypy** or **pyright** — type checking
- **pre-commit** — enforce linting + type checks on commit

## Testing
- **pytest** — universal
- **pytest-asyncio** — async test support
- **Faker** — test data generation
- **Factory Boy** — fixture factories
- **httpx** test client — FastAPI endpoint testing
- **Testcontainers** — spin up real Postgres/Redis in tests, current best practice over mocking

## Containerization
- **Docker** with multi-stage builds (keep images small)
- **Docker Compose** for local dev

## CI/CD
- **GitHub Actions** — default for most teams
- **GitLab CI** — enterprise shops
- Pipeline order: lint (Ruff + mypy) → test (pytest + testcontainers) → build image → push registry → deploy
- Image registries: GHCR, ECR (AWS), Docker Hub

## Infrastructure & IaC
- **Terraform** — IaC standard, highest team transferability
- **Pulumi** — Python/TypeScript alternative to Terraform HCL, growing
- **Helm** — Kubernetes packaging
- **ArgoCD** — GitOps-style deploys on K8s

## Compute
- **ECS Fargate** — AWS shops that don't need full K8s complexity
- **Kubernetes (EKS/GKE)** — teams at scale
- **Cloud Run** — GCP, simplest "real cloud" option

## Observability
- **OpenTelemetry** — standard instrumentation layer, vendor-agnostic, traces + metrics + logs
- **Grafana stack** — Loki (logs) + Tempo (traces) + Prometheus + Grafana (metrics), self-hosted or Grafana Cloud
- **Datadog** — enterprise/fintech default, expensive but full-featured
- **Sentry** — error tracking + performance, near universal
- **structlog** or **python-json-logger** — structured JSON logging

## Security
- **Dependabot** or **Renovate** — automated dependency updates
- **Trivy** — container image scanning in CI
- **Bandit** — Python static security analysis
- **SOPS** or **HashiCorp Vault** — secrets management in production
