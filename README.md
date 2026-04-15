# Claude SaaS Template

A ready-to-use Claude Code project template for building SaaS applications with **agentic AI coordination**.

## Features

- **Agentic Workflow** - 5-stage coordinated development: Brainstorm → Plan → Cook → Verify → Fix
- **7 Specialized Agents** - CTO, Backend, Frontend, Database, Analytics, Tester, Security
- **Modular Rules** - Load only relevant context per task
- **Session Tracking** - Always know where you left off
- **Quality Gates** - User confirms before each stage transition

## Quick Start

### 1. Clone/Copy Template

```bash
# Clone this template
git clone https://github.com/YOUR_USERNAME/claude-saas-template.git my-saas-project

# Or copy to existing project
cp -r claude-saas-template/.claude your-project/
cp claude-saas-template/CLAUDE.md your-project/
```

### 2. Customize CLAUDE.md

Edit `CLAUDE.md` with your project details:

```markdown
# Your Project Name

Brief description.

## Quick Reference
- **Stack:** [Your tech stack]
- **Model:** [Your business model]
- **Timeline:** [Your timeline]
```

### 3. Update Session

Edit `.claude/rules/session.md`:

```markdown
## Current Phase
**Phase 0: Setup Complete**

## What's Next
- [ ] Your first task here
```

### 4. Start Building

```bash
# Open Claude Code in your project
claude

# Start agentic workflow
/agentic [your feature]
```

---

## Structure

```
your-project/
├── CLAUDE.md                    # Project overview (keep small!)
└── .claude/
    ├── agents/                  # 7 specialized agents
    │   ├── cto.md              # Architecture decisions
    │   ├── backend-dev.md      # Backend implementation
    │   ├── frontend-dev.md     # Frontend implementation
    │   ├── database.md         # Database design
    │   ├── analytics.md        # Metrics & tracking
    │   ├── tester.md           # QA & testing
    │   └── security.md         # Security review
    │
    ├── rules/                   # Per-task rules (load selectively)
    │   ├── session.md          # Current state (check first!)
    │   ├── backend.md          # Backend conventions
    │   ├── frontend.md         # Frontend conventions
    │   ├── database.md         # Database conventions
    │   ├── ai-integration.md   # AI provider rules
    │   ├── payments.md         # Payment integration
    │   ├── security.md         # Security requirements
    │   └── testing.md          # Test conventions
    │
    ├── workflows/               # Agentic system
    │   ├── agentic-flow.md     # 5-stage flow
    │   ├── coordinator.md      # Agent coordination
    │   └── templates/          # Plan templates
    │
    ├── skills/                  # Custom commands
    │   ├── agentic.md          # /agentic command
    │   └── ...
    │
    ├── plans/                   # Feature plans
    │   └── completed/          # Archive
    │
    ├── hooks/                   # Git hooks
    └── memory/                  # Persistent context
```

---

## Agentic Workflow

### The Flow

```
User Request
    ↓
[1. BRAINSTORM] → CTO + domain experts discuss approaches
    ↓ (user confirms)
[2. PLAN] → Break into tasks, identify files
    ↓ (user approves)
[3. COOK] → Implement (backend + frontend can run parallel)
    ↓ (all tasks done)
[4. VERIFY] → Tester + Security review
    ↓ (no critical issues)
[5. FIX] → Address any issues found
    ↓
DONE → Session updated
```

### Commands

| Command | Description |
|---------|-------------|
| `/agentic [feature]` | Run full workflow with gates |
| `/agentic resume` | Continue from session.md |
| `/agentic brainstorm [feature]` | Only brainstorm stage |
| `/agentic plan [feature]` | Only plan stage |
| `/agentic cook [feature]` | Only implementation |
| `/agentic verify [feature]` | Only verification |

### Example

```bash
> /agentic add user authentication

[BRAINSTORM]
CTO: "Auth needs: API endpoint, DB migration, frontend form.
Approach A: Email/password (simple)
Approach B: OAuth only (complex)
Recommend: A for MVP"

> Go with A

[PLAN]
Tasks created:
- DB-1: Create users table
- BE-1: POST /api/auth/register
- BE-2: POST /api/auth/login  
- FE-1: Registration form
- FE-2: Login form

> Start

[COOK]
✓ DB-1 done
✓ BE-1 done
✓ BE-2 done
✓ FE-1 done
✓ FE-2 done

[VERIFY]
Tester: All tests pass
Security: No issues found

[DONE]
Session updated. Auth feature complete.
```

---

## Rules System

### Why Modular Rules?

Loading 500+ lines of context every task wastes tokens and reduces focus. Instead:

1. **Check `session.md` first** - See current state
2. **Load only relevant rules** - Backend task? Load `backend.md` only
3. **Keep context focused** - Better reasoning, faster responses

### Rule Files

| File | When to Load |
|------|--------------|
| `session.md` | Always (check first) |
| `backend.md` | Backend/API work |
| `frontend.md` | UI/React work |
| `database.md` | Migrations, queries |
| `ai-integration.md` | AI/LLM integration |
| `payments.md` | Stripe/payments |
| `security.md` | Auth, validation |
| `testing.md` | Writing tests |

---

## Agents

### Agent Roles

| Agent | Role | Used In |
|-------|------|---------|
| **CTO** | Architecture, tech decisions | Brainstorm, Plan |
| **Backend-dev** | API, services, DB operations | Plan, Cook |
| **Frontend-dev** | UI, components, state | Plan, Cook |
| **Database** | Schema, migrations, queries | Plan, Cook |
| **Analytics** | Metrics, tracking | Plan |
| **Tester** | Tests, QA | Verify |
| **Security** | Security review | Brainstorm, Verify |

### How Agents Coordinate

```
BRAINSTORM:
  Lead: CTO
  Consults: Security, Backend, Frontend

PLAN:
  Lead: CTO  
  Consults: Backend, Frontend, Database

COOK:
  Track A Lead: Backend-dev
  Track B Lead: Frontend-dev
  (parallel when possible)

VERIFY:
  Lead: Tester
  Consults: Security
```

---

## Customization

### Adding a New Agent

Create `.claude/agents/[agent-name].md`:

```markdown
# [Agent Name] Agent

## Role
[What this agent does]

## Responsibilities
- [Responsibility 1]
- [Responsibility 2]

## Context
[Background the agent needs]

## Output Format
[How the agent should respond]
```

### Adding a New Rule

Create `.claude/rules/[rule-name].md`:

```markdown
# [Topic] Rules

## [Section 1]
- Rule 1
- Rule 2

## [Section 2]
- Rule 3
```

Keep under 100 lines. Split if larger.

### Adding a New Skill

Create `.claude/skills/[skill-name].md`:

```markdown
# Skill: [Name]

## Purpose
[What this skill does]

## Usage
`/[skill-name] [args]`

## When Invoked
[Step-by-step what happens]
```

---

## Included Skills

| Skill | Description |
|-------|-------------|
| `/agentic` | Run agentic workflow |
| `/generate-api-endpoint` | Scaffold Go API endpoint |
| `/generate-component` | Scaffold React component |
| `/generate-migration` | Create DB migration |
| `/add-template` | Add new template (for template-based SaaS) |
| `/security-audit` | Run security review |
| `/test-endpoint` | Generate API tests |

---

## Example: Starting a New SaaS

### 1. Copy Template

```bash
cp -r claude-saas-template my-awesome-saas
cd my-awesome-saas
```

### 2. Update CLAUDE.md

```markdown
# My Awesome SaaS

AI-powered [your thing] for [your audience].

## Quick Reference
- **Stack:** Go + Next.js + PostgreSQL + Stripe
- **Model:** Freemium ($0 / $19 / $49)
- **MVP:** 2 weeks
```

### 3. Update Rules for Your Stack

Edit `.claude/rules/backend.md` if using different framework.
Edit `.claude/rules/frontend.md` if using Vue/Svelte/etc.

### 4. Start Building

```bash
claude

> /agentic add user registration
> /agentic add billing with stripe  
> /agentic add core feature X
```

---

## Best Practices

### Do

- Check `session.md` at start of every session
- Use `/agentic` for features (not quick fixes)
- Update session.md when done
- Keep rule files under 100 lines
- Let agents coordinate through workflow

### Don't

- Load all rules at once
- Skip workflow gates
- Forget to update session state
- Create massive CLAUDE.md files

---

## Contributing

1. Fork this repo
2. Add your improvements
3. Submit PR

Ideas welcome:
- New agent types
- Additional skills
- Framework-specific rules (Vue, Django, Rails, etc.)
- Workflow improvements

---

## License

MIT - Use freely, attribution appreciated.

---

## Credits

Inspired by:
- Claude Code best practices
- Real SaaS development workflows
