# Restful Booker API Testing (Postman)

This project contains a **Postman collection** for testing the **Restful Booker API**, focusing on authentication and booking-related endpoints. It is designed for practicing API testing, validating requests/responses, and improving QA automation skills.

---

## Project Overview

This project is used to:

* Perform API testing using Postman
* Validate request and response structures
* Test authentication flow
* Test booking APIs (search and detail)

---

## Tools & Technologies

* Postman
* JSON (Postman Collection)
* Newman (optional for CLI execution)

---

## Collection Structure

```
test
├── Auth
│   └── login
└── Booking
    ├── search all
    ├── search by name
    ├── search by date
    └── detail
```

---

## Authentication - Login

### Request

* Method: `POST`
* Endpoint: `/auth`
* Headers:

  * Content-Type: `application/json`

### Request Body

```json
{
  "username": "admin",
  "password": "password123"
}
```

### Test Cases

* Validate status code is **200**
* Validate response contains `token`
* Validate token is not empty
* Validate token is a string

### Pre-request Validations

* Request method must be `POST`
* URL must contain `/auth`
* Content-Type must be `application/json`
* Request body must include:

  * username
  * password

---

## Booking APIs

###  1. Search All Bookings

**GET /booking**

#### Tests

* Status code should be **200**
* Response should be an **array**

#### Pre-request Checks

* Method must be `GET`
* Path must be `/booking`
* Authorization header must exist

---

###  2. Search by Name

**GET /booking?firstname=sally&lastname=brown**

#### Tests

* Status code should be **200**
* Response should be an **array**

#### Pre-request Checks

* Authorization header must exist
* Query params must include:

  * firstname = sally
  * lastname = brown

---

###  3. Search by Date

**GET /booking?checkin=YYYY-MM-DD&checkout=YYYY-MM-DD**

#### Tests

* Status code should be **200**

#### Pre-request Checks

* Authorization header must exist
* Query params must include:

  * checkin
  * checkout

---

###  4. Booking Detail

**GET /booking/:id**

#### Tests

* Status code should be **200**
* Response should contain:

  * firstname
  * lastname
  * bookingdates

Additional edge case:

* Should return **404** for invalid booking ID

#### Pre-request Checks

* Method must be `GET`
* URL must contain `/booking/{id}`
* Authorization header must exist

---

## How to Use

### 1. Import Collection

* Open Postman
* Click **Import**
* Upload the provided collection JSON file

---

### 2. Run Tests

#### Using Postman

* Run requests individually
  or
* Use **Collection Runner**

#### Using Newman (CLI)

```bash
npm install -g newman
newman run collection.json
```

---

##  Notes

*  Authorization currently uses a hardcoded token
*  It is recommended to store the token in environment variables
*  API data resets periodically

---

##  Improvement Ideas

* Store token dynamically using environment variables
* Use dynamic booking IDs instead of fixed values
* Increase test coverage (POST / PUT / DELETE)
* Integrate with CI/CD pipelines for automation
