# Security Rules

## Authentication
- Hash passwords (bcrypt cost 12+ or argon2)
- Short-lived access tokens (15min)
- Longer refresh tokens (7 days, httpOnly)
- Rate limit auth endpoints

## Input Validation
- Validate ALL inputs server-side
- Sanitize before database queries
- Sanitize before rendering HTML
- Limit request body size

## SQL Injection Prevention
```
// ALWAYS parameterized
db.query("SELECT * FROM users WHERE id = ?", id)

// NEVER concatenate
// db.query("SELECT * FROM users WHERE id = " + id)
```

## XSS Prevention
- Framework usually escapes by default
- Never use innerHTML/dangerouslySetInnerHTML with user data
- Sanitize any stored user content

## API Security
- HTTPS only (redirect HTTP)
- CORS: whitelist specific origins
- Rate limiting on all endpoints
- Request size limits

## Secrets
- Environment variables only
- Never commit secrets
- Different keys per environment
- Rotate keys periodically

## Headers
```
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Content-Security-Policy: default-src 'self'
Strict-Transport-Security: max-age=31536000
```
