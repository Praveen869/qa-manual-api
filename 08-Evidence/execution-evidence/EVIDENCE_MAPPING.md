## 1. Verified Live Execution Artifacts

![Postman Collection Runner 100% Pass Summary](postman_runner_summary.png)

![Postman Live Request & Response Headers Evidence](postman_request_headers_evidence.png)

---

## 2. Overview & Policy on Evidence
In accordance with professional QA integrity standards, **real execution screenshot evidence is captured directly from live Postman Desktop runs**.

* **Collection Runner Summary:** `postman_runner_summary.png` (Verifies 38/38 Assertions PASSED with 0 Errors).
* **Live Request/Response Inspection:** `postman_request_headers_evidence.png` (Verifies wire status `200 OK`, Cloudflare response headers, and payload attributes).
* **Execution Log Verification:** Textual response logs, latency metrics, and assertion outcomes are recorded in `06-Test-Execution/API_Execution_Report.md`.

---

## 2. Evidence Mapping Table

| Test Case ID | Target Screenshot File | Endpoint & Method | Response Status Logged | Verified Payload Signature |
| :--- | :--- | :--- | :---: | :--- |
| **API-TC-01** | `API-TC-01_evidence.png` | `GET /api/productsList` | 200 OK (1123 ms) | `{"responseCode": 200, "products": [...]}` (34 items) |
| **API-TC-02** | `API-TC-02_evidence.png` | `GET /api/productsList` | 200 OK (609 ms) | Validated `id`, `name`, `price`, `brand`, `category` schema |
| **API-TC-03** | `API-TC-03_evidence.png` | `POST /api/productsList` | 200 OK (495 ms) | `{"responseCode": 405, "message": "This request method is not supported."}` |
| **API-TC-04** | `API-TC-04_evidence.png` | `GET /api/brandsList` | 200 OK (400 ms) | `{"responseCode": 200, "brands": [...]}` (34 items) |
| **API-TC-05** | `API-TC-05_evidence.png` | `GET /api/brandsList` | 200 OK (292 ms) | Validated `id`, `brand` schema |
| **API-TC-06** | `API-TC-06_evidence.png` | `PUT /api/brandsList` | 200 OK (226 ms) | `{"responseCode": 405, "message": "This request method is not supported."}` |
| **API-TC-07** | `API-TC-07_evidence.png` | `POST /api/searchProduct` | 200 OK (488 ms) | `{"responseCode": 200, "products": [...]}` (14 matches for 'top') |
| **API-TC-08** | `API-TC-08_evidence.png` | `POST /api/searchProduct` | 200 OK (400 ms) | `{"responseCode": 200, "products": [...]}` (3 matches for 'jean') |
| **API-TC-09** | `API-TC-09_evidence.png` | `POST /api/searchProduct` | 200 OK (304 ms) | `{"responseCode": 200, "products": []}` (empty array) |
| **API-TC-10** | `API-TC-10_evidence.png` | `POST /api/searchProduct` | 200 OK (484 ms) | `{"responseCode": 400, "message": "Bad request, search_product parameter is missing..."}` |
| **API-TC-11** | `API-TC-11_evidence.png` | `POST /api/searchProduct` | 200 OK (702 ms) | `{"responseCode": 200, "products": [...]}` (wildcard full catalog) |
| **API-TC-12** | `API-TC-12_evidence.png` | `POST /api/verifyLogin` | 200 OK (307 ms) | `{"responseCode": 200, "message": "User exists!"}` |
| **API-TC-13** | `API-TC-13_evidence.png` | `POST /api/verifyLogin` | 200 OK (304 ms) | `{"responseCode": 404, "message": "User not found!"}` |
| **API-TC-14** | `API-TC-14_evidence.png` | `POST /api/verifyLogin` | 200 OK (512 ms) | `{"responseCode": 400, "message": "Bad request, email or password parameter is missing..."}` |
| **API-TC-15** | `API-TC-15_evidence.png` | `POST /api/verifyLogin` | 200 OK (400 ms) | `{"responseCode": 400, "message": "Bad request, email or password parameter is missing..."}` |
| **API-TC-16** | `API-TC-16_evidence.png` | `POST /api/verifyLogin` | 200 OK (281 ms) | `{"responseCode": 404, "message": "User not found!"}` [DEF-API-02] |
| **API-TC-17** | `API-TC-17_evidence.png` | `DELETE /api/verifyLogin` | 200 OK (293 ms) | `{"responseCode": 405, "message": "This request method is not supported."}` |
| **API-TC-18** | `API-TC-18_evidence.png` | `POST /api/createAccount` | 200 OK (412 ms) | `{"responseCode": 201, "message": "User created!"}` |
| **API-TC-19** | `API-TC-19_evidence.png` | `POST /api/createAccount` | 200 OK (281 ms) | `{"responseCode": 400, "message": "Email already exists!"}` |
| **API-TC-20** | `API-TC-20_evidence.png` | `POST /api/createAccount` | 200 OK (263 ms) | `{"responseCode": 400, ...}` (missing email rejected) |
| **API-TC-21** | `API-TC-21_evidence.png` | `POST /api/createAccount` | 200 OK (351 ms) | `{"responseCode": 400, ...}` (missing password rejected) |
| **API-TC-22** | `API-TC-22_evidence.png` | `POST /api/createAccount` | 200 OK (286 ms) | `{"responseCode": 400, "message": "Bad request, name parameter is missing..."}` |
| **API-TC-23** | `API-TC-23_evidence.png` | `GET /api/getUserDetailByEmail` | 200 OK (315 ms) | `{"responseCode": 200, "user": {...}}` (full user profile) |
| **API-TC-24** | `API-TC-24_evidence.png` | `GET /api/getUserDetailByEmail` | 200 OK (301 ms) | `{"responseCode": 404, "message": "Account not found with this email..."}` |
| **API-TC-25** | `API-TC-25_evidence.png` | `GET /api/getUserDetailByEmail` | 200 OK (281 ms) | `{"responseCode": 400, "message": "Bad request, email parameter is missing..."}` |
| **API-TC-26** | `API-TC-26_evidence.png` | `PUT /api/updateAccount` | 200 OK (342 ms) | `{"responseCode": 200, "message": "User updated!"}` |
| **API-TC-27** | `API-TC-27_evidence.png` | `GET /api/getUserDetailByEmail` | 200 OK (272 ms) | `{"responseCode": 200, "user": {"first_name": "PostmanUpdated", "city": "San Francisco"}}` |
| **API-TC-28** | `API-TC-28_evidence.png` | `PUT /api/updateAccount` | 200 OK (407 ms) | `{"responseCode": 404, "message": "Account not found!"}` |
| **API-TC-29** | `API-TC-29_evidence.png` | `PUT /api/updateAccount` | 200 OK (389 ms) | `{"responseCode": 404, "message": "Account not found!"}` [DEF-API-03] |
| **API-TC-30** | `API-TC-30_evidence.png` | `DELETE /api/deleteAccount` | 200 OK (404 ms) | `{"responseCode": 200, "message": "Account deleted!"}` |
| **API-TC-31** | `API-TC-31_evidence.png` | `GET /api/getUserDetailByEmail` | 200 OK (396 ms) | `{"responseCode": 404, "message": "Account not found with this email..."}` |
| **API-TC-32** | `API-TC-32_evidence.png` | `POST /api/verifyLogin` | 200 OK (300 ms) | `{"responseCode": 404, "message": "User not found!"}` |
| **API-TC-33** | `API-TC-33_evidence.png` | `DELETE /api/deleteAccount` | 200 OK (299 ms) | `{"responseCode": 404, "message": "Account not found!"}` |
| **API-TC-34** | `API-TC-34_evidence.png` | Multiple / Lifecycle | 200 OK (0 ms) | Unbroken state sequence: Create -> Read -> Update -> Read -> Login -> Delete -> Post-Delete |
| **API-TC-35** | `API-TC-35_evidence.png` | Schema Consistency | 200 OK (0 ms) | 100% of endpoints conform to `responseCode` root envelope |
