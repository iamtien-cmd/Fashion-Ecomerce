# Component Rules

## 1. Component Naming

React components use PascalCase.

Examples:

```text
ProductCard.tsx
ProductList.tsx
ProductFilter.tsx
CheckoutForm.tsx
```

## 2. File Naming

Use the project's established naming convention.

Preferred:

```text
PascalCase
```

for React component files.

Examples:

```text
ProductCard.tsx
ProductDetail.tsx
```

Lowercase/camelCase may be used for non-component modules according to the existing project convention.

## 3. Component Responsibility

A component should have one primary responsibility.

Avoid components that simultaneously handle:

* API communication
* Complex business logic
* Form management
* Global state
* Large UI trees

Extract responsibilities when complexity becomes meaningful.

## 4. Props

Props should be explicitly typed.

Example:

```typescript
type ProductCardProps = {
  product: Product;
  onAddToCart?: () => void;
};
```

Avoid:

```typescript
props: any
```

## 5. Reusability

Do not create a component merely because two lines of JSX are repeated.

Create reusable components when:

* The UI has a meaningful concept.
* The behavior is reused.
* The component improves readability.
* The component represents a domain/UI concept.

## 6. Hooks

Custom hooks use:

```text
use + Name
```

Examples:

```text
useProducts
useCart
useAuth
useProductFilters
```

Hooks should encapsulate reusable behavior, not arbitrary code fragments.

## 7. Business Logic

Do not put substantial business logic inside JSX.

Prefer:

* hooks
* services
* utility functions
* state modules

depending on the type of logic.

## 8. API Data

Components should not manually duplicate API transformation logic.

Use a consistent data-access layer.

## 9. Conditional Rendering

Keep JSX readable.

Avoid deeply nested ternary expressions.

For complex conditions, calculate values before the JSX.

## 10. Forms

Complex forms should use the project's standard form library.

Validation schemas should be reusable where appropriate.

## 11. Component Duplication

Before creating a new component:

1. Search existing components.
2. Check whether an existing component can be extended.
3. Check whether the desired behavior already exists.

Do not create:

```text
ProductCard
ProductCardNew
ProductCardV2
ProductCardUpdated
```

without a clear architectural reason.

## 12. UI State

Keep state as close as practical to where it is used.

Do not move local state into global state without justification.

## 13. Accessibility

Interactive components must support:

* Keyboard interaction
* Visible focus
* Appropriate semantic elements
* Labels for form controls
* Accessible names

## 14. Testing

Important reusable components should have tests when their behavior is non-trivial.

Test user-visible behavior rather than internal implementation details.
