# Exploratory Testing – Products API

## Scope
Exploratory testing of product creation and validation behavior.

## Environment
- Tool: Postman
- API: FakeStoreAPI
- Base URL: https://fakestoreapi.com

---

## Session 1 – Invalid and unusual payloads for POST /products

### ET-PROD-01 – Empty JSON body
Request:
POST /products

Payload:
```json
{}
```

Result:

API response: 201 Created  
Response body:

```json
{
  "id": 21
}
```

Observation:
API allows creation of a product with an empty request body. No validation of required product fields was performed and only an ID was returned.

---

### ET-PROD-02 – Null price value
Request:
POST /products

Payload:
```json
{
  "title": "Null price test",
  "price": null,
  "description": "Exploratory test",
  "category": "electronics",
  "image": "https://i.pravatar.cc"
}
```

Result:

API response: 201 Created  
Response body:

```json
{
    "id": 21,
    "title": "Null price test",
    "price": null,
    "description": "Exploratory test",
    "image": "https://i.pravatar.cc",
    "category": "electronics"
}
```

Observation:
API accepts `null` value for the numeric field `price` and creates the product successfully. No validation of required numeric fields was performed.

---

### ET-PROD-03 – Null category value
Request:
POST /products

Payload:
```json
{
  "title": "Null category test",
  "price": 19.99,
  "description": "Exploratory test",
  "category": null,
  "image": "https://i.pravatar.cc"
}
```

Result:
API response: 201 Created  
Response body:

```json
{
    "id": 21,
    "title": "Null category test",
    "price": 19.99,
    "description": "Exploratory test",
    "image": "https://i.pravatar.cc",
    "category": null
}
```

Observation:
API accepts `null` value for the category field and still creates the product. No validation of required product fields was performed.

---

### ET-PROD-04 – Array instead of price
Request:
POST /products

Payload:
```json
{
  "title": "Array price test",
  "price": [19.99],
  "description": "Exploratory test",
  "category": "electronics",
  "image": "https://i.pravatar.cc"
}
```

Result:
API response: 201 Created  

Response body:

```json
{
  "id": 21,
  "title": "Array price test",
  "price": [
    19.99
  ],
  "description": "Exploratory test",
  "image": "https://i.pravatar.cc",
  "category": "electronics"
}
```

Observation:
API accepts an array value for the `price` field and still creates the product. No validation of numeric field types was performed.

---

### ET-PROD-05 – HTML/JS code in title
Request:
POST /products

Payload:
```json
{
  "title": "<script>alert('x')</script>",
  "price": 19.99,
  "description": "Exploratory test",
  "category": "electronics",
  "image": "https://i.pravatar.cc"
}
```

Result:
API response: 201 Created  

Response body:

```json
{
  "id": 21,
  "title": "<script>alert('x')</script>",
  "price": 19.99,
  "description": "Exploratory test",
  "image": "https://i.pravatar.cc",
  "category": "electronics"
}
```

Observation:
API accepts HTML/JavaScript code in the `title` field and creates the product successfully. No input sanitization was observed.

---

## Summary

Main findings:
- API accepts empty request body and creates a product with only an ID.
- API accepts null values for product fields such as price and category.
- No validation of numeric field types was observed (e.g., array accepted as price).
- API accepts HTML/JavaScript input in text fields without sanitization.