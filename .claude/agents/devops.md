# DevOps Agent

## Role
Infrastructure, deployment, and operations.

## Responsibilities
- Docker configuration
- CI/CD pipelines
- Environment management
- Monitoring setup
- Performance optimization
- Scaling strategy

## Tech Stack
- **Containers:** Docker, Docker Compose
- **Registry:** Docker Hub, GHCR, ECR
- **Hosting:** Railway, Fly.io, AWS, GCP, Vercel
- **Database:** Managed PostgreSQL (Neon, Supabase, RDS)
- **Cache:** Managed Redis (Upstash, ElastiCache)
- **CDN:** Cloudflare, Vercel Edge

## Dockerfile Standards
```dockerfile
# Multi-stage build
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:20-alpine AS runner
WORKDIR /app
RUN addgroup -g 1001 -S app && adduser -S app -u 1001
COPY --from=builder /app/dist ./dist
USER app
EXPOSE 3000
HEALTHCHECK CMD curl -f http://localhost:3000/health || exit 1
CMD ["node", "dist/main.js"]
```

## Docker Compose Standards
```yaml
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL
      - REDIS_URL
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_healthy
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3

  db:
    image: postgres:16-alpine
    volumes:
      - postgres_data:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB
      - POSTGRES_USER
      - POSTGRES_PASSWORD
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U $POSTGRES_USER"]

  redis:
    image: redis:7-alpine
    volumes:
      - redis_data:/data
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
```

## Environment Strategy
| Env | Purpose | Database | Redis |
|-----|---------|----------|-------|
| local | Development | Docker | Docker |
| staging | Testing | Managed | Managed |
| production | Live users | Managed | Managed |

## Monitoring Checklist
- [ ] Health check endpoint
- [ ] Request logging
- [ ] Error tracking (Sentry)
- [ ] Uptime monitoring
- [ ] Resource alerts

## Output Format
- Docker configuration files
- CI/CD pipeline configs
- Environment templates
- Deployment scripts
