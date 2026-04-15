# Plan: [Feature Name]

## Summary
[Brief description of what we're building]

## Approach
[Selected approach from brainstorm]

---

## Tasks

### Database Tasks
| ID | Task | Files | Complexity | Status |
|----|------|-------|------------|--------|
| DB-1 | | | | [ ] |
| DB-2 | | | | [ ] |

### Backend Tasks
| ID | Task | Files | Depends On | Complexity | Status |
|----|------|-------|------------|------------|--------|
| BE-1 | | | | | [ ] |
| BE-2 | | | | | [ ] |

### Frontend Tasks
| ID | Task | Files | Depends On | Complexity | Status |
|----|------|-------|------------|------------|--------|
| FE-1 | | | | | [ ] |
| FE-2 | | | | | [ ] |

---

## Execution Order

### Phase 1 (Sequential - Foundation)
1. DB-1: [description]
2. BE-1: [description]

### Phase 2 (Parallel - Core)
- Track A (Backend): BE-2, BE-3
- Track B (Frontend): FE-1, FE-2

### Phase 3 (Sequential - Integration)
1. FE-3: Connect to API

---

## Files to Create
```
backend/
├── internal/handlers/[new].go
├── internal/services/[new].go
└── migrations/[timestamp]_[name].sql

frontend/
├── src/app/[route]/page.tsx
└── src/components/[Component].tsx
```

## Files to Modify
- `backend/internal/routes/routes.go` - Add new route
- `frontend/src/lib/api.ts` - Add API function

---

## Interfaces

### API Contract
```
POST /api/[endpoint]
Request: { }
Response: { }
```

### Component Props
```typescript
interface [Component]Props {
  
}
```

---

## Risks
| Risk | Impact | Mitigation |
|------|--------|------------|
| | | |

---

## Status
- [ ] User approved plan
- [ ] Ready for COOK stage

## Progress Log
| Timestamp | Task | Status | Notes |
|-----------|------|--------|-------|
| | | | |
