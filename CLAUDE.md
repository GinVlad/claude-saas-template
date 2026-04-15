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

**Always check `rules/session.md` first.**

---

## Structure
```
.claude/
├── rules/              # Per-task rules (keep context small)
│   └── session.md      # Current state (check first!)
├── workflows/          # Agentic flow system
│   ├── agentic-flow.md
│   ├── coordinator.md
│   └── templates/
├── agents/             # Role definitions (7 agents)
├── plans/              # Feature plans + progress
│   └── completed/
├── skills/             # Custom commands
├── hooks/              # Git hooks
└── memory/             # Persistent context
```

## Commands
```bash
# Add your project-specific commands here
make dev      # Start development
make test     # Run tests
make lint     # Run linters
```
