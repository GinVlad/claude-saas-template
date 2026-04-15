# Pre-Push Hook

## Purpose
Run comprehensive checks before pushing to remote.

## Checks
1. Full test suite
2. Build verification
3. Security scan

## Implementation
```bash
#!/bin/bash
set -e

echo "Running pre-push checks..."

# Full tests
echo "Running full test suite..."
# Add your test command

# Build
echo "Verifying build..."
# Add your build command

echo "All pre-push checks passed!"
```

## When to Run
- Before `git push` to any branch
- Can be skipped with `git push --no-verify` (not recommended)
