# Amazon-project
This is my Excel project from DSA Hub in my journey as a data analyst

##Amazon Product Review Analysis
## Project Overview
This project, undertaken as a Junior Data Analyst at RetailTech Insights, focuses on analyzing product and customer review data from Amazon to derive actionable insights. The goal is to guide product improvement, inform marketing strategies, and enhance customer engagement for sellers on e-commerce platforms.

### Dataset Description
The dataset (amazon.csv) contains information scraped from Amazon product pages. Each row represents a unique product, with aggregated reviewer data stored as comma-separated values where applicable.

## Key Details:

Total Records: 1,465 rows

Total Fields: 16 columns

Columns (Expected):
While the exact column names are not provided in the prompt, based on the analysis tasks, the dataset is expected to contain columns related to:

Product Details: product_name, category, price, discount, ratings (or average_rating)

Customer Engagement: user_reviews, review_titles, review_content, rating_count (or number_of_reviews)

actual_price (derived or explicit)

Other relevant product and review attributes.

## Analysis Tasks - Step-by-Step Process
The following analysis tasks were performed using pivot tables and calculated columns in Excel to extract meaningful insights from the dataset. Below are the general steps for each task:

### Data cleansing and Helper Columns
Delete duplicated Product_id
Remove blank space and special character in the data set 
Split the catagory column into 4 different column
create a new column for potential revenue, top reviews and range buckets

## General Excel Steps for Pivot Tables:

Select your entire dataset.

Go to Insert tab > PivotTable.

Choose New Worksheet or Existing Worksheet for placement.

Drag and drop fields into the Rows, Columns, Values, and Filters areas of the PivotTable Fields pane.

### 1. Average Discount Percentage by Product Category
Objective: Calculate the average discount applied to products within each category.

Steps:

Create a PivotTable.

Drag category to the Rows area.

Drag discount (it's a percentage ) to the Values area.

Change the Value Field Settings for discount to Average. Ensured the discount is represented as a decimal or percentage for correct averaging.

### 2. Products Listed Under Each Category
Objective: Determine the count of products belonging to each distinct product category.

Steps:

Create a PivotTable.

Drag category to the Rows area.

Drag product_name (or any unique product identifier) to the Values area.

Change the Value Field Settings for product_name to Count.

### 3. Total Number of Reviews Per Category
Objective: Sum the total number of customer reviews for all products within each category.

Steps:

Create a PivotTable.

Drag category to the Rows area.

Drag rating_count (or number_of_reviews) to the Values area.

Change the Value Field Settings for rating_count to Sum.

### 4. Products with the Highest Average Ratings
Objective: Identify the products that have received the highest average ratings from customers.

Steps:

Create a PivotTable.

Drag product_name to the Rows area.

Drag ratings (or average_rating) to the Values area.

Change the Value Field Settings for ratings to Average.

Sort the PivotTable results by the Average of ratings column in Descending order.

Apply a Value Filter (Top 10) on Average of ratings to show only the Top 5 or Top N items.

### 5. Average Actual Price vs. Discounted Price by Category
Objective: Compare the average original price to the average discounted price for products in each category.

Steps:

Create a PivotTable.

Drag category to the Rows area.

Drag actual_price to the Values area and set Value Field Settings to Average.

Drag discounted price to the Values area and set Value Field Settings to Average.

### 6. Products with the Highest Number of Reviews
Objective: Find the products that have accumulated the highest volume of customer reviews.

Steps:

Create a PivotTable.

Drag Product_ID to the Rows area.

Drag rating_count (or number_of_reviews) to the Values area.

Change the Value Field Settings for rating_count to Sum.

Sort the PivotTable results by the Sum of rating_count column in Descending order.


### 7. Products with a Discount of 50% or More
Objective: Count how many products are offered with a discount percentage equal to or greater than 50%.

Steps:

Create a calculated column in the raw data  using an IF formula: =IF(Discount_Percentage >= 0.5, YES, NO).

Create a PivotTable.

Drag Is_50_Percent_Plus_Discount to the Rows area.

Drag product_Id to the Values area and set Value Field Settings to Count.


### 8. Distribution of Product Ratings
Objective: Analyze the frequency of different rating values (e.g., how many products have a 3.0 rating, 4.0 rating, etc.).

Steps:

Create a PivotTable.

Drag ratings (or average_rating) to the Rows area.

Drag product_name (or any unique identifier) to the Values area.

Change the Value Field Settings for product_name to Count.

### 9. Total Potential Revenue by Category
Objective: Calculate the potential revenue for each category, defined as actual_price × rating_count.

Pre-computation: Create a calculated column in your raw data named Potential_Revenue with the formula: =Actual_Price * Rating_Count.

Steps:

Create a PivotTable.

Drag category to the Rows area.

Drag Potential_Revenue to the Values area.

Change the Value Field Settings for Potential_Revenue to Sum.

### 10. Number of Unique Products Per Price Range Bucket
Objective: Categorize products into price ranges (<₹200, ₹200–₹500, >₹500) and count the unique products within each bucket.

Pre-computation: Create a calculated column in your raw data named Price_Bucket using nested IF statements or a LOOKUP table, e.g., =IF(Price<200, "<₹200", IF(Price<=500, "₹200–₹500", ">₹500")).

Steps:

Create a PivotTable.

Drag Price_Bucket to the Rows area.

Drag product_name (or any unique identifier) to the Values area.

Change the Value Field Settings for product_name to Count (or Count of Unique Values).

### 11. How Does the Rating Relate to the Level of Discount?
Objective: Investigate how product ratings correlate with the level of discount offered.

Steps:

Create a PivotTable.

Drag discount (or Discount_Percentage) to the Rows area. You might want to Group the discount percentages into ranges (e.g., 0-10%, 11-20%, etc.) for better readability.

Drag ratings (or average_rating) to the Values area.

Change the Value Field Settings for ratings to Average.

Analyze the average rating for each discount group to observe any trends.

### 12. Products with Fewer Than 1,000 Reviews
Objective: Identify and count products that have received less than 1,000 reviews.

Steps:

Create a PivotTable.

Drag product_name to the Rows area.

Drag rating_count (or number_of_reviews) to the Values area.

Set Value Field Settings for rating_count to Sum.

Apply a Value Filter on Sum of rating_count where is less than 1000.

The count of rows in the filtered PivotTable will give you the number of such products.

### 13. Which Categories Have Products with the Highest Discounts?
Objective: Determine which product categories feature products with the most significant discounts.

Steps:

Create a PivotTable.

Drag category to the Rows area.

Drag discount (assuming numerical discount percentage) to the Values area.

Change the Value Field Settings for discount to Max (to find the highest individual discount within each category).

Sort the PivotTable by Max of discount in Descending order.

### 14. Identify the Top 5 Products in Terms of Rating and Number of Reviews Combined
Objective: Identify the top 5 products based on a combined consideration of their average rating and total number of reviews.

Pre-computation: This task often requires a custom scoring metric. Create a calculated column in your raw data (or a Calculated Field in PivotTable, though a raw data column is often more flexible for complex scoring) named Combined_Score. A simple example could be: Combined_Score = (Average_Rating * Weight_Rating) + (Normalized_Review_Count * Weight_Reviews). You would need to normalize rating_count if its scale is vastly different from ratings (e.g., Normalized_Review_Count = Rating_Count / MAX(Rating_Count)).

Steps:

Create a PivotTable.

Drag product_name to the Rows area.

Drag Combined_Score to the Values area.

Set Value Field Settings for Combined_Score to Sum or Average (depending on how you defined the score).

Sort the PivotTable by Sum/Average of Combined_Score in Descending order.

Apply a Value Filter (Top 10) on Combined_Score to show only the Top 5 items.

## Final Task: Dashboard Creation
A comprehensive Excel dashboard was built using the cleaned dataset and the outputs from the analysis tasks. This dashboard visually represents the key insights, allowing for easy interpretation and presentation of the findings to stakeholders. The dashboard typically includes:

Interactive elements (slicers) to filter data.

Charts (bar charts, pie charts, line charts) to visualize trends and distributions.

Key performance indicators (KPIs) showing aggregated metrics.

Clear and concise labels and titles.
