# AI Integration Rules

## Provider
- Start with [OpenAI / Anthropic / etc.]
- Abstract behind interface for future swap

## Interface
```
interface AIProvider {
  generate(request) → response
}

request {
  prompt: string
  maxTokens: number
  temperature: number
}
```

## Cost Control
- Set max tokens limit
- Log token usage per request
- Consider caching repeated queries
- Use cheaper models when possible

## Error Handling
- Retry on rate limit (with backoff)
- Timeout after 30 seconds
- Return user-friendly error on failure
- Don't expose raw API errors

## Security
- Sanitize user input before prompt
- Prevent prompt injection attacks
- No PII in prompts
- Log prompts for debugging (exclude sensitive data)

## Rate Limiting
- Limit requests per user per minute
- Queue requests if needed
- Show user-friendly "busy" message
