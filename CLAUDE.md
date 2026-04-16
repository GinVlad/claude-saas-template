# [Project Name]

[Brief description of your SaaS]

## Quick Reference
- **Stack:** [e.g., Go + Next.js + PostgreSQL + Stripe]
- **Model:** [e.g., Freemium ($0 / $19 / $49)]
- **MVP:** [e.g., 2 weeks]

---

## Agentic Workflow

Use `/agentic [feature]` to start coordinated implementation:

```
BRAINSTORM → PLAN → COOK → VERIFY → FIX → DONE
```

| Command | Action |
|---------|--------|
| `/agentic [feature]` | Full flow with gates |
| `/agentic resume` | Continue from session.md |
| `/agentic brainstorm [feature]` | Single stage |

**Agents coordinate automatically.** Session state tracked in `rules/session.md`.

---

## Rules System

Load only what's needed per task:

| Task | Rules to Load |
|------|---------------|
| Backend | `rules/backend.md` |
| Frontend | `rules/frontend.md` |
| Database | `rules/database.md` |
| AI | `rules/ai-integration.md` |
| Payments | `rules/payments.md` |
| Security | `rules/security.md` |
| Testing | `rules/testing.md` |
| Deployment | `rules/deployment.md` |
| Redis/Cache | `rules/redis.md` |

**Always check `rules/session.md` first.**

---

## Structure
```
.claude/
├── rules/              # Per-task rules (keep context small)
│   └── session.md      # Current state (check first!)
├── workflows/          # Agentic flow system
├── agents/             # 8 agents (CTO, Backend, Frontend, DB, Analytics, Tester, Security, DevOps)
├── plans/              # Feature plans + progress
├── skills/             # Commands (/agentic, /docker-setup, /deploy, etc.)
├── hooks/              # Git + deploy hooks
└── memory/             # Persistent context
```

## Commands
```bash
# Development
docker compose up -d              # Start all services
docker compose logs -f            # View logs
docker compose down               # Stop all

# Or without Docker
make dev                          # Start development
make test                         # Run tests
make lint                         # Run linters

# Deployment
/docker-setup full                # Generate Docker configs
/deploy-railway                   # Deploy to Railway
/deploy-fly                       # Deploy to Fly.io
```
