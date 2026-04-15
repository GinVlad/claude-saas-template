# Skill: Generate API Endpoint

## Purpose
Quickly scaffold a new REST API endpoint.

## Usage
`/generate-api-endpoint [method] [path] [description]`

## Example
`/generate-api-endpoint POST /api/users Create a new user`

## Output
Creates:
1. Handler function
2. Route registration
3. Request/Response structs
4. Basic test file

## Template

### Handler
```
function handler(request, response) {
  // 1. Parse request
  // 2. Validate input
  // 3. Call service
  // 4. Return response
}
```

### Route
```
router.[method]("[path]", handler)
```

### Test
```
test("[method] [path] - success", () => {
  // Setup
  // Execute
  // Assert
})
```
