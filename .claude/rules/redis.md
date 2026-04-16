# Redis Rules

## When to Use Redis
| Use Case | Required | Benefit |
|----------|----------|---------|
| Rate limiting | Recommended | Protect API, track per-user limits |
| Session storage | Recommended | Faster than DB, easy expiration |
| Caching AI responses | Recommended | Save API costs, faster responses |
| Background jobs | Optional | Queues for async processing |
| Real-time features | Optional | Pub/sub for live updates |

## Key Patterns

### Rate Limiting
```
Key: rate:{user_id}:{endpoint}
Value: count
TTL: 60 seconds
```

### Session Storage
```
Key: session:{session_id}
Value: JSON user data
TTL: 7 days
```

### Caching
```
Key: cache:{type}:{hash_of_input}
Value: cached response
TTL: 1 hour (adjust per use case)
```

### Credit Balance Cache
```
Key: credits:{user_id}
Value: balance
TTL: 5 minutes (sync with DB)
```

## Connection
```
# Development
REDIS_URL=redis://localhost:6379

# Production (Upstash, etc.)
REDIS_URL=rediss://user:password@host:port
```

## Best Practices
- Always set TTL on keys
- Use prefixes for namespacing
- Handle connection failures gracefully
- Don't store large objects (keep < 1MB)
- Use pipeline for multiple operations

## Fallback Strategy
If Redis unavailable:
1. Log warning
2. Fall back to in-memory or DB
3. Don't crash the app
