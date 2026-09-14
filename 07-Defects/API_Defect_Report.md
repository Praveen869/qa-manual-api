# API Defect Report — AutomationExercise

## Executive Summary
This document provides a detailed breakdown of all defects, protocol anomalies, and observation logs discovered during the execution of the 35 API test cases against the **AutomationExercise REST API**.

---

## Defect Summary Table

| Defect ID | Severity | Category | Target Endpoint / TCs | Summary Description | Status |
| :--- | :---: | :---: | :---: | :--- | :---: |
| **DEF-API-01** | Medium | Protocol Consistency | 20 TCs across 8 Endpoints | **HTTP Transport Status Code vs Payload Consistency Issue**: Server returns wire status `HTTP 200 OK` while embedding application status codes (`201`, `400`, `404`, `405`) inside the JSON response body. | Open / Reported |
| **DEF-API-02** | Medium | Validation Error Handling | `API-TC-16` (`POST /api/verifyLogin`) | **Missing Credentials in Login Returns 404 Instead of 400**: Sending empty request body returns `responseCode: 404` (`"User not found!"`) instead of `400 Bad Request`. | Open / Reported |
| **DEF-API-03** | Medium | Validation Error Handling | `API-TC-29` (`PUT /api/updateAccount`) | **Missing Email in Account Update Returns 404 Instead of 400**: Omitting mandatory `email` field returns `responseCode: 404` (`"Account not found!"`) instead of `400 Bad Request`. | Open / Reported |

---

## Detailed Defect Breakdown

### DEF-API-01: HTTP Transport Status Code vs API `responseCode` Discrepancy
* **Severity:** Medium
* **Priority:** High
* **Component:** Global API Transport Layer
* **Affected Scenarios:** 20 Test Cases across 8 Endpoints
* **Description:** 
  Standard REST API architectural design requires HTTP wire status codes (e.g., `201 Created`, `400 Bad Request`, `404 Not Found`, `405 Method Not Allowed`) to align with payload execution statuses. On the AutomationExercise API, the server returns wire `HTTP 200 OK` for almost all calls, embedding the actual status inside `jsonData.responseCode`.
* **Impact:** 
  Client-side HTTP libraries (such as Axios, Fetch, or Retrofit) fail to trigger standard catch/error handlers because the HTTP transport reports success (`200 OK`).

---

### DEF-API-02: Missing Credentials in Login Returns `404` Instead of `400`
* **Severity:** Medium
* **Priority:** Medium
* **Target:** `POST /api/verifyLogin` (`API-TC-16`)
* **Preconditions:** Valid endpoint URI.
* **Steps to Reproduce:**
  1. Trigger `POST https://automationexercise.com/api/verifyLogin` with an empty request body (no `email` and no `password` parameters).
  2. Inspect the JSON response payload.
* **Expected Result:**
  Response should be `responseCode: 400` with message `"Bad request, email or password parameter is missing in POST request."`
* **Actual Result:**
  Server returns `responseCode: 404` with message `"User not found!"`.

---

### DEF-API-03: Missing Email in Account Update Returns `404` Instead of `400`
* **Severity:** Medium
* **Priority:** Medium
* **Target:** `PUT /api/updateAccount` (`API-TC-29`)
* **Preconditions:** Valid user session / updated fields available.
* **Steps to Reproduce:**
  1. Trigger `PUT https://automationexercise.com/api/updateAccount` with body parameters (`name`, `city`, `password`) but **omit** the mandatory `email` parameter.
  2. Inspect the JSON response payload.
* **Expected Result:**
  Server should return `responseCode: 400` indicating missing mandatory identifier parameter `email`.
* **Actual Result:**
  Server returns `responseCode: 404` with message `"Account not found!"`.

---

## Logged Observations

### OBS-API-01: Payload Serialization Requirement
* **Category:** API Payload Processing
* **Observation:** The backend only accepts form-encoded parameter bodies (`application/x-www-form-urlencoded` or `multipart/form-data`). Raw `application/json` request bodies are ignored or parsed as empty requests.

### OBS-API-02: Empty String Wildcard Behavior in Search
* **Category:** Search API Logic
* **Observation:** Submitting `POST /api/searchProduct` with parameter `search_product=""` returns all 34 products in the catalog instead of a validation error or empty result.
