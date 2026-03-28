# Products test execution report

| Test ID | Status | Notes |
|-------|------|------|
| TC-PROD-01 | PASS | Products returned correctly |
| TC-PROD-02 | PASS | Product ID 1 returned correctly |
| TC-PROD-03 | PASS | All returned products have category "electronics" |
| TC-PROD-04 | PASS | Product created (simulated response) |
| TC-PROD-05 | PASS | Update endpoint returns modified payload |
| TC-PROD-06 | PASS | Response returned deleted product data |
| TC-PROD-07 | PASS | API returned status 200 with empty response body for non-existing product ID |
| TC-PROD-08 | FAIL | API returned status 200 with empty body for invalid id type. According to documentation id must be integer and request should return 400. See [BUG-PROD-01](./bug-reports.md#bug01)|
| TC-PROD-09 | FAIL | API allows creating product without required field "title". See [BUG-PROD-02](./bug-reports.md#bug02) |
| TC-PROD-10 | FAIL | API allows creating product with negative price. See [BUG-PROD-03](./bug-reports.md#bug03) |
| TC-PROD-11 | FAIL |  API accepts invalid data type for price ("abc"). See [BUG-PROD-04](./bug-reports.md#bug04) |
| TC-PROD-12 | PASS | API correctly rejects non-numeric product ID (400 Bad Request) |
| TC-PROD-13 | PASS | Product created successfully with extremely large price value |
| TC-PROD-14 | PASS | API handled very long title without error |
| TC-PROD-15 | PASS | Product created successfully with special characters in title |