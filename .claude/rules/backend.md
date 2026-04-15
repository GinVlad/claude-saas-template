# Backend Rules

## Project Layout
Customize for your language/framework:

```
backend/
├── cmd/                    # Entry points
├── internal/               # Private packages
│   ├── config/            # Configuration
│   ├── handlers/          # HTTP handlers
│   ├── middleware/        # Auth, logging, etc.
│   ├── models/            # Domain models
│   ├── repository/        # Database operations
│   ├── services/          # Business logic
│   └── dto/               # Request/Response structs
├── pkg/                   # Shared utilities
└── migrations/            # SQL migrations
```

## Conventions
- Handlers call services, services call repositories
- No business logic in handlers
- Return proper HTTP status codes
- Structured logging (JSON in prod)

## Error Handling
```
Return errors, don't panic/throw
Wrap errors with context
Log at appropriate level
Return user-friendly messages
```

## API Response Format
```json
{
  "success": true,
  "data": {},
  "error": null
}
```

## Dependencies
Customize for your stack:
- Router: [Your choice]
- Database driver: [Your choice]
- Auth: [JWT / Session]
- Validation: [Your choice]
