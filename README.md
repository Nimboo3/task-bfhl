# Webhook Challenge - Spring Boot Application

A Spring Boot application that automatically generates a webhook, solves a SQL problem, and submits the solution using JWT authentication.

---

## 🎯 Overview

This Spring Boot application performs the following automated tasks on startup:

1. **Webhook Generation**: Sends a POST request to generate a webhook with registration details  
2. **SQL Problem Solving**: Solves a predefined SQL query based on registration number (odd/even)  
3. **Solution Submission**: Submits the SQL solution to the webhook URL using JWT authentication  

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

## 🔧 Requirements

- **Java**: 11 or higher  
- **Maven**: 3.6.0 or higher  
- **Spring Boot**: 2.7.x or higher  
- **Internet Connection**: Required for API calls  

---

## 🚀 Setup Instructions

### 1. Clone the Repository
```bash
git clone <repository-url>
cd webhookchallenge

2. Build the Project
bashmvn clean install

3. Run the Application
bashmvn spring-boot:run

Or run the JAR file:
bashjava -jar target/webhookchallenge-0.0.1-SNAPSHOT.jar

```

## ⚙️ How It Works

### 🚀 Startup Flow
1. **Application Startup**: `ApplicationStartupRunner` executes automatically.  
2. **Webhook Generation**: `POST` request sent to generate webhook endpoint.  
3. **Response Processing**: Extract webhook URL and access token.  
4. **SQL Solution**: Solve the SQL problem based on registration number (`REG12347` - odd).  
5. **Solution Submission**: `POST` the SQL query to webhook URL with **JWT authentication**.  

---

### 📝 Registration Logic
- **Registration Number**: `REG12347` (ends in `47` → odd)  
- **Question Type**: Odd → **Question 1**  
  > Highest salary not on 1st day of month  

---

## 🌐 API Endpoints

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

## 🗄️ SQL Problem Statement

### 📂 Database Schema  

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

### 📊 Sample Data  

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

### 📝 Problem Requirements  
Find the **highest salary** credited to an employee, but only for transactions that were **NOT made on the 1st day of any month**.  

Extract the following fields:  
- **SALARY** → Highest salary amount  
- **NAME** → Full name (`FIRST_NAME + ' ' + LAST_NAME`)  
- **AGE** → Employee age (calculated from `DOB`)  
- **DEPARTMENT_NAME** → Department name  

---

### ⚖️ Constraints  
- Exclude payments made **on the 1st day** of any month.  
- Return **only the employee with the highest qualifying salary**.  
- Name must be combined as `"FirstName LastName"`.  
- Age must be calculated based on the **current date**.  

---

### ✅ Expected Output  
The query should return **one row** with columns:  

| SALARY | NAME             | AGE | DEPARTMENT_NAME |
|--------|------------------|-----|-----------------|
| 1667827| Olivia Davis     | 30  | HR              |

Example output format:
SALARY    | NAME        | AGE | DEPARTMENT_NAME
----------|-------------|-----|----------------
74998.00  | Emily Brown | 32  | Sales

## 🛠️ Technologies Used
- **Spring Boot 2.7.x** → Main framework  
- **RestTemplate** → HTTP client for API calls  
- **Maven** → Dependency management  
- **SLF4J** → Logging framework  
- **Jackson** → JSON processing  

---

## 📝 Logging
The application includes comprehensive logging for:  
- Application startup events  
- API request/response details  
- SQL query execution  
- Error handling and debugging  

### ⚙️ Log Configuration
Log levels can be configured in `application.properties`:  

```properties
logging.level.com.example.webhookchallenge=DEBUG
logging.level.org.springframework.web.client=DEBUG

2025-01-15 10:30:15.123 INFO  --- Starting webhook generation...
2025-01-15 10:30:16.456 DEBUG --- POST Request: https://bfhldevapigw.healthrx.co.in/hiring/generateWebhook/JAVA
2025-01-15 10:30:17.789 INFO  --- Received webhook URL and access token
2025-01-15 10:30:18.012 INFO  --- Submitting SQL solution...
2025-01-15 10:30:19.234 INFO  --- Solution submitted successfully

```

## 🔍 Troubleshooting

### ⚠️ Common Issues  

#### 1. Connection Timeout  
- Check internet connectivity  
- Verify API endpoints are accessible  
- Check firewall settings  

#### 2. Authentication Errors  
- Ensure JWT token is correctly formatted  
- Check header format:  
  ```http
  Authorization: <accessToken>
  ```
- Verify token hasn't expired

### 🐛 JSON Parsing Errors  
- Verify request body format matches expected structure  
- Check `Content-Type` headers are set correctly  
- Ensure special characters are properly escaped  

---

### 🗄️ SQL Query Issues  
- Verify SQL syntax is correct  
- Test query logic with sample data  
- Check date filtering conditions  

### 🐞 Debug Mode
Enable debug logging to see detailed request/response information:

```properties
logging.level.root=DEBUG
logging.level.org.springframework.web=DEBUG
```

### 🌐 HTTP Response Codes

| Code | Meaning                                   |
|------|-------------------------------------------|
| 200  | ✅ OK – Request successful                 |
| 400  | ❌ Bad Request – Invalid request format   |
| 401  | 🔑 Unauthorized – Invalid or missing JWT token |
| 500  | 💥 Internal Server Error – Server-side error |


Note: This application runs automatically on startup with no manual intervention required. The entire workflow is executed programmatically using the configured registration details (REG187 - odd question type).
