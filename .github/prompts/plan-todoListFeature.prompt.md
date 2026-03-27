# Plan: Add Todo List Feature

## Overview
Add an in-memory to-do list feature to the existing React + TypeScript + Vite app. Create a dedicated `TodoList` component in `src/components/`, style it with plain CSS (matching existing CSS variable system), and render it in `App.tsx`.

---

## Steps

### Phase 1 – Component

**1. Create `src/components/TodoList.tsx`**
- Define a `Todo` interface: `{ id: number; text: string }`
- Two state values: `todos: Todo[]` (seeded with a couple of sample items) and `input: string`
- `addTodo()` — appends a new todo, clears the input; guards against empty strings
- `deleteTodo(id: number)` — filters out the matching item
- JSX structure: input + button row at the top, a `<ul>` list where each item has a delete button
- Named export: `export const TodoList: FC = () => ...`

**2. Add styles to `src/App.css`**
- `.todo-section` — wrapper with padding, `border-top: 1px solid var(--border)`
- `.todo-form` — flex row with gap
- `.todo-input` — flex-grow, styled using `var(--border)`, `var(--bg)`, `var(--text)`
- `.todo-add-btn` — accent-colored button, follows the `.counter` style pattern
- `.todo-list` — resets list styles
- `.todo-item` — flex row with space-between, border-bottom separator
- `.todo-delete-btn` — small red delete button

**3. Update `src/App.tsx`**
- Import `TodoList` from `./components/TodoList`
- Render `<TodoList />` inside a new `<section id="todo">` after the existing `<div className="ticks">` divider

---

### Phase 2 – Validation

**4.** Run `npm run lint` — verify no ESLint errors
**5.** Run `npm run build` — verify TypeScript strict mode passes (`noUnusedLocals`, `noUnusedParameters`)

---

## Relevant Files
- `src/components/TodoList.tsx` — new file to create
- `src/App.css` — add todo styles
- `src/App.tsx` — import and render `<TodoList />`
- `src/index.css` — reference for CSS variables (`--accent`, `--border`, `--text`, `--bg`, etc.)

## Verification
1. Dev server shows todo list below existing content
2. Typing + clicking Add → new todo appears
3. Clicking Delete → todo is removed
4. Submitting empty input → no todo added (guard)
5. `npm run build` exits with no errors

## Decisions
- **Styling**: Plain CSS (no Tailwind — not installed in this project), reuse existing CSS variables from `index.css`
- **Placement**: New `<section id="todo">` in `App.tsx` — additive, preserves all existing content
- **No persistence**: in-memory only via `useState`
- **TypeScript**: Named export, explicit `FC` type, `Todo` interface, no `any`
