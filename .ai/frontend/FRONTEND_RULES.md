# Frontend Rules

## 1. Technology

Default frontend stack:

* React
* TypeScript
* Vite
* Tailwind CSS
* React Router
* TanStack Query
* Zustand
* React Hook Form
* Zod

Use the project's actual configured technologies.

Do not introduce another state-management or data-fetching library without justification.

## 2. TypeScript

Use TypeScript strictly.

Avoid:

```typescript
any
```

unless there is a documented technical reason.

Prefer explicit types.

Do not duplicate types unnecessarily.

## 3. Components

Components should have one clear responsibility.

Prefer:

```text
ProductCard
ProductList
ProductFilter
ProductDetail
```

over one giant `ProductPage` containing all logic.

## 4. Pages

Pages coordinate:

* Routing
* Data loading
* Page-level state
* Composition of components

Reusable UI logic should live in components/hooks rather than being duplicated across pages.

## 5. API Communication

API calls should use the project's centralized API/data-fetching approach.

Do not scatter raw `fetch`/`axios` calls throughout components.

Prefer dedicated query/mutation functions or hooks.

## 6. Server State

Use TanStack Query for server state where configured.

Do not duplicate server state unnecessarily in Zustand/local state.

## 7. Client State

Use Zustand only for genuine client/application state.

Examples:

* Cart UI state when appropriate
* Theme
* UI preferences

Do not copy entire API responses into global state without a reason.

## 8. Forms

Use React Hook Form for non-trivial forms.

Use Zod for schema validation when configured.

Frontend validation improves UX but does not replace backend validation.

## 9. Routing

Routes should be centralized and predictable.

Do not duplicate route definitions.

Protected routes must not rely only on hiding UI elements.

Authorization remains a backend responsibility.

## 10. Error Handling

Handle:

* Loading
* Success
* Empty
* Error

states explicitly where relevant.

Do not silently swallow API errors.

## 11. Loading States

Avoid displaying broken or partially initialized UI while asynchronous data is loading.

Use appropriate loading states.

## 12. Forms and User Input

Never assume frontend validation is sufficient.

Always expect the backend to reject invalid input.

Handle backend validation errors clearly.

## 13. E-Commerce Rules

Never calculate authoritative:

* Product price
* Discount
* Inventory
* Order total

on the frontend and trust the result.

The frontend may display calculated estimates, but the backend is authoritative.

## 14. Accessibility

Interactive elements should be accessible.

Prefer semantic HTML.

Buttons should be buttons.

Links should be links.

Form inputs should have labels.

Images should have meaningful alt text when appropriate.

## 15. Styling

Use the existing styling system.

Do not introduce another CSS framework.

Avoid unnecessary inline styles.

Reuse existing design tokens/components.

## 16. Performance

Avoid unnecessary:

* Re-renders
* API requests
* Large client-side data loads
* Duplicate queries

Do not prematurely optimize without evidence.

## 17. Security

Never store sensitive secrets in frontend source code.

Never assume frontend route protection is authorization.

Do not expose private API credentials to the browser.
