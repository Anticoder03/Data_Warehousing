# Data Warehousing Notes

## Topics Covered
1. Data Warehouse
2. Data Warehousing & ETL
3. Data Warehouse Architecture
4. Data Mart
5. Star Schema
6. Snowflake Schema
7. Fact Constellation Schema
8. Fact Table & Dimension Table
9. OLAP Operations
10. OLTP vs OLAP
11. Data Cube
12. Metadata

# 1. What is a Data Warehouse?

A **Data Warehouse** is a system used to **store large amounts of historical data** from different sources so that companies can **analyze data and make business decisions**.

It is **not used for daily operations** (like inserting customer orders), it is used for **analysis and reporting**.

### Simple Example:

A company has data in:

* Sales system
* CRM system
* Website
* Accounting software

All this data is stored in one place → **Data Warehouse** → Used to generate reports like:

* Monthly sales report
* Customer purchase trends
* Profit analysis
* Future predictions

### Definition (Exam Ready):

> A Data Warehouse is a subject-oriented, integrated, time-variant, and non-volatile collection of data used to support management decision making.

These 4 words are VERY important for exams:

* **Subject-Oriented** → Organized by subject (sales, customer, product)
* **Integrated** → Data comes from multiple sources
* **Time-Variant** → Stores historical data (5–10 years)
* **Non-Volatile** → Data is not frequently changed (read-only)

---

# 2. Data Warehousing

**Data Warehousing** is the **process of collecting data from multiple sources, cleaning it, transforming it, and storing it in a Data Warehouse**.

This process is done using **ETL**.

### ETL Process:

* **E – Extract** → Take data from different sources
* **T – Transform** → Clean, format, remove errors
* **L – Load** → Store into Data Warehouse

### Example:

| Source  | Data      |
| ------- | --------- |
| Excel   | Sales     |
| MySQL   | Customers |
| Website | Orders    |
| ERP     | Finance   |

All this goes through ETL → Stored in Data Warehouse → Used for Reports

---

# 3. Data Warehouse Architecture

There are **3 main types of Data Warehouse Architecture**:

1. Single Tier Architecture
2. Two Tier Architecture
3. Three Tier Architecture (Most Important)

---

## (1) Single Tier Architecture

* Only one layer
* Directly connected to source and analysis tools
* Not used much in real life
* Used to reduce data redundancy

**Flow:**
Source → Data Warehouse → Analysis

---

## (2) Two Tier Architecture

![Image](https://scaler.com/topics/images/architecture-of-data-warehoue-image-two-tier-data-warehouse.webp)

![Image](https://scaler.com/topics/images/architecture-of-data-warehoue-image-two-tier.webp)

![Image](https://substackcdn.com/image/fetch/%24s_%21g3db%21%2Cw_1200%2Ch_675%2Cc_fill%2Cf_jpg%2Cq_auto%3Agood%2Cfl_progressive%3Asteep%2Cg_auto/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2F4a38175b-11e8-40ae-879c-ab3ce2027089_2008x1252.png)

* Client – Server architecture
* Data Warehouse + Client tools
* Faster than single tier
* Used in small organizations

**Flow:**
Source → Data Warehouse → Client (Analysis Tools)

---

## (3) Three Tier Architecture (MOST IMPORTANT)

![Image](https://www.gtu-paper-solution.com/upload/2170715/TTA.png)

![Image](https://scaler.com/topics/images/architecture-of-data-warehoue-image-data-warehouse.webp)

![Image](https://www.researchgate.net/publication/3729537/figure/fig1/AS%3A670700968882186%401536918980292/Three-Tier-Architecture-for-Data-Warehouse.png)

This is the **most commonly used architecture**.

### It has 3 layers:

## 1. Bottom Tier – Data Source Layer

This layer contains:

* Databases
* ERP
* CRM
* Flat files
* APIs

Here **ETL process happens**.

So:
Source → ETL → Data Warehouse Database

---

## 2. Middle Tier – OLAP Server

OLAP = **Online Analytical Processing**

This layer is used for:

* Fast data analysis
* Multidimensional analysis
* Cube creation

Types of OLAP:

* **ROLAP** → Relational OLAP
* **MOLAP** → Multidimensional OLAP
* **HOLAP** → Hybrid OLAP

---

## 3. Top Tier – Front End Tools

This layer is used by users:

* Reports
* Dashboards
* Data Visualization
* Data Mining
* BI Tools (Power BI, Tableau)

---

### Flow of Three Tier Architecture:

```
Data Sources
     ↓
     ETL
     ↓
Data Warehouse
     ↓
   OLAP
     ↓
Reports / Dashboard / Analysis
```

---

# 4. Components of Data Warehouse Architecture

| Component         | Description                              |
| ----------------- | ---------------------------------------- |
| Data Sources      | Original data                            |
| ETL               | Extract Transform Load                   |
| Data Warehouse DB | Central storage                          |
| Data Mart         | Small part of DW for specific department |
| OLAP              | Data analysis                            |
| Front End Tools   | Reports & dashboards                     |

---

# 5. Data Mart

**Data Mart** = Small part of Data Warehouse for specific department.

Example:

* Sales Data Mart
* HR Data Mart
* Finance Data Mart

So instead of accessing full Data Warehouse, departments access only their Data Mart.

---

# 6. Difference: Database vs Data Warehouse

| Database                  | Data Warehouse    |
| ------------------------- | ----------------- |
| Used for daily operations | Used for analysis |
| Current data              | Historical data   |
| OLTP                      | OLAP              |
| Frequently updated        | Rarely updated    |
| Normalized                | Denormalized      |

**OLTP** = Online Transaction Processing (banking, orders)
**OLAP** = Online Analytical Processing (reports, analysis)

---

# 7. Short Exam Summary (Very Important)

If exam question comes **“Explain Data Warehouse Architecture”**, write this:

1. Data Warehouse is used for decision making and analysis.
2. Data is collected from multiple sources.
3. ETL process is used to clean and load data.
4. Three tier architecture is used:

   * Bottom Tier – Data Sources & ETL
   * Middle Tier – OLAP Server
   * Top Tier – Front End Tools
5. Users access data using reports, dashboards, and data mining tools.

---


# 1. What is a Schema in Data Warehouse?

A **schema** is the **structure of how data is organized in the data warehouse** — basically how fact table and dimension tables are connected.

There are mainly two schemas:

* Star Schema
* Snowflake Schema

---

# 2. Star Schema

![Image](https://www.researchgate.net/publication/337697722/figure/fig3/AS%3A961667403874309%401606290784356/The-Star-Schema-for-the-Data-Warehouse.png)

![Image](https://docs.precisely.com/docs/sftw/spectrum/22.1/en/webhelp/EnterpriseDataIntegrationGuide/Images/EDI_StarSchemaDbDiagram.png)

![Image](https://www.researchgate.net/profile/Elzbieta-Malinowski/publication/235934897/figure/fig2/AS%3A643206937051136%401530363892251/Example-of-a-star-schema-for-analyzing-sales.png)

## Definition:

**Star Schema** is a data warehouse schema in which a **central fact table** is connected to multiple **dimension tables**, forming a star-like shape.

### Structure:

* One **Fact Table** (center)
* Multiple **Dimension Tables** (around it)

### Example:

**Fact Table (Sales):**

* Sale_ID
* Product_ID
* Customer_ID
* Time_ID
* Amount_Sold

**Dimension Tables:**

* Product (Product_ID, Product_Name, Category)
* Customer (Customer_ID, Customer_Name, City)
* Time (Time_ID, Date, Month, Year)
* Store (Store_ID, Store_Name, Location)

### Important Point:

* Fact table contains **numerical data** (sales, profit, quantity)
* Dimension table contains **descriptive data** (name, city, product)

### Advantages:

* Simple structure
* Fast query performance
* Easy to understand
* Used widely

### Disadvantages:

* Data redundancy (data repeated)
* Takes more storage

---

# 3. Snowflake Schema

![Image](https://media.licdn.com/dms/image/v2/D5612AQGI2Z8ds9HRfA/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1721192465350?e=2147483647\&t=dwGMRhd0fJfGztLzp7Y2m3jEvg99bQz7fzts_U6YztI\&v=beta)

![Image](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b2/Snowflake-schema.png/1280px-Snowflake-schema.png)

![Image](https://media2.dev.to/dynamic/image/width%3D1080%2Cheight%3D1080%2Cfit%3Dcover%2Cgravity%3Dauto%2Cformat%3Dauto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Ftrj6hz7qc22ygzfo6b2o.png)

## Definition:

**Snowflake Schema** is an extension of star schema where **dimension tables are further divided into sub-dimension tables**, forming a snowflake-like structure.

### Structure:

* One **Fact Table**
* Dimension tables are **normalized** into multiple related tables

### Example:

Instead of one Product table, it is divided into:

* Product (Product_ID, Product_Name, Category_ID)
* Category (Category_ID, Category_Name)

So dimension tables are split into smaller tables.

### Advantages:

* Less data redundancy
* Saves storage space
* Better data integrity

### Disadvantages:

* Complex structure
* Slower query performance (because more joins)
* Harder to understand

---

# 4. Star vs Snowflake Schema (Very Important Table for Exam)

| Star Schema     | Snowflake Schema    |
| --------------- | ------------------- |
| Simple          | Complex             |
| Denormalized    | Normalized          |
| Faster queries  | Slower queries      |
| More redundancy | Less redundancy     |
| More storage    | Less storage        |
| Easy to design  | Difficult to design |

---

# 5. Key Terms (Very Important)

| Term            | Meaning                            |
| --------------- | ---------------------------------- |
| Fact Table      | Contains numerical/measurable data |
| Dimension Table | Contains descriptive data          |
| Denormalization | Data is combined in one table      |
| Normalization   | Data divided into multiple tables  |

---

# 6. Exam Definition (Write This)

### Star Schema:

> Star Schema is a data warehouse schema in which a central fact table is connected to multiple dimension tables forming a star structure. It is denormalized and provides fast query performance.

### Snowflake Schema:

> Snowflake Schema is a data warehouse schema in which dimension tables are normalized into multiple related tables forming a snowflake structure. It reduces redundancy but increases complexity.

---

# 7. Simple Diagram Understanding

### Star Schema Flow:

```
        Product
           |
Customer — Fact Table — Time
           |
         Store
```

### Snowflake Schema Flow:

```
        Category
           |
        Product
           |
Customer — Fact Table — Time — Year
           |
         Store — City — State
```

---

# 8. Short 5-Mark Answer Format

If exam question is **“Explain Star and Snowflake Schema”**, write:

1. Star schema has one fact table and multiple dimension tables.
2. Snowflake schema is a normalized form of star schema.
3. Star schema is simple and fast.
4. Snowflake schema is complex but reduces redundancy.
5. Star uses denormalization, Snowflake uses normalization.


----
----

1. Star Schema
2. Snowflake Schema
3. Fact Constellation Schema (Galaxy Schema)

---

# 1. Fact Constellation Schema (Galaxy Schema)

![Image](https://www.researchgate.net/publication/340546587/figure/fig3/AS%3A878651792949249%401586498320920/Fact-Constellation-Schema-or-Multi-Star-Schema.jpg)

![Image](https://www.researchgate.net/publication/220473706/figure/fig3/AS%3A277527865118730%401443179207546/Simplified-data-warehouse-galaxy-schema.png)

![Image](https://cdn.buttercms.com/hDC8gYTwRLqAwSYUFxw6)

## Definition:

> Fact Constellation Schema is a data warehouse schema that contains **multiple fact tables** sharing **dimension tables**.

This is why it is called **constellation/galaxy** — because there are multiple stars (fact tables).

---

# 2. Simple Example

Imagine a company has two types of data:

* Sales
* Shipping

So there will be **two fact tables**:

* Sales_Fact
* Shipping_Fact

But both use same dimension tables:

* Time
* Product
* Customer
* Location

So instead of making separate star schemas, we connect both fact tables to same dimension tables → This becomes **Fact Constellation Schema**.

---

# 3. Structure

| Fact Tables | Dimension Tables |
| ----------- | ---------------- |
| Sales       | Time             |
| Shipping    | Product          |
| Inventory   | Customer         |
|             | Location         |

So:

* **Multiple Fact Tables**
* **Shared Dimension Tables**

This is the main point.

---

# 4. Difference Between All Schemas

| Schema             | Fact Table | Dimension Table | Structure    |
| ------------------ | ---------- | --------------- | ------------ |
| Star               | One        | Denormalized    | Simple       |
| Snowflake          | One        | Normalized      | Complex      |
| Fact Constellation | Multiple   | Shared          | Very Complex |

---

# 5. When Fact Constellation is Used

Used in **large organizations** where there are multiple business processes:

* Sales
* Inventory
* Shipping
* Finance
* HR

Each process has its own fact table but uses common dimensions like time, product, customer.

---

# 6. Diagram Understanding (Simple Way)

### Star Schema:

One fact → Many dimensions

### Snowflake:

One fact → Dimensions → Sub-dimensions

### Fact Constellation:

**Many facts → Shared dimensions**

That’s the easiest way to remember.

---

# 7. Exam Definition (Write This)

> Fact Constellation Schema is a schema in which multiple fact tables share common dimension tables. It is also known as Galaxy Schema and is used for complex data warehouse applications.

---

# 8. Final Summary Table (Very Important)

| Feature          | Star         | Snowflake  | Fact Constellation |
| ---------------- | ------------ | ---------- | ------------------ |
| Fact Tables      | 1            | 1          | Multiple           |
| Dimension Tables | Denormalized | Normalized | Shared             |
| Complexity       | Low          | Medium     | High               |
| Query Speed      | Fast         | Medium     | Slow               |
| Storage          | High         | Low        | Medium             |
| Usage            | Small DW     | Medium DW  | Large DW           |

---

# 9. One Line Memory Trick

Remember like this:

| Schema        | Remember                  |
| ------------- | ------------------------- |
| Star          | One fact, many dimensions |
| Snowflake     | Normalized dimensions     |
| Constellation | Multiple fact tables      |

---

OLAP = **Online Analytical Processing** → Used to analyze data from different dimensions.

Example dimensions:

* Time
* Product
* Location
* Customer

Example data:
Sales of Product A in Pune in January = 5000

Now OLAP operations help us **analyze this data in different ways**.

---

# 1. Roll-Up (Aggregation)

## Meaning:

**Roll-up means summarize data** (go from detailed data to summarized data).

### Example:

You have sales data:

* City → Pune
* State → Maharashtra
* Country → India

Roll-up:

* Pune → Maharashtra → India (Summary level increases)

Or:

* Daily sales → Monthly sales → Yearly sales

### Simple Definition:

> Roll-up is the process of aggregating data by climbing up a hierarchy or by reducing dimensions.

---

# 2. Drill-Down (Opposite of Roll-Up)

![Image](https://cci.drexel.edu/faculty/song/courses/info%20607/tutorial_OLAP/images/rollupanddrilldown.JPG)

![Image](https://www.scaler.com/topics/images/olap-operations-in-data-mining-1.webp)

![Image](https://scaler.com/topics/images/example-olap.webp)

## Meaning:

**Drill-down means going from summary to detailed data**.

### Example:

* Year → Month → Day
* Country → State → City

So:

* India → Maharashtra → Pune

### Simple Definition:

> Drill-down is the process of viewing data in more detail by moving down the hierarchy.

---

# 3. Slice

![Image](https://cci.drexel.edu/faculty/song/courses/info%20607/tutorial_OLAP/images/diceandslice.JPG)

![Image](https://www.scaler.com/topics/images/olap-operations-in-data-mining-3.webp)

![Image](https://www.tutorialspoint.com/dwh/images/slice.jpg)

## Meaning:

**Slice means selecting only one layer from a data cube**.

### Example:

If you have data of:

* Product
* Time
* Location

Slice:

* Select only **Year = 2025**
* Now you analyze only 2025 data

So slice = **one dimension fixed**

### Definition:

> Slice operation selects a single dimension value from a data cube resulting in a smaller sub-cube.

---

# 4. Dice

![Image](https://cci.drexel.edu/faculty/song/courses/info%20607/tutorial_OLAP/images/diceandslice.JPG)

![Image](https://cdn.mescius.io/assets/developer/blogs/legacy/c1/2014/11/OLAP_cube.png)

![Image](https://www.ssp.sh/brain/Pasted%20image%2020240120144605.png)

## Meaning:

**Dice means selecting multiple values from multiple dimensions**.

### Example:

Select:

* Year = 2024, 2025
* Location = Pune, Mumbai
* Product = Laptop

Now you get a smaller cube with selected values.

### Definition:

> Dice operation selects multiple dimension values to produce a sub-cube.

---

# 5. Pivot (Rotate)

![Image](https://www.tutorialspoint.com/dwh/images/pivot.jpg)

![Image](https://www.infodiagram.com/api/img/f%3Apng/w%3A3072/aHR0cHM6Ly9zdG9yYWdlLmdvb2dsZWFwaXMuY29tL2luZm9kaWFncmFtLmFwcHNwb3QuY29tL3B1YmxpYy9zLzQ3Nzc5NjgyNjgyMTQyNzIvcGl2b3Rpbmctcm90YXRpb24tb2xhcC1vcGVyYXRpb24tLnBuZw%3D%3D)

![Image](https://www.researchgate.net/publication/320654558/figure/fig5/AS%3A554074708086788%401509113112098/Pivot-Table-in-Excel-Implements-OLAP-Cube.png)

## Meaning:

**Pivot means rotating the data view** to see data from different perspectives.

### Example:

You change rows into columns:

* Rows → Product
* Columns → Year

After Pivot:

* Rows → Year
* Columns → Product

Same data, different view.

### Definition:

> Pivot operation rotates the data cube to provide an alternative presentation of data.

---

# Summary Table (Very Important for Exam)

| Operation  | Meaning                          |
| ---------- | -------------------------------- |
| Roll-up    | Summary (City → State → Country) |
| Drill-down | Detailed (Year → Month → Day)    |
| Slice      | Select one dimension             |
| Dice       | Select multiple dimensions       |
| Pivot      | Rotate data view                 |

---

# Real Life Example (Easy to Remember)

Imagine a **sales cube**:

| Product | City   | Year | Sales  |
| ------- | ------ | ---- | ------ |
| Laptop  | Pune   | 2024 | 50,000 |
| Laptop  | Mumbai | 2024 | 70,000 |
| Mobile  | Pune   | 2025 | 30,000 |

Now:

* **Roll-up** → Total sales by Year
* **Drill-down** → Sales by City in Maharashtra
* **Slice** → Sales only for 2024
* **Dice** → Sales for Laptop in Pune & Mumbai for 2024–2025
* **Pivot** → Show Product vs Year table

---

# Exam 5-Mark Answer (Write This)

> OLAP operations are used to analyze multidimensional data in a data warehouse. The main OLAP operations are Roll-up, Drill-down, Slice, Dice, and Pivot. Roll-up summarizes data, Drill-down shows detailed data, Slice selects a single dimension, Dice selects multiple dimensions, and Pivot rotates the data for better analysis.



---



# 1. OLTP (Online Transaction Processing)

**OLTP** is used for **day-to-day operations** of an organization.

It handles **transactions** like:

* Insert
* Update
* Delete

### Examples:

* Banking system
* ATM
* Online shopping order system
* Railway reservation
* Billing system

### Example Table (OLTP):

| Order_ID | Customer | Product | Amount | Date |
| -------- | -------- | ------- | ------ | ---- |

This data is **continuously updated**.

### Characteristics of OLTP:

* Used for daily operations
* Large number of small transactions
* Data is current (not historical)
* Fast insert/update/delete
* Highly normalized tables

---

# 2. OLAP (Online Analytical Processing)

**OLAP** is used for **data analysis and decision making**.

It is used to:

* Analyze sales
* Generate reports
* Find trends
* Forecast future sales
* Business Intelligence

### Example:

* Total sales per year
* Top selling product
* Sales by region
* Profit analysis

This uses **historical data** from Data Warehouse.

### Characteristics of OLAP:

* Used for analysis
* Complex queries
* Historical data
* Read-only data
* Denormalized tables
* Slower than OLTP but used for analysis

---

# 3. OLTP vs OLAP (Very Important Table)

| OLTP                          | OLAP                         |
| ----------------------------- | ---------------------------- |
| Online Transaction Processing | Online Analytical Processing |
| Used for daily operations     | Used for analysis            |
| Current data                  | Historical data              |
| Insert, Update, Delete        | Read-only                    |
| Small queries                 | Complex queries              |
| Normalized tables             | Denormalized tables          |
| Faster transactions           | Slower queries               |
| Example: ATM                  | Example: Sales Report        |

---

# 4. Simple Real-Life Example

Imagine a **shopping website**:

| System                              | Type |
| ----------------------------------- | ---- |
| Customer placing order              | OLTP |
| Admin checking monthly sales report | OLAP |
| Updating customer address           | OLTP |
| Finding top selling product         | OLAP |

So:

* **OLTP = Running the business**
* **OLAP = Analyzing the business**

---

# 5. Exam Definition (Write This)

### OLTP:

> OLTP is a system used to manage daily transactions such as insert, update, and delete operations in an organization.

### OLAP:

> OLAP is a system used for analyzing historical data and supporting decision making.

---

# 6. One Line Difference (Easy to Remember)

> OLTP is used to run the business, OLAP is used to analyze the business.

---



---

# Fact Table (Short Explanation)

A **Fact Table** contains **numerical/measurable data** about business processes.

It usually stores:

* Sales amount
* Quantity sold
* Profit
* Revenue
* Number of items

Fact table also contains **foreign keys** that connect to dimension tables.

### Example: Sales Fact Table

| Sale_ID | Product_ID | Customer_ID | Time_ID | Amount | Quantity |
| ------- | ---------- | ----------- | ------- | ------ | -------- |

Here:

* **Amount, Quantity** → Facts (numerical data)
* Other fields → Foreign keys (links to dimension tables)

### One Line Definition (Exam):

> Fact table contains numerical data (measures) and foreign keys that reference dimension tables.

---

# Dimension Table (Short Explanation)

A **Dimension Table** contains **descriptive information** about the data in the fact table.

It describes:

* Product name
* Customer name
* City
* Date
* Category
* Store name

### Example: Product Dimension Table

| Product_ID | Product_Name | Category | Price |
| ---------- | ------------ | -------- | ----- |

### Example: Customer Dimension Table

| Customer_ID | Customer_Name | City | State |
| ----------- | ------------- | ---- | ----- |

### One Line Definition (Exam):

> Dimension table contains descriptive attributes related to fact data.

---

# Fact vs Dimension Table (Quick Difference)

| Fact Table                    | Dimension Table         |
| ----------------------------- | ----------------------- |
| Numerical data                | Descriptive data        |
| Contains measures             | Contains attributes     |
| Large size                    | Smaller size            |
| Connected to dimension tables | Connected to fact table |
| Example: Sales amount         | Example: Product name   |

---

# Easy Way to Remember

Think like this:

| Table           | Contains |
| --------------- | -------- |
| Fact Table      | Numbers  |
| Dimension Table | Details  |

**Fact = Numbers**
**Dimension = Description**

---

# Very Short Exam Answer (2–3 Marks)

> Fact table contains numerical values called measures and foreign keys that connect to dimension tables. Dimension table contains descriptive attributes such as product name, customer name, time, and location. Fact tables are large and dimension tables are smaller.


---

# 1. Data Cube

![Image](https://i.sstatic.net/iGY3r.png)

![Image](https://www.slideteam.net/media/catalog/product/cache/1280x720/d/a/data_cube_products_location_and_time_Slide01.jpg)

![Image](https://www.scaler.com/topics/images/data-cube.webp)

## What is a Data Cube?

A **Data Cube** is a **multidimensional representation of data** used in OLAP to analyze data from multiple dimensions.

In simple words:

> A Data Cube allows data to be viewed and analyzed in multiple dimensions like Time, Product, Location, etc.

---

## Example:

Suppose a company wants to analyze **Sales** based on:

* Time
* Product
* Location

Then the data cube will look like a **3D cube**:

| Dimension | Example          |
| --------- | ---------------- |
| Time      | 2023, 2024, 2025 |
| Product   | Laptop, Mobile   |
| Location  | Pune, Mumbai     |

And inside the cube → **Sales Amount**

So cube = **Dimensions + Measure**

* **Dimensions** → Time, Product, Location
* **Measure** → Sales

---

## Types of Data Cubes

| Type     | Meaning                                    |
| -------- | ------------------------------------------ |
| 1D Cube  | One dimension (Time)                       |
| 2D Cube  | Two dimensions (Time, Product)             |
| 3D Cube  | Three dimensions (Time, Product, Location) |
| n-D Cube | Multiple dimensions                        |

---

## Operations on Data Cube

(You already studied these)

* Roll-up
* Drill-down
* Slice
* Dice
* Pivot

These operations are performed on the **Data Cube**.

---

## Exam Definition:

> A Data Cube is a multidimensional data model used in data warehousing to represent data along multiple dimensions for analysis.

---

# 2. Metadata

## What is Metadata?

**Metadata = Data about Data**

It describes:

* Where data comes from
* How data is stored
* Table structure
* Column names
* Data type
* ETL process
* Data source
* Data refresh time

So metadata is basically **information about the data warehouse data**.

---

## Example:

If a table is:

**Sales Table**

| Column       | Data Type |
| ------------ | --------- |
| Product_ID   | Integer   |
| Product_Name | Varchar   |
| Amount       | Float     |

This information (column name, type, size) = **Metadata**

---

## Types of Metadata

| Type                 | Description                         |
| -------------------- | ----------------------------------- |
| Technical Metadata   | Table structure, data types, schema |
| Business Metadata    | Business meaning of data            |
| Operational Metadata | ETL process info, data refresh time |

---

## Example Table:

| Metadata Type | Example                 |
| ------------- | ----------------------- |
| Technical     | Table name, column name |
| Business      | Meaning of sales        |
| Operational   | Last updated date       |

---

## Why Metadata is Important?

* Helps understand data
* Helps ETL process
* Helps data analysts
* Helps in data integration
* Helps in data management

---

## Exam Definition:

> Metadata is data that describes the structure, operations, and contents of data in a data warehouse.

---

# Final Quick Summary Table

| Topic              | Meaning                     |
| ------------------ | --------------------------- |
| Data Warehouse     | Storage for historical data |
| ETL                | Extract Transform Load      |
| Star Schema        | One fact + dimension tables |
| Snowflake          | Normalized dimensions       |
| Fact Constellation | Multiple fact tables        |
| OLTP               | Daily operations            |
| OLAP               | Data analysis               |
| Data Cube          | Multidimensional data       |
| Metadata           | Data about data             |

---

## Exam Tips

### 2 Marks
- Define Data Warehouse
- Define Metadata
- Define Fact Table
- Define Dimension Table
- What is OLAP?

### 5 Marks
- Explain ETL Process
- Explain OLTP vs OLAP
- Explain Data Cube
- Explain OLAP Operations
- Explain Star Schema

### 10 Marks
- Explain Data Warehouse Architecture
- Explain Star vs Snowflake Schema
- Explain Fact Constellation Schema
- Explain OLAP Operations with example
- Explain Data Warehousing

If you study all these topics, your **Data Warehousing  is complete**.
