# ETL-Data-Warehousing
This project aims to demonstrate the full ETL (Extract, Transform, Load) process

---

## 📦 Dataset

- **Source**: Sales markets
- **Domain**: Financials  
- **Description**: the selected dataset contains sales transactions across different markets. Each record captures the segment, country, product, discount band, units sold, pricing details, gross sales, discounts, net sales, cost of goods sold (COGS), and profit, along with date information


## 🧱 Star Schema Design

- **Fact Table**:  
  ●	Sales_ID (PK)
  ●	Segment_ID (FK)
  ●	Country_ID (FK)
  ●	Product_ID (FK)
  ●	Date_ID (FK)
  ●	Units_Sold
  ●	Manufacturing_Price
  ●	Sale_Price
  ●	Gross_Sales
  ●	Discounts
  ●	Sales
  ●	COGS
  ●	Profit

- **Dimension Tables**:  
  ●	Dim_Segment (Segment_ID, Segment)
  ●	Dim_Country (Country_ID, Country)
  ●	Dim_Product (Product_ID, Product)
  ●	Dim_Date (Date_ID, Date,Month_Number, Month_Name, Year)
---

## ⚙️ ETL Pipeline

- **Tool Used**: SQL Server Integration Services (SSIS)
- **Steps**:
  1. **Data Extraction**  
     ●	Source: Data was extracted from a CSV source containing sales records.
     ●	Tools: SSIS (SQL Server Integration Services) was used for this project. SSIS is a component of Microsoft SQL Server that can be used to perform a broad range of data migration and ETL tasks.
     ●	Process: SSIS was used to connect to the CSV file.The data was read into the SSIS data flow.Data types were initially defined, noting that some columns required later conversion.

  2. **Data Transformation**  
       ●	Surrogate Keys: Textual values (Segment, Country, Product, Date) were transformed into surrogate keys using Lookup transformations. This improves query performance and reduces storage.
      ●	Data Cleaning: Numeric columns were cleaned by removing extra symbols like "$" and ",". Values with "S-" in the Discounts column were handled by assuming they represent zero and replacing them with "0". This assumption was made due to the lack of context in the original data
    ●	Null/Empty Value Handling: Null or empty values were handled with default replacements or removed depending on relevance to ensure data integrity.

  3. **Data Loading**  
     ●	OLE DB Destination was used to connect to the target data warehouse database.
     ●	"Table or View - Fast load" was employed for efficient data insertion.
     ●	Error handling was implemented within the SSIS packages to manage potential issues during the loading process


---

## 📊 Data Analysis & Insights

After analyzing the data warehouse, the following insights were observed:
●	The Government and Midmarket segments have the highest sales volume, indicating they are key customer segments.
●	Specific countries (Canada, Germany) and products ( VTT) contribute more significantly to overall profit, suggesting areas of strength.
●	Seasonal trends are identifiable, with sales peaking during certain months (e.g., October, November), which could be linked to specific promotions or market cycles.
●	Discount bands correlate directly with profit margins; higher discount bands may lead to increased sales volume but potentially lower profit margins.

