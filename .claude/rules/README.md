# Rules System

## Purpose
Folder-based rules to keep context small and focused. Load only what's needed per task.

## Structure
```
rules/
├── README.md           # This file
├── session.md          # Current session state (check first!)
├── backend.md          # Backend conventions
├── frontend.md         # Frontend conventions
├── database.md         # Database conventions
├── ai-integration.md   # AI/LLM rules (if applicable)
├── payments.md         # Payment integration
├── security.md         # Security requirements
└── testing.md          # Test conventions
```

## Usage

### Starting a Session
1. Read `session.md` to see last state
2. Load only relevant rule files for your task
3. Update `session.md` when done

### In Plan Mode
- Load ONLY the rules relevant to the feature
- Example: Planning auth? Load `backend.md` + `security.md`
- Example: Planning UI? Load `frontend.md` only

### Context Budget
- Each rule file should be < 100 lines
- If a file grows too large, split it
- Don't load all rules — pick what's needed
