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

### Branches
CREATE TABLE Branches (
    BranchID INT AUTO_INCREMENT PRIMARY KEY,
    BranchName VARCHAR(150),
    Location VARCHAR(200)
);


### Employees & HR
CREATE TABLE Employees (
    EmployeeID INT AUTO_INCREMENT PRIMARY KEY,
    BranchID INT,
    FirstName VARCHAR(100),
    LastName VARCHAR(100),
    Position VARCHAR(100),
    FOREIGN KEY (BranchID) REFERENCES Branches(BranchID)
);

CREATE TABLE HR (
    HRID INT AUTO_INCREMENT PRIMARY KEY,
    EmployeeID INT,
    HireDate DATE,
    Salary DECIMAL(15,2),
    FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID)
);


### Insurance
CREATE TABLE Insurance (
    PolicyID INT AUTO_INCREMENT PRIMARY KEY,
    CustomerID INT,
    PolicyNumber VARCHAR(50) UNIQUE,
    CoverageAmount DECIMAL(15,2),
    Premium DECIMAL(15,2),
    StartDate DATE,
    EndDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);


### Stocks
CREATE TABLE Stocks (
    StockID INT AUTO_INCREMENT PRIMARY KEY,
    CustomerID INT,
    StockSymbol VARCHAR(10) UNIQUE,
    Quantity INT,
    PurchasePrice DECIMAL(15,2),
    CurrentPrice DECIMAL(15,2),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);


### Mortgages
CREATE TABLE Mortgages (
    MortgageID INT AUTO_INCREMENT PRIMARY KEY,
    CustomerID INT,
    PropertyAddress TEXT,
    LoanAmount DECIMAL(15,2),
    InterestRate DECIMAL(5,2),
    StartDate DATE,
    EndDate DATE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);


### BVN & ATM Request
CREATE TABLE BVN_ATM_Requests (
    RequestID INT AUTO_INCREMENT PRIMARY KEY,
    CustomerID INT,
    RequestType ENUM('BVN','ATM'),
    RequestDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    Status ENUM('Pending','Approved','Rejected'),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

### 📊 Entity Relationship (ER) Overview

Customers → Accounts, Loans, Insurance, Stocks, Mortgages, BVN/ATM Requests.

Accounts → Transactions.

Branches → Employees → HR.

This schema ensures data integrity with foreign keys and supports scalability with indexing on key fields.

### 🚀 Usage

Clone this repository.

Run the SQL scripts in MySQL (or any SQL-based DBMS).

Extend by adding triggers, procedures, or data for testing.

### 📜 License

This project is open-source and free to use.
