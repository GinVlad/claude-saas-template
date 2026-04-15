# Agentic Workflow System

## Overview
Automatic task coordination that flows through stages like a real team.

```
User Request
    ↓
[1. BRAINSTORM] → ideas, approaches, trade-offs
    ↓
[2. PLAN] → concrete steps, files to create/modify
    ↓
[3. COOK] → implementation (code writing)
    ↓
[4. VERIFY] → tests, security check, review
    ↓
[5. FIX] → address issues found in verify
    ↓
Done → Update session.md
```

---

## Stage 1: BRAINSTORM

**Agent:** CTO + relevant domain agent

**Input:** User request

**Actions:**
1. Understand the request
2. Identify affected areas (backend, frontend, db, etc.)
3. List 2-3 approaches with trade-offs
4. Recommend one approach
5. Get user confirmation

**Output:** `plans/[feature]-brainstorm.md`

**Gate:** User must confirm approach before proceeding

---

## Stage 2: PLAN

**Agent:** CTO + domain agents (backend-dev, frontend-dev, database)

**Input:** Confirmed approach from brainstorm

**Actions:**
1. Break into concrete tasks
2. Identify files to create/modify
3. Define interfaces between components
4. Estimate complexity per task
5. Order tasks by dependencies

**Output:** `plans/[feature]-plan.md`

**Gate:** User reviews plan, can adjust

---

## Stage 3: COOK

**Agent:** Domain agents (backend-dev, frontend-dev, database)

**Input:** Approved plan

**Actions:**
1. Load relevant rules (backend.md, frontend.md, etc.)
2. Implement task by task
3. Update session.md progress after each task
4. Commit logical chunks

**Output:** Working code

**Gate:** All tasks in plan completed

---

## Stage 4: VERIFY

**Agent:** Tester + Security

**Input:** Completed implementation

**Actions:**
1. **Tester agent:**
   - Run existing tests
   - Write new tests for new code
   - Check edge cases
   - Verify happy path works

2. **Security agent:**
   - Check for vulnerabilities
   - Validate input handling
   - Review auth/authz
   - Check for secrets in code

**Output:** `plans/[feature]-verify.md` with findings

**Gate:** Pass = no critical/high issues. Fail = go to FIX stage

---

## Stage 5: FIX

**Agent:** Original domain agents

**Input:** Issues from verify stage

**Actions:**
1. Address each issue
2. Re-run verify for fixed items
3. Loop until all issues resolved

**Output:** Fixed code

**Gate:** Verify passes

---

## Final: UPDATE

**Actions:**
1. Update `rules/session.md` with:
   - What was completed
   - Any decisions made
   - Notes for next session
2. Move plan files to `plans/completed/`
3. Clean up any temp files

---

## Invoking the Workflow

### Full Flow
```
/agentic [feature description]
```
Runs all stages automatically with gates.

### Single Stage
```
/agentic brainstorm [feature]
/agentic plan [feature]
/agentic cook [feature]
/agentic verify [feature]
/agentic fix [feature]
```

### Resume
```
/agentic resume
```
Reads session.md and continues from last point.

---

## Agent Coordination Rules

1. **One lead agent per stage** - Others consult
2. **Handoff with artifacts** - Each stage produces .md file
3. **No skipping gates** - User confirms before next stage
4. **Parallel where possible** - Backend + Frontend can cook in parallel
5. **Always update session.md** - Track progress for resume
