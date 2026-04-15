# Skill: Security Audit

## Purpose
Run a security audit on a file or the entire project.

## Usage
`/security-audit [file|all]`

## Example
`/security-audit src/handlers/auth.js`
`/security-audit all`

## Checks

### Authentication
- Password hashing
- Token implementation
- Session management
- Rate limiting

### Input Validation
- SQL injection vectors
- XSS vulnerabilities
- Command injection
- Path traversal

### API Security
- CORS configuration
- Authentication on protected routes
- Authorization checks
- Rate limiting

### Data Protection
- Secrets in code
- Sensitive data logging
- Encryption

## Output Format
```markdown
## Security Audit Report

### File: [filename]

#### Critical
- [Issue description]
  - Location: line X
  - Risk: [description]
  - Fix: [recommendation]

#### High
- ...

#### Medium
- ...

#### Low
- ...

### Summary
- Critical: X
- High: X
- Medium: X
- Low: X
```
