# Nigerian-Real-Estate-Market-Analytics-With-Power-BI
This project analyzes real estate property, listing, transaction, customer, and market data to identify key trends, pricing patterns, demand drivers, and market performance. The analysis covers data preparation, modeling, feature engineering, and interactive Power BI visualizations to support data-driven insights into the real estate market.

## Table of Content
1. Project Overview
2. Dataset Overview
3. Data Model & Relationships
4. Data Quality Assessment and Cleaning
5. Feature Engineering
6. Power BI Measures & Calculations
7. Exploratory & Descriptive Analysis
8. Summary of Key Findings & Insights
9. Strategic Business Recommendations
10. Conclusion

## PROJECT OVERVIEW
**Project Objective**

To analyze real estate market data to understand property pricing, customer demand, location performance, property characteristics, listing performance, and transaction activity to support data-driven business decisions.

**Business Questions**
- What is the overall performance of the real estate market?
- How do market activity and transaction values change over time?
- Which locations generate the highest demand and transaction value?
- Which agents and property types perform best?
- Who are the major customer segments?
- How efficiently do listings convert into completed transactions?
- What factors are associated with property pricing and transaction value?

**Tools**
- Power BI — Data cleaning, transformation, analysis, DAX, and visualization
- Python/Google Colab — Dataset generation
- CSV — Data storage and input format

**Project Scope**

The analysis covers properties, customers, agents, listings, and transactions across selected Nigerian locations from 2021–2025.

**Expected Business Value**

The analysis provides insights to support:
- Pricing decisions
- Location strategy
- Property inventory planning
- Customer targeting
- Listing management
- Agent performance monitoring
- Sales and rental strategy

## DATASET OVERVIEW
**Dataset Description**

The dataset is a synthetically generated Nigerian real estate dataset designed to simulate real-world property, customer, agent, listing, and transaction activities.

**Dataset Period**

2021–2025

**Dataset Structure**

The dataset contains 7 tables:

**1. `dim_location`**

| Field | Data Type | Key | Description | Analytical Use |
|---|---|---|---|---|
| `location_id` | Text | PK | Unique identifier for each location | Linking locations to properties, customers, and agents |
| `city` | Text | — | City or specific locality where the property is located | City-level analysis |
| `state` | Text | — | Nigerian state or Federal Capital Territory | State-level analysis |
| `region` | Text | — | Broad Nigerian geographic region | Regional comparison |
| `active_location` | Integer | — | Indicates whether the location is currently active in the dataset | Location filtering |

**2. `dim_date`**

| Field | Data Type | Key | Description | Analytical Use |
|---|---|---|---|---|
| `date_id` | Integer | PK | Numeric representation of the date in YYYYMMDD format | Relationship with fact tables |
| `date` | Date | — | Actual calendar date | Time-series analysis |
| `year` | Integer | — | Calendar year | Yearly analysis |
| `quarter` | Text | — | Quarter of the year, e.g. Q1, Q2 | Quarterly analysis |
| `month_number` | Integer | — | Numerical month from 1–12 | Correct chronological month sorting |
| `month_name` | Text | — | Name of the month | Monthly reporting |
| `month_year` | Text | — | Month and year combination, e.g. Jan-2024 | Trend visualization |
| `week_number` | Integer | — | ISO week number | Weekly analysis |
| `day` | Integer | — | Day of the month | Daily analysis |
| `day_name` | Text | — | Name of the day | Day-of-week analysis |
| `is_weekend` | Boolean | — | Indicates whether the date falls on a weekend | Weekend vs weekday analysis |

**3. `dim_property`**

| Field | Data Type | Key | Description | Analytical Use |
|---|---|---|---|---|
| `property_id` | Text | PK | Unique identifier for each property | Property identification and relationships |
| `location_id` | Text | FK | Identifies the property's location | Location analysis |
| `property_type` | Text | — | Type/category of property | Property-type analysis |
| `bedrooms` | Integer | — | Number of bedrooms | Pricing and demand analysis |
| `bathrooms` | Integer | — | Number of bathrooms | Property feature analysis |
| `property_size_sqm` | Decimal | — | Property size measured in square metres | Price-per-square-metre analysis |
| `year_built` | Integer | — | Year the property was constructed | Property age analysis |
| `furnishing_status` | Text | — | Furnishing condition of the property | Pricing and demand analysis |

**4. `dim_customer`**

| Field | Data Type | Key | Description | Analytical Use |
|---|---|---|---|---|
| `customer_id` | Text | PK | Unique identifier for each customer | Customer identification |
| `first_name` | Text | — | Customer's first name | Customer identification |
| `last_name` | Text | — | Customer's surname | Customer identification |
| `gender` | Text | — | Customer gender | Demographic analysis |
| `age` | Integer | — | Customer age | Age segmentation |
| `marital_status` | Text | — | Customer marital status | Customer profiling |
| `occupation` | Text | — | Customer's occupation | Customer segmentation |
| `income_segment` | Text | — | Broad income classification | Affordability/customer segmentation |
| `home_location_id` | Text | FK | Location associated with the customer's home | Geographic customer analysis |

**5. `dim_agent`**

| Field | Data Type | Key | Description | Analytical Use |
|---|---|---|---|---|
| `agent_id` | Text | PK | Unique identifier for each real estate agent | Agent identification |
| `agent_name` | Text | — | Name assigned to the agent | Agent reporting |
| `gender` | Text | — | Agent gender | Agent demographics |
| `age` | Integer | — | Agent age | Agent demographic analysis |
| `base_location_id` | Text | FK | Agent's primary operating location | Geographic agent analysis |
| `specialization` | Text | — | Primary area of real estate specialization | Agent specialization analysis |
| `years_experience` | Integer | — | Number of years the agent has worked in real estate | Experience/performance analysis |

**6. `fact_listing`**

| Field | Data Type | Key | Description | Analytical Use |
|---|---|---|---|---|
| `listing_id` | Text | PK | Unique identifier for each listing | Listing identification |
| `property_id` | Text | FK | Property associated with the listing | Property analysis |
| `agent_id` | Text | FK | Agent responsible for the listing | Agent performance |
| `date_id` | Integer | FK | Links listing to the date dimension | Time-series analysis |
| `listing_date` | Date | — | Date the property was listed | Listing trends |
| `listing_type` | Text | — | Indicates whether the property is offered for sale or rent | Sales vs rental analysis |
| `listing_status` | Text | — | Current/outcome status of the listing | Listing performance |
| `asking_price` | Decimal | — | Price requested by the seller/landlord | Pricing analysis |
| `days_on_market` | Integer | — | Number of days the property remained on the market | Market efficiency analysis |

**7. `fact_transaction`**

| Field | Data Type | Key | Description | Analytical Use |
|---|---|---|---|---|
| `transaction_id` | Text | PK | Unique identifier for each transaction | Transaction identification |
| `listing_id` | Text | FK | Listing associated with the transaction | Connects transactions to listings |
| `property_id` | Text | FK | Property involved in the transaction | Property analysis |
| `customer_id` | Text | FK | Customer involved in the transaction | Customer analysis |
| `agent_id` | Text | FK | Agent responsible for the transaction | Agent performance |
| `date_id` | Integer | FK | Links transaction to the date dimension | Time-series analysis |
| `transaction_date` | Date | — | Date the transaction occurred | Transaction trends |
| `transaction_type` | Text | — | Indicates whether transaction was a sale or rental | Sales vs rental analysis |
| `transaction_status` | Text | — | Indicates whether transaction was completed or cancelled | Transaction performance |
| `transaction_amount` | Decimal | — | Financial value of the transaction | Revenue/value analysis |
| `annual_rent` | Decimal | — | Annual rental amount associated with a rental transaction | Rental analysis |
| `commission_rate` | Decimal | — | Percentage commission associated with the transaction | Commission analysis |
| `commission_amount` | Decimal | — | Monetary value of the commission | Revenue analysis |

**Dataset Size**

| Table | Records |
|---|---:|
| Properties | 10,000+ |
| Customers | 5,000+ |
| Agents | 300 |
| Listings | 18,000 |
| Transactions | 12,000 |
| Locations | 34 |
| Dates | 1,826 |

Note: The property and customer tables initially contained intentional duplicate records for data-cleaning purposes; the final analytical dataset contains 10,000 properties and 5,000 customers after cleaning.

**Key Data Areas**

The dataset covers:
- Property characteristics
- Customer demographics
- Agent performance
- Property listings
- Sales and rental transactions
- Pricing
- Location
- Market activity over time

## DATA MODEL & RELATIONSHIPS
**Data Model**

The project uses a star schema consisting of dimension tables and fact tables.

**Dimension Tables**
- dim_location — Location information
- dim_date — Calendar and time information
- dim_property — Property characteristics
- dim_customer — Customer information
- dim_agent — Agent information

**Fact Tables**
- fact_listing — Property listing activities
- fact_transaction — Sales and rental transactions

**Key Relationships**
- dim_location → dim_property
- dim_location → dim_customer
- dim_location → dim_agent
- dim_property → fact_listing
- dim_property → fact_transactiondim_customer → fact_transaction
- dim_agent → fact_listing
- dim_agent → fact_transaction
- dim_date → fact_listing
- dim_date → fact_transaction

**Relationship Configuration**

Relationships use one-to-many (1:*) cardinality with single-direction filtering from dimension tables to fact tables.

**Model Purpose**

The model separates descriptive information from transactional data, enabling consistent analysis of market trends, locations, customers, agents, properties, listings, and transactions in Power BI.

![](https://github.com/Oluwaseun2024-ctrl/Nigerian-Real-Estate-Market-Analytics-With-Power-BI/blob/main/Data%20Modelling.png)


## DATA QUALITY ASSESSMENT
**Data Quality Assessment**

The dataset was assessed for missing values, duplicates, inconsistent values, invalid values, outliers, data types, and referential integrity.

**Identified Issues**
| Issue | Affected Data | Treatment |
|---|---|---|
| Duplicate records | Properties, Customers | Removed confirmed duplicates |
| Missing property size | Properties | Retained as missing |
| Blank furnishing status | Properties | Replaced with `Not Specified` |
| Zero bedrooms | Properties | Retained and flagged where applicable |
| Missing occupation | Customers | Replaced with `Not Specified` |
| Inconsistent location names | Locations | Standardized |
| Missing asking price | Listings | Retained as missing |
| Extreme asking prices | Listings | Investigated and flagged |
| Missing annual rent | Transactions | Retained where valid for sales; rental records investigated |
| Invalid numerical values | Listings/Transactions | Checked and corrected where necessary |
| Foreign key mismatches | All related tables | Validated against dimension tables |

## FEATURE ENGINEERING
Additional features were created to improve the analysis of property characteristics, pricing, and transaction dates.

**Property Age at Listing**

Property Age at Listing represents the estimated age of a property at the time it was listed. It was calculated by comparing the property’s construction year with its listing year.

Some records returned negative values. This can occur when a property was listed before its recorded construction year, which may represent off-plan or pre-construction properties marketed before completion. These values were therefore retained as they may reflect a valid stage of the property lifecycle.

DAX Formula:
```
Property Age at Listing = YEAR([Listing Date]) - [Construction Year]
```

**Price per Square Metre**

Price per Square Metre measures the property price relative to its size. This provides a standardized basis for comparing property values across properties of different sizes.

DAX Formula:
```
Price Per Sqm =
DIVIDE(
    [Transaction Price],
    [Property Size Sqm]
)
```

**Weekday Number**

Weekday Number assigns a numerical value to each transaction date based on the day of the week. This supports analysis of transaction activity by weekday and enables consistent sorting of weekday names in visualizations.

DAX Formula:
```
Weekday Number =
WEEKDAY(
    [Transaction Date],
    1
)
```

## POWER BI MEASURES & CALCULATIONS
This section provides a detailed technical reference for all 23 key performance measures constructed within the Nigerian Real Estate Market Analytics model. Each entry defines the calculated measure, its business purpose, the exact DAX formula implemented, and the specific metric figure derived from the executive dashboard.   

**1.	Market Inventory & Platform Base**

**Total Properties**

Total Properties represents the count of unique physical real estate assets cataloged in the system database. It establishes the baseline physical real estate portfolio managed across all locations and property types.  

DAX Formula: 
```
Total Properties = DISTINCTCOUNT(dim_property[property_id])
```
Calculated Figure: 10,000   

**Total Listings**

Total Listings captures the cumulative volume of listing instances created across all marketing periods. This metric is essential for measuring active supply expansion and tracking marketing inventory velocity over time.   

DAX Formula:
```
Total Listings = DISTINCTCOUNT(fact_listing[listing_id])
```
Calculated Figure: 18,000  

**Total Transactions**

Total Transactions reflects the total number of buy, sale, or lease transactions initiated on the platform. It serves as the primary indicator of consumer interest, market demand, and overall deal pipeline volume.   

DAX Formula:
```
Total Transactions = DISTINCTCOUNT(fact_transaction[transaction_id])
```
Calculated Figure: 12,000   

**Total Customers**

Total Customers measures the count of unique registered clients, including buyers, tenants, and real estate investors. It evaluates overall customer base growth and market reach expansion.   

DAX Formula:
```
Total Customers = DISTINCTCOUNT(dim_customer[customer_id])
```
Calculated Figure: 5,000   

**Total Agents**

Total Agents tracks the total active real estate brokers and agents operating within the network. It allows the business to assess broker network capacity and agent distribution footprint across regions.   

DAX Formula:
```
Total Agents = DISTINCTCOUNT(dim_agent[agent_id])
```
Calculated Figure: 300   

**2.	Operational Fulfillment & Execution**

**Completed Transactions**

Completed Transactions denotes the total deals successfully closed across both sales and rental contracts. It acts as the core operational metric for evaluating successful transaction fulfillment and execution.   
DAX Formula:
```
Completed Trans. = 
CALCULATE(
    [Total Transactions],
    fact_transaction[transaction_status] = "Completed"
)
```
Calculated Figure: 9,005   

**Completed Sales**

Completed Sales measures the total outright property sales successfully finalized on the platform. It is used to track performance and deal flow within the high-value capital property acquisition sector.   

DAX Formula:
```
Completed Sales = 
CALCULATE(
    DISTINCTCOUNT(fact_transaction[transaction_id]),
    fact_transaction[transaction_status] = "Completed",
    fact_transaction[transaction_type] = "Sale"
)
```
Calculated Figure: 4,419   

**Completed Rentals**

Completed Rentals accounts for the total lease and rental tenancy agreements successfully executed. This measure monitors volume and turnover within the recurring residential and commercial lease sector.   

DAX Formula:
```
Completed Rentals = 
CALCULATE(
    DISTINCTCOUNT(fact_transaction[transaction_id]),
    fact_transaction[transaction_status] = "Completed",
    fact_transaction[transaction_type] = "Rental"
)
```
Calculated Figure: 4,586   

**Cancelled Transactions**

Cancelled Transactions indicates the total initiated transaction requests that failed, expired, or were aborted before closure. It is critical for highlighting deal attrition, friction points, and operational drop-offs in the sales funnel.   

DAX Formula:
```
Cancelled Trans. = 
CALCULATE(
    [Total Transactions],
    fact_transaction[transaction_status] = "cancelled"
)
```
Calculated Figure: 2,995

**Customers with Completed Transactions**

Customers with Completed Transactions isolates the count of unique customers who finalized at least one successful deal. It is used to evaluate customer conversion efficiency and active purchasing user share.   

DAX Formula:
```
Customers with Completed Trans. = 
CALCULATE(
    DISTINCTCOUNT(fact_transaction[customer_id]),
    fact_transaction[transaction_status] = "Completed"
)
```
Calculated Figure: 4,175   

**3.	Pricing, Valuation & Market Velocity**

**Average Property Size**

Average Property Size represents the mean physical land or build area, measured in square meters, per listed property. It benchmarks spatial characteristics across different property configurations and categories.   

DAX Formula:
```
Avg Property Size = AVERAGE(dim_property[property_size_sqm])
```
Calculated Figure: 690.83 sqm   

**Average Days on Market**

Average Days on Market measures the average duration in days that a listing stays active prior to transaction closure. It serves as a key measure of asset liquidity, demand strength, and market absorption velocity.   

DAX Formula:
```
Avg Day On Market = AVERAGE(fact_listing[days_on_market])
```
Calculated Figure: 247.07 Days   

**Average Asking Price**

Average Asking Price calculates the average initial list price set by sellers or landlords across all property listings. It helps evaluate baseline market supply valuations and initial seller pricing expectations.   

DAX Formula:
```
Avg Asking Price = AVERAGE(fact_listing[asking_price])
```
Calculated Figure: ₦163.43M   

**Average Price per Square Meter**

Average Price per Square Meter determines the mean property cost per square meter across cataloged listings. It provides a normalized spatial valuation metric to accurately benchmark land and property values across different locations.   

DAX Formula:
```
Avg Price/Sqm = AVERAGE(fact_listing[price_per_sqm])
```
Calculated Figure: ₦304.50K   

**4.	Financial Performance & Monetization**

**Total Sales Value**

Total Sales Value represents the cumulative monetary value realized from all completed property sales. It benchmarks major capital investment volume across the outright sales portfolio.   

DAX Formula:
```
Total Sales Value = 
CALCULATE(
    SUM(fact_transaction[transaction_amount]),
    fact_transaction[transaction_status] = "Completed",
    fact_transaction[transaction_type] = "Sale"
)
```
Calculated Figure: ₦1.27T   

**Completed Transaction Value**

Completed Transaction Value sums the total gross merchandise value (GMV) closed across all combined sales and leases. It measures the overall financial capital flow and monetary volume processed through the platform.   

DAX Formula:
```
Completed Trans. Value = 
CALCULATE(
    SUM(fact_transaction[transaction_amount]),
    fact_transaction[transaction_status] = "Completed"
)
```
Calculated Figure: ₦1.34T   

**Total Annual Rent**

Total Annual Rent calculates the total annualized tenancy contract value generated from completed rentals. It quantifies recurring rental cash flow and overall yield across lease properties.   

DAX Formula:
```
Total Annual Rent = 
CALCULATE(
    SUM(fact_transaction[annual_rent]),
    fact_transaction[transaction_status] = "Completed",
    fact_transaction[transaction_type] = "Rental"
)
```
Calculated Figure: ₦74.61bn   

**Average Annual Rent**
Average Annual Rent reflects the mean annual rent value derived per completed rental agreement. It establishes typical rental yield benchmarks for landlords, investors, and prospective tenants.   

DAX Formula:
```
Avg Annual Rent = 
CALCULATE(
    AVERAGE(fact_transaction[annual_rent]),
    fact_transaction[transaction_status] = "Completed",
    fact_transaction[transaction_type] = "Rental"
)
```
Calculated Figure: ₦16.27M   

**Average Sale Value**

Average Sale Value tracks the average gross deal size per finalized property sale. It provides visibility into ticket size trends for capital acquisitions over time.   

DAX Formula:
```
Average Sale Value = 
CALCULATE(
    AVERAGE(fact_transaction[transaction_amount]),
    fact_transaction[transaction_status] = "Completed",
    fact_transaction[transaction_type] = "Sale"
)
```
Calculated Figure: ₦287.12M   

**Average Completed Transaction Value**

Average Completed Transaction Value establishes the overall mean monetary value per completed deal across all transaction types. It provides a consolidated baseline metric for general deal size across both sales and leases.   

DAX Formula:
```
Avg Completed Trans. Value = 
CALCULATE(
    AVERAGE(fact_transaction[transaction_amount]),
    fact_transaction[transaction_status] = "Completed"
)
```
Calculated Figure: ₦149.19M   

**Total Commission**

Total Commission measures the cumulative brokerage and platform commission fees collected on completed transactions. It serves as a direct indicator of platform monetization, agent earnings, and net operational revenue.   

DAX Formula:
```
Total Commission = 
CALCULATE(
    SUM(fact_transaction[commission_amount]),
    fact_transaction[transaction_status] = "Completed"
)
```
Calculated Figure: ₦66.86bn   


**5.	Conversion & Efficiency Ratios**

**Transaction Completion Rate**

Transaction Completion Rate calculates the percentage of initiated transactions that are successfully brought to final closure. It is the primary KPI for evaluating operational efficiency, pipeline health, and overall deal retention.   

DAX Formula:
```
Trans. Completion Rate = 
DIVIDE(
    [Completed Trans.],
    [Total Transactions]
)
```
Calculated Figure: 75.04%   

**Listing Conversion Rate

Listing Conversion Rate evaluates the ratio of total transactions generated relative to the total available inventory of listings. It assesses inventory utilization efficiency and demand generation capacity per active listing.   

DAX Formula:
```
Listing Conversion Rate = 
DIVIDE(
    [Completed Trans.],
    [Total Listings]
)
```
Calculated Figure: 50.03%   

**Executive Summary & Analytical Insights**

The platform demonstrates high operational conversion efficiency, achieving a 75.04% Transaction Completion Rate by closing 9,005 of 12,000 initiated deal requests. Revenue generation remains strongly balanced; while outright property sales drive primary gross merchandise value (₦1.27T across 4,419 completed sales out of ₦1.34T total GMV), the rental sector generates high recurring cash flow (4,586 completed rentals delivering ₦74.61bn in total annual rent at an average of ₦16.27M per agreement). Properties spend an average of 247.07 days on market (~8 months) before closing, with completed sales averaging ₦287.12M, well above the average initial asking price of ₦163.43M. Finally, with a 50.03% Listing Conversion Rate across 18,000 total listings, the ecosystem has yielded ₦66.86bn in total commission revenue for brokers and platform operations.

**Dashboard**

![](https://github.com/Oluwaseun2024-ctrl/Nigerian-Real-Estate-Market-Analytics-With-Power-BI/blob/main/KPIs.png)


## EXPLORATORY & DESCRIPTIVE ANALYSIS
**Trend Analysis**

This section presents the exploratory and descriptive trend analysis evaluating historical market performance across both Transaction Volume (number of completed deals) and Transaction Value (monetary GMV realized). The analysis examines temporal patterns across annual, quarterly, monthly, and daily operational cycles to identify seasonality, market trajectory, and settlement behavior.   

**1.	Annual Trend Analysis**

**Annual Completed Transactions (Volume)**

Annual transaction volume exhibits a sharp initial contraction from 1,825 transactions in 2021 down to a market trough of 1,748 transactions in 2022. This was followed by a substantial recovery in 2023, reaching a peak of 1,854 transactions. Post-2023 performance stabilized at predictable operational levels, recording 1,786 transactions in 2024 and 1,792 transactions in 2025.   

**Annual Completed Transaction Value (GMV)**

Monetary transaction value closely mirrored transaction volume trends over the five-year period. Total completed value dropped from ₦278bn in 2021 to a low of ₦248bn in 2022, before surging to an all-time high of ₦292bn in 2023. Following this peak, annualized transaction value normalized to ₦265bn in 2024 and ₦260bn in 2025.   

**2.	Quarterly Trend Analysis**

**Quarterly Completed Transactions (Volume)**

Quarterly transaction volume highlights strong mid-year deal momentum. Starting at 2,142 completed transactions in Q1, deal volume rises steadily through Q2 (2,260 transactions) to reach its annual peak in Q3 (2,320 transactions). Volume remains strong into year-end, closing at 2,283 transactions in Q4.   

**Quarterly Completed Transaction Value (GMV)**

Quarterly monetary realization exhibits a similar Q3 concentration. After starting at ₦328.9bn in Q1 and troughing slightly at ₦326.1bn in Q2, revenue execution surges to ₦348.0bn in Q3. Q4 maintains high capital realization, closing at ₦340.5bn.   

**3.	Monthly Trend Analysis & Seasonality**

**Monthly Completed Transactions (Volume)**

Monthly deal execution displays recurring seasonal fluctuations. Following an initial dip in February (630 transactions), transaction volume ramps up in March (765 transactions) and reaches its primary peak in May (813 transactions). A secondary mid-summer surge occurs in July (804 transactions) and August (796 transactions), before leveling off toward year-end (747 transactions in December).   

**Monthly Completed Transaction Value (GMV)**

Monetary performance tracks volume spikes closely, with capital inflow peaking during mid-year months. Following a low in February (₦98.4bn), sales revenue expands in March (₦117.5bn) and May (₦119.6bn), reaching its highest single-month total in August (₦126.1bn). Secondary highs are achieved in July (₦121.1bn) and November (₦120.9bn).   

**4.	Daily Operational Trend Analysis**

**Daily Completed Transactions (Volume)**

Daily deal closures show heavy concentration during mid-week execution cycles. Deal completions peak on Wednesday (1,325 transactions) and Tuesday (1,319 transactions)—which combined account for over 2,640 completed deals. Deal activity drops significantly toward the end of the work week, reaching its lowest point on Friday (1,220 transactions), before rebounding over the weekend (1,284 transactions on Saturday and Sunday).   

**Daily Completed Transaction Value (GMV)**

Daily settlement value steadily escalates throughout the business week. Capital outflow increases from Sunday (₦183.2bn) through Tuesday (₦199.1bn) and Wednesday (₦202.1bn), reaching a major settlement peak on Thursday (₦206.2bn). Corresponding with transaction volume, capital processing drops to its weekly low on Friday (₦180.1bn) before stabilizing on Saturday (₦187.1bn).   


**Executive Key Takeaways & Analytical Summary**

1.	Mid-Year Market Peak: Both deal volume (2,320 transactions) and gross transaction value (₦348.0bn) consistently peak in Q3, driven by high transactional velocity across May, July, and August.   
2.	Mid-Week Operational Focus: Operational execution and capital settlement favor mid-week processing, with transaction volume peaking on Wednesday (1,325 deals) and financial settlement peaking on Thursday (₦206.2bn). Friday represents the slowest operational day across both metrics.   
3.	Market Stabilization: Following post-2021 market contraction and a major recovery surge in 2023 (1,854 transactions | ₦292bn GMV), the market has settled into a predictable baseline averaging ~1,790 annual transactions and ~₦260bn–₦265bn in annual transaction value.   

**Dashboard**

![](https://github.com/Oluwaseun2024-ctrl/Nigerian-Real-Estate-Market-Analytics-With-Power-BI/blob/main/Trend%20Analysis%201.png)

![](https://github.com/Oluwaseun2024-ctrl/Nigerian-Real-Estate-Market-Analytics-With-Power-BI/blob/main/Trend%20Analysis%202.png)

**Location Analysis**

This section presents the geographic and spatial performance analysis across the Nigerian Real Estate Market Analytics platform, evaluating performance across Region, State, and City/Micro-Market levels. The documentation assesses two core dimensions: Completed Transaction Value (Gross Merchandise Value) and Average Price per Square Meter (Property Density Valuation).   

**1.	Geographical Revenue Performance (Completed Transaction Value)**

**Regional Revenue Distribution**

Market capital realization shows strong geographic concentration in South West and North Central Nigeria, which together account for 66.08% of the ₦1.34T total transaction value. The South West dominates overall revenue generation at 45.62%, followed by North Central at 20.46%. The remaining market share is distributed across the South South (18.0%), North West (10.81%), and South East (5.01%) regions.   

**State-Level Performance**

State-level total sales performance is overwhelmingly anchored by Lagos State and the Federal Capital Territory (FCT). Lagos State leads national transaction value at ₦436.25bn, followed by FCT at ₦274.81bn. Secondary commercial markets also demonstrate significant scale, led by Rivers State (₦102.63bn) and Oyo State (₦101.67bn), with Kano (₦79.62bn), Ogun (₦75.01bn), and Edo (₦72.27bn) capturing key regional trade flows.   

**Top Urban Micro-Markets (City Level)**

Urban center performance highlights high capital concentration in elite commercial and diplomatic hubs. Victoria Island (Lagos) represents the highest grossing city market at ₦76bn, closely followed by Asokoro (Abuja) at ₦73bn. Other premier micro-markets driving top-tier transaction values include Maitama (₦60bn), Ikoyi (₦59bn), Lekki (₦48bn), Magodo (₦47bn), and Kano City (₦46bn).   

**2.	Density Pricing & Valuation Performance (Avg Price/Sqm)**

**Regional Density Valuation**

Property density valuation across the country averages ₦304.50K per square meter. Valuation is led by North Central at 23.91% and South West at 21.22% of overall spatial land value. Density pricing stays relatively competitive across all five zones, with South South contributing 18.71%, North West 18.63%, and South East 17.53%.   

**State-Level Density Valuation**

At the state level, administrative power centers command the highest spatial price points. FCT captures the highest average land valuation nationwide at ₦351.95K/sqm, followed by Lagos State at ₦338.22K/sqm. Emerging high-density state valuation hubs include Kaduna State (₦283.30K/sqm), Edo State (₦277.12K/sqm), Delta State (₦276.60K/sqm), and Rivers State (₦273.19K/sqm).   

**City-Level Spatial Price Leaders**

An elite tier of luxury urban enclaves commands prices above half a million Naira per square meter. Victoria Island leads national land density pricing at ₦560.64K/sqm, followed by Asokoro at ₦535.60K/sqm, Lekki at ₦523.10K/sqm, Ikoyi at ₦510.05K/sqm, and Maitama at ₦493.66K/sqm. Outside these primary hubs, commercial zones such as Warri (₦312.11K/sqm) and GRA Benin (₦293.35K/sqm) command strong regional pricing premiums.   

**Executive Key Takeaways & Analytical Summary**

1.	High Revenue Concentration: Lagos State (₦436.25bn) and FCT (₦274.81bn) act as the dual economic engine of the platform, driving over 53% of the ₦1.34T national completed transaction value.   
2.	Elite Micro-Market Premium: Four prime micro-markets—Victoria Island (₦560.64K/sqm), Asokoro (₦535.60K/sqm), Lekki (₦523.10K/sqm), and Ikoyi (₦510.05K/sqm)—exceed ₦500K/sqm, establishing them as the highest land value enclaves in the country.   
3.	Emerging Secondary Growth Corridors: Strong liquidity and market scale outside the Lagos-Abuja axis are anchored by Rivers (₦102.63bn) and Oyo (₦101.67bn), highlighting viable opportunities for portfolio diversification in regional urban hubs.

**Dashboard**

![](https://github.com/Oluwaseun2024-ctrl/Nigerian-Real-Estate-Market-Analytics-With-Power-BI/blob/main/Location%20Analysis%201.png)

![](https://github.com/Oluwaseun2024-ctrl/Nigerian-Real-Estate-Market-Analytics-With-Power-BI/blob/main/Location%20Analysis%202.png)

**Agent Performance Analysis**

This section provides a structured documentation of broker network operational efficiency and revenue contribution across the platform. The analysis evaluates four key metrics: Commission Earnings, Completed Transaction Volume, Completed Transaction Value (GMV), and Specialization Segment Distribution.   

**1.	Individual Agent Performance**

**Top 10 Commission Earnings**

Commission distribution is led by a distinct group of top-performing brokers. Agent Joy Bello earns the highest commission earnings at ₦1,436.67M, followed closely by Agent Victor Adeyemi at ₦1,418.18M. The top earnings tier is rounded out by Agent Chioma Williams (₦1,264.33M), Agent Esther Okafor (₦1,149.48M), and Agent John Abdullahi (₦1,029.16M). Additional high earners include Agent Mary Ibrahim (₦968.28M), Agent James Adeyemi (₦892.00M), Agent Mary Eze (₦882.55M), Agent Peter Okonkwo (₦878.19M), and Agent Amaka Mohammed (₦876.57M).   

**Top 10 Completed Transactions (Volume)**

Deal execution velocity shows strong alignment with earnings leaderboard rankings. Agent Joy Bello achieves the highest transaction volume, followed by Agent Victor Adeyemi with 167 completed transactions. Other major drivers of transaction volume include Agent Chioma Williams (156 deals), Agent Esther Okafor (143 deals), Agent James Adeyemi (137 deals), Agent John Abdullahi (134 deals), and Agent Mary Ibrahim (129 deals). Mid-tier high volume producers include Agent Amaka Mohammed (108 deals), Agent Esther Olawale (108 deals), and Agent Chioma Adeyemi (102 deals).   

**Top 10 Completed Transaction Value (GMV Realized)**

When assessing total transaction capital processed, high-ticket deal execution shifts top rankings. Agent Victor Adeyemi commands the highest total transaction value at ₦29bn, followed by Agent Chioma Williams at ₦27bn and Agent Joy Bello at ₦26bn. Significant capital settlement is also generated by Agent Esther Okafor (₦24bn) and Agent James Adeyemi (₦20bn). Secondary capital producers each processed significant deal volume, including Agent Mary Ibrahim (₦19bn), Agent John Abdullahi (₦19bn), Agent Mary Eze (₦19bn), Agent Esther Olawale (₦18bn), and Agent Amaka Mohammed (₦18bn).   

**2.	Completed Transactions by Specialization**

Transaction fulfillment is balanced across all primary real estate product specializations:   
- Land: 1.9K completed transactions.
- Property Management: 1.9K completed transactions.
- Luxury: 1.9K completed transactions.
- Commercial: 1.7K completed transactions.
- Residential: 1.6K completed transactions.   

**Executive Key Takeaways & Analytical Summary**

1.	Top Producer Dominance: Platform earnings are anchored by elite brokers led by Agent Joy Bello (₦1,436.67M commission) and Agent Victor Adeyemi (167 completed deals | ₦29bn transaction value).   
2.	Deal Size vs. Deal Volume Efficiency: While Agent Joy Bello leads in total completed transaction volume, Agent Victor Adeyemi captures the highest gross deal value (₦29bn), demonstrating higher average transaction sizing.   
3.	Balanced Specialization Model: Platform deal fulfillment maintains an even distribution across sectors, led by Land, Property Management, and Luxury properties at 1.9K deals each, demonstrating strong service diversification across both asset classes and management verticals.

**Dashboard**

![](https://github.com/Oluwaseun2024-ctrl/Nigerian-Real-Estate-Market-Analytics-With-Power-BI/blob/main/Agent%20Analysis.png)

**Customer Analysis**

This section details the demographic and behavioral breakdown of the platform's client base, comparing overall platform acquisition (Total Customers = 5,000) against transactional fulfillment (Completed Transactions = 9,005). The analysis evaluates four key demographic dimensions: Age Distribution, Income Segmentation, Gender Ratio, and Professional Specialization.   

**1.	Demographics & Market Segmentation**

**Age Group Distribution**

Customer engagement increases progressively with age, anchored by senior demographic groups.   
- Total Registered Customers: Buyers aged 55+ represent the largest single age cohort at 1,574 customers, followed by 35–44 (1,050), 45–54 (1,044), 25–34 (994), and 18–24 (338).
- Completed Transactions: Transaction fulfillment heavily reflects this mature demographic, led by 55+ (2,812 completed deals). Active purchasing volume continues across 35–44 (1,944 deals), 45–54 (1,881 deals), 25–34 (1,764 deals), and 18–24 (604 deals).   

**Income Segment Breakdown**

Platform demand is predominantly driven by middle-income and upper-middle-income brackets.   
- Total Registered Customers: The Middle Income segment accounts for 1,928 customers, followed by Upper-Middle (1,513), Low (1,046), and High (513). Middle and Upper-Middle segments together represent 3,441 total customers.
- Completed Transactions: Transaction execution is strongly concentrated in these core segments, with Middle Income driving 3,449 deals and Upper-Middle driving 2,717 deals—combining for 6,166 completed transactions. The Low Income cohort accounted for 1,946 deals, while the High Income bracket completed 893 deals.   

**Gender Ratio & Distribution**
Platform engagement and transaction completion rates remain closely balanced across gender lines.   
- Total Registered Customers: Out of the 5K total registered customer base, males account for 51.76% (~3K), while females represent 48.24% (~2K).
- Completed Transactions: Transaction completion rates flip slightly to favor female clients, with females accounting for 52.06% (~5K deals) and males accounting for 47.94% (~4K deals) out of 9K total completed deals.   

**2.	Professional & Occupational Specialization**

**Top Customer Occupations (Registered Base)**

Client acquisition spans a diverse array of formal, commercial, and technical professions:   
- Teachers represent the largest professional cohort, followed by Traders (377), Accountants (375), and Business Owners (371).
- Tech, corporate, and investor participation is led by Software Developers (357), Real Estate Investors (349), Students (349), Bankers (344), Doctors (342), and Engineers (340).
- Secondary professional groups include Other (336), Lawyers (331), Consultants (322), Civil Servants (316), and Unknown (100).   

**Top Customer Occupations (Completed Deals)**

Deal execution across professional sectors closely aligns with initial customer acquisition patterns:   
- Teachers lead total transaction execution, followed by Accountants (685 deals), Real Estate Investors (666 deals), Traders (652 deals), and Business Owners (644 deals).
- High deal conversion is sustained across technical and professional fields, including Engineers (633 deals), Students (629 deals), Software Developers (612 deals), Doctors (602 deals), and Bankers (596 deals).
- Additional contributing occupations include Consultants (590 deals), Other (588 deals), Civil Servants (580 deals), Lawyers (561 deals), and Unknown (199 deals).   

**Executive Key Takeaways & Analytical Summary**
1. Mature & Middle-Income Core: The primary commercial driver of the platform consists of mature clients aged 55+ (1,574 customers | 2,812 deals) and middle-to-upper-middle income earners, who together account for 6,166 completed transactions.   
2. Balanced Gender Conversion: While male registered clients hold a slight majority (51.76%), female customers demonstrate higher overall deal execution efficiency, representing 52.06% of all completed transactions.   
3. Broad Occupational Penetration: Platform usage is not confined to institutional investors; strong transaction volume is generated across essential workforce sectors led by Teachers, Accountants, Real Estate Investors, Traders, and Business Owners.

**Dashboard**

![](https://github.com/Oluwaseun2024-ctrl/Nigerian-Real-Estate-Market-Analytics-With-Power-BI/blob/main/Customer%20Analysis%201.png)

![](https://github.com/Oluwaseun2024-ctrl/Nigerian-Real-Estate-Market-Analytics-With-Power-BI/blob/main/Customer%20Analysis%202.png)

**Property Analysis**

This section provides a structured technical reference for the asset-level performance metrics within the Nigerian Real Estate Market Analytics platform. The documentation evaluates catalog inventory distribution, valuation benchmarks, transactional throughput, liquidity speed, and spatial dimensions across various property types and bedroom configurations.   

**1.	Inventory Composition & Structural Attributes**

**Inventory Distribution by Property Type & Bedrooms**

The platform catalog is heavily anchored by multi-unit residential structures, led by Apartments which comprise the largest volume share across all bedroom tiers. Non-residential and undeveloped land parcels represent standalone inventory classes, recorded at 632 Land units and 425 Commercial Properties.   
- Apartment: 473 (1-Bed), 482 (2-Bed), 522 (3-Bed), 512 (4-Bed), 512 (5-Bed), 483 (6-Bed).
- Detached House: 230 (1-Bed), 283 (2-Bed), 251 (3-Bed), 301 (4-Bed), 274 (5-Bed), 257 (6-Bed).
- Duplex: 245 (1-Bed), 212 (2-Bed), 232 (3-Bed), 216 (4-Bed), 256 (5-Bed), 222 (6-Bed).
- Semi-Detached House: 191 (1-Bed), 199 (2-Bed), 203 (3-Bed), 204 (4-Bed), 195 (5-Bed), 212 (6-Bed).
- Terraced House: 212 (1-Bed), 183 (2-Bed), 185 (3-Bed), 187 (4-Bed), 208 (5-Bed), 199 (6-Bed).
- Bungalow: 101 (1-Bed), 96 (2-Bed), 100 (3-Bed), 93 (4-Bed), 98 (5-Bed), 114 (6-Bed).   

**Total Inventory Breakdown by Bedrooms**

Residential unit inventory demonstrates remarkable consistency across configuration tiers, maintaining an even spread from 1-bedroom to 6-bedroom units averaging between 1,450 and 1,540 properties per tier:   
- 0 Bedroom: 1,057 properties (comprising Land and Commercial inventory).
- 1 Bedroom: 1,452 properties.
- 2 Bedrooms: 1,455 properties.
- 3 Bedrooms: 1,493 properties.
- 4 Bedrooms: 1,513 properties.
- 5 Bedrooms: 1,543 properties
- 6 Bedrooms: 1,487 properties.   

**Inventory Distribution by Furnishing Status**

Property listings reflect a balanced split across furnishing categories to accommodate diverse tenant and buyer preferences:   
- Semi-Furnished: 3,328 properties (33.28%)
- Unfurnished: 3,322 properties (33.22%)
- Furnished: 3,270 properties (32.70%)
- Not Specified: 80 properties (0.80%)   

**2.	Pricing, Valuation & Size Benchmarks**

**Asking Price & Spatial Valuation by Asset Class**

Terraced Houses, Apartments, and Duplexes command the highest baseline asking prices and density valuations nationwide.   
- Terraced House: ₦177.28M Avg Asking Price | ₦353.63K Avg Price/Sqm
- Apartment: ₦177.28M Avg Asking Price | ₦334.59K Avg Price/Sqm
- Duplex: ₦176.78M Avg Asking Price | ₦336.16K Avg Price/Sqm
- Detached House: ₦175.61M Avg Asking Price | ₦326.52K Avg Price/Sqm
- Semi-Detached House: ₦173.22M Avg Asking Price | ₦322.16K Avg Price/Sqm
- Bungalow: ₦159.46M Avg Asking Price | ₦335.30K Avg Price/Sqm
- Commercial Property: ₦81.67M Avg Asking Price | ₦64.44K Avg Price/Sqm
- Land: ₦25.92M Avg Asking Price | ₦20.48K Avg Price/Sqm   

**Average Spatial Size by Property Type**

Spatial footprint is led by commercial assets and undeveloped land parcels, while residential asset classes maintain consistent size profiles:   
- Commercial Property: 1,693 sqm
- Land: 1,693 sqm
- Detached House: 536 sqm
- Apartment: 534 sqm
- Duplex: 534 sqm
- Semi-Detached House: 528 sqm
- Terraced House: 516 sqm
- Bungalow: 509 sqm   

**3.	Financial Fulfillment & Market Velocity**

**Commercial Output (GMV, Sales Value & Rent)**

Residential properties serve as the primary engine for platform GMV and revenue realization.   
- Apartment: ₦419.60bn Completed Trans. Value | ₦396bn Total Sales Value | ₦18M Avg Annual Rent
- Detached House: ₦252.48bn Completed Trans. Value | ₦239bn Total Sales Value | ₦18M Avg Annual Rent
- Duplex: ₦194.88bn Completed Trans. Value | ₦183bn Total Sales Value | ₦18M Avg Annual Rent
- Semi-Detached House: ₦184.80bn Completed Trans. Value | ₦176bn Total Sales Value | ₦17M Avg Annual Rent
- Terraced House: ₦179.80bn Completed Trans. Value | ₦170bn Total Sales Value | ₦18M Avg Annual Rent
- Bungalow: ₦72.28bn Completed Trans. Value | ₦68bn Total Sales Value | ₦16M Avg Annual Rent
- Commercial Property: ₦26.74bn Completed Trans. Value | ₦26bn Total Sales Value | ₦7M Avg Annual Rent
- Land: ₦12.84bn Completed Trans. Value | ₦12bn Total Sales Value | ₦3M Avg Annual Rent   

**Days on Market (Liquidity Speed)**

Listing absorption speed remains remarkably uniform across all real estate categories, spanning a narrow range of 241 to 251 days (~8 months) to transaction closure:   
- Semi-Detached House: 251 Days
- Detached House: 251 Days
- Bungalow: 249 Days
- Duplex: 248 Days
- Commercial Property: 248 Days
- Terraced House: 245 Days
- Apartment: 245 Days
- Land: 241 Days   

**Executive Key Takeaways & Analytical Summary**
1.	Dominance of Residential Sector: Apartments lead total market activity, accounting for ₦419.60bn in completed deal value and ₦396bn in direct sales value.   
2.	Density Pricing Leadership: Terraced Houses command the highest density price benchmark at ₦353.63K/sqm, while rental yields remain steady across major residential categories at ₦16M–₦18M annually.   
3.	Consistent Market Velocity: Asset liquidity displays remarkable stability across property classes, requiring an average of 241 to 251 days on market from initial listing to finalized contract completion.

**Dashboard**

![](https://github.com/Oluwaseun2024-ctrl/Nigerian-Real-Estate-Market-Analytics-With-Power-BI/blob/main/Property%20Analysis%201.png)

![](https://github.com/Oluwaseun2024-ctrl/Nigerian-Real-Estate-Market-Analytics-With-Power-BI/blob/main/Property%20Analysis%202.png)


## SUMMARY OF KEY INSIGHTS & FINDINGS
This section synthesizes the core findings and operational takeaways derived across the platform.   

**Key Executive Findings**
1.	Conversion & Financial Scale: The platform converted 75.04% of initiated transactions (9,005 deals) and 50.03% of active listings, generating ₦1.34T in completed GMV and ₦66.86bn in broker commissions. Direct sales drove ₦1.27T, while rentals generated ₦74.61bn at an average of ₦16.27M per lease.   
2.	Seasonality & Workflow: Activity peaks in Q3 (2,320 deals | ₦348.0bn GMV), led by May, July, and August. Operations favor mid-week execution, peaking on Wednesday for deal closures (1,325 deals) and Thursday for financial settlement (₦206.2bn). Annual GMV has stabilized at ~₦260bn–₦265bn.
3.	Geographic Concentration: Lagos State (₦436.25bn) and the FCT (₦274.81bn) drive 53% of total national GMV. Victoria Island (₦560.64K/sqm) and Asokoro (₦535.60K/sqm) command the highest urban density pricing, while Rivers (₦102.63bn) and Oyo (₦101.67bn) represent key growth corridors.
4.	Broker & Sector Distribution: Agent Joy Bello led in earnings (₦1,436.67M) and deal volume, while Agent Victor Adeyemi commanded the highest total transaction value (₦29bn). Deal execution remained evenly balanced across Land, Property Management, and Luxury verticals (1.9K deals each).
5.	Client Demographics: Primary demand is driven by mature buyers aged 55+ (2,812 deals) and middle-to-upper-middle income earners (6,166 deals). While males represent 51.76% of registered users, females completed 52.06% of all finalized deals.
6.	Asset Performance & Velocity: Apartments generated the highest capital realization (₦419.60bn GMV). Residential rental yields averaged ₦16M–₦18M annually, while market absorption speed remained consistent across all property types at 241 to 251 days (~8 months).



## STRATEGIC BUSINESS RECOMMENDATIONS
Based on the empirical findings across platform performance, geographical revenue concentration, broker efficiency, client demographics, and asset absorption, the following actionable business strategies are recommended to maximize revenue, optimize operational efficiency, and expand market share.

**1. Geographical Expansion & Micro-Market Capitalization**
- Deepen Penetration in Ultra-High-Yield Hubs: Victoria Island, Asokoro, Lekki, Ikoyi, and Maitama command land density valuations reaching ₦493K–₦560K/sqm and drive the bulk of high-value transactions. Premium listing placements, tailored luxury broker incentives, and dedicated concierge onboarding should be prioritized in these five micro-markets.
- Scale Secondary Growth Corridors: Rivers State (₦102.63bn GMV) and Oyo State (₦101.67bn GMV) have established themselves as key liquidity hubs outside Lagos and Abuja. Expanding physical regional offices and developer partnerships in Port Harcourt and Ibadan will capture rising regional demand.

**2. Inventory Strategy & Portfolio Optimization**
- Scale Apartment & Multi-Family Supply: Apartments represent the platform’s primary revenue driver (₦419.60bn GMV). Developer onboarding initiatives should focus heavily on mid-to-high-tier apartment inventory to meet sustained transactional velocity.
- Capitalize on Uniform Rental Yields: With annual rents averaging ₦16M–₦18M across all residential asset classes, the platform should launch automated long-term lease management and digital rent collection services to capture recurring fee revenue from the rental market (₦74.61bn total rental value).

**3. Operational & Settlement Workflow Optimization**
- Optimize Mid-Week Settlement Velocity: Transaction closures peak on Wednesday (1,325 deals) and financial settlements peak on Thursday (₦206.2bn). Financial processing workflows, banking integrations, and legal verification support should be scaled up mid-week to prevent bottlenecks.
- Reduce Days on Market (DOM): With average listing absorption holding steady at 241 to 251 days (~8 months) across all categories, implementing automated price matching, instant virtual tours, and automated buyer-seller matchmaking algorithms can help compress transaction cycles below 180 days.

**4. Targeted Customer Acquisition & Engagement**
- Target Mature & Middle-Income Cohorts: Clients aged 55+ and middle-to-upper-middle income earners generate 6,166 completed transactions. Marketing campaigns and financial products (e.g., estate planning, property syndication, long-term asset security) should directly target these mature buyer segments.
- Optimize Campaign Messaging for High-Volume Occupations: Professional engagement is led by Teachers, Accountants, Real Estate Investors, Traders, and Business Owners. Tailoring flexible payment plans and institutional investment offerings toward these specific occupational groups will increase conversion rates.
- Female Buyer Engagement: Female clients achieve higher overall transaction completions (52.06% of total deals). Tailored homeownership seminars and targeted digital marketing campaigns should be designed to support and expand female real estate investors and homeowners.

**5. Broker Network & Performance Incentive Models**
- Implement Performance-Based Broker Retention: Broker earnings and deal throughput are highly concentrated among top producers like Agent Joy Bello (₦1,436.67M commission) and Agent Victor Adeyemi (₦29bn GMV). Tiered commission structures, exclusive listing rights, and retention packages must be deployed to retain top-tier talent.
- Sustain Balanced Vertical Coverage: Because transaction fulfillment is evenly distributed across Land, Property Management, and Luxury segments (1.9K deals each), agent cross-training programs should be formalized to ensure secondary brokers maintain multi-sector deal execution capability.


## CONCLUSION
The comprehensive analysis across the platform demonstrates a resilient, mature, and highly profitable ecosystem within the Nigerian real estate sector. With ₦1.34T in completed transaction value achieved across 9,005 successfully closed deals, the market exhibits strong liquidity, structured growth, and highly predictable performance metrics.

The platform's commercial foundation is firmly anchored by high-density urban powerhouses—most notably Lagos State and the Federal Capital Territory (FCT)—which together process over 53% of national transaction volume. This spatial dominance is complimented by robust secondary growth corridors in Rivers and Oyo states, alongside sustained demand for Apartment inventory and a balanced multi-sector service model spanning Land, Luxury, and Property Management. Furthermore, customer demographics reveal a stable purchasing engine driven by mature, middle-income, and upper-middle-income demographics, alongside balanced gender participation in deal completion.

By executing targeted growth strategies—focusing on high-yield micro-market expansion, compressing transaction absorption cycles, incentivizing top-tier broker talent, and tailoring product offerings to core workforce cohorts—the platform is uniquely positioned to capitalize on evolving macroeconomic trends, strengthen its market share, and maximize long-term shareholder value.

