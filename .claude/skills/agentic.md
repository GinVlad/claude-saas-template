# Skill: Agentic Workflow

## Purpose
Coordinate tasks through Brainstorm → Plan → Cook → Verify → Fix stages automatically.

## Usage
```
/agentic [feature description]      # Full flow
/agentic brainstorm [feature]       # Single stage
/agentic plan [feature]
/agentic cook [feature]  
/agentic verify [feature]
/agentic fix [feature]
/agentic resume                     # Continue from session.md
```

## When Invoked

### 1. Check Session State
```
Read: .claude/rules/session.md
- What phase are we in?
- Any in-progress features?
- Any blockers?
```

### 2. Determine Stage
- If new feature → Start at BRAINSTORM
- If resuming → Continue from last stage
- If specific stage requested → Go there

### 3. Execute Stage

#### BRAINSTORM
```
Agents: CTO (lead), domain experts (consult)

1. Parse user request
2. Identify scope (backend? frontend? both?)
3. Load relevant rules ONLY
4. Generate 2-3 approaches
5. Compare trade-offs
6. Recommend one

Output: plans/[feature]-brainstorm.md
Ask: "Does this approach work for you?"
```

#### PLAN
```
Agents: CTO (lead), Backend-dev, Frontend-dev, Database

1. Read brainstorm output
2. Break into tasks with:
   - Task ID
   - Description
   - Files to create/modify
   - Dependencies
   - Estimated complexity (S/M/L)
3. Order by dependencies
4. Identify parallel tracks

Output: plans/[feature]-plan.md
Ask: "Ready to start implementation?"
```

#### COOK
```
Agents: Backend-dev, Frontend-dev (parallel if possible)

1. Read plan
2. For each task:
   a. Load relevant rules
   b. Implement
   c. Mark task done in plan
   d. Update session.md
3. Commit after each logical chunk

Output: Working code
Gate: All tasks checked off
```

#### VERIFY
```
Agents: Tester (lead), Security

1. Tester:
   - Run tests
   - Write tests for new code
   - Manual verification if UI

2. Security:
   - Scan for vulnerabilities
   - Check input validation
   - Review auth flow

Output: plans/[feature]-verify.md
Gate: No critical/high issues
```

#### FIX
```
Agents: Original implementers

1. Read verify issues
2. Fix each issue
3. Re-verify fixed items
4. Loop until clean

Output: Fixed code
Gate: Verify passes
```

### 4. Update Session
After each stage:
```
Update: .claude/rules/session.md
- Current phase
- What's done
- What's next
- Any blockers
```
