# API Test Cases Catalog — AutomationExercise

## Summary
This catalog documents all **35 executable test scenarios** (`API-TC-01` to `API-TC-35`) covering all 14 REST API endpoints.

---

## Complete Test Scenarios Catalog

| TC ID | Module | Endpoint & Method | Scenario Description | Expected Status | Expected Response Code |
| :--- | :--- | :--- | :--- | :---: | :---: |
| **API-TC-01** | Products | `GET /api/productsList` | Fetch all products list | `200 OK` | `200` |
| **API-TC-02** | Products | `GET /api/productsList` | Validate products array structure & attributes | `200 OK` | `200` |
| **API-TC-03** | Products | `POST /api/productsList` | Submit POST method to read-only products endpoint | `405 Method Not Allowed` | `405` |
| **API-TC-04** | Brands | `GET /api/brandsList` | Fetch all brands list | `200 OK` | `200` |
| **API-TC-05** | Brands | `GET /api/brandsList` | Validate brands array schema & attributes | `200 OK` | `200` |
| **API-TC-06** | Brands | `PUT /api/brandsList` | Submit PUT method to read-only brands endpoint | `405 Method Not Allowed` | `405` |
| **API-TC-07** | Search | `POST /api/searchProduct` | Search product with keyword `tshirt` | `200 OK` | `200` |
| **API-TC-08** | Search | `POST /api/searchProduct` | Search product with keyword `jean` (Partial Match) | `200 OK` | `200` |
| **API-TC-09** | Search | `POST /api/searchProduct` | Search product with non-matching string `xyz999` | `200 OK` | `200` (Empty Array) |
| **API-TC-10** | Search | `POST /api/searchProduct` | Search product without `search_product` parameter | `400 Bad Request` | `400` |
| **API-TC-11** | Search | `POST /api/searchProduct` | Search product with empty string `search_product=""` | `200 OK` | `200` (Wildcard List) |
| **API-TC-12** | Auth | `POST /api/verifyLogin` | Authenticate with valid email and password | `200 OK` | `200` |
| **API-TC-13** | Auth | `POST /api/verifyLogin` | Authenticate with incorrect password | `404 Not Found` | `404` |
| **API-TC-14** | Auth | `POST /api/verifyLogin` | Authenticate without `email` parameter | `400 Bad Request` | `400` |
| **API-TC-15** | Auth | `POST /api/verifyLogin` | Authenticate without `password` parameter | `400 Bad Request` | `400` |
| **API-TC-16** | Auth | `POST /api/verifyLogin` | Authenticate with completely empty body | `400 Bad Request` | `400` *(Observed 404 - DEF-API-02)* |
| **API-TC-17** | Auth | `DELETE /api/verifyLogin` | Submit unsupported DELETE to login endpoint | `405 Method Not Allowed` | `405` |
| **API-TC-18** | CRUD | `POST /api/createAccount` | Register fresh user account with valid details | `201 Created` | `201` |
| **API-TC-19** | CRUD | `POST /api/createAccount` | Register duplicate email address | `400 Bad Request` | `400` |
| **API-TC-20** | CRUD | `POST /api/createAccount` | Register account without `name` parameter | `400 Bad Request` | `400` |
| **API-TC-21** | CRUD | `POST /api/createAccount` | Register account without `email` parameter | `400 Bad Request` | `400` |
| **API-TC-22** | CRUD | `POST /api/createAccount` | Register account without `password` parameter | `400 Bad Request` | `400` |
| **API-TC-23** | CRUD | `POST /api/createAccount` | Register account with completely empty payload | `400 Bad Request` | `400` |
| **API-TC-24** | CRUD | `GET /api/getUserDetailByEmail` | Retrieve details for existing user by email | `200 OK` | `200` |
| **API-TC-25** | CRUD | `GET /api/getUserDetailByEmail` | Retrieve details for non-existent email | `404 Not Found` | `404` |
| **API-TC-26** | CRUD | `GET /api/getUserDetailByEmail` | Retrieve details without `email` query parameter | `400 Bad Request` | `400` |
| **API-TC-27** | CRUD | `PUT /api/updateAccount` | Update existing user profile attributes | `200 OK` | `200` |
| **API-TC-28** | CRUD | `PUT /api/updateAccount` | Verify updated profile details via GET call | `200 OK` | `200` |
| **API-TC-29** | CRUD | `PUT /api/updateAccount` | Update profile without `email` identifier | `400 Bad Request` | `400` *(Observed 404 - DEF-API-03)* |
| **API-TC-30** | CRUD | `PUT /api/updateAccount` | Update non-existent user profile | `404 Not Found` | `404` |
| **API-TC-31** | CRUD | `DELETE /api/deleteAccount` | Delete existing user account | `200 OK` | `200` |
| **API-TC-32** | CRUD | `GET /api/getUserDetailByEmail` | Verify deleted account cannot be retrieved | `404 Not Found` | `404` |
| **API-TC-33** | Auth | `POST /api/verifyLogin` | Verify deleted account cannot authenticate | `404 Not Found` | `404` |
| **API-TC-34** | CRUD | `DELETE /api/deleteAccount` | Delete non-existent or already deleted account | `404 Not Found` | `404` |
| **API-TC-35** | E2E | Full Account Lifecycle | Validate unbroken sequential state chain | `200/201` | All Lifecycle Stages |

---

> **Note:** Detailed step-by-step preconditions and parameter payloads are also stored in [API_Test_Cases.xlsx](file:///c:/Users/prave/Downloads/qa-manual-api/03-Test-Cases/API_Test_Cases.xlsx).
