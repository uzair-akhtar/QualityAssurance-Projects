# 🔌 REST API Testing — ReqRes Public API

**Project Type:** API Testing  
**Tools Used:** Postman  
**API Under Test:** [ReqRes.in](https://reqres.in) — A hosted REST API for testing  
**Status:** ✅ Complete

---

## 📌 Project Overview

This project demonstrates structured API testing against the ReqRes public REST API. The goal was to validate all four core HTTP methods (GET, POST, PUT, DELETE), verify correct status codes, and confirm the integrity of request/response payloads including headers and JSON structures.

ReqRes simulates a real user management backend — making it an ideal sandbox for practising the same testing techniques used in production Fintech and SaaS applications.

---

## 🎯 What I Tested

The testing covered the complete CRUD lifecycle of a user resource:

**GET** — Retrieving lists and individual user records, verifying pagination and correct data fields.  
**POST** — Creating new users and verifying the server returns a 201 Created response with the correct body.  
**PUT** — Updating existing records and confirming the response reflects the changes.  
**DELETE** — Removing a resource and verifying the server returns 204 No Content with an empty body.

Beyond the happy path, I tested negative scenarios including invalid endpoints (404), missing required fields (400), and unauthorized access (401).

---

## 📂 Folder Structure

```
rest-api-testing/
├── README.md                        ← You are here
├── test-cases.md                    ← All test cases in table format
├── postman-collection.json          ← Import this into Postman to run all tests
└── screenshots/
    ├── TC001-get-users-200.png
    ├── TC002-get-single-user-200.png
    ├── TC003-get-invalid-user-404.png
    ├── TC004-post-create-user-201.png
    ├── TC005-put-update-user-200.png
    └── TC006-delete-user-204.png
```

---

## 🔧 How to Run These Tests

**Step 1:** Install [Postman](https://www.postman.com/downloads/) if you haven't already.  
**Step 2:** Open Postman → click **Import** → select `postman-collection.json` from this folder.  
**Step 3:** Click **Run Collection** to execute all requests automatically.  
**Step 4:** Review the test results in the Postman Runner — all assertions are written as test scripts inside each request.

---

## ✅ Test Summary

| HTTP Method | Endpoint | Expected Status | Result |
|-------------|----------|-----------------|--------|
| GET | /api/users?page=1 | 200 OK | ✅ Pass |
| GET | /api/users/2 | 200 OK | ✅ Pass |
| GET | /api/users/999 | 404 Not Found | ✅ Pass |
| POST | /api/users | 201 Created | ✅ Pass |
| POST | /api/users (empty body) | 400 Bad Request | ✅ Pass |
| PUT | /api/users/2 | 200 OK | ✅ Pass |
| DELETE | /api/users/2 | 204 No Content | ✅ Pass |

---

## 💡 Key Learnings

Through this project I learned to write Postman test scripts using `pm.test()` to automatically assert status codes, response times, and JSON body values — moving beyond manual validation into lightweight automation. I also learned that validating the *structure* of a JSON response (not just the status code) is critical, because an API can return 200 but still send wrong or missing data fields.
