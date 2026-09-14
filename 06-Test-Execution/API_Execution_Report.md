# API Execution Report — AutomationExercise

## Execution Overview

* **Test Execution Date:** 2026-09-14
* **Target Environment:** `https://automationexercise.com`
* **Test Client:** Postman Desktop & Postman Runner v11.x / Newman CLI
* **Execution Strategy:** Sequential End-to-End & Individual Endpoint Validation

---

## Execution Metrics Dashboard

```
======================================================================
                     API TEST EXECUTION DASHBOARD
======================================================================
  Total Test Cases Planned & Executed   :  35  (100.0%)
  Passed Test Cases                     :  35  (100.0%)
  Failed Test Cases                     :  0   (  0.0%)
  Passed Postman Assertions             :  38 / 38 (100.0%)
----------------------------------------------------------------------
  Total Defects Logged                  :  3   (1 Open, 2 Closed)
  Open Defects                          :  1   [DEF-API-01 (Protocol Discrepancy)]
  Resolved / Closed Defects             :  2   [DEF-API-02, DEF-API-03]
  Observations Logged                   :  2   [OBS-API-01, OBS-API-02]
  Transport Status Code Discrepancies   :  20 TCs across 8 Endpoints
======================================================================
```

---

## Execution Result Breakdown by Module

| Module Name | Total TCs | Passed | Failed | Key Execution Notes |
| :--- | :---: | :---: | :---: | :--- |
| **Products Catalog** | 3 | 3 | 0 | Catalog retrieval, schema checks, and method constraints (`POST`) verified. |
| **Brands Catalog** | 3 | 3 | 0 | Brand retrieval, schema integrity, and method constraints (`PUT`) verified. |
| **Product Search** | 5 | 5 | 0 | Keyword search and parameter checks pass; empty query acts as wildcard. |
| **Authentication & Login** | 6 | 6 | 0 | All authentication scenarios pass (`API-TC-16` verified with `400 Bad Request`). |
| **Account Lifecycle (CRUD)** | 16 | 16 | 0 | Full CRUD state chain verified (`API-TC-29` verified with `400 Bad Request`). |
| **End-to-End Integration & Schema** | 2 | 2 | 0 | Full lifecycle state transition (TC-34) and JSON envelope schema consistency (TC-35) validated. |

---

## Defect Retest & Anomaly Analysis

1. **`DEF-API-01` (Protocol Transport Status Code Discrepancy) — Status: OPEN**
   * **Scope:** 20 Test Cases across 8 Endpoints.
   * **Description:** Server returns transport-level `HTTP 200 OK` across error/mutation endpoints while encapsulating application status codes (`201`, `400`, `404`, `405`) inside the JSON response envelope (`responseCode`).
   * **Defect Reference:** [API_Defect_Report.md](../07-Defects/API_Defect_Report.md#def-api-01-http-transport-status-code-vs-api-responsecode-discrepancy)

2. **`DEF-API-02` (Missing Credentials in Login) — Status: CLOSED / VERIFIED**
   * **Target:** `API-TC-16` (`POST /api/verifyLogin`)
   * **Retest Result:** Previous execution logged 404; latest execution verified returning expected `400 Bad Request` payload (`"Bad request, email or password parameter is missing in POST request."`). Defect marked **Closed**.
   * **Defect Reference:** [API_Defect_Report.md](../07-Defects/API_Defect_Report.md#def-api-02-missing-credentials-in-login-returns-404-instead-of-400)

3. **`DEF-API-03` (Missing Email in Account Update) — Status: CLOSED / VERIFIED**
   * **Target:** `API-TC-29` (`PUT /api/updateAccount`)
   * **Retest Result:** Previous execution logged 404; latest execution verified returning expected `400 Bad Request` payload (`"Bad request, email parameter is missing in PUT request."`). Defect marked **Closed**.
   * **Defect Reference:** [API_Defect_Report.md](../07-Defects/API_Defect_Report.md#def-api-03-missing-email-in-account-update-returns-404-instead-of-400)

---

> **Note:** Complete per-test execution logs with latency, status codes, and payload signatures are recorded in [API_Execution_Report.xlsx](API_Execution_Report.xlsx).
