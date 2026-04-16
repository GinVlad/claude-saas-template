# Skill: Deploy to Fly.io

## Purpose
Deploy your SaaS to Fly.io with managed PostgreSQL and Redis.

## Usage
```
/deploy-fly
```

## Why Fly.io
- Edge deployment (low latency globally)
- Generous free tier
- Simple CLI
- Good for apps needing global presence
- Auto-scaling built-in

## Prerequisites
- Fly.io account (fly.io)
- Fly CLI installed: `curl -L https://fly.io/install.sh | sh`
- Project has Dockerfile

---

## Generated Files

### fly.toml
```toml
app = "your-app-name"
primary_region = "sjc"

[build]
  dockerfile = "Dockerfile"

[env]
  APP_ENV = "production"
  PORT = "8080"

[http_service]
  internal_port = 8080
  force_https = true
  auto_stop_machines = true
  auto_start_machines = true
  min_machines_running = 1

[[http_service.checks]]
  grace_period = "10s"
  interval = "30s"
  method = "GET"
  path = "/health"
  timeout = "5s"

[[vm]]
  cpu_kind = "shared"
  cpus = 1
  memory_mb = 512
```

---

## Setup Steps

### 1. Login
```bash
fly auth login
```

### 2. Launch App
```bash
fly launch
# Follow prompts, select region
# Say NO to deploying now
```

### 3. Create PostgreSQL
```bash
fly postgres create --name your-app-db
fly postgres attach your-app-db
# DATABASE_URL auto-added to secrets
```

### 4. Create Redis
```bash
fly redis create --name your-app-redis
# Note the connection string
fly secrets set REDIS_URL="redis://..."
```

### 5. Set Secrets
```bash
fly secrets set JWT_SECRET="your-secret-here"
fly secrets set OPENAI_API_KEY="sk-xxx"
fly secrets set STRIPE_SECRET_KEY="sk_live_xxx"
fly secrets set STRIPE_WEBHOOK_SECRET="whsec_xxx"
```

### 6. Deploy
```bash
fly deploy
```

### 7. Get URL
```bash
fly status
# URL: https://your-app-name.fly.dev
```

---

## Multi-Service Setup (Backend + Frontend)

### Backend (fly.toml)
```toml
app = "your-app-backend"
primary_region = "sjc"

[build]
  dockerfile = "backend/Dockerfile"

[http_service]
  internal_port = 8080
```

### Frontend (fly.toml in frontend/)
```toml
app = "your-app-frontend"
primary_region = "sjc"

[build]
  dockerfile = "Dockerfile"

[env]
  NEXT_PUBLIC_API_URL = "https://your-app-backend.fly.dev"

[http_service]
  internal_port = 3000
```

---

## Environment Variables Reference

| Variable | Source | Required |
|----------|--------|----------|
| `DATABASE_URL` | `fly postgres attach` | Auto |
| `REDIS_URL` | Manual (from redis create) | Yes |
| `JWT_SECRET` | Manual | Yes |
| `OPENAI_API_KEY` | Manual | Yes |
| `STRIPE_SECRET_KEY` | Manual | Yes |
| `STRIPE_WEBHOOK_SECRET` | Manual | Yes |

---

## Useful Commands
```bash
fly logs                  # View logs
fly logs -f               # Stream logs
fly status                # App status
fly ssh console           # SSH into machine
fly secrets list          # List secrets
fly scale count 2         # Scale to 2 instances
fly scale memory 1024     # Increase RAM
fly deploy                # Deploy latest
fly rollback              # Rollback to previous
```

---

## Scaling

### Horizontal (more instances)
```bash
fly scale count 3 --region sjc
```

### Vertical (more resources)
```bash
fly scale memory 1024
fly scale vm shared-cpu-2x
```

### Multi-region
```bash
fly regions add iad lhr
fly scale count 1 --region iad
fly scale count 1 --region lhr
```

---

## Troubleshooting

### Deploy fails
- Check `fly logs` for errors
- Verify Dockerfile builds locally
- Check health check endpoint

### Machine keeps stopping
- Set `min_machines_running = 1` in fly.toml
- Or disable auto_stop: `auto_stop_machines = false`

### Database connection issues
- Run `fly postgres attach your-app-db`
- Check `fly secrets list` for DATABASE_URL

---

## Cost Estimate (2026)
- **Free tier:** 3 shared-cpu VMs, 160GB bandwidth
- **Machines:** ~$1.94/month per shared-cpu-1x (256MB)
- **PostgreSQL:** ~$1.94/month (single node)
- **Redis:** ~$1.94/month (single node)

For MVP: $5-15/month total (often free tier covers it).
