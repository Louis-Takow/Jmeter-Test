# 🧪 JMeter API Test Suite for Restful Booker

This project contains a comprehensive JMeter test plan to validate the full **CRUD operations** and **authentication flow** of the [Restful Booker API](https://restful-booker.herokuapp.com/). It is designed to help QA Engineers and developers quickly validate REST API functionality using Apache JMeter.

---

## 📁 Repository Structure

```
Jmeter-Test/
├── Herokuapp Test plan.jmx   # Main JMeter test plan
├── README.md                   
```

---

## ✅ Scope of the Test Plan

The test plan covers the following endpoints of the Restful Booker API:

| Feature                   | HTTP Method | Endpoint                                  |
|---------------------------|-------------|--------------------------------------------|
| Authentication            | POST        | `/auth`                                    |
| Create Booking            | POST        | `/booking`                                 |
| Get All Booking IDs       | GET         | `/booking`                                 |
| Get Booking by ID         | GET         | `/booking/:id`                             |
| Full Update Booking       | PUT         | `/booking/:id` (requires auth token)       |
| Partial Update Booking    | PATCH       | `/booking/:id` (requires auth token)       |
| Delete Booking            | DELETE      | `/booking/:id` (requires auth token)       |

Each request uses proper headers, and token handling is managed using **JMeter’s JSON Extractors** and **variables**.

---

## ⚙️ Prerequisites

Before running the test plan, ensure you have the following installed on your local machine:

- **Java 8+** (JMeter requires Java)
- **Apache JMeter 5.5 or higher**  
  [Download JMeter](https://jmeter.apache.org/download_jmeter.cgi)

---

## 🚀 Getting Started

### 1. Clone this repository

```bash
git clone https://github.com/Louis-Takow/Jmeter-Test.git
cd Jmeter-Test
```

### 2. Open JMeter GUI

- Launch JMeter via:
  - macOS/Linux:
    ```bash
    ./bin/jmeter
    ```
  - Windows:
    ```
    bin\jmeter.bat
    ```

### 3. Load the Test Plan

- In the JMeter GUI, go to **File > Open**
- Select the file: `Herokuapp Test plan.jmx`

### 4. Run the Test

- Click the **Start (green triangle)** button in the JMeter toolbar.
- View results in:
  - **View Results Tree**
  - **Summary Report**
  - **View Results in Table**
  - **Graph Results**
  - **Assertion Results** 

---

## 🧠 How It Works

The test flow is structured in this order:

1. **Auth - CreateToken**
   - Sends a POST request with valid credentials.
   - Extracts and stores the token for reuse in PUT/PATCH/DELETE operations.

2. **Create Booking**
   - Creates a new booking and extracts the `bookingid` for all subsequent requests.

3. **Get Booking IDs**
   - Fetches a list of all bookings.

4. **Get Booking by ID**
   - Fetches the booking just created using `bookingid`.

5. **Update Booking (PUT)**
   - Performs a full update with new data using the `token`.

6. **Partial Update Booking (PATCH)**
   - Modifies only specific fields (e.g., firstname, lastname) using the `token`.

7. **Delete Booking**
   - Deletes the booking using the `token`.

All requests are dynamically parameterized using variables and extractors.

---

## ✅ Sample Test Data Used

- **Auth Credentials:**
  - Username: `admin`
  - Password: `password123`

- **Booking Payload:**
  ```json
  {
    "firstname": "Jim",
    "lastname": "Brown",
    "totalprice": 111,
    "depositpaid": true,
    "bookingdates": {
        "checkin": "2018-01-01",
        "checkout": "2019-01-01"
    },
    "additionalneeds": "Breakfast"
  }
  ```

- **Partial Update Payload:**
  ```json
  {
    "firstname": "James",
    "lastname": "Brown"
  }
  ```

---

## 📦 Output

- Each response will be visible in the **View Results Tree**
- Assertions are added to verify specific response codes, keys, or values.

---

## 🤝 Contributing

Feel free to fork this repo and modify the test plan to fit other use cases like:

- Negative test cases (invalid token, bad payloads)
- Load/Stress testing via `Thread Group` configs
- Assertions and CSV-driven data sets

---

## 🧼 Cleanup

All test data (bookings) created during the run are deleted automatically at the end of the test.

---

## 📩 Questions or Issues?

Open an [issue](https://github.com/Louis-Takow/Jmeter-Test/issues) or reach out if you have any questions or suggestions.

---

**Happy Testing!**

**Author: Louis Takow**
