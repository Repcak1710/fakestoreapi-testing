# Fake Store API Manual Testing Project

This repository contains manual API testing artifacts created while testing the Fake Store API.

API tested:
https://fakestoreapi.com

Testing includes:

- test case design
- test execution
- bug reporting
- exploratory testing

Tools used:
- Postman

Testing approach:
- Manual API testing

---

# Test Plan

General testing approach is described in:

[Test plan](./test_plan.md)

---

# Test Reports

Products API:  
[Products Test Report](./products/report.md)

Users API: TODO

Carts API: TODO

Auth API: TODO

---

# Postman Collection

The Postman collection used during testing is available here:

[Postman Collection](./FakeStoreAPI.postman_collection.json)

It contains requests used during manual testing of the API endpoints. 
The request names correspond to IDs used in the repository documentation.

---

# Overall Observations

Initial testing of the Products API revealed several validation issues:

- missing validation for required fields
- incorrect data types accepted
- HTML/JS input accepted without sanitization
- non-numeric IDs accepted

These findings are documented in the product testing report.