# Products API – Test Summary Report

## Scope
Testing of the `Products` endpoints from FakeStoreAPI.

Base URL:
https://fakestoreapi.com

Tested endpoints:

- GET /products
- GET /products/{id}
- GET /products/category/{category}
- POST /products
- PUT /products/{id}
- DELETE /products/{id}

---

# Test Coverage

The following testing techniques were used:
- Functional test cases
- Negative test cases
- Edge case testing
- Exploratory testing

Artifacts created:
- Test cases
- Test execution log
- Bug reports
- Postman collection
- Exploratory testing notes

---

# Test Results

Total test cases executed: **15**

Result summary:

| Result | Count |
|------|------|
| Passed | 11 |
| Failed | 4 |
| Blocked | 0 |

(Note: FakeStoreAPI simulates some operations, therefore some behaviors may differ from real production APIs.)

---

# Key Findings

During testing several validation issues were observed:

1. API accepts non-numeric product IDs.
2. API accepts invalid payload structures.
3. Required fields are not validated consistently.
4. API allows unexpected data types (e.g. arrays for numeric fields).
5. HTML/JavaScript input is accepted without sanitization.

These behaviors do not crash the API but indicate **missing validation rules**.

---

# Reported Bugs

Bug reports created:

- BUG-PROD-01 – Invalid ID type accepted
- BUG-PROD-02 – Missing validation for required fields
- BUG-PROD-03 – Product can be created with negative price
- BUG-PROD-04 – API accepts invalid data type for price

(See [bug-reports.md](./bug-reports.md) for details.)

---

# Exploratory Testing

Exploratory testing focused on payload validation for product creation.

Key observations:

- API accepts empty request bodies
- API accepts null values
- API accepts incorrect data types
- API does not sanitize HTML/JS input

Details available in: [exploratory-testing.md](./exploratory-testing.md)


---

# Limitations

FakeStoreAPI simulates data persistence.  
Some operations (POST / PUT / DELETE) may not permanently modify server data.

Because of this limitation:

- some validation scenarios cannot be fully verified
- behavior may not reflect real production APIs

---

# Tools Used

- Postman
- Markdown documentation
- Manual API testing

---

# Status

Products API testing: **Completed**