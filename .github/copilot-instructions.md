---
description: >-
  Workspace instructions for the GitHub Copilot Leverage Demo project.
  Provides coding conventions, build commands, and development guidelines for
  React + TypeScript + Vite applications.
---

# GitHub Copilot Leverage Demo – Workspace Instructions

This file guides AI agents working in this React + TypeScript + Vite project. Follow these conventions to maintain consistency and productivity.

## Project Overview

- **Stack**: React 19 + TypeScript + Vite
- **Purpose**: Demonstration project for GitHub Copilot best practices
- **Build Tool**: Vite with React plugin (uses Oxc)
- **Type Checking**: TypeScript with strict mode
- **Linting**: ESLint with React Hooks plugin

## Build & Development Commands

Run these commands from the workspace root:

```bash
npm run dev       # Start Vite dev server (HMR enabled)
npm run build     # Type check (tsc) then build optimized bundle
npm run lint      # Run ESLint on all files
npm run preview   # Preview production build locally
```

**Important**: The `build` command runs `tsc -b` first to catch type errors before bundling.

## Code Conventions

### Component Architecture

- **Use functional components only** – never class components
- **Hooks for state & side effects** – `useState`, `useEffect`, `useContext`, custom hooks
- **Props as TypeScript interfaces** – explicitly type component props
- **Component files**: One component per file in `src/` or feature subdirectories

Example:

```typescript
import { FC, ReactNode } from 'react'

interface ButtonProps {
  label: string
  onClick: () => void
  children?: ReactNode
}

export const Button: FC<ButtonProps> = ({ label, onClick }) => (
  <button onClick={onClick}>{label}</button>
)
```

### Styling

- **Tailwind CSS for all new styles** – utility-first approach
- **Avoid CSS files** unless absolutely necessary (scoped component styles)
- **Class names via className prop** – use Tailwind utilities directly
- Current project uses plain CSS for legacy (App.css) – migrate to Tailwind when refactoring

### TypeScript Requirements

- **Strict mode enabled** – leverage type safety
- **Explicit return types** – specify React component return types (`FC`, `React.FC`)
- **No `any` types** – use proper typing or generics
- **tsconfig.json & tsconfig.app.json** – maintain strict settings
- **TypeScript files**: Use `.tsx` for components, `.ts` for utilities

### File Organization

```
src/
  components/          # Reusable feature components
  pages/              # Route-level pages (if using routing)
  hooks/              # Custom React hooks
  utils/              # Helper functions & utilities
  types/              # Shared TypeScript types & interfaces
  App.tsx             # Root component
  main.tsx            # React DOM mount point
```

## Development Workflow

### Creating New Components

1. Create a `.tsx` file in `src/components/`
2. Export as a named exported component with explicit types
3. Use hooks for state management
4. Add Tailwind classes for styling
5. Run `npm run lint` before committing

### Adding Dependencies

- Always prefer npm packages with TypeScript support
- Update `package.json` manually or via `npm install <package>`
- Ensure types are available (`@types/*` if needed)

### Type Checking & Linting

- **Before committing**: Run `npm run lint` to catch errors
- **Build validation**: `npm run build` checks types first, then bundles
- **ESLint config**: `eslint.config.js` – extends Flat Config format

## Common Pitfalls

- ❌ Importing CSS files into components – migrate to Tailwind
- ❌ Using class components – always use functional components with hooks
- ❌ Loose TypeScript types – no `any`, explicit interfaces for props
- ❌ Missing return types on components – specify `FC<Props>`
- ❌ Ignoring linting errors – `npm run lint` must pass before deployment

## Key Files

- [vite.config.ts](../vite.config.ts) – Build configuration
- [eslint.config.js](../eslint.config.js) – Linting rules
- [tsconfig.json](../tsconfig.json) – TypeScript compiler options
- [package.json](../package.json) – Dependencies and scripts
- [src/App.tsx](../src/App.tsx) – Root component example
- [src/main.tsx](../src/main.tsx) – React DOM entry point

## Related Preferences

- ✅ Functional components with hooks
- ✅ Tailwind CSS for styling
- ✅ TypeScript strict mode
- ✅ ESLint for code quality

---

For questions or updates to these guidelines, consult the project README and official documentation:
- [Vite Docs](https://vite.dev/)
- [React Docs](https://react.dev/)
- [TypeScript Docs](https://www.typescriptlang.org/)
