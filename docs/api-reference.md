# API Reference

## Overview

This document describes the API endpoints and utilities available in TestRepo.

## Base Configuration

```typescript
const API_URL = process.env.VITE_API_URL || 'http://localhost:3000';
const API_VERSION = 'v1';
```

## HTTP Methods

| Method | Purpose | Returns |
|--------|---------|---------|
| `GET` | Retrieve data | 200 OK, 404 Not Found |
| `POST` | Create new resource | 201 Created, 400 Bad Request |
| `PUT` | Update entire resource | 200 OK, 404 Not Found |
| `PATCH` | Partial update | 200 OK, 404 Not Found |
| `DELETE` | Remove resource | 204 No Content, 404 Not Found |

## Authentication

All API requests require an authentication token:

```typescript
const headers = {
  'Authorization': `Bearer ${token}`,
  'Content-Type': 'application/json'
};
```

## Error Handling

Standard error response format:

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable error message",
    "details": {
      "field": "error details"
    }
  }
}
```

### Common Error Codes

| Code | Status | Description |
|------|--------|-------------|
| `INVALID_REQUEST` | 400 | Invalid request parameters |
| `UNAUTHORIZED` | 401 | Missing or invalid authentication |
| `FORBIDDEN` | 403 | Insufficient permissions |
| `NOT_FOUND` | 404 | Resource not found |
| `CONFLICT` | 409 | Resource already exists |
| `INTERNAL_ERROR` | 500 | Server error |

## Endpoints

### Users

#### Get Current User
```
GET /api/v1/users/me
```

Response:
```json
{
  "id": "user123",
  "name": "John Doe",
  "email": "john@example.com",
  "role": "admin",
  "createdAt": "2026-11-01T00:00:00Z"
}
```

#### Get User by ID
```
GET /api/v1/users/:id
```

Parameters:
- `id` (string, required): User ID

#### Update User
```
PUT /api/v1/users/:id
```

Request:
```json
{
  "name": "Jane Doe",
  "email": "jane@example.com"
}
```

#### Delete User
```
DELETE /api/v1/users/:id
```

### Products

#### List Products
```
GET /api/v1/products?page=1&limit=20&sort=name
```

Query Parameters:
- `page` (number, optional): Page number (default: 1)
- `limit` (number, optional): Items per page (default: 20)
- `sort` (string, optional): Sort field

Response:
```json
{
  "data": [
    {
      "id": "prod123",
      "name": "Product Name",
      "description": "Product description",
      "price": 99.99,
      "category": "electronics",
      "inStock": true,
      "createdAt": "2026-11-01T00:00:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 100,
    "pages": 5
  }
}
```

#### Get Product by ID
```
GET /api/v1/products/:id
```

#### Create Product
```
POST /api/v1/products
```

Request:
```json
{
  "name": "New Product",
  "description": "Product description",
  "price": 99.99,
  "category": "electronics"
}
```

#### Update Product
```
PUT /api/v1/products/:id
```

#### Delete Product
```
DELETE /api/v1/products/:id
```

### Orders

#### List Orders
```
GET /api/v1/orders?status=pending&sort=-createdAt
```

Query Parameters:
- `status` (string, optional): Filter by status
- `sort` (string, optional): Sort field

#### Get Order by ID
```
GET /api/v1/orders/:id
```

Response:
```json
{
  "id": "order123",
  "userId": "user123",
  "items": [
    {
      "productId": "prod123",
      "quantity": 2,
      "price": 99.99
    }
  ],
  "status": "pending",
  "total": 199.98,
  "createdAt": "2026-11-01T00:00:00Z"
}
```

#### Create Order
```
POST /api/v1/orders
```

Request:
```json
{
  "items": [
    {
      "productId": "prod123",
      "quantity": 2
    }
  ]
}
```

#### Update Order Status
```
PATCH /api/v1/orders/:id
```

Request:
```json
{
  "status": "shipped"
}
```

## Rate Limiting

API enforces rate limits:

| Tier | Requests | Window |
|------|----------|--------|
| Free | 100 | 1 hour |
| Pro | 1000 | 1 hour |
| Enterprise | Unlimited | - |

Headers:
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 50
X-RateLimit-Reset: 1699795200
```

## Pagination

Standard pagination parameters:

```
GET /api/v1/resource?page=1&limit=20
```

Response includes:
```json
{
  "data": [...],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 500,
    "pages": 25
  }
}
```

## Filtering

Use query parameters to filter:

```
GET /api/v1/products?category=electronics&inStock=true&price__lte=500
```

Operators:
- `__eq`: Equal to
- `__ne`: Not equal to
- `__lt`: Less than
- `__lte`: Less than or equal to
- `__gt`: Greater than
- `__gte`: Greater than or equal to
- `__in`: In array
- `__nin`: Not in array

## Sorting

Specify sort field with optional direction:

```
GET /api/v1/products?sort=-price,name
```

- `-` prefix for descending order
- Default: ascending order

## Versioning

API versioning via URL path: `/api/v1/`, `/api/v2/`

Deprecation headers:
```
Deprecation: true
Sunset: 2027-11-16T00:00:00Z
Link: </api/v2/resource>; rel="successor-version"
```

## Examples

### cURL

```bash
# Get products
curl -H "Authorization: Bearer token123" \
  https://api.example.com/api/v1/products

# Create product
curl -X POST \
  -H "Authorization: Bearer token123" \
  -H "Content-Type: application/json" \
  -d '{"name":"Product","price":99.99}' \
  https://api.example.com/api/v1/products
```

### TypeScript

```typescript
async function getProducts() {
  const response = await fetch('/api/v1/products', {
    headers: {
      'Authorization': `Bearer ${token}`
    }
  });
  return response.json();
}
```

### JavaScript (Fetch)

```javascript
fetch('/api/v1/products', {
  method: 'POST',
  headers: {
    'Authorization': `Bearer ${token}`,
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    name: 'Product',
    price: 99.99
  })
})
.then(res => res.json())
.then(data => console.log(data));
```

## Support

- 📚 [Getting Started Guide](./getting-started.md)
- 🐛 [Report Issue](https://github.com/saaysalim/TestRepo/issues)
- 💬 [Ask Question](https://github.com/saaysalim/TestRepo/discussions)

---

**Last Updated**: November 16, 2026
