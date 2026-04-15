# 📘 Data Dictionary

## 📊 Overview
This document describes the structure and meaning of each dataset used in the **E-Commerce Sales Analytics Power BI Dashboard**.  
The data model follows a **Star Schema**, with a central **fact table** connected to multiple **dimension tables**.

---

## 🧾 1. fact_table.csv

**Description:**  
Contains transactional sales data. Each row represents a single sales transaction.

| Column Name     | Data Type | Description |
|-----------------|-----------|-------------|
| transaction_id  | Integer   | Unique identifier for each transaction |
| customer_id     | Integer   | Unique identifier linking to `customer_dim` |
| item_id         | Integer   | Unique identifier linking to `item_dim` |
| store_id        | Integer   | Unique identifier linking to `store_dim` |
| time_id         | Integer   | Unique identifier linking to `time_dim` |
| quantity        | Integer   | Number of units sold in the transaction |
| unit_price      | Decimal   | Price per unit of the product |
| total_price     | Decimal   | Total transaction value (`quantity × unit_price`) |

---

## 👤 2. customer_dim.csv

**Description:**  
Stores information about customers.

| Column Name     | Data Type | Description |
|-----------------|-----------|-------------|
| customer_id     | Integer   | Unique identifier for each customer |
| customer_name   | Text      | Name of the customer |
| gender          | Text      | Gender of the customer |
| city            | Text      | City where the customer resides |
| state           | Text      | State or region of the customer |
| country         | Text      | Country of the customer |
| segment         | Text      | Customer segment (e.g., Consumer, Corporate) |

---

## 📦 3. item_dim.csv

**Description:**  
Contains product-related information.

| Column Name     | Data Type | Description |
|-----------------|-----------|-------------|
| item_id         | Integer   | Unique identifier for each product |
| item_name       | Text      | Name or description of the product |
| category        | Text      | Product category |
| sub_category    | Text      | Product sub-category |
| brand           | Text      | Brand of the product |
| unit_cost       | Decimal   | Cost per unit of the product |

---

## 🏬 4. store_dim.csv

**Description:**  
Provides details about store or sales locations.

| Column Name     | Data Type | Description |
|-----------------|-----------|-------------|
| store_id        | Integer   | Unique identifier for each store |
| store_name      | Text      | Name of the store |
| city            | Text      | City where the store is located |
| state           | Text      | State or region |
| country         | Text      | Country |
| region          | Text      | Sales region (e.g., North, South) |

---

## 📅 5. time_dim.csv

**Description:**  
Contains date-related attributes used for time intelligence analysis.

| Column Name     | Data Type | Description |
|-----------------|-----------|-------------|
| time_id         | Integer   | Unique identifier for each date |
| date            | Date      | Full calendar date |
| day             | Integer   | Day of the month |
| month           | Integer   | Month number (1–12) |
| month_name      | Text      | Name of the month |
| quarter         | Integer   | Quarter of the year (1–4) |
| year            | Integer   | Calendar year |
| week_number     | Integer   | Week number of the year |

---

## 💳 6. Trans_dim.csv

**Description:**  
Contains additional transaction-related information such as payment and order details.

| Column Name        | Data Type | Description |
|--------------------|-----------|-------------|
| transaction_id     | Integer   | Unique identifier linking to `fact_table` |
| order_type         | Text      | Type of order (e.g., Online, In-Store) |
| payment_method     | Text      | Payment method (e.g., Cash, Card, UPI) |
| shipping_mode      | Text      | Shipping method used |
| order_priority     | Text      | Priority level of the order |

---

## 🔗 Data Model Relationships

The datasets are connected using the following relationships:

| From Table      | Column        | To Table        | Column        | Relationship |
|-----------------|---------------|-----------------|---------------|-------------|
| fact_table      | customer_id   | customer_dim    | customer_id   | Many-to-One |
| fact_table      | item_id       | item_dim        | item_id       | Many-to-One |
| fact_table      | store_id      | store_dim       | store_id      | Many-to-One |
| fact_table      | time_id       | time_dim        | time_id       | Many-to-One |
| fact_table      | transaction_id| Trans_dim       | transaction_id| One-to-One / Many-to-One |

---

## ⭐ Key Features of the Data Model

- **Star Schema:** Ensures efficient querying and performance in Power BI.
- **Time Intelligence:** Enabled through the `time_dim` table.
- **Scalability:** Additional dimensions can be easily integrated.
- **Data Integrity:** Relationships maintain referential consistency.

---

## 🛠️ Tools Used

- **Power BI Desktop**
- **Power Query**
- **DAX (Data Analysis Expressions)**
- **CSV Data Sources**

---

