# Project Rules

## 1. Purpose

This document defines the global engineering rules for the project.

These rules apply to the entire repository unless a more specific rule overrides them.

## 2. General Engineering Principles

### 2.1 Existing Code First

Before creating a new file, class, component, service, utility, endpoint, or abstraction:

1. Search for existing implementations.
2. Inspect related code.
3. Determine whether the existing implementation can be reused or extended.

Do not create duplicates.

### 2.2 Minimal Change

Implement the smallest change that correctly satisfies the task.

Do not:

* Refactor unrelated code.
* Rename unrelated files.
* Reformat unrelated files.
* Upgrade dependencies without a reason.
* Change architecture unnecessarily.
* Replace working implementations without justification.

### 2.3 No Unapproved Architecture Changes

Do not introduce:

* Microservices
* New architectural layers
* New frameworks
* New persistence technologies
* New messaging systems
* New authentication systems

unless explicitly requested or approved.

The default architecture is a modular monolith.

### 2.4 Dependencies

Before adding a dependency:

1. Check whether the required functionality already exists.
2. Check whether an existing dependency provides it.
3. Explain why a new dependency is necessary.

Do not add dependencies for trivial functionality.

### 2.5 Code Quality

Code should be:

* Readable
* Testable
* Maintainable
* Explicit
* Consistent with the existing project

Avoid:

* Giant methods
* Giant classes
* Deep nesting
* Duplicate logic
* Magic numbers
* Magic strings
* Premature abstractions
* Unnecessary generic utilities

## 3. Architecture

The application follows a modular monolith architecture.

Backend dependency direction:

Controller
↓
Service
↓
Repository
↓
Database

Rules:

* Controllers handle HTTP concerns.
* Services contain business logic.
* Repositories handle persistence.
* Entities represent persistence/domain state.
* DTOs represent API input/output.
* Mappers convert between entities and DTOs when appropriate.

Controllers must not contain business logic.

Repositories must not contain business workflows.

Services must not depend on HTTP-specific concerns unless explicitly justified.

## 4. Feature Organization

Prefer feature-based organization.

Example:

```text
product/
├── controller/
├── service/
├── repository/
├── entity/
├── dto/
├── mapper/
└── exception/
```

Do not create large global folders such as:

```text
controllers/
services/
repositories/
```

unless required by an existing project convention.

Keep related code close together.

## 5. API Design

API rules are defined in:

`.ai/backend/API_RULES.md`

All API implementation must follow that document.

## 6. Database Design

Database rules are defined in:

`.ai/backend/DATABASE_RULES.md`

All database-related implementation must follow that document.

## 7. Backend

Backend implementation must follow:

* `.ai/backend/BACKEND_RULES.md`
* `.ai/backend/JAVA_NAMING.md`

Additional rules must be loaded when relevant.

## 8. Frontend

Frontend implementation must follow:

* `.ai/frontend/FRONTEND_RULES.md`

Component-specific work must also follow:

* `.ai/frontend/COMPONENT_RULES.md`

## 9. Security

Never:

* Store plaintext passwords.
* Commit secrets.
* Trust client-provided authorization.
* Trust client-provided prices.
* Trust client-provided inventory.
* Expose sensitive internal information in API errors.
* Log passwords, tokens, or payment credentials.

Authentication and authorization decisions must be enforced on the backend.

## 10. E-Commerce Domain Rules

### Product

Product and ProductVariant are different concepts.

Product represents the logical product.

ProductVariant represents a purchasable SKU/variation.

Example:

```text
Product:
    Classic T-Shirt

Variants:
    Black / S
    Black / M
    Black / L
    White / S
    White / M
```

Inventory belongs to ProductVariant, not Product.

Every purchasable variant must have a unique SKU.

### Money

Use precise decimal types for monetary values.

Never use floating-point types for money.

The backend is the source of truth for:

* Product price
* Discounts
* Taxes
* Shipping fees
* Order totals
* Inventory

Never trust totals calculated by the frontend.

### Orders

OrderItem must preserve the purchase price at the time of ordering.

Do not calculate historical order prices from the current Product price.

Shipping/billing address information required for historical orders must be stored as an order snapshot.

### Inventory

Inventory must never become negative.

Stock-changing operations must account for concurrent requests.

Do not rely on frontend stock validation.

### Payment

Payment status is separate from Order status.

Payment callbacks/webhooks must be idempotent.

Never trust the amount supplied by the client.

### Order State

Order status transitions must be explicit.

Example:

```text
PENDING
→ CONFIRMED
→ PROCESSING
→ SHIPPED
→ DELIVERED
```

Invalid state transitions must be rejected.

## 11. Validation

Use validation at the appropriate layer.

API input validation:

* Request DTO validation.

Business validation:

* Service layer.

Database constraints:

* Database layer.

Do not rely on only one validation layer for critical business invariants.

## 12. Error Handling

Use centralized exception handling.

API errors must use a consistent response structure.

Do not expose stack traces or internal implementation details to clients.

## 13. Testing

Every important business rule must have automated tests.

Bug fixes should include a regression test when practical.

Tests must verify behavior rather than implementation details.

Do not write tests merely to increase coverage numbers.

## 14. Modification Rules

Before modifying a file:

1. Read the file.
2. Inspect its callers/usages.
3. Inspect related interfaces.
4. Inspect relevant tests.
5. Understand its role in the architecture.
6. Make the smallest safe change.

Do not blindly overwrite existing files.

## 15. Final Verification

Before declaring a task complete, verify:

* Compilation/build
* Tests
* Naming
* Imports
* API contract
* Database consistency
* Security
* Architecture boundaries
* No unintended file changes
* Documentation/state updates when required

If verification cannot be performed, explicitly report that fact.
