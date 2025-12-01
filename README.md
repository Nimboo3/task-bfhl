# Webhook Challenge - Spring Boot Application

A Spring Boot application designed to automate the process of generating a webhook, solving a SQL challenge, and submitting the solution via JWT authentication.

---

## 🎯 Overview

Upon startup, this application automatically executes the following sequence of tasks:

1. **Webhook Creation**: Initiates a POST request to register and generate a webhook endpoint.
2. **SQL Challenge Resolution**: Computes the solution for a specific SQL problem determined by the registration number (odd/even logic).
3. **Submission**: Transmits the derived SQL query to the webhook URL, authenticated with a JWT.

---

## 📁 Project Structure
bash
```
webbookchallenge
├── .mvn
│   └── wrapper
│       ├── maven-wrapper.jar
│       └── maven-wrapper.properties
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── example
│   │   │           └── webbookchallenge
│   │   │               ├── config
│   │   │               │   └── RestConfig.java
│   │   │               ├── model
│   │   │               │   ├── SolutionRequest.java
│   │   │               │   ├── WebhookRequest.java
│   │   │               │   └── WebhookResponse.java
│   │   │               ├── runner
│   │   │               │   └── ApplicationStartupRunner.java
│   │   │               ├── service
│   │   │               │   └── WebhookChallengeService.java
│   │   │               └── WebbookchallengeApplication.java
│   │   └── resources
│   │       ├── static
│   │       ├── templates
│   │       └── application.properties
│   └── test
│       └── java
│           └── com
│               └── example
│                   └── webbookchallenge
│                       └── (Test files not fully visible)
├── target
│   ├── classes
│   ├── generated-sources
│   ├── generated-test-sources
│   ├── maven-archiver
│   ├── maven-status
│   ├── surefire-reports
│   └── test-classes
├── .gitattributes
├── HELP.md
├── mvnw
├── mvnw.cmd
└── pom.xml
```

## 🔧 Prerequisites

- **Java**: Version 11 or newer
- **Maven**: Version 3.6.0 or newer
- **Spring Boot**: Version 2.7.x or newer
- **Network**: Active internet connection for external API communication

---

## 🚀 Installation & Usage

### 1. Clone the Repository
```bash
git clone <repository-url>
cd webhookchallenge

2. Build the Project
bashmvn clean install

3. Launch the Application
bashmvn spring-boot:run

Alternatively, execute the JAR directly:
bashjava -jar target/webhookchallenge-0.0.1-SNAPSHOT.jar

```

## ⚙️ Workflow

### 🚀 Execution Sequence
1. **Startup**: The `ApplicationStartupRunner` triggers automatically when the app launches.
2. **Webhook Request**: A `POST` request is dispatched to create a webhook endpoint.
3. **Response Handling**: The application parses the response to retrieve the webhook URL and access token.
4. **SQL Logic**: The system solves the SQL challenge corresponding to the registration number (`REG12347` - odd).
5. **Final Submission**: The constructed SQL query is `POST`ed to the webhook URL using **JWT authentication**.

---

### 📝 Registration Details
- **Reg Number**: `REG12347` (ends with `47` → odd)
- **Challenge Type**: Odd → **Question 1**
  > Identify the highest salary that was not paid on the 1st of the month.

---

## 🌐 API Reference

bash
```
1. Generate Webhook
httpPOST https://bfhldevapigw.healthrx.co.in/hiring/generateWebhook/JAVA
Content-Type: application/json

{
  "name": "John Doe",
  "regNo": "REG12347",
  "email": "john@example.com"
}
2. Submit Solution
httpPOST https://bfhldevapigw.healthrx.co.in/hiring/testWebhook/JAVA
Authorization: <accessToken>
Content-Type: application/json

{
  "finalQuery": "YOUR_SQL_QUERY_HERE"
}
```

## 🗄️ SQL Challenge Description

### 📂 Database Structure

#### **DEPARTMENT Table**
| Column          | Type    | Description                |
|-----------------|---------|----------------------------|
| DEPARTMENT_ID   | INT     | Primary Key                |
| DEPARTMENT_NAME | VARCHAR | Department Name            |

#### **EMPLOYEE Table**
| Column      | Type    | Description                        |
|-------------|---------|------------------------------------|
| EMP_ID      | INT     | Primary Key                        |
| FIRST_NAME  | VARCHAR | Employee First Name                |
| LAST_NAME   | VARCHAR | Employee Last Name                 |
| DOB         | DATE    | Date of Birth                      |
| GENDER      | VARCHAR | Gender                             |
| DEPARTMENT  | INT     | Foreign Key → DEPARTMENT.DEPARTMENT_ID |

#### **PAYMENTS Table**
| Column       | Type      | Description                     |
|--------------|-----------|---------------------------------|
| PAYMENT_ID   | INT       | Primary Key                     |
| EMP_ID       | INT       | Foreign Key → EMPLOYEE.EMP_ID   |
| AMOUNT       | DECIMAL   | Salary Amount                   |
| PAYMENT_TIME | TIMESTAMP | Payment Date & Time             |

---

### 📊 Sample Dataset

#### **DEPARTMENT**
| DEPARTMENT_ID | DEPARTMENT_NAME |
|---------------|-----------------|
| 1             | HR              |
| 2             | Finance         |
| 3             | Engineering     |
| 4             | Sales           |
| 5             | Marketing       |
| 6             | IT              |

#### **EMPLOYEE**
| EMP_ID | FIRST_NAME | LAST_NAME | DOB        | GENDER | DEPARTMENT |
|--------|------------|-----------|------------|--------|------------|
| 1      | John       | Williams  | 1980-05-15 | Male   | 3          |
| 2      | Sarah      | Johnson   | 1990-07-20 | Female | 2          |
| 3      | Michael    | Smith     | 1985-02-10 | Male   | 3          |
| 4      | Emily      | Brown     | 1992-11-30 | Female | 4          |
| 5      | David      | Jones     | 1988-09-05 | Male   | 5          |
| 6      | Olivia     | Davis     | 1995-04-12 | Female | 1          |
| 7      | James      | Wilson    | 1983-03-25 | Male   | 6          |
| 8      | Sophia     | Anderson  | 1991-08-17 | Female | 4          |
| 9      | Liam       | Miller    | 1979-12-01 | Male   | 1          |
| 10     | Emma       | Taylor    | 1993-06-28 | Female | 5          |

#### **PAYMENTS**
| PAYMENT_ID | EMP_ID | AMOUNT | PAYMENT_TIME              |
|------------|--------|--------|---------------------------|
| 1          | 2      | 65784  | 2025-01-01 13:44:12.824   |
| 2          | 4      | 62736  | 2025-01-06 18:36:37.892   |
| 3          | 3      | 169437 | 2025-01-01 10:19:21.563   |
| 4          | 3      | 367183 | 2025-01-02 17:21:57.341   |
| 5          | 2      | 266273 | 2025-02-01 11:49:15.764   |
| 6          | 5      | 571475 | 2025-01-01 07:24:14.453   |
| 7          | 7      | 170837 | 2025-02-03 19:11:31.553   |
| 8          | 6      | 669628 | 2025-01-02 10:41:15.113   |
| 9          | 4      | 471876 | 2025-02-01 12:16:47.807   |
| 10         | 3      | 370098 | 2025-02-03 10:11:17.341   |
| 11         | 6      | 1667827| 2025-02-02 19:21:27.753   |
| 12         | 5      | 569871 | 2025-02-05 17:54:17.453   |
| 13         | 2      | 327984 | 2025-03-05 09:37:35.974   |
| 14         | 1      | 167982 | 2025-03-01 06:09:51.983   |
| 15         | 6      | 670198 | 2025-03-02 10:34:35.753   |
| 16         | 7      | 647998 | 2025-03-02 09:27:26.162   |

---

### 📝 Query Objectives
Determine the **maximum salary** paid to an employee, excluding any transactions that occurred **on the 1st day of the month**.

The result must include:
- **SALARY** → The maximum salary figure
- **NAME** → Full name formatted as (`FIRST_NAME + ' ' + LAST_NAME`)
- **AGE** → Current age of the employee (derived from `DOB`)
- **DEPARTMENT_NAME** → Name of the department

---

### ⚖️ Rules & Constraints
- Filter out payments made **on the 1st**.
- Output **only the single record** with the highest valid salary.
- Name format: `"FirstName LastName"`.
- Age calculation: Based on the **current date**.

---

### ✅ Desired Output
The query should yield **a single row** with the following columns:

| SALARY | NAME             | AGE | DEPARTMENT_NAME |
|--------|------------------|-----|-----------------|
| 1667827| Olivia Davis     | 30  | HR              |

Sample output format:
SALARY    | NAME        | AGE | DEPARTMENT_NAME
----------|-------------|-----|----------------
74998.00  | Emily Brown | 32  | Sales

## 🛠️ Tech Stack
- **Spring Boot 2.7.x** → Core application framework
- **RestTemplate** → Client for HTTP requests
- **Maven** → Build and dependency tool
- **SLF4J** → Logging abstraction
- **Jackson** → JSON serialization/deserialization

---

## 📝 Logging Details
The application features detailed logging covering:
- Startup sequence
- API request and response payloads
- SQL query generation
- Error tracking

### ⚙️ Log Settings
Adjust log levels in `application.properties`:

```properties
logging.level.com.example.webhookchallenge=DEBUG
logging.level.org.springframework.web.client=DEBUG

2025-01-15 10:30:15.123 INFO  --- Starting webhook generation...
2025-01-15 10:30:16.456 DEBUG --- POST Request: https://bfhldevapigw.healthrx.co.in/hiring/generateWebhook/JAVA
2025-01-15 10:30:17.789 INFO  --- Received webhook URL and access token
2025-01-15 10:30:18.012 INFO  --- Submitting SQL solution...
2025-01-15 10:30:19.234 INFO  --- Solution submitted successfully

```

## 🔍 Troubleshooting Guide

### ⚠️ Potential Issues

#### 1. Timeouts
- Verify your internet connection.
- Ensure the API endpoints are reachable.
- Check for firewall restrictions.

#### 2. Auth Failures
- Confirm the JWT token format.
- Verify the header structure:
  ```http
  Authorization: <accessToken>
  ```
- Ensure the token is still valid.

### 🐛 JSON Errors
- Check that the request body matches the required schema.
- Confirm `Content-Type` is set to `application/json`.
- Ensure proper escaping of special characters.

---

### 🗄️ SQL Troubleshooting
- Validate SQL syntax.
- Test logic against the provided sample data.
- Double-check date exclusion logic.

### 🐞 Debugging
Activate debug logs for granular request/response inspection:

```properties
logging.level.root=DEBUG
logging.level.org.springframework.web=DEBUG
```

### 🌐 HTTP Status Codes

| Code | Meaning                                   |
|------|-------------------------------------------|
| 200  | ✅ OK – Operation successful               |
| 400  | ❌ Bad Request – Malformed request        |
| 401  | 🔑 Unauthorized – Invalid/missing token   |
| 500  | 💥 Internal Server Error – Server failure |


Note: This application is designed to run autonomously upon startup. The complete workflow executes programmatically using the pre-configured registration data (REG187 - odd question type).
