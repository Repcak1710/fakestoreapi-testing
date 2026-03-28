# Bug Reports – Products API

Note:
Fake Store API simulates create, update and delete operations.
This limitation may affect persistence-related scenarios, but it should not affect request validation or documented request schema requirements.

<a name="bug01"></a>
## BUG-PROD-01 – Invalid ID type accepted

Related test case: TC-PROD-08

Endpoint:
GET /products/{id}

Description:
API accepts non-numeric id values (e.g. "abc") and returns status 200 with empty body.

Steps to reproduce:
1. Send GET request to /products/abc

Expected result:
- Status code = 400 Bad Request (according to API documentation where id must be integer)

Actual result:
- Status code = 200
- Response body is empty.

Severity:
Low

<a name="bug02"></a>
## BUG-PROD-02 – Missing validation for required fields

Related test case: TC-PROD-09

Endpoint:
POST /products

Description:
API allows creating a product even when the required field "title" is missing.

Steps to reproduce:
1. Send POST request to /products
2. Use request body without "title":

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
- Validation error indicating missing required field "title" in payload.

Actual result:
- Status code = 201 Created  
- Product is created successfully and returned in response body.

Severity:
Medium

<a name="bug03"></a>
## BUG-PROD-03 – Product can be created with negative price

Related test case: TC-PROD-10

Endpoint:
POST /products

Description:
API allows creating a product with a negative price value.

Steps to reproduce:
1. Send POST request to /products
2. Use request body:

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
- Validation error indicating invalid price value.

Actual result:
- Status code = 201 Created  
- Product is created successfully with negative price.

Severity:
Medium

<a name="bug04"></a>
## BUG-PROD-04 – API accepts invalid data type for price

Related test case: TC-PROD-11

Endpoint:
PUT /products/{id}

Description:
API accepts invalid data type for the "price" field. Instead of a numeric value, a string value ("abc") is accepted and stored.

Steps to reproduce:
1. Send PUT request to /products/1
2. Use request body:

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
- Validation error indicating invalid data type for "price".

Actual result:
- Status code = 200 OK  
- Product is updated successfully with "price": "abc".

Severity:
Medium