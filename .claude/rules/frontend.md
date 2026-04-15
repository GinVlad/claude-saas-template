# Frontend Rules

## Project Layout
Customize for your framework:

```
frontend/
├── src/
│   ├── app/                # Pages/routes
│   ├── components/
│   │   ├── ui/            # Reusable UI components
│   │   └── features/      # Feature-specific components
│   ├── hooks/             # Custom hooks
│   ├── lib/               # Utilities, API client
│   ├── stores/            # State management
│   └── types/             # TypeScript types
├── public/
└── package.json
```

## Conventions
- TypeScript (recommended)
- Functional components
- Custom hooks for shared logic
- Mobile-first responsive design

## Component Pattern
```tsx
interface Props {
  // Props here
}

export function ComponentName({ prop }: Props) {
  return (
    <div className="...">
      {/* Content */}
    </div>
  );
}
```

## Styling
- [Tailwind / CSS Modules / Your choice]
- Mobile-first responsive design
- Consistent spacing/colors

## Data Fetching
- Server state: [React Query / SWR / etc.]
- Client state: [Zustand / Context / etc.]

## Dependencies
Customize for your stack:
- UI framework: [Your choice]
- Styling: [Your choice]
- Icons: [Your choice]
- Forms: [Your choice]
