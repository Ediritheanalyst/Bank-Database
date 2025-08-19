# Bank-Database
Used MySQL to build a standard bank database. 

# 🌍 AFRICA_BANK Database Schema

### This project is a relational database design for a core banking system called AFRICA_BANK.
It models customers, accounts, loans, insurance, stock investments, mortgages, employees, HR, and more — representing the essential operations of a modern financial institution.

### 📌 Features

Customer Management – Track customer personal details and linked accounts.

Bank Accounts – Supports multiple account types and balances.

Loans – Loan requests, amounts, interest rates, and due dates.

Transactions – Deposits, withdrawals, transfers linked to accounts.

Branch Management – Branch details with assigned employees.

Employee & HR – Employee data, salaries, and HR records.

Insurance – Customer insurance policies with coverage and premiums.

Stocks – Customer stock holdings and market values.

Mortgages – Home loan and mortgage management.

Service Requests – BVN and ATM card requests linked to customers.

## 🏗️ Database Schema
### customers
CREATE TABLE Customers (
    CustomerID INT AUTO_INCREMENT PRIMARY KEY,
    FirstName VARCHAR(100),
    LastName VARCHAR(100),
    Email VARCHAR(150) UNIQUE,
    Phone VARCHAR(20),
    Address TEXT
);

### Accounts
CREATE TABLE Accounts (
    AccountID INT AUTO_INCREMENT PRIMARY KEY,
    CustomerID INT,
    AccountNumber VARCHAR(20) UNIQUE,
    AccountType VARCHAR(50),
    Balance DECIMAL(15,2),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);


### Loans
CREATE TABLE Loans (
    LoanID INT AUTO_INCREMENT PRIMARY KEY,
    CustomerID INT,
    LoanAmount DECIMAL(15,2),
    InterestRate DECIMAL(5,2),
    LoanDate DATE,
    DueDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);


### Transaction
CREATE TABLE Transactions (
    TransactionID INT AUTO_INCREMENT PRIMARY KEY,
    AccountID INT,
    TransactionType ENUM('Deposit','Withdrawal','Transfer'),
    Amount DECIMAL(15,2),
    TransactionDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (AccountID) REFERENCES Accounts(AccountID)
);
