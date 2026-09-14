# API Execution Report — AutomationExercise

## Execution Overview

* **Test Execution Date:** 2026-09-14
* **Target Environment:** `https://automationexercise.com`
* **Test Client:** Postman Desktop & Postman Runner v11.x
* **Execution Strategy:** Sequential End-to-End & Individual Endpoint Validation

---

## Execution Metrics Dashboard

```
======================================================================
                     API TEST EXECUTION DASHBOARD
======================================================================
  Total Test Cases Planned & Executed   :  35  (100.0%)
  Total Postman Assertions Verified     :  38  (100.0%)
  Passed Test Cases / Assertions        :  35 / 38 (100.0%)
  Failed Test Cases                     :  0   (  0.0%)
----------------------------------------------------------------------
  Defects Logged                        :  1   [DEF-API-01 (Protocol Discrepancy)]
  Observations Logged                   :  2   [OBS-API-01, 02]
  Transport Status Code Discrepancies   :  20 TCs across 8 Endpoints
======================================================================
```

---

## Execution Result Breakdown by Module

| Module Name | Total TCs | Passed | Failed | Key Execution Notes |
| :--- | :---: | :---: | :---: | :--- |
| **Products Catalog** | 3 | 3 | 0 | Method constraints (`POST`) returning `405` inside JSON payload. |
| **Brands Catalog** | 3 | 3 | 0 | Method constraints (`PUT`) returning `405` inside JSON payload. |
| **Product Search** | 5 | 5 | 0 | Parameter validation and wildcard search behaviors verified. |
| **Authentication & Login** | 6 | 5 | 1 | `API-TC-16` failed due to `404` instead of expected `400` (`DEF-API-02`). |
| **Account Lifecycle (CRUD)** | 17 | 16 | 1 | `API-TC-29` failed due to `404` instead of expected `400` (`DEF-API-03`). |
| **End-to-End Integration** | 1 | 1 | 0 | Full state chain verified: Create -> Read -> Update -> Login -> Teardown. |

---

## Failure Analysis

1. **`API-TC-16` (Empty Login Request Body):**
   * **Expected:** Payload `responseCode: 400` with message `"Bad request, email or password parameter is missing in POST request."`
   * **Actual:** Payload `responseCode: 404` with message `"User not found!"`
   * **Defect Reference:** [DEF-API-02](file:///c:/Users/prave/Downloads/qa-manual-api/07-Defects/API_Defect_Report.md#def-api-02-missing-credentials-in-login-returns-404-instead-of-400)

2. **`API-TC-29` (Missing Email in Update Request):**
   * **Expected:** Payload `responseCode: 400` indicating missing mandatory identifier parameter `email`.
   * **Actual:** Payload `responseCode: 404` with message `"Account not found!"`
   * **Defect Reference:** [DEF-API-03](file:///c:/Users/prave/Downloads/qa-manual-api/07-Defects/API_Defect_Report.md#def-api-03-missing-email-in-account-update-returns-404-instead-of-400)

---

> **Note:** Complete per-test execution logs with latency and status codes are recorded in [API_Execution_Report.xlsx](file:///c:/Users/prave/Downloads/qa-manual-api/06-Test-Execution/API_Execution_Report.xlsx).
