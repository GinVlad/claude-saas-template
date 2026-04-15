# Testing Rules

## Coverage Targets (MVP)
- Business logic: 80%+
- API endpoints: 100% happy path
- Frontend: Key components

## Test Types

### Unit Tests
- Location: Next to source file
- Focus: Pure functions, business logic
- Mock: External dependencies

### Integration Tests
- Focus: API endpoints, DB operations
- Use: Test database
- Clean up after each test

### E2E Tests
- Focus: Critical user flows only
- Tools: Playwright, Cypress
- Flows: Auth, payment, core feature

## Test Pattern
```
describe('Feature', () => {
  it('should do X when Y', () => {
    // Arrange
    // Act
    // Assert
  });
});
```

## What to Test
- Business logic
- Input validation
- Error handling
- Edge cases
- Authorization

## What NOT to Test
- Third-party libraries
- Simple getters/setters
- Framework internals
- Implementation details
