# Nigerian-Real-Estate-Market-Analytics-With-Power-BI
This project analyzes real estate property, listing, transaction, customer, and market data to identify key trends, pricing patterns, demand drivers, and market performance. The analysis covers data preparation, modeling, feature engineering, and interactive Power BI visualizations to support data-driven insights into the real estate market.

## Table of Content
1. Project Overview
2. Dataset Overview
3. Data Model & Relationships
4. Data Quality Assessment
5. Data Cleaning & Transformation
6. Feature Engineering
7. Power BI Measures & Calculations
8. Exploratory & Descriptive Analysis
9. Summary of Key Findings & Insights
10. Strategic Business Recommendations
11. Conclusion

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
