# Skill: Generate Component

## Purpose
Quickly scaffold a new UI component.

## Usage
`/generate-component [name] [description]`

## Example
`/generate-component UserCard Display user avatar, name, and email`

## Output
Creates:
1. Component file
2. Types/Props interface
3. Basic test file

## Template

### Component
```tsx
interface [Name]Props {
  // Props based on description
}

export function [Name]({ ...props }: [Name]Props) {
  return (
    <div>
      {/* Implementation */}
    </div>
  );
}
```

### Test
```tsx
test('[Name] renders correctly', () => {
  render(<[Name] />);
  // Assertions
});
```

## Conventions
- Functional components only
- Props interface named `[Name]Props`
- Export as named export
