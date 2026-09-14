# API Requirements Specification — AutomationExercise

## 1. Application Overview
* **Application Under Test:** [Automation Exercise](https://www.automationexercise.com/)
* **Application Type:** Practice E-commerce Web Application for QA Engineers
* **API Documentation Source:** [Automation Practice for API Testing Documentation](https://www.automationexercise.com/api_list)
* **Base URL:** `https://automationexercise.com`
* **API Scope:** All 14 publicly documented REST API endpoints covering Products Catalog, Brands, Product Search, Authentication, and User Account Lifecycle Management.

---

## 2. API Endpoints & Contract Specifications

### 2.1 Products Catalog Module
1. **GET `/api/productsList`**
   * **Purpose:** Retrieve complete catalog of all available products.
   * **Parameters:** None.
   * **Documented Response:** Status `200 OK`.
   * **Documented Body:** JSON object containing `responseCode: 200` and `products` array with attributes: `id` (int), `name` (string), `price` (string), `brand` (string), `category` (object with `usertype` and `category`).
2. **POST `/api/productsList`**
   * **Purpose:** Method constraint verification on read-only products endpoint.
   * **Parameters:** None.
   * **Documented Response:** Status `405 Method Not Supported`.
   * **Documented Body:** `responseCode: 405`, `message: "This request method is not supported."`

### 2.2 Brands Module
3. **GET `/api/brandsList`**
   * **Purpose:** Retrieve complete list of all brands.
   * **Parameters:** None.
   * **Documented Response:** Status `200 OK`.
   * **Documented Body:** JSON object containing `responseCode: 200` and `brands` array with attributes: `id` (int) and `brand` (string).
4. **PUT `/api/brandsList`**
   * **Purpose:** Method constraint verification on read-only brands endpoint.
   * **Parameters:** None.
   * **Documented Response:** Status `405 Method Not Supported`.
   * **Documented Body:** `responseCode: 405`, `message: "This request method is not supported."`

### 2.3 Product Search Module
5. **POST `/api/searchProduct` (With Query)**
   * **Purpose:** Search products by keyword.
   * **Parameters:** `search_product` (String, required; e.g., `top`, `tshirt`, `jean`).
   * **Documented Response:** Status `200 OK`.
   * **Documented Body:** `responseCode: 200`, `products` array matching query.
6. **POST `/api/searchProduct` (Without Query)**
   * **Purpose:** Parameter validation when search query parameter is omitted.
   * **Parameters:** None.
   * **Documented Response:** Status `400 Bad Request`.
   * **Documented Body:** `responseCode: 400`, `message: "Bad request, search_product parameter is missing in POST request."`

### 2.4 Authentication & Login Verification Module
7. **POST `/api/verifyLogin` (Valid Credentials)**
   * **Purpose:** Authenticate an existing user account.
   * **Parameters:** `email` (String, required), `password` (String, required).
   * **Documented Response:** Status `200 OK`.
   * **Documented Body:** `responseCode: 200`, `message: "User exists!"`
8. **POST `/api/verifyLogin` (Missing Parameters)**
   * **Purpose:** Parameter validation when email or password is omitted.
   * **Parameters:** Only one or neither provided.
   * **Documented Response:** Status `400 Bad Request`.
   * **Documented Body:** `responseCode: 400`, `message: "Bad request, email or password parameter is missing in POST request."`
9. **POST `/api/verifyLogin` (Invalid Credentials)**
   * **Purpose:** Authentication failure handling for non-existent or incorrect credentials.
   * **Parameters:** `email` (invalid), `password` (invalid).
   * **Documented Response:** Status `404 Not Found`.
   * **Documented Body:** `responseCode: 404`, `message: "User not found!"`
10. **DELETE `/api/verifyLogin`**
    * **Purpose:** Method constraint verification on login endpoint.
    * **Parameters:** None.
    * **Documented Response:** Status `405 Method Not Supported`.
    * **Documented Body:** `responseCode: 405`, `message: "This request method is not supported."`

### 2.5 User Account Lifecycle & Management (CRUD Module)
11. **POST `/api/createAccount`**
    * **Purpose:** Register/Create a new user account profile.
    * **Parameters:** `name`, `email`, `password`, `title`, `birth_date`, `birth_month`, `birth_year`, `firstname`, `lastname`, `company`, `address1`, `address2`, `country`, `zipcode`, `state`, `city`, `mobile_number`.
    * **Documented Response:** Status `201 Created`.
    * **Documented Body:** `responseCode: 201`, `message: "User created!"`
12. **GET `/api/getUserDetailByEmail`**
    * **Purpose:** Retrieve profile details for an existing user account.
    * **Parameters:** `email` (Query Parameter, required).
    * **Documented Response:** Status `200 OK`.
    * **Documented Body:** `responseCode: 200`, `user` object containing all profile attributes.
13. **PUT `/api/updateAccount`**
    * **Purpose:** Update profile attributes of an existing user.
    * **Parameters:** Profile attributes with updated values (identified by mandatory `email`).
    * **Documented Response:** Status `200 OK`.
    * **Documented Body:** `responseCode: 200`, `message: "User updated!"`
14. **DELETE `/api/deleteAccount`**
    * **Purpose:** Permanently remove an existing user account.
    * **Parameters:** `email` (String, required), `password` (String, required).
    * **Documented Response:** Status `200 OK`.
    * **Documented Body:** `responseCode: 200`, `message: "Account deleted!"`

---

## 3. End-to-End Account Lifecycle Requirements
To validate end-to-end transactional integrity, the system must support an uninterrupted sequential state transition:
1. **Create Account:** Register a fresh, unique email address (`POST /api/createAccount` -> `201`).
2. **Read Details:** Verify database persistence and accurate field retrieval (`GET /api/getUserDetailByEmail` -> `200`).
3. **Update Details:** Modify specific user attributes such as Firstname and City (`PUT /api/updateAccount` -> `200`).
4. **Verify Update:** Confirm modified fields reflect updated values (`GET /api/getUserDetailByEmail` -> `200`).
5. **Verify Login:** Confirm user can authenticate with the active credentials (`POST /api/verifyLogin` -> `200`).
6. **Delete Account:** Execute account teardown/cleanup (`DELETE /api/deleteAccount` -> `200`).
7. **Post-Deletion Assertions:** Ensure deleted records cannot be fetched (`GET` -> `404`) and cannot authenticate (`POST` -> `404`).

---

## 4. Documented vs. Observed Behavior Distinction

| Feature / Behavior | Documented Requirement | Observed Execution Behavior | Classification |
| :--- | :--- | :--- | :--- |
| **HTTP Transport Status Code** | Endpoints return distinct HTTP codes (`201`, `400`, `404`, `405`). | Server consistently returns wire status `HTTP 200 OK`; the documented status is embedded inside JSON `responseCode`. | **DEF-API-01** |
| **Empty Login Body** (`API-TC-16`) | Missing credentials should trigger missing parameter validation (`400 Bad Request`). | Server bypassed parameter check and returned `responseCode: 404` (`"User not found!"`). | **DEF-API-02** |
| **Missing Email in Update** (`API-TC-29`) | Missing mandatory identifier `email` should trigger validation error (`400 Bad Request`). | Server returned `responseCode: 404` (`"Account not found!"`). | **DEF-API-03** |
| **Request Payload Encoding** | Documented as general request parameters. | Only `application/x-www-form-urlencoded` and `multipart/form-data` are accepted; raw JSON bodies fail to parse. | **OBS-API-01** |
| **Empty Search String** (`API-TC-11`) | Not explicitly specified in documentation. | Passing `search_product=""` acts as a wildcard returning all products rather than an error. | **Observation / Ambiguity** |
