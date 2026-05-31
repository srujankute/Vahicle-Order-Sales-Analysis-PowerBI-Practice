# Vahicle-Order-Sales-Analysis-PowerBI-Practice

An end-to-end Power BI business intelligence dashboard analyzing global vehicle order volumes, revenue distribution, and supply chain performance across key international markets including North America, Europe, Japan, and Africa.

## Project Architecture

### 1. Extract, Transform, Load (ETL) & Power Query
Raw transactional data was ingested, cleansed, and optimized for analytical querying:
* **Data Cleansing:** Handled inconsistent formatting, addressed missing fields in regional records, and standardized country definitions.
* **Structural Transformations:** Applied conditional columns to categorize vehicles by type (e.g., Sedans, SUVs, Commercial, Luxury) and segmented order volumes.
* **Performance Tuning:** Filtered out unreferenced system metadata and set precise data profiles to minimize data model memory footprint.

### 2. Relational Data Modeling
Built an optimized **Star Schema** to ensure high-performance filtering, slicing, and scalability across global dimensions.
* **Fact Table:** `Fact_Orders` (Contains transactional metrics: Quantity Ordered, Unit Price, Sales Amount).
* **Dimension Tables:** `Dim_Customers`, `Dim_Vehicles` (Make, Model, Segment), `Dim_Geography` (Country, Region, Continent), and a dedicated `Dim_Calendar`.
* **Relationships:** Enforced 1-to-many ($1:*$) cardinality with strict unidirectional cross-filtering to guarantee referential integrity.

### 3. Advanced DAX Calculations
Developed high-performance Data Analysis Expressions (DAX) to drive dynamic time-intelligence and regional metrics:

```dax
Total_Sales = SUMX(Fact_Orders, Fact_Orders[QuantityOrdered] * Fact_Orders[UnitPrice])

