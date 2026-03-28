# Products API test cases

Base URL:
https://fakestoreapi.com

---

## Happy path

### TC-PROD-01
Title: Get all products

Endpoint:
GET /products

Steps:
1. Send GET request to /products

Expected result:
- Status code = 200 Success
- Response body is JSON array
- Array contains product objects
- Each object contains fields: id, title, price, description, category, image, rating
- "rating" is an object containing fields: rate, count

---

### TC-PROD-02
Title: Get single product by valid ID

Endpoint:
GET /products/1

Steps:
1. Send GET request to /products/1

Expected result:
- Status code = 200 Success
- Response body is JSON object
- Product id = 1
- Response contains fields: id, title, price, description, category, image, rating
- "rating" is an object containing fields: rate, count

---

### TC-PROD-03
Title: Get products by valid category

Endpoint:
GET /products/category/electronics

Steps:
1. Send GET request to /products/category/electronics

Expected result:
- Status code = 200 Success
- Response body is JSON array
- Each product has category "electronics"

---

### TC-PROD-04
Title: Create product with valid payload

Endpoint:
POST /products

Steps:
1. Send POST request to /products
2. Send valid product JSON payload

Request payload:
```json
{
  "title": "Test Product",
  "price": 19.99,
  "description": "Product created during API testing",
  "category": "electronics",
  "image": "https://i.pravatar.cc"
}
```

Expected result:
- Status code = 201 Product created successfully
- Response body contains created product object
- Response contains id field

Note:
FakeStoreAPI simulates creation and may not persist data.

---

### TC-PROD-05
Title: Update product with valid payload

Endpoint:
PUT /products/1

Steps:
1. Send PUT request to /products/1
2. Send valid updated product payload

Request payload:
```json
{
  "title": "Updated Product",
  "price": 29.99,
  "description": "Updated during API testing",
  "category": "electronics",
  "image": "https://i.pravatar.cc"
}
```

Expected result:
- Status code = 200 Product updated successfully
- Response body contains updated product data

---

### TC-PROD-06
Title: Delete product with valid ID

Endpoint:
DELETE /products/1

Steps:
1. Send DELETE request to /products/1

Expected result:
- Status code = 200 Product delated successfully
- Response body contains deleted product object
- Response contains id = 1

Note:
Operation may be simulated.

---

## Negative cases

### TC-PROD-07
Title: Get product with non-existing ID

Endpoint:
GET /products/999999

Steps:
1. Send GET request to /products/999999

Expected result:
- Status code = 200 Success
- Response body is empty

---

### TC-PROD-08
Title: Get product with non-numeric ID

Endpoint:
GET /products/abc

Steps:
1. Send GET request to /products/abc

Expected result:
- Status code = 400 Bad Request
- Bad request id -> integer required

---

### TC-PROD-09
Title: Create product with missing title

Endpoint:
POST /products

Steps:
1. Send POST request to /products
2. Send payload without "title"

Request payload:
```json
{
  "price": 19.99,
  "description": "Missing title test",
  "category": "electronics",
  "image": "https://i.pravatar.cc"
}
```

Expected result:
- Status code = 400 Bad Request
- Response body with validation error or empty error response

---

### TC-PROD-10
Title: Create product with negative price

Endpoint:
POST /products

Steps:
1. Send POST request to /products
2. Set price to negative value

Request payload:
```json
{
  "title": "Negative price test",
  "price": -10,
  "description": "Invalid price value",
  "category": "electronics",
  "image": "https://i.pravatar.cc"
}
```

Expected result:
- Status code = 400 Bad Request
- API rejects invalid input

---

### TC-PROD-11
Title: Update product with invalid data type

Endpoint:
PUT /products/1

Steps:
1. Send PUT request to /products/1
2. Set "price" as string

Request payload:
```json
{
  "title": "Invalid type test",
  "price": "abc",
  "description": "Price as string",
  "category": "electronics",
  "image": "https://i.pravatar.cc"
}
```

Expected result:
- Status code = 400 Bad Request
- Response body contains validation error for invalid data type or empty error response

---

### TC-PROD-12
Title: Delete product with non-numeric ID

Endpoint:
DELETE /products/abc

Steps:
1. Send DELETE request to /products/abc

Expected result:
- Status code = 400 Bad Request
- Response body contains error information or empty error response

---

## Edge cases

### TC-PROD-13
Title: Create product with extremely large price value

Endpoint:
POST /products

Steps:
1. Send POST request to /products
2. Use request body with extremely large price value

Request payload:
```json
{
  "title": "Huge price test",
  "price": 999999999999,
  "description": "Edge case price test",
  "category": "electronics",
  "image": "https://i.pravatar.cc",
}
```

Expected result:
- Status code = 201 Product created successfully
- Response body contains created product object
- Product contains fields: id, title, price, description, category, image
- Response remains valid price

---

### TC-PROD-14
Title: Create product with very long title

Endpoint:
POST /products

Steps:
1. Send POST request to /products
2. Set title to very long string (e.g. 500+ characters)

Request payload:
```json
{
  "title": "AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA",
  "price": 19.99,
  "description": "Very long title test",
  "category": "electronics",
  "image": "https://i.pravatar.cc"
}
```

Expected result:
- Status code = 201 Product created successfully
- Response body contains created product object
- Product contains fields: id, title, price, description, category, image
- Response remains valid title


---

### TC-PROD-15
Title: Create product with special characters in title

Endpoint:
POST /products

Steps:
1. Send POST request to /products
2. Set title to special characters (e.g. !@#$%^&*)

Request payload:
```json
{
  "title": "!@#$%^&*()<>?/{}[]|~`+=_-",
  "price": 19.99,
  "description": "Special characters test",
  "category": "electronics",
  "image": "https://i.pravatar.cc"
}
```

Expected result:
- Status code = 201 Product created successfully
- Response body contains created product object
- Product contains fields: id, title, price, description, category, image
- Response remains valid title