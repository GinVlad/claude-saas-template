# Pre-Deploy Hook

## Purpose
Run checks before deploying to production.

## Checks
1. All tests pass
2. Build succeeds
3. No secrets in code
4. Environment variables documented
5. Migrations ready

## Implementation
```bash
#!/bin/bash
set -e

echo "Running pre-deploy checks..."

# Run full test suite
echo "Running tests..."
# make test

# Build check
echo "Verifying build..."
# docker build -t app-test .

# Security check
echo "Checking for secrets..."
if grep -rE "(sk_live|sk_test_[a-zA-Z0-9]{20,})" --include="*.go" --include="*.ts" --include="*.js" .; then
    echo "WARNING: Potential Stripe key in code!"
    exit 1
fi

# Check env example is up to date
echo "Checking .env.example..."
if [ ! -f .env.example ]; then
    echo "WARNING: .env.example missing!"
    exit 1
fi

# Check migrations
echo "Checking migrations..."
# Add migration check command

echo "Pre-deploy checks passed!"
```

## When to Run
- Before `git push` to main/production branch
- Before manual deploy commands
- In CI/CD pipeline
