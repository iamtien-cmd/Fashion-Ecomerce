# API Rules

## 1. Base Path

Use:

```text
/api/v1
```

Version APIs explicitly.

## 2. Resource Naming

Use nouns.

Good:

```text
GET    /api/v1/products
GET    /api/v1/products/{id}
POST   /api/v1/products
PATCH  /api/v1/products/{id}
DELETE /api/v1/products/{id}
```

Avoid:

```text
/getProducts
/createProduct
/deleteProduct
```

## 3. HTTP Methods

### GET

Read resources.

### POST

Create resources or trigger a clearly defined command/action when appropriate.

### PUT

Full replacement when the API semantics require it.

### PATCH

Partial update.

### DELETE

Delete/deactivate a resource according to domain requirements.

## 4. HTTP Status Codes

Use appropriate status codes.

```text
200 OK
201 Created
204 No Content
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
409 Conflict
422 Unprocessable Entity
500 Internal Server Error
```

Use `422` only if the project explicitly adopts this convention.

## 5. Response Format

Use a consistent API response format where the project defines one.

Do not introduce multiple incompatible response structures.

## 6. Validation Errors

Validation errors should clearly identify the invalid field when possible.

Example:

```json
{
  "code": "VALIDATION_ERROR",
  "message": "Validation failed",
  "errors": [
    {
      "field": "name",
      "message": "Name is required"
    }
  ]
}
```

Follow the project's actual error contract if one already exists.

## 7. Resource IDs

Use path parameters for resource identification.

Example:

```text
GET /products/{productId}
```

Do not put resource IDs redundantly in both path and body unless required.

## 8. Filtering

Use query parameters.

Example:

```text
GET /api/v1/products?category=shirts&size=M
```

Do not create separate endpoints for every filter combination.

## 9. Pagination

Use query parameters consistently.

Example:

```text
?page=0&size=20
```

Follow the existing project pagination convention.

## 10. Sorting

Use query parameters.

Example:

```text
?sort=createdAt,desc
```

Do not accept arbitrary database expressions from clients.

## 11. Security

Authorization must be enforced server-side.

Never trust:

* `userId` from request body
* `role` from request body
* price from frontend
* total from frontend

Derive authenticated user identity from the authentication context.

## 12. API Changes

Before changing an existing endpoint:

1. Find all usages.
2. Check frontend consumers.
3. Check tests.
4. Identify compatibility impact.

Do not silently break consumers.
