# 🏦 Banking Management System

A console-based Banking Management System built using **Core Java** and **MySQL**. This project simulates real banking operations like user registration, login, account creation, deposits, withdrawals, money transfers, and balance inquiry — all connected to a live MySQL database using **JDBC**.

---

## 🎯 Features

- ✅ User Registration & Login
- ✅ Open a Bank Account with Security PIN
- ✅ Deposit Money (Credit)
- ✅ Withdraw Money (Debit)
- ✅ Transfer Money to Another Account
- ✅ Check Account Balance
- ✅ Secure Transactions using JDBC Transaction Management (commit/rollback)
- ✅ SQL Injection Prevention using PreparedStatement

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Java (JDK 21) | Core programming language |
| MySQL 8.0 | Database to store user and account data |
| JDBC | Connects Java code to MySQL database |
| mysql-connector-j 8.0.33 | MySQL JDBC Driver (JAR file) |
| VS Code | IDE used for development |

---

## 📁 Project Structure

```
Banking-Management-System-master/
├── .idea/
│   └── lib/
│       └── mysql-connector-j-8.0.33.jar   ← JDBC Driver
├── src/
│   └── BankingManagementSystem/
│       ├── BankingApp.java       ← Main file (entry point + DB connection)
│       ├── User.java             ← Register & Login logic
│       ├── Accounts.java         ← Open account & account number generation
│       └── AccountManager.java   ← Debit, Credit, Transfer, Balance
├── .vscode/
│   ├── settings.json
│   └── launch.json
└── README.md
```

---

## 🗄️ Database Setup

Open MySQL and run the following commands:

```sql
CREATE DATABASE banking_system;
USE banking_system;

CREATE TABLE User (
    id INT AUTO_INCREMENT PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(100) NOT NULL
);

CREATE TABLE Accounts (
    account_number BIGINT PRIMARY KEY,
    full_name VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL,
    balance DOUBLE DEFAULT 0.0,
    security_pin VARCHAR(10) NOT NULL,
    FOREIGN KEY (email) REFERENCES User(email)
);
```

---

## ⚙️ How to Run

### Prerequisites
- JDK 17 or above installed
- MySQL 8.0 installed and running
- mysql-connector-j-8.0.33.jar in `.idea/lib/` folder

### Steps

**1. Clone the repository**
```bash
git clone https://github.com/YourUsername/Banking-Management-System.git
cd Banking-Management-System
```

**2. Update your MySQL password**

Open `src/BankingManagementSystem/BankingApp.java` and update line 9:
```java
private static final String password = "YOUR_MYSQL_PASSWORD";
```

**3. Create the database**

Run the SQL commands from the Database Setup section above in MySQL.

**4. Compile the project**
```bash
cd src
javac -cp ".;../.idea/lib/mysql-connector-j-8.0.33.jar" BankingManagementSystem/*.java
```

**5. Run the project**
```bash
java -cp ".;../.idea/lib/mysql-connector-j-8.0.33.jar" BankingManagementSystem.BankingApp
```

> **Note:** On Mac/Linux replace `;` with `:` in the classpath

---

## 💻 How the App Works

```
*** WELCOME TO BANKING SYSTEM ***

1. Register
2. Login
3. Exit

Enter your choice: 1

Full Name: Apurva Waghmode
Email: apurva@gmail.com
Password: ********
Registration Successful!

Enter your choice: 2
Email: apurva@gmail.com
Password: ********
User Logged In!

1. Debit Money
2. Credit Money
3. Transfer Money
4. Check Balance
5. Log Out
```

---

## 🔌 What is JDBC?

JDBC (Java Database Connectivity) is a Java API that allows Java programs to connect to and interact with relational databases like MySQL.

In this project JDBC is used to:
- Connect Java to MySQL using `DriverManager.getConnection()`
- Run SQL queries using `PreparedStatement`
- Read database results using `ResultSet`
- Handle safe transactions using `commit()` and `rollback()`

---

## 🔒 Security Features

- **PreparedStatement** used everywhere to prevent SQL Injection
- **Security PIN** required for every financial transaction
- **Transaction Management** — money transfers use commit/rollback to ensure funds are never lost

---

## 📊 Database Schema

```
User Table                          Accounts Table
─────────────────────               ──────────────────────────────
id          INT (PK)                account_number  BIGINT (PK)
full_name   VARCHAR(100)            full_name       VARCHAR(100)
email       VARCHAR(100) UNIQUE     email           VARCHAR(100) (FK)
password    VARCHAR(100)            balance         DOUBLE
                                    security_pin    VARCHAR(10)
```

---

## 👩‍💻 Author

**Apurva Vinay Waghmode**  
📧 apurvawaghmode1975@gmail.com  
🔗 [GitHub Profile](https://github.com/ApurvaWaghmode)

---


