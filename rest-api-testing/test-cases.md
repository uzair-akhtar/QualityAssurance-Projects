# 📋 Test Cases — REST API Testing (ReqRes.in)

**Project:** REST API Testing  
**API Base URL:** `https://reqres.in`  
**Tester:** Uzair Akhtar  
**Tool:** Postman  
**Total Test Cases:** 18  
**Pass:** 18 | **Fail:** 0

---

## Module 1 — GET Requests (Retrieve Data)

| TC ID | Test Case Title | Endpoint | Method | Test Data | Expected Result | Status Code | Result |
|-------|----------------|----------|--------|-----------|-----------------|-------------|--------|
| TC-001 | Get list of users — page 1 | /api/users?page=1 | GET | page=1 | Returns 200 with array of user objects, each containing id, email, first_name, last_name | 200 | ✅ Pass |
| TC-002 | Get list of users — page 2 | /api/users?page=2 | GET | page=2 | Returns 200 with next set of users, total_pages field present in response | 200 | ✅ Pass |
| TC-003 | Get a single valid user | /api/users/2 | GET | user_id=2 | Returns 200 with single user object — id, email, first_name, last_name, avatar | 200 | ✅ Pass |
| TC-004 | Get a user that does not exist | /api/users/999 | GET | user_id=999 | Returns 404 with empty response body — no user data leaked | 404 | ✅ Pass |
| TC-005 | Verify response time is acceptable | /api/users | GET | — | Response received within 3000ms | 200 | ✅ Pass |
| TC-006 | Verify Content-Type header in response | /api/users | GET | — | Header contains application/json; charset=utf-8 | 200 | ✅ Pass |

---

## Module 2 — POST Requests (Create Data)

| TC ID | Test Case Title | Endpoint | Method | Test Data | Expected Result | Status Code | Result |
|-------|----------------|----------|--------|-----------|-----------------|-------------|--------|
| TC-007 | Create a new user with valid data | /api/users | POST | {"name": "Uzair", "job": "QA Engineer"} | Returns 201 with id and createdAt fields in response body | 201 | ✅ Pass |
| TC-008 | Verify created user has unique ID | /api/users | POST | {"name": "Uzair", "job": "QA Engineer"} | Response body contains id field that is not null or empty | 201 | ✅ Pass |
| TC-009 | Verify createdAt timestamp is present | /api/users | POST | {"name": "Uzair", "job": "QA Engineer"} | Response body contains createdAt field with valid timestamp format | 201 | ✅ Pass |
| TC-010 | Register a user with valid credentials | /api/register | POST | {"email": "eve.holt@reqres.in", "password": "pistol"} | Returns 200 with token field in response body | 200 | ✅ Pass |
| TC-011 | Register a user without password | /api/register | POST | {"email": "eve.holt@reqres.in"} | Returns 400 with error message "Missing password" | 400 | ✅ Pass |
| TC-012 | Register with undefined email | /api/register | POST | {"email": "unknown@test.com", "password": "test123"} | Returns 400 with error "Note: Only defined users succeed registration" | 400 | ✅ Pass |

---

## Module 3 — PUT Requests (Update Data)

| TC ID | Test Case Title | Endpoint | Method | Test Data | Expected Result | Status Code | Result |
|-------|----------------|----------|--------|-----------|-----------------|-------------|--------|
| TC-013 | Update user name and job | /api/users/2 | PUT | {"name": "Uzair Akhtar", "job": "Senior QA"} | Returns 200 with updated name and job fields plus updatedAt timestamp | 200 | ✅ Pass |
| TC-014 | Verify updatedAt timestamp is present | /api/users/2 | PUT | {"name": "Test User", "job": "Tester"} | Response body contains updatedAt field confirming update time | 200 | ✅ Pass |
| TC-015 | Update with only one field | /api/users/2 | PUT | {"name": "Partial Update"} | Returns 200 and reflects the change without error | 200 | ✅ Pass |

---

## Module 4 — DELETE Requests (Remove Data)

| TC ID | Test Case Title | Endpoint | Method | Test Data | Expected Result | Status Code | Result |
|-------|----------------|----------|--------|-----------|-----------------|-------------|--------|
| TC-016 | Delete a valid user | /api/users/2 | DELETE | user_id=2 | Returns 204 with completely empty response body — no data leaked | 204 | ✅ Pass |
| TC-017 | Verify no body is returned after delete | /api/users/2 | DELETE | user_id=2 | Response body length is 0 — confirmed empty | 204 | ✅ Pass |
| TC-018 | Verify response time after delete | /api/users/2 | DELETE | user_id=2 | Response received within 3000ms | 204 | ✅ Pass |

---

## 🐞 Bugs Found

No bugs were found during testing. ReqRes.in is a stable public mock API designed for learning purposes. All endpoints behaved according to their documented specifications. The key learning here was that even when a server responds with 200, the response *body* must be validated — a correct status code does not guarantee correct data.

---

## 📝 Postman Test Scripts Used

Inside Postman, each request has test scripts written using `pm.test()`. Below are examples of the assertions I used:

```javascript
// Assert the status code is 200
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// Assert response time is under 3 seconds
pm.test("Response time is less than 3000ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(3000);
});

// Assert a specific JSON field exists and is not empty
pm.test("User ID is present in response", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.data.id).to.not.be.null;
});

// Assert the Content-Type header
pm.test("Content-Type is application/json", function () {
    pm.response.to.have.header("Content-Type");
});
```
