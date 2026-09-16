# sql.proct1
Data Digger is a SQL-based database management project designed to manage customer, product, order, and order details. It performs CRUD operations, data retrieval, filtering, sorting, aggregation functions, and JOIN queries to generate useful reports.



# 🔎 Data Digger — SQL Data Analysis Project

![MySQL](https://img.shields.io/badge/MySQL-Database-blue?style=for-the-badge\&logo=mysql)
![SQL](https://img.shields.io/badge/SQL-Data%20Analysis-orange?style=for-the-badge)
![Database](https://img.shields.io/badge/Database-Relational-purple?style=for-the-badge)
![CRUD](https://img.shields.io/badge/SQL-CRUD-success?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge)

# 📌 Project Overview

**Data Digger** is a practical **MySQL SQL Data Analysis project** designed to demonstrate how relational business data can be stored, managed, queried, transformed and analyzed using SQL.

The project simulates a simple **e-commerce/order management system** containing information about:

* 👥 Customers
* 🛒 Orders
* 📦 Products
* 🧾 Order Details

The database connects customers with their orders and connects orders with the products purchased.

This project demonstrates practical SQL concepts ranging from basic database operations to multi-table JOINs and aggregate analysis.

---

# 🎯 Project Objectives

The main objectives of the **Data Digger** project are:

1. Create a relational e-commerce database.
2. Store customer information.
3. Store customer orders.
4. Maintain product information.
5. Track products included in each order.
6. Establish relationships between tables.
7. Perform CRUD operations.
8. Filter customer and order information.
9. Analyze order values.
10. Analyze product prices and stock.
11. Calculate total revenue.
12. Identify top ordered products.
13. Count product sales.
14. Combine information using SQL JOINs.
15. Generate a complete order report.
16. Practice real-world SQL data-analysis techniques.

---

# 🗄️ Database Information

## Database Name

```text
DataDigger
```

The database is created using:

```sql
CREATE DATABASE DataDigger;

USE DataDigger;
```

---

# 🏗️ Database Architecture

The database contains **4 main tables**:

```text
DataDigger
│
├── Customers
│
├── Orders
│
├── Products
│
└── OrderDetails
```

The tables are connected through primary-key and foreign-key relationships.

---

# 🔗 Entity Relationship Structure

The overall relationship can be represented as:

```text
┌──────────────────────┐
│      Customers       │
├──────────────────────┤
│ CustomerID PK        │
│ Name                 │
│ Email                │
│ Address              │
└──────────┬───────────┘
           │
           │ 1 : Many
           ▼
┌──────────────────────┐
│        Orders        │
├──────────────────────┤
│ OrderID PK           │
│ CustomerID FK        │
│ OrderDate            │
│ TotalAmount          │
└──────────┬───────────┘
           │
           │ 1 : Many
           ▼
┌──────────────────────┐
│    OrderDetails      │
├──────────────────────┤
│ OrderDetailID PK     │
│ OrderID FK           │
│ ProductID FK         │
│ Quantity             │
│ SubTotal             │
└──────────┬───────────┘
           │
           │ Many : 1
           ▼
┌──────────────────────┐
│       Products       │
├──────────────────────┤
│ ProductID PK         │
│ ProductName          │
│ Price                │
│ Stock                │
└──────────────────────┘
```

---

# 🔄 Relationship Explanation

## Customer → Orders

One customer can place multiple orders.

```text
1 Customer
     ↓
Many Orders
```

Example:

```text
Alice
 ├── Order 1
 └── Order 4
```

---

## Order → OrderDetails

One order can contain multiple product line items.

```text
1 Order
   ↓
Many OrderDetails
```

---

## Product → OrderDetails

One product can appear in multiple order-detail records.

```text
1 Product
    ↓
Many OrderDetails
```

---

## Orders ↔ Products

Orders and products have a **many-to-many relationship**.

This relationship is handled through the `OrderDetails` table.

```text
Orders
   │
   ▼
OrderDetails
   ▲
   │
Products
```

This is a common relational database design pattern used in e-commerce systems.

---

# 📊 Table 1 — Customers

The `Customers` table stores customer information.

## Structure

| Column     | Data Type    | Description               |
| ---------- | ------------ | ------------------------- |
| CustomerID | INT          | Unique customer ID        |
| Name       | VARCHAR(100) | Customer name             |
| Email      | VARCHAR(100) | Customer email            |
| Address    | VARCHAR(200) | Customer location/address |

## Primary Key

```text
CustomerID
```

The `CustomerID` uniquely identifies each customer.

---

# 🛒 Table 2 — Orders

The `Orders` table stores information about customer orders.

## Structure

| Column      | Data Type     | Description                   |
| ----------- | ------------- | ----------------------------- |
| OrderID     | INT           | Unique order ID               |
| CustomerID  | INT           | Customer who placed the order |
| OrderDate   | DATE          | Date of order                 |
| TotalAmount | DECIMAL(10,2) | Total order amount            |

## Primary Key

```text
OrderID
```

## Foreign Key

```text
CustomerID
```

The foreign key connects orders to customers.

```text
Orders.CustomerID
       ↓
Customers.CustomerID
```

---

# 📦 Table 3 — Products

The `Products` table stores product information.

## Structure

| Column      | Data Type     | Description         |
| ----------- | ------------- | ------------------- |
| ProductID   | INT           | Unique product ID   |
| ProductName | VARCHAR(100)  | Product name        |
| Price       | DECIMAL(10,2) | Product price       |
| Stock       | INT           | Available inventory |

Example products:

* Laptop
* Mobile
* Keyboard
* Mouse
* Headphones

---

# 🧾 Table 4 — OrderDetails

The `OrderDetails` table stores individual products included in orders.

## Structure

| Column        | Data Type     | Description             |
| ------------- | ------------- | ----------------------- |
| OrderDetailID | INT           | Unique order-detail ID  |
| OrderID       | INT           | Related order           |
| ProductID     | INT           | Related product         |
| Quantity      | INT           | Number of units ordered |
| SubTotal      | DECIMAL(10,2) | Line-item value         |

## Foreign Keys

```text
OrderID → Orders.OrderID
ProductID → Products.ProductID
```

This table acts as a bridge between orders and products.

---

# 🧩 Database Design Concept

The project follows a simple relational model:

```text
Customer
   ↓
Order
   ↓
Order Details
   ↓
Product
```

For example:

```text
Alice
  ↓
Order #1
  ↓
Laptop × 1
  ↓
Subtotal = 55,000
```

This structure allows detailed analysis of customer purchases and product sales.

---

# 📥 Sample Customer Data

The project includes five sample customers:

| CustomerID | Name    | Email                                         | City    |
| ---------: | ------- | --------------------------------------------- | ------- |
|          1 | Alice   | [alice@gmail.com](mailto:alice@gmail.com)     | Delhi   |
|          2 | Bob     | [bob@gmail.com](mailto:bob@gmail.com)         | Mumbai  |
|          3 | Charlie | [charlie@gmail.com](mailto:charlie@gmail.com) | Jaipur  |
|          4 | David   | [david@gmail.com](mailto:david@gmail.com)     | Udaipur |
|          5 | Emma    | [emma@gmail.com](mailto:emma@gmail.com)       | Pune    |

---

# 🛒 Sample Order Data

The project contains sample orders:

| OrderID | CustomerID | OrderDate  | TotalAmount |
| ------: | ---------: | ---------- | ----------: |
|       1 |          1 | 2026-05-01 |        2500 |
|       2 |          2 | 2026-05-05 |        1500 |
|       3 |          3 | 2026-05-10 |        3000 |
|       4 |          1 | 2026-05-15 |        4500 |
|       5 |          4 | 2026-05-20 |        1200 |

---

# 📦 Sample Product Data

| ProductID | ProductName | Price | Stock |
| --------: | ----------- | ----: | ----: |
|         1 | Laptop      | 55000 |    10 |
|         2 | Mobile      | 20000 |    15 |
|         3 | Keyboard    |  1000 |    30 |
|         4 | Mouse       |   500 |    50 |
|         5 | Headphones  |  2500 |    20 |

---

# 🧾 Sample Order Details

| OrderDetailID | OrderID | ProductID | Quantity | SubTotal |
| ------------: | ------: | --------: | -------: | -------: |
|             1 |       1 |         1 |        1 |    55000 |
|             2 |       2 |         2 |        1 |    20000 |
|             3 |       3 |         5 |        2 |     5000 |
|             4 |       4 |         3 |        3 |     3000 |
|             5 |       5 |         4 |        2 |     1000 |

---

# 🔄 CRUD Operations

The project demonstrates basic database operations.

```text
C → Create
R → Read
U → Update
D → Delete
```

---

# 👥 Customer Queries

## 1️⃣ Retrieve All Customers

```sql
SELECT * FROM Customers;
```

### Purpose

Displays all records from the `Customers` table.

---

# 2️⃣ Update Customer Address

```sql
UPDATE Customers
SET Address = 'Bangalore'
WHERE CustomerID = 2;
```

### Purpose

Updates the address of the customer with `CustomerID = 2`.

This demonstrates the `UPDATE` operation.

---

# 3️⃣ Delete Customer

```sql
DELETE FROM Customers
WHERE CustomerID = 5;
```

### Purpose

Deletes the customer with ID 5.

### Important

Because `Customers` is related to `Orders`, deleting a customer who has related orders may fail depending on foreign-key constraints.

In this sample dataset, Customer 5 has no orders, so the deletion can proceed.

---

# 4️⃣ Find Customer Named Alice

```sql
SELECT *
FROM Customers
WHERE Name = 'Alice';
```

### Purpose

Filters customers based on their name.

### SQL Concept

```text
WHERE
```

---

# 🛒 Orders Analysis

# 5️⃣ Retrieve Orders for a Specific Customer

```sql
SELECT *
FROM Orders
WHERE CustomerID = 1;
```

### Purpose

Displays all orders placed by Customer 1.

This can be used for customer purchase-history analysis.

---

# 6️⃣ Update Order Amount

```sql
UPDATE Orders
SET TotalAmount = 5000
WHERE OrderID = 2;
```

### Purpose

Updates the total amount of Order 2.

This demonstrates modification of existing transactional data.

---

# 7️⃣ Delete an Order

```sql
DELETE FROM Orders
WHERE OrderID = 5;
```

### Purpose

Deletes Order 5.

### Important

Because `OrderDetails` contains a foreign key referencing `Orders`, deleting an order that has related order-detail records may be blocked by the foreign-key constraint.

In a production database, related records would need to be handled according to the chosen referential-action design.

---

# 8️⃣ Orders From the Last 30 Days

```sql
SELECT *
FROM Orders
WHERE OrderDate >= CURDATE() - INTERVAL 30 DAY;
```

### Purpose

Returns orders placed within the previous 30 days relative to the current date.

### SQL Concepts

```text
CURDATE()
INTERVAL
DATE arithmetic
WHERE
```

Because `CURDATE()` changes over time, the result is dynamic.

---

# 📊 9️⃣ Highest, Lowest and Average Order Amount

```sql
SELECT
    MAX(TotalAmount) AS HighestOrder,
    MIN(TotalAmount) AS LowestOrder,
    AVG(TotalAmount) AS AverageOrder
FROM Orders;
```

### Purpose

Calculates three important order metrics:

* Highest order value
* Lowest order value
* Average order value

### Aggregate Functions

```text
MAX()
MIN()
AVG()
```

These functions are commonly used in business reporting.

---

# 📦 Product Analysis

# 🔟 Products Sorted by Price

```sql
SELECT *
FROM Products
ORDER BY Price DESC;
```

### Purpose

Displays products from highest price to lowest price.

### SQL Concept

```text
ORDER BY ... DESC
```

---

# 1️⃣1️⃣ Update Product Price

```sql
UPDATE Products
SET Price = 22000
WHERE ProductID = 2;
```

### Purpose

Updates the price of the Mobile product.

This demonstrates how product pricing can be modified in the database.

---

# 1️⃣2️⃣ Delete Out-of-Stock Products

```sql
DELETE FROM Products
WHERE Stock = 0;
```

### Purpose

Removes products whose stock quantity is zero.

This represents a simple inventory-management operation.

### Important

If a product is referenced by `OrderDetails`, deleting it may be blocked by the foreign-key constraint unless the database has an appropriate referential-action rule.

---

# 1️⃣3️⃣ Products Between ₹500 and ₹2,000

```sql
SELECT *
FROM Products
WHERE Price BETWEEN 500 AND 2000;
```

### Purpose

Finds products within a specific price range.

### SQL Concept

```text
BETWEEN
```

The range is inclusive.

---

# 1️⃣4️⃣ Most Expensive and Cheapest Product Price

```sql
SELECT
    MAX(Price) AS MostExpensive,
    MIN(Price) AS Cheapest
FROM Products;
```

### Purpose

Finds the highest and lowest product prices.

### Functions

```text
MAX()
MIN()
```

---

# 🧾 Order Details Analysis

# 1️⃣5️⃣ Retrieve Details for a Specific Order

```sql
SELECT *
FROM OrderDetails
WHERE OrderID = 1;
```

### Purpose

Shows all product-level details belonging to Order 1.

---

# 💰 1️⃣6️⃣ Calculate Total Revenue

```sql
SELECT
    SUM(SubTotal) AS TotalRevenue
FROM OrderDetails;
```

### Purpose

Calculates the total revenue represented by the `SubTotal` values in the order-detail table.

### Function

```text
SUM()
```

### Analytical Concept

```text
Individual SubTotals
        ↓
       SUM()
        ↓
Total Revenue
```

---

# 🏆 1️⃣7️⃣ Top 3 Most Ordered Products

```sql
SELECT
    ProductID,
    SUM(Quantity) AS TotalOrdered
FROM OrderDetails
GROUP BY ProductID
ORDER BY TotalOrdered DESC
LIMIT 3;
```

### Purpose

Identifies the top three products based on total quantity ordered.

### SQL Concepts

* `SUM()`
* `GROUP BY`
* `ORDER BY`
* `DESC`
* `LIMIT`

### Analytical Flow

```text
Product
   ↓
Quantity
   ↓
SUM()
   ↓
Total Ordered
   ↓
Sort Descending
   ↓
Top 3
```

---

# 1️⃣8️⃣ Count How Many Times Each Product Was Sold

```sql
SELECT
    ProductID,
    COUNT(*) AS TimesSold
FROM OrderDetails
GROUP BY ProductID;
```

### Purpose

Counts the number of order-detail records associated with each product.

### SQL Concepts

```text
COUNT()
GROUP BY
```

### Important Distinction

`COUNT(*)` here counts **order-detail rows**, not total units sold.

For total units sold, `SUM(Quantity)` is more appropriate.

---

# 🔗 JOIN Analysis

One of the most important parts of the Data Digger project is combining information from multiple tables.

---

# 1️⃣9️⃣ Customer Order Details

```sql
SELECT
    Customers.Name,
    Orders.OrderID,
    Orders.TotalAmount
FROM Customers
INNER JOIN Orders
ON Customers.CustomerID = Orders.CustomerID;
```

### Purpose

Connects customers with their orders.

Example output concept:

```text
Alice
  ↓
Order 1
  ↓
Order Amount
```

### SQL Concept

```text
INNER JOIN
```

Only matching customer and order records are returned.

---

# 2️⃣0️⃣ Product Order Details

```sql
SELECT
    Products.ProductName,
    OrderDetails.Quantity
FROM Products
INNER JOIN OrderDetails
ON Products.ProductID = OrderDetails.ProductID;
```

### Purpose

Connects products with their order quantities.

Example:

```text
Laptop → Quantity 1
Mobile → Quantity 1
Headphones → Quantity 2
```

---

# 📋 2️⃣1️⃣ Complete Order Report

This is the most comprehensive JOIN query in the project.

```sql
SELECT
    Customers.Name,
    Orders.OrderID,
    Products.ProductName,
    OrderDetails.Quantity,
    OrderDetails.SubTotal
FROM Customers
JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
JOIN OrderDetails
ON Orders.OrderID = OrderDetails.OrderID
JOIN Products
ON Products.ProductID = OrderDetails.ProductID;
```

### Purpose

Combines all four tables into one report.

The result provides:

* Customer name
* Order ID
* Product name
* Quantity
* Subtotal

### Data Flow

```text
Customers
    ↓
Orders
    ↓
OrderDetails
    ↓
Products
    ↓
Complete Order Report
```

This type of query is useful for creating detailed business reports.

---

# 🧠 SQL Concepts Demonstrated

The project covers several levels of SQL.

## Beginner

```text
CREATE DATABASE
USE
CREATE TABLE
INSERT
SELECT
WHERE
ORDER BY
```

## Intermediate

```text
UPDATE
DELETE
INNER JOIN
BETWEEN
GROUP BY
LIMIT
COUNT()
SUM()
AVG()
MAX()
MIN()
```

## Advanced / Analytical

```text
Multi-table JOINs
Foreign-key relationships
Date arithmetic
Aggregate analysis
Top-N analysis
Relational data modeling
```

---

# 📚 SQL Functions Used

| Function / Feature | Purpose                    |
| ------------------ | -------------------------- |
| `MAX()`            | Find maximum value         |
| `MIN()`            | Find minimum value         |
| `AVG()`            | Calculate average          |
| `SUM()`            | Calculate total            |
| `COUNT()`          | Count records              |
| `CURDATE()`        | Get current date           |
| `INTERVAL`         | Perform date arithmetic    |
| `BETWEEN`          | Filter a range             |
| `ORDER BY`         | Sort data                  |
| `GROUP BY`         | Group records              |
| `LIMIT`            | Restrict number of results |
| `INNER JOIN`       | Combine matching records   |

---

# 🔐 Database Constraints

The project uses important relational database constraints.

## Primary Key

Each main table has a unique identifier.

Examples:

```text
Customers → CustomerID
Orders → OrderID
Products → ProductID
OrderDetails → OrderDetailID
```

---

## Foreign Keys

Foreign keys maintain relationships between tables.

### Orders

```sql
FOREIGN KEY (CustomerID)
REFERENCES Customers(CustomerID)
```

### OrderDetails

```sql
FOREIGN KEY (OrderID)
REFERENCES Orders(OrderID)
```

and:

```sql
FOREIGN KEY (ProductID)
REFERENCES Products(ProductID)
```

---

# 📊 Analytical Questions Answered

The Data Digger project can answer practical business questions such as:

## Customer Questions

* Who are the customers?
* Where are customers located?
* Which customer placed a particular order?
* Which customers have order history?
* How can customer information be updated?

## Order Questions

* What orders has a customer placed?
* What is the highest order value?
* What is the lowest order value?
* What is the average order value?
* Which orders were placed recently?

## Product Questions

* Which products are available?
* Which product is the most expensive?
* Which product is the cheapest?
* Which products fall within a specific price range?
* Which products are out of stock?
* Which products are ordered most frequently?

## Revenue Questions

* What is the total revenue from order details?
* Which products contribute to order quantities?
* What are the top ordered products?

---

# 💼 Business Use Cases

This project represents a simplified e-commerce data system.

It can be used as a foundation for:

### 🛒 E-commerce Analysis

* Order analysis
* Product analysis
* Customer analysis
* Revenue analysis
* Inventory analysis

### 👥 Customer Analytics

Businesses can analyze:

* Customer purchase history
* Customer locations
* Number of orders
* Customer spending

### 📦 Inventory Analytics

Product data can be used to identify:

* Available stock
* Out-of-stock products
* Product prices
* Product demand

### 💰 Revenue Analytics

Order-detail data can be used to calculate:

* Total revenue
* Product-level revenue
* Order-level revenue
* Sales trends

---

# 🔄 Complete Data Flow

The project follows this data flow:

```text
                 CUSTOMER
                     │
                     ▼
                   ORDER
                     │
                     ▼
              ORDER DETAILS
                     │
                     ▼
                  PRODUCT
```

The database can therefore answer:

```text
Who bought?
    ↓
What did they buy?
    ↓
How many did they buy?
    ↓
How much was generated?
```

---

# 🧪 Data Validation

The project includes queries to display all table records.

```sql
SELECT * FROM Customers;

SELECT * FROM Orders;

SELECT * FROM Products;

SELECT * FROM OrderDetails;
```

These queries can be used to verify:

* Table creation
* Data insertion
* Updates
* Deletions
* Relationships
* Final table state

---

# ⚠️ Important Execution Notes

There are a few important points when running this SQL file from top to bottom.

## Customer Deletion

This statement:

```sql
DELETE FROM Customers
WHERE CustomerID = 5;
```

is safe for the provided sample data because Customer 5 does not have an order.

If a customer has related records in `Orders`, the foreign-key constraint may prevent deletion.

---

## Order Deletion

This statement:

```sql
DELETE FROM Orders
WHERE OrderID = 5;
```

comes before the final table-display queries.

Because Order 5 has a corresponding record in `OrderDetails`, the delete may be rejected by the foreign-key constraint.

To make the script fully executable from top to bottom, the related `OrderDetails` record would need to be handled first, or the database would need an appropriate `ON DELETE` rule.

---

## Product Deletion

This statement:

```sql
DELETE FROM Products
WHERE Stock = 0;
```

does not delete anything with the current sample data because all products have stock greater than zero.

If a product has related `OrderDetails`, its deletion may also be restricted by the foreign-key relationship.

---

# 🗑️ Optional Database Cleanup

The project includes an optional section to remove the tables.

Because of foreign-key dependencies, the child tables should be removed before their parent tables.

Correct dependency order:

```text
OrderDetails
      ↓
Orders
      ↓
Customers

Products
```

Therefore:

```sql
DROP TABLE OrderDetails;
DROP TABLE Orders;
DROP TABLE Products;
DROP TABLE Customers;
```

This removes the project tables from the database.

---

# ▶️ How to Run the Project

## Step 1 — Install MySQL

Install:

* MySQL Server
* MySQL Workbench

or another MySQL-compatible SQL client.

---

## Step 2 — Open the SQL File

Open the project SQL file:

```text
DataDigger.sql
```

---

## Step 3 — Create Database

Run:

```sql
CREATE DATABASE DataDigger;

USE DataDigger;
```

---

## Step 4 — Create Tables

Run the four `CREATE TABLE` statements.

The tables will be created in the required relational order.

---

## Step 5 — Insert Sample Data

Run all `INSERT INTO` statements.

---

## Step 6 — Run CRUD Queries

Execute the customer, order and product CRUD queries.

---

## Step 7 — Run Analytical Queries

Execute:

* Revenue analysis
* Product analysis
* Order analysis
* Aggregate functions
* JOIN queries

---

## Step 8 — Verify Data

Run:

```sql
SELECT * FROM Customers;
SELECT * FROM Orders;
SELECT * FROM Products;
SELECT * FROM OrderDetails;
```

---

# 📂 Recommended GitHub Project Structure

```text
Data-Digger-SQL/
│
├── DataDigger.sql
│
├── README.md
│
└── Screenshots/
    ├── database.png
    ├── customers.png
    ├── orders.png
    ├── products.png
    ├── orderdetails.png
    ├── revenue-analysis.png
    ├── joins.png
    └── complete-order-report.png
```

---

# 🚀 Future Improvements

The current project can be expanded into a much larger e-commerce analytics system.

## 👥 Customer Analytics

Add:

* Customer lifetime value
* Total spending per customer
* Number of orders per customer
* Repeat customers
* Customer segmentation
* Customer purchase frequency

---

## 🛒 Order Analytics

Add:

* Monthly sales
* Yearly sales
* Average order value
* Sales growth
* Daily sales
* Monthly order trends
* Order status
* Payment status

---

## 📦 Product Analytics

Add:

* Product category
* Brand
* Supplier
* Cost price
* Profit
* Profit margin
* Stock alerts
* Product performance

---

## 📊 Advanced SQL

Future versions can include:

```text
CTEs
Window Functions
ROW_NUMBER()
RANK()
DENSE_RANK()
LAG()
LEAD()
CASE
Views
Stored Procedures
Triggers
Indexes
Query Optimization
```

---

# 📈 Power BI / Python Integration

The Data Digger database can also become the data source for a complete Data Analytics project.

```text
             MySQL
               ↓
          Data Digger
               ↓
      ┌────────┴────────┐
      ↓                 ↓
   Python            Power BI
      ↓                 ↓
 Analysis            Dashboard
      └────────┬────────┘
               ↓
        Business Insights
```

Possible dashboard KPIs:

```text
Total Revenue
Total Orders
Total Customers
Total Products
Average Order Value
Top Products
Customer Spending
Sales by City
Product Stock
```

---

# 🎓 Learning Outcomes

By completing this project, the following practical SQL skills are demonstrated:

* Relational database design
* MySQL
* Table creation
* Primary keys
* Foreign keys
* Data insertion
* CRUD operations
* Data filtering
* Data sorting
* Aggregate functions
* JOIN operations
* Revenue calculation
* Product analysis
* Customer analysis
* Inventory analysis
* Date filtering
* Top-N analysis
* GROUP BY
* Business-oriented SQL queries

---

# 💼 Data Analyst Skills Demonstrated

This project demonstrates several skills that are useful in a Data Analyst workflow.

```text
DATA ANALYST SQL SKILLS
│
├── Database Understanding
├── Relational Da
```
