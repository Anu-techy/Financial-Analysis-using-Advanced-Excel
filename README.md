# Financial-Analysis-using-advanced-MS Excel
Track key performance indicators (KPIs) of the company
**Aim**

1. Track key performance indicators (KPIs) of the company
2. Create Profit and Loss (P&L) reports by Fiscal year
3. Create Profit and Loss (P&L) reports by Markets
4. Evaluation of financial performance, support decision-making, and facilitate communication with stakeholders.

**Description:**

Atliq is a hardware company which manufactures electronic hardware items like PC, Laptop, Hard Drive, mouse, Keyboards, pendrives etc It has operations all over the globe. 

P&L (profit and loss) statement is a financial report that provides an overview of a company's financial performance over a period of time, typically a 
month, quarter, or year.

P&L statements include several critical metrics which evaluate a company's financial performance, profitability and pricing 

**Important Metrics**

**COGS(Cost of Goods Sold)** = Manufacturing Cost + Freight/Transport Cost + Other Cost

**Gross Margin** = Net Sales - COGS

**Gross Margin %** = Gross Margin/Net Sales

**Data Collection:**

Data is given in various excel sheets. Extracted Data through various sources

Dimension tables : dim_customer, dim_product, dim_market

Fact table/Transaction table : fact_sales_monthly

**Data Transformations in Power Query**

Removed duplicate values

Removed data with missing values (only 3 rows)

Identified, replaced spelling mistakes in customer names

Replaced nan category in market table to NA (North American Region) ater confirming with business owners

Few rows have negative quantity , Replaced with positive after clear confirmation

Named all the data transformation steps

Load the data to data model

Created dim_date table with date, month, FY (fiscal_year) columns.

Created a **calculated column** in fact_sales_monthly as 

**Total_COGS** = fact_sales_monthly[freight_cost] + fact_sales_monthly[manufacturing_cost] 

The **Dim_Date** table helps in analysis by providing a structured way to categorize and group data based on time (e.g., by day, month, quarter, or year), enabling easier and more flexible time-based analysis, such as trend analysis, period-over-period comparisons, and time-based calculations (like YTD or MTD). Fiscal year of Atliq hardware is from september through August.

**Data Modelling**

dim_custommer(customer_code) ---> fact_sales_monthly(customer_code) one to many

dim_product(product_code) ---> fact_sales_monthly(product_code) one to many

We cannot connect dim_market directly to fact_sales_monthly as there is no common column between dim_market and fact_sales_monthly table. Hence we connect dim_market to dim_customer

dim_market(market) ---> dim_customer(market) one to many

dim_date(date) ---> fact_sales_monthy(date) one to many

**DAX Measures created for P & L by Year Report**

In the Power Pivot, Created the following DAX measures in the fact_sales_monthly table

**Measure 1:** Net Sales = SUM(fact_sales_monthly[net_sales_amount])

**Measure 2:** COGS = SUM(fact_sales_monthlu[Total_COGS])

**Measure 3:** Gross Margin = [Net Sales] - [COGS] 

**Measure 4:** GM % = DIVIDE([Gross Margin],[Net Sales],0)

**Final P & L by Fiscal Year Report Designing**

In the **Power Pivot:**

**Values:**

                    Net Sales
      
                    COGS

                    Gross Margin

                    Gross Margin %
                    
**Filters:**           
                    Region (dim_market)

                    Market  (dim_market)
      
                    Division (dim_product)

                    Customer (dim_customer)

**Columns:**
                    FY (dim_date)
                    
Added conditional formatting and improved aesthetics

=========================================================

**P & L by Month Report Designing**

Inorder to make this report, I should add months and quarters in Data Model

So in power query, in dim_date table, we create month column as =FORMAT([date],"MMM")

we create quarter column as fy_month_no =MONTH(DATE(YEAR([date]),MONTH([date])+4,1))

                            Quarter =  "Q" & ROUNDUP([fy_month_no]/3,0)


In the **Power Pivot:**

**Values:**

                    Net Sales
      
                    COGS

                    Gross Margin

                    Gross Margin %
                    
**Filters:**           
                    Region (dim_market)

                    Market  (dim_market)
      
                    Division (dim_product)

                    Customer (dim_customer)

                    FY (dim_date)

**Columns:**
                    quarter (dim_date)

                    month (dim_date)
                    
Added conditional formatting and improved aesthetics


**Recommendations**

Use Report to

Benchmarking against competitors and plan for budgeting and forecasting

Align financial planning with strategic goals.

Slice and dice data to drill down the hidden insights













