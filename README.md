# 🏦 Banking Management System

A web-based Banking Management System built using **Node.js, Express.js, EJS, and MySQL**. This project aims to simulate basic banking operations such as user registration, login, account creation, deposits, withdrawals, money transfers, and balance inquiry through a dynamic web application connected to a MySQL database.

The project demonstrates backend development concepts, including Express routing, middleware, server-side rendering, database connectivity, CRUD operations, and transaction management.

---

## 🎯 Features

- ✅ User Registration and Login
- ✅ Secure Authentication and Session Management
- ✅ Bank Account Creation
- ✅ View Account Details
- ✅ Deposit Money (Credit)
- ✅ Withdraw Money (Debit)
- ✅ Transfer Money Between Accounts
- ✅ Check Account Balance
- ✅ View Transaction History
- ✅ Search and Manage Customer Records
- ✅ Dynamic Web Pages Using EJS
- ✅ Express.js Routing and Middleware
- ✅ MySQL Database Integration
- ✅ Server-Side Form Validation
- ✅ SQL Injection Prevention Using Parameterized Queries
- ✅ Database Transaction Management for Financial Operations
- ✅ Error Handling and User-Friendly Messages

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Node.js | JavaScript runtime for executing server-side code |
| Express.js | Backend framework for handling routes, requests, responses, and middleware |
| EJS | Template engine for rendering dynamic HTML pages |
| MySQL 8.0 | Database for storing customers, accounts, and transaction records |
| mysql2 | Connects Node.js to MySQL and executes SQL queries |
| HTML5 | Creates forms and structures web pages |
| CSS3 | Styles the user interface |
| JavaScript | Handles client-side interactions and validation |
| express-session | Manages user sessions and login state |
| bcrypt | Hashes passwords securely |
| dotenv | Stores environment variables and database configuration |
| VS Code | IDE used for development |
| Git & GitHub | Version control and project hosting |

---

## 📁 Project Structure

```text
Banking-Management-System/
│
├── config/
│   └── db.js
│
├── controllers/
│   ├── authController.js
│   ├── accountController.js
│   ├── dashboardController.js
│   └── transactionController.js
│
├── models/
│   ├── customerModel.js
│   ├── accountModel.js
│   └── transactionModel.js
│
├── routes/
│   ├── authRoutes.js
│   ├── dashboardRoutes.js
│   ├── accountRoutes.js
│   └── transactionRoutes.js
│
├── middlewares/
│   ├── authMiddleware.js
│   ├── validateUser.js
│   ├── validateTransaction.js
│   └── errorHandler.js
│
├── views/
│   ├── home.ejs
│   ├── auth/
│   │   ├── register.ejs
│   │   └── login.ejs
│   ├── dashboard/
│   │   └── index.ejs
│   ├── accounts/
│   │   ├── index.ejs
│   │   └── details.ejs
│   ├── transactions/
│   │   ├── deposit.ejs
│   │   ├── withdraw.ejs
│   │   ├── transfer.ejs
│   │   └── history.ejs
│   └── partials/
│       ├── navbar.ejs
│       └── footer.ejs
│
├── public/
│   ├── css/
│   │   └── style.css
│   └── js/
│       └── script.js
│
├── .env
├── .gitignore
├── app.js
├── package.json
├── package-lock.json
└── README.md
```

---

## 🗄️ Database Setup

Open MySQL and execute the following commands.

### 1. Create the Database

```sql
CREATE DATABASE banking_system;

USE banking_system;
```

### 2. Create the Customers Table

```sql
CREATE TABLE customers (
    id INT AUTO_INCREMENT PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 3. Create the Accounts Table

```sql
CREATE TABLE accounts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT NOT NULL,
    account_number VARCHAR(20) UNIQUE NOT NULL,
    balance DECIMAL(15,2) NOT NULL DEFAULT 0.00,
    status ENUM('active', 'blocked') NOT NULL DEFAULT 'active',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    FOREIGN KEY (customer_id)
        REFERENCES customers(id),

    CHECK (balance >= 0)
);
```

### 4. Create the Transactions Table

```sql
CREATE TABLE transactions (
    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    account_id INT NOT NULL,
    type ENUM(
        'deposit',
        'withdrawal',
        'transfer_debit',
        'transfer_credit'
    ) NOT NULL,
    amount DECIMAL(15,2) NOT NULL,
    reference VARCHAR(50) NOT NULL,
    description VARCHAR(255),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,

    FOREIGN KEY (account_id)
        REFERENCES accounts(id),

    CHECK (amount > 0),

    INDEX idx_account_created (account_id, created_at)
);
```

**Note:** These SQL statements define the initial database schema. Execute them before running the application. If you change the schema later, update the corresponding models and queries.

---

## ⚙️ Installation and Setup

### Prerequisites

Make sure the following software is installed:

- Node.js
- npm
- MySQL Server 8.0
- Visual Studio Code
- Git

### 1. Clone the Repository

```bash
git clone YOUR_REPOSITORY_URL
```

### 2. Navigate to the Project Directory

```bash
cd Banking-Management-System
```

### 3. Install Dependencies

Install the required packages:

```bash
npm install express ejs mysql2 dotenv express-session bcrypt
```

If the project already includes a `package.json` file with all dependencies listed, you can install them using:

```bash
npm install
```

### 4. Configure Environment Variables

Create a `.env` file in the root directory.

```env
PORT=3000

DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_mysql_password
DB_NAME=banking_system

SESSION_SECRET=replace_with_a_long_random_secret
```

Replace the example database credentials with your own local configuration.

**Important:** Never upload your `.env` file, database password, or session secret to GitHub.

### 5. Create the Database

Open MySQL Workbench or your MySQL terminal and execute the SQL statements provided in the Database Setup section.

### 6. Start the Application

If your `package.json` contains a start script:

```bash
npm start
```

Alternatively, if you have not configured a start script:

```bash
node app.js
```

If you use `node --watch app.js` during development, make sure your installed Node.js version supports it.

### 7. Open the Application

Visit the following address in your browser:

```text
http://localhost:3000
```

---

## 🌐 Application Routes

The application uses Express.js routes to handle customer requests.

| HTTP Method | Route | Purpose |
|---|---|---|
| GET | `/` | Display the home page |
| GET | `/register` | Display the registration form |
| POST | `/register` | Register a new customer |
| GET | `/login` | Display the login form |
| POST | `/login` | Authenticate a customer |
| POST | `/logout` | Log out the customer |
| GET | `/dashboard` | Display the customer dashboard |
| GET | `/accounts` | Display customer accounts |
| GET | `/accounts/:id` | Display account details |
| GET | `/accounts/:id/deposit` | Display the deposit form |
| POST | `/accounts/:id/deposit` | Deposit money |
| GET | `/accounts/:id/withdraw` | Display the withdrawal form |
| POST | `/accounts/:id/withdraw` | Withdraw money |
| GET | `/accounts/:id/transfer` | Display the transfer form |
| POST | `/accounts/:id/transfer` | Transfer money |
| GET | `/accounts/:id/transactions` | Display transaction history |

These are the planned routes. Implement and test each route before presenting it as a completed feature.

---

## 🔄 How the Application Works

### 1. User Registration

- The customer opens the registration page.
- The customer submits their name, email, and password.
- Express receives the submitted data through `req.body`.
- Middleware validates the submitted information.
- The password is hashed before being stored.
- The customer record is inserted into the MySQL database.

### 2. User Login

- The customer submits their email and password.
- Express retrieves the matching customer record.
- The submitted password is compared with the stored password hash.
- If the credentials are valid, the application establishes an authenticated session.
- The customer is redirected to the dashboard.

### 3. Deposit Money

- The customer opens the deposit form.
- The customer enters the amount.
- Express validates the request and verifies account ownership.
- The application updates the account balance and records the transaction.
- The database transaction is committed if all operations succeed.

### 4. Withdraw Money

- The customer submits a withdrawal request.
- The application validates the amount and verifies the account.
- The application checks that sufficient funds are available.
- The balance is updated and the transaction is recorded.
- The operation is committed only when all required database operations succeed.

### 5. Transfer Money

- The customer selects the destination account and enters an amount.
- The application validates the request and verifies ownership of the source account.
- The database transaction checks available funds and updates both accounts.
- Corresponding transaction records are created for the debit and credit.
- The operation is committed only if all required changes succeed; otherwise, it is rolled back.

### 6. Transaction History

- The application retrieves transaction records from MySQL.
- Express passes the results to an EJS template.
- EJS dynamically displays the transaction history.

---

## 🔌 What Is Express.js?

Express.js is a web framework for Node.js that simplifies the development of server-side applications.

In this project, Express.js is used to:

- Define application routes using `app.get()` and `app.post()`.
- Handle requests and responses using `req` and `res`.
- Process submitted form data using middleware.
- Render dynamic pages using `res.render()`.
- Organize application routes using `express.Router()`.
- Validate user input and handle application errors.

---

## 🗄️ What Is MySQL Integration?

MySQL is a relational database used to store customer information, account balances, and transaction records.

The `mysql2` package allows Node.js to connect to MySQL and execute SQL queries.

It is used to:

- Insert new customer records.
- Retrieve customer and account information.
- Update account balances.
- Delete or modify eligible records.
- Retrieve transaction history.
- Execute parameterized queries.
- Manage database transactions using `beginTransaction()`, `commit()`, and `rollback()`.

---

## 🔒 Security Features

The project aims to implement the following security measures:

- **Password Hashing:** Store password hashes instead of plain-text passwords.
- **Session-Based Authentication:** Maintain the customer's authenticated session.
- **Server-Side Validation:** Validate submitted data before processing it.
- **Parameterized SQL Queries:** Reduce the risk of SQL injection.
- **Account Ownership Verification:** Prevent customers from accessing accounts they do not own.
- **Authorization:** Restrict administrative actions to authorized users.
- **Database Transactions:** Maintain consistency when performing deposits, withdrawals, and transfers.
- **Environment Variables:** Keep database credentials and session secrets out of source code.
- **Secure Session Configuration:** Configure session cookies and use HTTPS in production.

---

## 📚 Concepts Demonstrated

- Node.js Fundamentals
- Express.js Framework
- Routing and Dynamic Routing
- HTTP Methods: GET and POST
- Request and Response Handling
- Middleware and Validation
- EJS Template Rendering
- MySQL Database Connectivity
- SQL CRUD Operations
- Relational Database Design
- MVC Architecture
- Authentication and Authorization
- Session Management
- Parameterized SQL Queries
- Database Transaction Management
- Error Handling

---

## 👩‍💻 Author

**Apurva Vinay Waghmode**

Computer Science Engineering

GitHub: https://github.com/ApurvaWaghmode

---

## ⭐ Support

If you find this project useful, consider giving the repository a star!
