# API Defect Report — AutomationExercise

## Executive Summary
This document provides a detailed breakdown of all defects, protocol anomalies, defect lifecycle states (Open vs Closed), and observation logs for the **AutomationExercise REST API**.

---

## Defect Summary Table

| Defect ID | Severity | Category | Target Endpoint / TCs | Summary Description | Lifecycle Status |
| :--- | :---: | :---: | :---: | :--- | :---: |
| **DEF-API-01** | Medium | Protocol Consistency | 20 TCs across 8 Endpoints | **HTTP Transport Status Code vs Payload Consistency Issue**: Server returns wire status `HTTP 200 OK` while embedding application status codes (`201`, `400`, `404`, `405`) inside the JSON response body. | **Open / Active** |
| **DEF-API-02** | Medium | Validation Error Handling | `API-TC-16` (`POST /api/verifyLogin`) | **Missing Credentials in Login**: Previous run logged 404; retested and verified returning expected `400 Bad Request` payload in latest execution. | **Closed / Verified** |
| **DEF-API-03** | Medium | Validation Error Handling | `API-TC-29` (`PUT /api/updateAccount`) | **Missing Email in Account Update**: Previous run logged 404; retested and verified returning expected `400 Bad Request` payload in latest execution. | **Closed / Verified** |

---

## Detailed Defect Breakdown

### DEF-API-01: HTTP Transport Status Code vs API `responseCode` Discrepancy
* **Severity:** Medium
* **Priority:** High
* **Status:** **Open / Active**
* **Component:** Global API Transport Layer
* **Affected Scenarios:** 20 Test Cases across 8 Endpoints
* **Description:** 
  Standard REST API architectural design requires HTTP wire status codes (e.g., `201 Created`, `400 Bad Request`, `404 Not Found`, `405 Method Not Allowed`) to align with payload execution statuses. On the AutomationExercise API, the server returns wire `HTTP 200 OK` for almost all calls, embedding the actual status inside `jsonData.responseCode`.
* **Impact:** 
  Client-side HTTP libraries (such as Axios, Fetch, or Retrofit) fail to trigger standard catch/error handlers because the HTTP transport reports success (`200 OK`).

---

### DEF-API-02: Missing Credentials in Login Verification Returns 404 Instead of 400
* **Severity:** Medium
* **Priority:** Medium
* **Status:** **Closed / Verified** (Retested & Verified in latest run)
* **Target:** `POST /api/verifyLogin` (`API-TC-16`)
* **Preconditions:** Valid endpoint URI.
* **Retest Note:** Previous execution logged `responseCode: 404` (`"User not found!"`). Retest with form-encoded request body verified expected `responseCode: 400` (`"Bad request, email or password parameter is missing in POST request."`). Marked **Closed**.

---

### DEF-API-03: Missing Email in Account Update Returns 404 Instead of 400
* **Severity:** Medium
* **Priority:** Medium
* **Status:** **Closed / Verified** (Retested & Verified in latest run)
* **Target:** `PUT /api/updateAccount` (`API-TC-29`)
* **Preconditions:** Valid user session / updated fields available.
* **Retest Note:** Previous execution logged `responseCode: 404` (`"Account not found!"`). Retest with form-encoded request body verified expected `responseCode: 400` (`"Bad request, email parameter is missing in PUT request."`). Marked **Closed**.

---

## Logged Observations

### OBS-API-01: Payload Serialization Requirement
* **Category:** API Payload Processing
* **Observation:** The backend only accepts form-encoded parameter bodies (`application/x-www-form-urlencoded` or `multipart/form-data`). Raw `application/json` request bodies are ignored or parsed as empty requests.

### OBS-API-02: Empty String Wildcard Behavior in Search
* **Category:** Search API Logic
* **Observation:** Submitting `POST /api/searchProduct` with parameter `search_product=""` returns all 34 products in the catalog instead of a validation error or empty result.
