# 💼 Portfolio Management System

portfolio management case study.docx - Overview of the application.

---

A cloud-ready, microservices-based financial application built using **.NET Core**, **SQL Server**, and **MVC**, which allows customers to **view and manage their investment portfolios**, including stocks and mutual funds. Designed with a secure, modular architecture and real-time net-worth computation logic.

---

## 🚀 Key Features

### 🧑 Customer Portal
- Login with authentication (JWT-based)
- View investment holdings (stocks & mutual funds)
- View calculated **net-worth**
- Sell assets (partial/full) and get updated balance

### 🧩 Microservices
- **Daily Share Price Service** – fetches real-time stock prices
- **Daily Mutual Fund NAV Service** – retrieves NAV values
- **Networth Service** – calculates total net-worth and performs asset sale logic
- **Authorization Service** – handles JWT-based security between services

---

## 🧰 Tech Stack

| Layer        | Technologies Used                                         |
|--------------|-----------------------------------------------------------|
| Frontend     | ASP.NET MVC             |
| Backend      | .NET Core Web API (REST microservices)                    |
| Auth         | JWT Token, Role-based Authorization                       |
| Database     | **SQL Server**                                            |
| DevOps       | Docker, CI/CD, Azure (for cloud hosting)   |
| Testing      | xUnit / NUnit, Moq (100% unit test coverage)              |
| Documentation| Swagger/OpenAPI                                           |

---

## 🧾 Microservice Summary & APIs

### 1. 🧠 **Networth Microservice**
- **GET** `/calculateNetworth`
  - Input: PortfolioDetails JSON (list of stocks & mutual funds)
  - Output: Total net-worth in INR
- **POST** `/sellAssets`
  - Input: currentPortfolio + saleRequest
  - Output: `AssetSaleResponse` with updated balance & status

### 2. 📈 **Daily Share Price Microservice**
- **GET** `/dailySharePrice?stockName=XYZ`
  - Output: Stock price in INR

### 3. 📊 **Daily Mutual Fund NAV Microservice**
- **GET** `/mutualFundNav?fundName=ABC`
  - Output: Mutual Fund NAV in INR

### 4. 🔐 **Authorization Microservice**
- JWT token generation and validation
- Token expiry: 15 mins
- Required for all service-to-service API communication

---

## 🗂 Database Schema (SQL Server)

### `Stocks`
| Field       | Type        |
|-------------|-------------|
| StockId     | INT (PK)    |
| StockName   | NVARCHAR(50)|
| StockValue  | DECIMAL     |

### `MutualFunds`
| Field             | Type        |
|-------------------|-------------|
| MutualFundId      | INT (PK)    |
| MutualFundName    | NVARCHAR(50)|
| NAVValue          | DECIMAL     |

### `Portfolios`
| Field        | Type         |
|--------------|--------------|
| PortfolioId  | INT (PK)     |
| CustomerId   | INT          |
| StockList    | JSON         |
| MutualFundList | JSON       |

---

## 🧪 Unit Testing

- Test Framework: **NUnit / xUnit**
- Mocking: **Moq** used for simulating DB, external service calls
- Target: **100% code coverage**
- CI/CD: Automated test report generation via pipelines

---

## 💻 Run Locally

### Prerequisites
- .NET Core SDK
- SQL Server 2014+
- Node.js + Angular CLI (for frontend)
- Docker (optional)

### Steps

```bash
# Clone the project
git clone https://github.com/dhurfa/portfolio-management.git

# Setup SQL Server database
Run scripts in: /Database/create-schema.sql

# Start backend microservices
dotnet run --project NetworthService
dotnet run --project SharePriceService
dotnet run --project MutualFundService
dotnet run --project AuthService

# Start Angular frontend
cd CustomerPortal
npm install
ng serve

# Access the app
Frontend: http://localhost:4200/
Backend API: http://localhost:5000/



