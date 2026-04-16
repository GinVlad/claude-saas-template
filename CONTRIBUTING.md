# Contributing to Claude SaaS Template

Thanks for your interest in contributing!

## Ways to Contribute

1. **Deployment Plugins** - Add support for new platforms
2. **Agent Improvements** - Enhance existing agents
3. **New Skills** - Add useful automation commands
4. **Rule Updates** - Improve conventions and best practices
5. **Bug Fixes** - Fix issues in existing files
6. **Documentation** - Improve README and guides

---

## Adding a Deployment Plugin

Deployment plugins live in `.claude/skills/` with the naming pattern `deploy-{platform}.md`.

### Current Plugins
- `deploy-railway.md` - Railway.app
- `deploy-fly.md` - Fly.io

### Plugin Template

Create `.claude/skills/deploy-{platform}.md`:

```markdown
# Skill: Deploy to {Platform}

## Purpose
Deploy your SaaS to {Platform} with managed PostgreSQL and Redis.

## Usage
\`\`\`
/deploy-{platform}
\`\`\`

## Why {Platform}
- [Reason 1]
- [Reason 2]
- [Reason 3]

## Prerequisites
- {Platform} account
- CLI installed: `{install command}`
- Project has Dockerfile

---

## Generated Files

### {config-file-name}
\`\`\`{format}
{example configuration}
\`\`\`

---

## Setup Steps

### 1. Login
\`\`\`bash
{login command}
\`\`\`

### 2. Initialize/Create Project
\`\`\`bash
{init commands}
\`\`\`

### 3. Add PostgreSQL
\`\`\`bash
{database setup}
\`\`\`

### 4. Add Redis
\`\`\`bash
{redis setup}
\`\`\`

### 5. Set Environment Variables
\`\`\`bash
{env var commands}
\`\`\`

### 6. Deploy
\`\`\`bash
{deploy command}
\`\`\`

---

## Environment Variables Reference

| Variable | Source | Required |
|----------|--------|----------|
| `DATABASE_URL` | {how it's set} | {Yes/Auto} |
| `REDIS_URL` | {how it's set} | {Yes/Auto} |
| `JWT_SECRET` | Manual | Yes |
| `OPENAI_API_KEY` | Manual | Yes |
| `STRIPE_SECRET_KEY` | Manual | Yes |
| `STRIPE_WEBHOOK_SECRET` | Manual | Yes |

---

## Useful Commands
\`\`\`bash
{common commands with descriptions}
\`\`\`

---

## Troubleshooting

### {Common Issue 1}
{Solution}

### {Common Issue 2}
{Solution}

---

## Cost Estimate (2026)
- {Pricing tier 1}
- {Pricing tier 2}

For MVP: {estimated monthly cost}
```

### Plugin Requirements

1. **Managed services focus** - Must support PostgreSQL + Redis (managed preferred)
2. **Docker-based** - Assume user has a Dockerfile
3. **Complete setup** - From zero to deployed
4. **Environment variables** - Document all required vars
5. **Troubleshooting** - Include common issues
6. **Cost estimate** - Help users budget

### Platforms We'd Love to See

- [ ] Render
- [ ] Vercel (frontend-focused)
- [ ] DigitalOcean App Platform
- [ ] Google Cloud Run
- [ ] AWS App Runner
- [ ] Heroku

**Note:** We intentionally exclude raw VPS guides (EC2, Droplets, Hetzner) because configuration varies too much. Focus on managed platforms with built-in PostgreSQL/Redis support.

---

## Adding a New Agent

Agents live in `.claude/agents/` and define specialized roles.

### Agent Template

```markdown
# {Name} Agent

## Role
{One-line description}

## Responsibilities
- {Responsibility 1}
- {Responsibility 2}
- {Responsibility 3}

## Context
{Background the agent needs to do its job}

## When Consulted
- {Situation 1}
- {Situation 2}

## Output Format
{How the agent should structure responses}
```

---

## Adding a New Skill

Skills live in `.claude/skills/` and define custom commands.

### Skill Template

```markdown
# Skill: {Name}

## Purpose
{What this skill does}

## Usage
\`\`\`
/{skill-name} [args]
\`\`\`

## Example
\`\`\`
/{skill-name} example-input
\`\`\`

## When Invoked
1. {Step 1}
2. {Step 2}
3. {Step 3}

## Output
{What gets generated/created}
```

---

## Adding a New Rule

Rules live in `.claude/rules/` and define conventions.

### Rule Guidelines

- Keep under 100 lines
- Focus on one topic
- Include code examples
- Be prescriptive, not descriptive

---

## Pull Request Process

1. Fork the repo
2. Create a branch: `git checkout -b add-deploy-render`
3. Make your changes
4. Test if applicable
5. Submit PR with clear description

### PR Checklist

- [ ] Follows existing file structure
- [ ] Uses consistent formatting
- [ ] Includes all required sections (for plugins)
- [ ] No sensitive data or real API keys
- [ ] Updated README if adding new skill

---

## Questions?

Open an issue or discussion on GitHub.
