# API Test Plan — AutomationExercise Manual API Testing

## 1. Document Control
* **Project Name:** AutomationExercise Manual API Testing Project
* **Author:** QA Engineering
* **Document Version:** 1.0 (Final)
* **Date:** 2026-09-14
* **Testing Type:** Manual API Testing (Using Postman Client)

---

## 2. Objective
The primary objective of this project is to perform comprehensive, scenario-driven **Manual API Testing** of the [Automation Exercise REST API](https://www.automationexercise.com/api_list). The testing validates endpoint functionality, HTTP method constraints, mandatory input validation, error handling, JSON schema consistency, and end-to-end user account lifecycle integrity.

> **Important Note on Testing Methodology:**  
> This project represents **Manual API Testing executed via Postman**. While Postman collection scripts and assertions are utilized to evaluate status codes and payload structures systematically, the test design, data crafting, execution flow, response verification, and defect logging are driven manually by the QA tester. It is not an automated CI/CD framework.

---

## 3. Scope of Testing

### 3.1 In-Scope
* All 14 publicly documented REST API endpoints on `https://automationexercise.com/api_list`:
  * Products catalog retrieval (`GET`, `POST`)
  * Brands catalog retrieval (`GET`, `PUT`)
  * Product search functionality (`POST`)
  * User authentication & credential verification (`POST`, `DELETE`)
  * User account lifecycle: Create (`POST`), Read (`GET`), Update (`PUT`), Delete (`DELETE`)
* Validation of wire-level HTTP response status codes vs. application-level JSON `responseCode`.
* Form-encoded payload serialization (`x-www-form-urlencoded` / `multipart/form-data`).
* Total 35 approved test scenarios (`API-TC-01` to `API-TC-35`).

### 3.2 Out-of-Scope
* Non-functional testing (Performance, Load, Stress testing).
* Frontend web UI validation (covered in separate UI test suite).
* Security vulnerability / Penetration testing.
* Third-party payment gateway transaction processing.

---

## 4. Test Approach & Test Types
Testing is conducted manually using Postman to construct and trigger HTTP requests against the live server:
1. **Positive Functional Testing (Happy Path):** Validating successful data retrieval and valid resource creation.
2. **Negative & Boundary Testing:** Submitting invalid credentials, unregistered emails, and empty strings.
3. **HTTP Method Constraint Testing:** Submitting unsupported HTTP verbs (e.g., `POST` to `GET` endpoints, `PUT` to read-only lists, `DELETE` to login endpoint) to ensure proper rejection.
4. **Required Parameter Validation:** Omitting mandatory parameters (`email`, `password`, `search_product`, `name`) to verify validation error messaging.
5. **End-to-End CRUD Lifecycle State Testing:** Executing an unbroken state-transition chain: Create -> Read -> Update -> Read Verification -> Login Verification -> Delete -> Post-Deletion Verification.
6. **Response Schema & Envelope Validation:** Confirming root-level structure consistency across all endpoints (`responseCode`, `message`, `products`, `brands`, `user`).

---

## 5. Test Environment & Tools
* **Base URL:** `https://automationexercise.com`
* **Test Client:** Postman Desktop & Postman Web Client (v10 / v11)
* **Format Version:** Postman Collection Schema v2.1.0
* **Operating System:** Cross-platform (Windows / macOS / Linux)
* **Environment Variables:**
  * `{{base_url}}`: `https://automationexercise.com`
  * `{{test_email}}`: Dynamic unique test email (`postman_run_user_<timestamp>@example.com`)
  * `{{test_password}}`: Strong test password (`PostmanPass123!`)
  * `{{updated_firstname}}`: `PostmanUpdated`
  * `{{updated_city}}`: `San Francisco`

---

## 6. Test Data Strategy
* **Lifecycle Isolation:** A unique timestamped email is used for each execution run to prevent collisions with existing accounts.
* **Payload Format:** `application/x-www-form-urlencoded` is enforced for all mutating requests as required by the backend.
* **Boundary Inputs:** Special characters (`!@#$%^&*()`), empty strings (`""`), missing keys, and non-existent IDs.

---

## 7. Entry & Exit Criteria

### 7.1 Entry Criteria
* [Automation Exercise API](https://www.automationexercise.com/api_list) is accessible and online.
* Approved 35 API Test Cases specification is finalized.
* Postman Environment with active base URL and variables is configured.

### 7.2 Exit Criteria
* 100% of the 35 approved test cases are executed.
* All actual HTTP status codes, JSON response codes, latencies, and response payloads are logged.
* Any discrepancy between expected and actual behavior is documented as a Defect or Observation.
* Final deliverables (Test Cases, Test Data, Postman Collection/Environment, Execution Report, Defect Report, Closure Report) are completed and reconciled.

---

## 8. Defect Management & Classification
Defects are classified based on standard QA severity levels:
* **High:** Core transaction blocker or total failure of critical functionality.
* **Medium:** Deviation from documented contract, incorrect status code, or parameter validation bypass.
* **Low / Informational:** Minor message typos, undocumented behavior, or serialization constraints.

---

## 9. Risks and Mitigations
* **Risk 1: Practice Environment Volatility:** Automation Exercise is a public testing ground; shared data could cause collisions.  
  * *Mitigation:* Generate unique timestamped emails (`postman_run_user_<timestamp>@example.com`) and execute account deletion cleanup at the end of every run.
* **Risk 2: Status Code Layering:** Backend returns HTTP 200 with embedded error codes.  
  * *Mitigation:* Explicitly assert and report both the transport status code and the JSON `responseCode`.

---

## 10. Deliverables
1. `API_Requirements.md`
2. `API_Test_Plan.md`
3. `API_Test_Cases.xlsx`
4. `API_Test_Data.xlsx`
5. `AutomationExercise_API_Test_Suite.postman_collection.json`
6. `AutomationExercise.postman_environment.json`
7. `API_Execution_Report.xlsx`
8. `API_Defect_Report.xlsx`
9. `08-Evidence/execution-evidence/`
10. `API_Test_Closure_Report.md`
11. `README.md`
