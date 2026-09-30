# Java Naming Rules

## Classes

Use PascalCase.

Examples:

* `Product`
* `ProductService`
* `ProductController`
* `ProductRepository`
* `ProductResponse`
* `CreateProductRequest`
* `ProductNotFoundException`

## Interfaces

Use PascalCase.

Examples:

* `PaymentService`
* `ProductMapper`

Do not prefix interfaces with `I`.

Bad:

```text
IProductService
```

Good:

```text
ProductService
```

## Methods

Use camelCase.

Examples:

```java
createProduct()
findProductById()
updateProduct()
deleteProduct()
```

Methods should use verbs when they represent actions.

## Variables

Use camelCase.

Examples:

```java
product
productId
productVariant
availableStock
```

Avoid abbreviations unless they are established technical terms.

## Constants

Use UPPER_SNAKE_CASE.

Examples:

```java
MAX_PAGE_SIZE
DEFAULT_PAGE_SIZE
MAX_LOGIN_ATTEMPTS
```

## Boolean Names

Boolean fields/methods should normally communicate a boolean meaning.

Examples:

```text
isActive
isDeleted
hasPermission
canCancel
```

Avoid unclear names such as:

```text
flag
statusBoolean
check
```

## DTO Naming

Prefer:

```text
CreateProductRequest
UpdateProductRequest
ProductResponse
ProductSummaryResponse
```

Avoid:

```text
ProductDTO1
ProductData
ProductObject
```

unless the project has an established convention.

## Exception Naming

Exceptions must end with:

```text
Exception
```

Examples:

```text
ProductNotFoundException
InsufficientStockException
InvalidOrderStateException
```

## Enum Naming

Enum type:

```text
OrderStatus
```

Enum values:

```text
PENDING
CONFIRMED
PROCESSING
SHIPPED
DELIVERED
CANCELLED
```

## Repository Naming

Examples:

```text
ProductRepository
ProductVariantRepository
OrderRepository
```

## Service Naming

Examples:

```text
ProductService
OrderService
InventoryService
```

If an implementation class is necessary:

```text
ProductServiceImpl
```

Do not create an implementation class merely because an interface exists.

## Controller Naming

Examples:

```text
ProductController
OrderController
UserController
```

## Package Naming

Use lowercase.

Examples:

```text
product
product.controller
product.service
product.repository
product.dto
```

Never use PascalCase package names.
