# Backend Rules

## 1. Technology

Default backend stack:

* Java 21
* Spring Boot 3
* Spring Web
* Spring Data JPA
* PostgreSQL
* Maven
* JUnit 5
* Mockito

Use the project's actual configured versions when they differ.

Do not upgrade versions without explicit justification.

## 2. Layer Responsibilities

### Controller

Responsible for:

* HTTP requests
* Request validation
* Authentication context extraction
* HTTP response mapping

Controllers must not contain business logic.

### Service

Responsible for:

* Business logic
* Business validation
* Transaction boundaries
* Coordination between repositories
* Domain workflows

Services should not directly depend on HTTP request/response objects.

### Repository

Responsible for:

* Database access
* Queries
* Persistence

Repositories must not implement business workflows.

## 3. Transactions

Use transactions deliberately.

Transactions should cover business operations that must be atomic.

Examples:

* Creating an order
* Reserving inventory
* Processing checkout
* Updating payment/order state

Do not use transactions indiscriminately.

## 4. DTOs

Do not expose JPA entities directly through public APIs.

Use request/response DTOs.

Examples:

* `ProductCreateRequest`
* `ProductUpdateRequest`
* `ProductResponse`

DTOs should contain only data required by the API contract.

## 5. Mapping

Use explicit mapping between entities and DTOs.

Do not expose persistence implementation details through API responses.

For simple mappings, explicit code is preferred over unnecessary abstraction.

## 6. Exception Handling

Use centralized exception handling.

Business exceptions should be meaningful.

Examples:

* `ResourceNotFoundException`
* `BusinessException`
* `InsufficientStockException`
* `InvalidOrderStateException`

Do not use generic `RuntimeException` for every business failure.

## 7. Configuration

Configuration must be externalized.

Do not hardcode:

* Passwords
* API keys
* JWT secrets
* Database credentials
* Payment credentials

Use environment variables or the project's configuration mechanism.

## 8. Logging

Logs must be useful and safe.

Never log:

* Passwords
* Access tokens
* Refresh tokens
* Payment credentials
* Sensitive personal information

Use appropriate log levels.

Avoid excessive debug logging in production paths.

## 9. Persistence

Do not perform database queries inside controllers.

Do not manually construct SQL when an existing JPA repository/query mechanism is sufficient.

Use explicit queries when query behavior requires them.

Optimize based on actual query requirements rather than premature optimization.

## 10. Fetching

Be conscious of:

* N+1 queries
* Lazy loading
* Entity relationships
* Pagination
* Query size

Do not blindly use `EAGER` relationships.

Prefer explicit fetching strategies based on use cases.

## 11. Pagination

Collection endpoints should support pagination when the dataset can grow significantly.

Do not return unbounded large collections from production APIs.

## 12. Business Rules

Critical business rules belong in services/domain logic, not controllers.

Examples:

* Stock cannot become negative.
* Order cannot be cancelled after shipment.
* User cannot modify another user's order.
* Coupon cannot be used outside its validity period.

## 13. Concurrency

For inventory and other critical shared resources:

* Consider concurrent requests.
* Use appropriate database constraints, locking, or atomic operations.
* Never rely only on a preliminary read.

Example:

Checking:

```text
stock > requestedQuantity
```

and then updating stock separately can create race conditions.

The implementation must ensure the operation is safe under concurrent requests.

## 14. IDs

Use the project's standard ID strategy consistently.

Do not mix multiple ID strategies without a documented reason.

## 15. API Compatibility

Do not silently change an existing API contract.

If changing:

* Request fields
* Response fields
* Status codes
* Endpoint paths
* Authentication behavior

identify the compatibility impact.

## 16. Code Style

Prefer:

* Small methods
* Clear names
* Explicit control flow
* Constructor injection
* Immutable values where practical

Avoid:

* Field injection
* Giant service classes
* Generic `Utils` classes
* Boolean parameters with unclear meaning
* Deep nesting
