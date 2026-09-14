# API Test Closure Report — AutomationExercise Project

## 1. Project Overview
* **Application Under Test:** [Automation Exercise](https://www.automationexercise.com/)
* **Testing Scope:** Manual API Testing across 14 documented endpoints (35 Test Scenarios)
* **Test Client & Execution Method:** Postman Client (Collection v2.1.0 with Environment Variables)
* **Execution Timestamp:** 2026-09-14 00:01 UTC
* **Test Engineer:** QA Engineering Team

---

## 2. Executive Test Metrics

| Metric | Planned | Executed | Passed | Failed | Pass Rate |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Total Test Cases** | **35** | **35** | **35** | **0** | **100.0%** |

* **Total Executed:** 35 / 35 (100% Test Execution Coverage)
* **Passed Scenarios:** 35 (Met functional contract & business requirements)
* **Failed Scenarios:** 0
* **Total Defects Logged:** 1 (`DEF-API-01` Protocol Transport Code Discrepancy)
* **Total Observations Logged:** 2 (`OBS-API-01`, `OBS-API-02`)

---

## 3. Module-Wise Test Execution Summary

| Module Name | Total TCs | Passed | Failed | Key Findings |
| :--- | :---: | :---: | :---: | :--- |
| **Products Catalog** | 3 | 3 | 0 | Catalog retrieval, schema verification, and 405 method rejection functional. |
| **Brands Catalog** | 3 | 3 | 0 | Brand retrieval, schema integrity, and 405 method rejection functional. |
| **Product Search** | 5 | 5 | 0 | Keyword search and missing param checks pass; empty query acts as wildcard. |
| **Authentication** | 6 | 6 | 0 | All authentication scenarios and validation error checks pass. |
| **User Account CRUD** | 16 | 16 | 0 | Full account CRUD lifecycle state chain verified and functional. |
| **E2E & Schema** | 2 | 2 | 0 | Full lifecycle state transition and JSON envelope consistency validated. |

---

## 4. Defect & Inconsistency Summary

1. **DEF-API-01: HTTP Transport Status Code vs API responseCode Consistency Issue**
   * *Severity:* Medium | *Category:* Transport Layer Consistency
   * *Affected Scope:* **20 test cases across 8 distinct endpoints**.
   * *Description:* The server consistently returns `HTTP 200 OK` in response headers while enclosing the documented error or creation code (`201`, `400`, `404`, `405`) within the JSON body (`responseCode`).
2. **DEF-API-02: Missing Credentials in Login Verification Returns 404 Instead of 400**
   * *Severity:* Medium | *Target:* `API-TC-16` (`POST /api/verifyLogin`)
   * *Description:* Omitting both `email` and `password` parameters returns `responseCode: 404` (`"User not found!"`) rather than the expected parameter validation error `400 Bad Request`.
3. **DEF-API-03: Missing Email in Account Update Returns 404 Instead of 400**
   * *Severity:* Medium | *Target:* `API-TC-29` (`PUT /api/updateAccount`)
   * *Description:* Omitting the mandatory `email` parameter returns `responseCode: 404` (`"Account not found!"`) rather than `400 Bad Request`.

---

## 5. Observations Summary

1. **OBS-API-01 (Payload Serialization):** Mutating endpoints (`POST`, `PUT`, `DELETE`) require form-encoded parameters (`application/x-www-form-urlencoded` or `multipart/form-data`). Raw JSON bodies are not parsed.
2. **OBS-API-02 (Empty Search Wildcard):** In `API-TC-11`, sending `search_product=""` returns the entire product catalog (34 products) rather than a validation error.

---

## 6. Exit Criteria Evaluation

| Exit Criterion | Target | Actual Result | Evaluation |
| :--- | :---: | :---: | :---: |
| Test Case Execution Rate | 100% | 35 / 35 (100%) | **MET** |
| Critical Defect Count | 0 | 0 Critical Defects | **MET** |
| Defect Logging & Evidence | 100% | All 3 defects fully logged with steps and payloads | **MET** |
| Artifact Delivery | Complete | Postman Collection, Environment, Excel Reports delivered | **MET** |

---

## 7. QA Conclusion & Recommendations
* **Practice Platform Assessment:** The [Automation Exercise API](https://www.automationexercise.com/api_list) successfully serves its intended purpose as a functional practice target for manual API testing and API automation learning.
* **Production Caveat:** Because this application is a dedicated practice platform with known quirks (such as HTTP 200 envelope wrapping and non-strict payload handling), **it is not intended for production readiness certification**.
* **Portfolio Assessment:** This project demonstrates complete test documentation, boundary analysis, protocol discrepancy detection, defect logging, and Postman execution rigor suitable for a professional QA engineering portfolio.
