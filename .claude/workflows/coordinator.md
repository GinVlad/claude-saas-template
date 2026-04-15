# Workflow Coordinator

## Role
Orchestrate agents through the agentic workflow stages.

## Stage → Agent Mapping

| Stage | Lead Agent | Consulting Agents |
|-------|------------|-------------------|
| BRAINSTORM | CTO | Backend, Frontend, Security |
| PLAN | CTO | Backend, Frontend, Database |
| COOK (Backend) | Backend-dev | Database |
| COOK (Frontend) | Frontend-dev | - |
| VERIFY | Tester | Security |
| FIX | Original implementer | - |

---

## Coordination Protocol

### Starting a Feature
```
1. User: /agentic [feature]
2. Coordinator:
   a. Read session.md
   b. Check for in-progress work
   c. Create plans/[feature]-brainstorm.md
   d. Update session.md with active workflow
   e. Hand off to BRAINSTORM stage
```

### Stage Transitions
```
BRAINSTORM → PLAN
  Trigger: User confirms approach
  Action: Create plans/[feature]-plan.md

PLAN → COOK
  Trigger: User approves plan
  Action: Begin implementation

COOK → VERIFY
  Trigger: All tasks marked done
  Action: Create plans/[feature]-verify.md

VERIFY → FIX
  Trigger: Critical/High issues found
  Action: List issues to fix

VERIFY → DONE
  Trigger: No critical/high issues
  Action: Update session, move files

FIX → VERIFY
  Trigger: Fixes complete
  Action: Re-run verification
```

### Parallel Execution
```
When COOK has independent tracks:

[Backend Track]          [Frontend Track]
    BE-1                      FE-1
     ↓                         ↓
    BE-2                      FE-2
     ↓                         ↓
    BE-3                      FE-3
         \                   /
          → Integration task ←
```

---

## Agent Communication Format

### Handoff Message
```markdown
## Handoff: [FROM_STAGE] → [TO_STAGE]

### Context
[Brief summary of work done]

### Artifacts
- [file1.md]
- [file2.md]

### Key Decisions
- [Decision 1]
- [Decision 2]

### Action Required
[What the next agent needs to do]
```

### Consultation Request
```markdown
## Consult: [AGENT_NAME]

### Question
[Specific question]

### Context
[Relevant background]

### Options (if applicable)
A. [Option A]
B. [Option B]
```

### Consultation Response
```markdown
## Response: [AGENT_NAME]

### Recommendation
[Clear recommendation]

### Reasoning
[Why this choice]

### Caveats
[Things to watch out for]
```

---

## Progress Tracking

### In session.md
```markdown
## Active Workflow
**Feature:** User Authentication
**Stage:** COOK
**Plan File:** plans/auth-plan.md

### Workflow Progress
[x] BRAINSTORM - completed 2026-04-15
[x] PLAN - completed 2026-04-15
[>] COOK - in progress (3/5 tasks done)
[ ] VERIFY
[ ] FIX (if needed)
[ ] DONE
```

### In plan file
```markdown
## Progress Log
| Timestamp | Task | Status | Notes |
|-----------|------|--------|-------|
| 2026-04-15 10:00 | DB-1 | Done | Migration created |
| 2026-04-15 10:15 | BE-1 | Done | Handler added |
| 2026-04-15 10:30 | BE-2 | In Progress | Working on service |
```

---

## Recovery Procedures

### Resuming After Break
```
1. Read session.md
2. Find active workflow
3. Read plan file for progress
4. Continue from last incomplete task
```

### Handling Failure
```
1. Log failure in plan file
2. Update session.md with blocker
3. Ask user how to proceed:
   - Skip task?
   - Try different approach?
   - Stop workflow?
```

### Rollback
```
1. If COOK fails badly:
   - git stash or git reset
   - Return to PLAN stage
   - Revise approach
```

---

## Quality Gates

### BRAINSTORM → PLAN
- [ ] User explicitly confirmed approach
- [ ] Scope clearly defined
- [ ] No major unknowns

### PLAN → COOK
- [ ] User approved task list
- [ ] Dependencies identified
- [ ] Files to modify listed

### COOK → VERIFY
- [ ] All tasks checked off
- [ ] Code compiles/builds
- [ ] No obvious errors

### VERIFY → DONE
- [ ] No critical issues
- [ ] No high issues
- [ ] Tests pass
