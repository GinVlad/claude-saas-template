# Deployment Rules

## Strategy
- **Development:** Docker Compose (local)
- **Production:** Docker containers on cloud (Railway, Fly.io, AWS ECS, etc.)

## Docker Structure
```
project/
├── docker-compose.yml          # Local dev
├── docker-compose.prod.yml     # Production override
├── Dockerfile                  # Backend
├── Dockerfile.frontend         # Frontend (if separate)
└── .dockerignore
```

## Environment Files
```
.env.example      # Template (commit this)
.env              # Local dev (never commit)
.env.production   # Prod values (never commit)
```

## Required Services
| Service | Dev | Prod | Purpose |
|---------|-----|------|---------|
| Backend | Docker | Docker | API server |
| Frontend | Docker/Local | Docker/CDN | Web UI |
| PostgreSQL | Docker | Managed (Neon, Supabase, RDS) | Database |
| Redis | Docker | Managed (Upstash, ElastiCache) | Cache, sessions, rate limiting |

## Redis Usage (Recommended)
- **Session storage** — Faster than DB
- **Rate limiting** — Track API calls per user
- **Caching** — AI responses, templates
- **Queue** — Background jobs (optional)

## Docker Best Practices
- Multi-stage builds (smaller images)
- Non-root user in container
- Health checks defined
- `.dockerignore` to exclude unnecessary files
- Pin base image versions

## Deployment Checklist
- [ ] Environment variables set
- [ ] Database migrations run
- [ ] Redis connection verified
- [ ] HTTPS configured
- [ ] Health check endpoint working
- [ ] Logging configured
- [ ] Error tracking setup (Sentry, etc.)

## CI/CD Pipeline
```
Push to main
    → Run tests
    → Build Docker image
    → Push to registry
    → Deploy to staging
    → (manual) Deploy to production
```
