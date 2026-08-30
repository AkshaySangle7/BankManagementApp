# 🏦 BankManagementApp

<div align="center">
  <img src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=java&logoColor=white" alt="Java" />
  <img src="https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white" alt="Spring Boot" />
  <img src="https://img.shields.io/badge/Hibernate-59666C?style=for-the-badge&logo=Hibernate&logoColor=white" alt="Hibernate" />
  <img src="https://img.shields.io/badge/MySQL-005C84?style=for-the-badge&logo=mysql&logoColor=white" alt="MySQL" />
  <img src="https://img.shields.io/badge/Security-000000?style=for-the-badge&logo=springsecurity&logoColor=white" alt="Spring Security" />
</div>

<br/>

A robust, secure, and scalable backend system for managing core banking operations. This application provides a streamlined RESTful API for user account management, secure fund transfers, transaction history tracking, and balance inquiries, mimicking real-world financial workflows.

## 🛠️ Tech Stack

*   **Language:** Java 17
*   **Framework:** Spring Boot 3.x
*   **Database:** MySQL
*   **ORM:** Spring Data JPA, Hibernate
*   **Security:** Spring Security & JWT (JSON Web Tokens)
*   **Build Tool:** Maven
*   **API Documentation:** Swagger / OpenAPI 3.0

## 🏗️ Architecture Overview

The application follows a standard **N-Tier Layered Architecture** to maintain clean separation of concerns, ensuring high maintainability and testability:

1.  **Controller Layer (`@RestController`):** Intercepts client HTTP requests, validates input payloads (DTOs), and routes them to corresponding services.
2.  **Service Layer (`@Service`):** The core engine where complex business logic resides (e.g., processing transactions, ACID compliance, sufficient balance checks).
3.  **Repository Layer (`@Repository`):** Handles seamless data persistence to the MySQL database utilizing Spring Data JPA.
4.  **Security Layer:** Uses a custom JWT Authentication Filter to secure sensitive endpoints. Only authenticated users can transfer funds or view private statements.
5.  **Exception Handling:** Global exception handling using `@ControllerAdvice` to provide clean, unified error responses (e.g., `InsufficientBalanceException`, `AccountNotFoundException`).

## 🌐 API Endpoints

Here are the core REST API endpoints exposed by the application:

### 👤 User Authentication
| Method | Endpoint | Description | Access |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/auth/register` | Register a new bank customer | Public |
| `POST` | `/api/auth/login` | Authenticate customer & generate JWT | Public |

### 💳 Account Operations
| Method | Endpoint | Description | Access |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/accounts/{accountNumber}/balance` | Check current account balance | Protected |
| `POST` | `/api/accounts/deposit` | Deposit funds into an account | Protected |
| `POST` | `/api/accounts/withdraw` | Withdraw funds from an account | Protected |

### 💸 Transactions
| Method | Endpoint | Description | Access |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/transactions/transfer` | Transfer money between two accounts | Protected |
| `GET` | `/api/transactions/history/{accountNumber}` | Get transaction history (Mini-Statement) | Protected |

*(Note: Endpoints marked as `Protected` require a valid JWT token in the `Authorization` header formatted as `Bearer <token>`)*.

## ⚙️ How To Run

### Prerequisites
*   JDK 17 or higher installed.
*   Maven installed.
*   MySQL Server running locally on port `3306`.

### Installation Steps

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/AkshaySangle7/BankManagementApp.git](https://github.com/AkshaySangle7/BankManagementApp.git)
    cd BankManagementApp
    ```

2.  **Database Configuration:**
    Create a new database in MySQL:
    ```sql
    CREATE DATABASE bank_db;
    ```
    Update the `src/main/resources/application.properties` with your database credentials:
    ```properties
    spring.datasource.url=jdbc:mysql://localhost:3306/bank_db
    spring.datasource.username=your_mysql_username
    spring.datasource.password=your_mysql_password
    
    # Hibernate Settings
    spring.jpa.hibernate.ddl-auto=update
    spring.jpa.show-sql=true
    ```

3.  **Build the Project:**
    ```bash
    mvn clean install
    ```

4.  **Run the Application:**
    ```bash
    mvn spring-boot:run
    ```
    *The server will start successfully on `http://localhost:8080`.*

## 🔮 Future Enhancements

*   **Role-Based Access Control (RBAC):** Differentiate between `CUSTOMER` and `ADMIN` (Bank Manager) roles.
*   **Email & SMS Alerts:** Integrate Spring Mail and Twilio to notify users of successful transfers and low balances in real-time.
*   **PDF Statement Generation:** Allow users to generate and download their monthly account statements in PDF format.
*   **Redis Caching:** Cache user details and frequent balance queries to optimize database hits.
*   **Rate Limiting:** Implement API rate limiting to prevent brute-force attacks on the login and transaction endpoints.

---
