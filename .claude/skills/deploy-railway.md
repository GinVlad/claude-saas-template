# Skill: Deploy to Railway

## Purpose
Deploy your SaaS to Railway.app with managed PostgreSQL and Redis.

## Usage
```
/deploy-railway
```

## Why Railway
- Simple setup (connect GitHub, done)
- Managed PostgreSQL + Redis plugins
- Auto-deploy on push
- Free tier for testing
- Good for MVPs and small-medium scale

## Prerequisites
- Railway account (railway.app)
- Railway CLI installed: `npm install -g @railway/cli`
- Project has Dockerfile

---

## Generated Files

### railway.json
```json
{
  "$schema": "https://railway.app/railway.schema.json",
  "build": {
    "builder": "DOCKERFILE",
    "dockerfilePath": "Dockerfile"
  },
  "deploy": {
    "healthcheckPath": "/health",
    "healthcheckTimeout": 30,
    "restartPolicyType": "ON_FAILURE",
    "restartPolicyMaxRetries": 3
  }
}
```

---

## Setup Steps

### 1. Login
```bash
railway login
```

### 2. Initialize Project
```bash
railway init
# Select "Empty Project" or link existing
```

### 3. Add PostgreSQL
```bash
railway add --plugin postgresql
```

### 4. Add Redis
```bash
railway add --plugin redis
```

### 5. Set Environment Variables
```bash
# Required
railway variables set JWT_SECRET="your-secret-here"
railway variables set OPENAI_API_KEY="sk-xxx"
railway variables set STRIPE_SECRET_KEY="sk_live_xxx"
railway variables set STRIPE_WEBHOOK_SECRET="whsec_xxx"

# Auto-injected by Railway plugins:
# DATABASE_URL, REDIS_URL
```

### 6. Deploy
```bash
railway up
```

### 7. Get URL
```bash
railway domain
# Or set custom domain in dashboard
```

---

## Multi-Service Setup (Backend + Frontend)

### Option A: Monorepo
```bash
# Deploy backend
cd backend
railway up --service backend

# Deploy frontend  
cd ../frontend
railway up --service frontend
```

### Option B: Separate Repos
- Create two Railway projects
- Or use Railway's service linking

---

## Environment Variables Reference

| Variable | Source | Required |
|----------|--------|----------|
| `DATABASE_URL` | Railway PostgreSQL plugin | Auto |
| `REDIS_URL` | Railway Redis plugin | Auto |
| `JWT_SECRET` | Manual | Yes |
| `OPENAI_API_KEY` | Manual | Yes |
| `STRIPE_SECRET_KEY` | Manual | Yes |
| `STRIPE_WEBHOOK_SECRET` | Manual | Yes |
| `APP_ENV` | Manual | Yes (production) |

---

## Useful Commands
```bash
railway logs              # View logs
railway logs --follow     # Stream logs
railway status            # Service status
railway shell             # SSH into container
railway variables         # List env vars
railway down              # Stop service
```

---

## Troubleshooting

### Build fails
- Check Dockerfile exists and builds locally
- Check `railway logs` for errors

### Health check fails
- Ensure `/health` endpoint returns 200
- Increase `healthcheckTimeout` if app is slow to start

### Database connection issues
- Verify `DATABASE_URL` is set (check `railway variables`)
- Ensure app uses SSL for PostgreSQL (`?sslmode=require`)

---

## Cost Estimate (2026)
- **Starter:** $5/month (includes $5 usage)
- **Pro:** $20/month (team features)
- **Usage:** ~$0.000231/GB-hour RAM, $0.000463/vCPU-hour

For MVP: Expect $5-20/month total.
