 # PART 1: Connecting & Shaping the Data

### 1) Connected to the MavenMarket csv file

### 2)Changed the Table Names according to the naming convetion and confirmed that data types are accurate

### 3)Added a new column in "Customers" Table named "full_name" to merge the the "first_name" and "last_name" columns, separated by a space.
Created a new column named "birth_year" to extract the year from the "birthdate" column, and format as text
Created a conditional column named "has_children" which equals "N" if "total_children" = 0, otherwise "Y"

### 4) Added a calculated column in "Products" Table named "discount_price", equal to 90% of the original retail price
Format as a fixed decimal number, and then use the rounding tool to round to 2 digits
Replacede "null" values with zeros in both the "recyclable" and "low-fat" columns

### 5) Added a calculated column in "Stores" named "full_address", by merging "store_city", "store_state", and "store_country", separated by a comma and space.
Added a calculated column named "area_code", by extracting the characters before the dash ("-") in the "store_phone" field 

### 6)In "Calendar" Table,Used the date tools in the query editor to add the following columns:
Start of Week (starting Sunday)
Name of Day
Start of Month
Name of Month
Quarter of Year
Yea

### 7) Added a new folder in the documents named "MavenMarket Transactions", containing both the MavenMarket_Transactions_1997 and MavenMarket_Transactions_1998 csv files.
Connected to the folder path, and choose "Edit" (vs. Combine and Edit).
Removed the "Source.Name" column

### 8) Saved the .pbix file (i.e. "MavenMarket_Report")

# PART 2: Creating the Data Model

### 1) In the MODEL view, arranged the tables with the lookup tables above the data tables.
Connected Transaction_Data to Customers, Products, and Stores using valid primary/foreign keys.
Connected Transaction_Data to Calendar using both date fields, with an inactive "stock_date" relationship.
Connected Return_Data to Products, Calendar, and Stores using valid primary/foreign keys.
Connected Stores to Regions as a "snowflake" schema.

### 2) Confirmed the following:
All the relationships follow one-to-many cardinality, with primary keys (1) on the lookup side and foreign keys (*) on the data side
Filters are all one-way (no two-way filters)
Filter context flows "downstream" from lookup tables to data tables
Data tables are connected via shared lookup tables (not directly to each other)

### 3) Hide all foreign keys in both data tables from Report View, as well as "region_id" from the Stores table

### 4) In the DATA view:
Updated all date fields (across all tables) to the "M/d/yyyy" format using the formatting tools in the Modeling tab
Updated "product_retail_price", "product_cost", and "discount_price" to Currency ($ English) format
In the Customers table, categorized "customer_city" as City, "customer_postal_code" as Postal Code, and "customer_country" as Country/Region
In the Stores table, categorized "store_city" as City, "store_state" as State or Province, "store_country" as Country/Region, and "full_address" as Address .

### 5) Saved your .pbix file

# PART 3: Adding DAX Measures

### 1) In the DATA view, added these following calculated columns:

In the Calendar table, added a column named "Weekend"
Equals "Y" for Saturdays or Sundays (otherwise "N")

In the Calendar table, added a column named "End of Month"
Returns the last date of the current month for each row

In the Customers table, adedd a column named "Current Age"
Calculates current customer ages using the "birthdate" column and the TODAY() function

In the Customers table, added a column named "Priority"
Equals "High" for customers who own homes and have Golden membership cards (otherwise "Standard")   

In the Customers table, added a column named "Short_Country"
Returns the first three characters of the customer country, and converts to all uppercase 

In the Customers table, added a column named "House Number"
Extracts all characters/numbers before the first space in the "customer_address" column (hint: use SEARCH)

In the Products table, added a column named "Price_Tier"
Equals "High" if the retail price is >$3, "Mid" if the retail price is >$1, and "Low" otherwise

In the Stores table, added a column named "Years_Since_Remodel"
Calculates the number of years between the current date (TODAY()) and the last remodel date


### 2) In the REPORT view, added the following measures (Assigned to tables as you see fit, and use a matrix to match the "spot check" values)

Created new measures named "Quantity Sold" and "Quantity Returned" to calculate the sum of quantity from each data table

Created new measures named "Total Transactions" and "Total Returns" to calculate the count of rows from each data table

Created a new measure named "Return Rate" to calculate the ratio of quantity returned to quantity sold (formated as %)

Created a new measure named "Weekend Transactions" to calculate transactions on weekends

Created a new measure named "% Weekend Transactions" to calculate weekend transactions as a percentage of total transactions (formated as %)

Created new measures named "All Transactions" and "All Returns" to calculate grand total transactions and returns (regardless of filter context)

Created a new measure to calculate "Total Revenue" based on transaction quantity and product retail price, and formated as $

Created a new measure to calculate "Total Cost" based on transaction quantity and product cost, and formated as $ 

Created a new measure named "Total Profit" to calculate total revenue minus total cost, and formated as $

Created a new measure to calculate "Profit Margin" by dividing total profit by total revenue calculate total revenue (formated as %)

Created a new measure named "Unique Products" to calculate the number of unique product names in the Products table

Created a new measure named "YTD Revenue" to calculate year-to-date total revenue, and format as $

Created a new measure named "60-Day Revenue" to calculate a running revenue total over a 60-day period, and format as $

Created new measures named  "Last Month Transactions", "Last Month Revenue", "Last Month Profit", and "Last Month Returns"

Created a new measure named "Revenue Target" based on a 5% lift over the previous month revenue, and formated as $

# PART 4: Building the Report


### 1) Renamed the tab "Topline Performance" and inserted the Maven Market logo

### 2) Inserted a Matrix visual to show Total Transactions, Total Profit, Profit Margin, and Return Rate by Product_Brand (on rows)
Added conditional formatting to show data bars on the Total Transactions column, and color scales on Profit Margin (White to Green) and Return Rate (White to Red)
Added a visual level Top N filter to only show the top 30 product brands, then sort descending by Total Transactions

### 3) Added a KPI Card to show Total Transactions, with Start of Month as the trend axis and Last Month Transactions as the target goal
Updated the title to "Current Month Transactions", and formated as seen fit
Created two more copies: one for Total Profit (vs. Last month Profit) and one for Total Returns (vs. Last Month Returns)
Change the Returns chart to color coding to "Low is Good"

### 4) Added a Map visual to show Total Transactions by store city
Added a slicer for store country 
Under the "selection controls" menu in the formatting pane, activate the "Show Select All" option

### 5) Next to the map, added a Treemap visual to break down Total Transactions by store country
Pulled in store_state and store_city beneath store_country in the "Group" field to enable drill-up and drill-down functionality

### 6) Beneath the map, added a Column Chart to show Total Revenue by week, and format as you see fit
Added a report level filter to only show data for 1998
Updated the title to "Weekly Revenue Trending"

### 7) In the lower right, added a Gauge Chart to show Total Revenue against Revenue Target
Added a visual level Top N filter to show the latest Start of Month
Removed data labels, and update the title to "Revenue vs. Target"

### 8) Selected the Matrix and activate the  Edit interactions option to prevent the Treemap from filtering

### 9) Select "USA" in the country slicer, and drill down to select "Portland" in the Treemap
Added a new bookmark named "Portland 1000 Sales"
Added a new report page, named "Notes"
Inserted a text box and write something about the observation regarding Portland
Added a button and used the "Action" properties to link it to the bookmark created.































