# Skill: Test API Endpoint

## Purpose
Generate comprehensive tests for an API endpoint.

## Usage
`/test-endpoint [method] [path]`

## Example
`/test-endpoint POST /api/auth/login`

## Output
Creates test file with:
1. Happy path test
2. Validation error tests
3. Authentication tests
4. Edge case tests

## Template

```javascript
describe('[METHOD] [PATH]', () => {
  
  it('should succeed with valid input', async () => {
    // Arrange: valid request
    // Act: make request
    // Assert: 200 OK
  });

  it('should fail without authentication', async () => {
    // Arrange: no auth token
    // Act: make request
    // Assert: 401 Unauthorized
  });

  it('should fail with invalid input', async () => {
    // Arrange: invalid request
    // Act: make request
    // Assert: 400 Bad Request
  });

  describe('edge cases', () => {
    it('should handle empty input', () => {});
    it('should handle special characters', () => {});
    it('should handle large payloads', () => {});
  });
});
```
