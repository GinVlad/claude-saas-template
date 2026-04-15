# Pre-Commit Hook

## Purpose
Run checks before allowing commits to ensure code quality.

## Checks
1. Code formatting
2. Linting
3. Type checking
4. Unit tests (fast ones)
5. No secrets in code

## Implementation
```bash
#!/bin/bash
set -e

echo "Running pre-commit checks..."

# Format check
echo "Checking formatting..."
# Add your format check command

# Lint
echo "Running linter..."
# Add your lint command

# Type check (if applicable)
echo "Running type check..."
# Add your type check command

# Fast tests
echo "Running tests..."
# Add your test command

# Secret detection
echo "Checking for secrets..."
if grep -rE "(api_key|secret|password).*['\"][a-zA-Z0-9]{20,}['\"]" --include="*.js" --include="*.ts" --include="*.go" .; then
    echo "Potential secret detected!"
    exit 1
fi

echo "All checks passed!"
```

## Skip Hook
Use `git commit --no-verify` only when necessary.
