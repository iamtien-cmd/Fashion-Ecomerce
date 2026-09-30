# Database Rules

## 1. Database

Default database:

```text
PostgreSQL
```

Use the project's configured database version.

## 2. Schema Changes

Database schema changes must be deliberate.

Do not modify schema manually in a way that bypasses the project's migration strategy.

Every structural change should have a corresponding migration when migrations are used.

## 3. IDs

Use a consistent ID strategy.

Do not mix ID generation strategies without justification.

## 4. Money

Never use floating-point types for monetary values.

Use:

```java
BigDecimal
```

for Java monetary calculations.

Database monetary representation must preserve precision.

## 5. Timestamps

Use consistent timestamp types.

Prefer timezone-aware timestamps when the application operates across regions.

Use a consistent convention for:

* `createdAt`
* `updatedAt`
* `deletedAt`

## 6. Naming

Database naming should follow one consistent convention.

Preferred:

```text
snake_case
```

Examples:

```text
product_id
created_at
updated_at
order_item
```

Do not mix:

```text
productId
product_id
PRODUCT_ID
```

within the same schema.

## 7. Constraints

Use database constraints for critical invariants where appropriate.

Examples:

* NOT NULL
* UNIQUE
* FOREIGN KEY
* CHECK

Do not rely exclusively on application validation for critical data integrity.

## 8. Unique Fields

Fields that must be globally unique should have database-level uniqueness.

Example:

```text
SKU
```

must not rely only on Java validation.

## 9. Foreign Keys

Relationships must use appropriate foreign keys.

Do not store relationships only as arbitrary IDs without database integrity unless explicitly justified.

## 10. Indexes

Add indexes based on actual query patterns.

Likely candidates may include:

* Foreign keys
* Unique identifiers
* Frequently filtered fields
* Frequently sorted fields

Do not create indexes on every column.

## 11. Product / Variant

Product and ProductVariant must be separate entities.

Example:

```text
Product
    id
    name
    description

ProductVariant
    id
    product_id
    sku
    size
    color
    price
```

Inventory belongs to ProductVariant.

## 12. Orders

OrderItem must store the price snapshot at purchase time.

Do not calculate historical order totals from the current product price.

OrderItem should preserve sufficient historical information for the order to remain accurate even if the product changes.

## 13. Address Snapshot

Historical order addresses must not depend only on the user's current address.

Store the required address information as an order snapshot.

## 14. Inventory Integrity

Stock must never become negative.

Critical inventory updates must be safe under concurrent requests.

Database constraints and transactional/locking strategies should be used where appropriate.

## 15. Soft Delete

Do not introduce soft delete globally unless the domain requires it.

If soft delete is used:

* Define which entities support it.
* Define how queries treat deleted records.
* Prevent deleted records from unexpectedly appearing in normal APIs.

## 16. Query Performance

Avoid:

* N+1 queries
* Unbounded result sets
* Loading unnecessary columns/relationships
* Missing indexes for important query paths

Optimize based on real use cases.

## 17. Data Integrity

Application validation and database constraints should complement each other.

Critical invariants should have database-level protection where practical.
