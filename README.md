# DSA-AMAZON-DATA-ANALYSIS-PROJECT
### This project analyzes product and customer review data from Amazon using Excel. It uses PivotTables, calculated fields, and a dynamic dashboard to generate insights that can help sellers improve products, marketing strategies, and customer engagement. 

## ✅ Tools Used
- Microsoft Excel (PivotTables, Formulas, Charts) [Download here](https://www.microsoft.com)
- Power Query (for optional cleaning) [Download here](https://apps.microsoft.com/detail/9ntxr16hnw1t?launch=true&mode=full&hl=en-us&gl=ng&ocid=bingwebsearch)
- GitHub (for version control & presentation) [sign-up here](https://github.com/)
  
## 📂 Dataset Description
- 1,465 Amazon product listings
- 16 columns: product details, pricing, review stats, and more
- Aggregated review data per product

## 🎯 Analysis Objectives
Use pivot tables and calculated columns where necessary to answer the following: 
1. What is the average discount percentage by product category? 
2. How many products are listed under each category? 
3. What is the total number of reviews per category?  
4. Which products have the highest average ratings? 
5. What is the average actual price vs the discounted price by category? 
6. Which products have the highest number of reviews? 
7. How many products have a discount of 50% or more? 
8. What is the distribution of product ratings (e.g., how many products are rated 3.0, 4.0, etc.)? 
9. What is the total potential revenue (actual_price × rating_count) by category? 
10. What is the number of unique products per price range bucket (e.g., <₹200,₹200–₹500, >₹500)? 
11. How does the rating relate to the level of discount? 
12. How many products have fewer than 1,000 reviews? 
13. Which categories have products with the highest discounts? 
14. Identify the top 5 products in terms of rating and number of reviews combined.
15. Using your cleaned dataset and pivot outputs, build an Excel dashboard.

## 🧹 Data Cleansing & Calculated Column Guide – Amazon Case Study
This document outlines all the data preparation steps and formulas used to cleanse the dataset and derive additional columns for analysis in Excel.

### 🔧1. Identification removal of duplicate dataset using Unique Product_ID
- 114 duplicate rows was identified and removed. Hence, reducing the rows from 1465 to 1351
### 🔧 2. Clean actual_price and discounted_price
*Problem:* Values contain currency symbols (₹), commas, or are stored as text.  
*Solution:*
excel
=VALUE(SUBSTITUTE(SUBSTITUTE(A2, "₹", ""), ",", ""))

### 🔧 3. Convert rating to number
excel
=VALUE(A2)

### 🔧 4. Clean rating_count (Handle missing/non-numeric values)
excel
=IF(ISNUMBER(A2), A2, 0)

---
### 🔧 5. Extract main_category from category path
excel
=LEFT(A2, FIND("|", A2 & "|") - 1)

---
### 🔧 6. Create price_bucket based on discounted price
excel
=IF([@discounted_price]<200,"<200",
   IF([@discounted_price]<=500,"200–500",">500"))

---
### 🔧 7. Calculate discount_percentage
excel
=([@actual_price] - [@discounted_price]) / [@actual_price]

---
### 🔧 8. Flag discount_50_plus
excel
=IF([@discount_percentage] >= 50%, "Yes", "No")

---
### 🔧 9. Flag products with fewer than 1,000 reviews
excel
=IF([@rating_count_clean] < 1000, "Yes", "No")

---
### 🔧 10. Calculate Total_Potential_Revenue
excel
=[@actual_price] * [@rating_count_clean]

---
### 🔧 11. Create Normalized_Rating (0 to 1 scale)
excel
=[@rating_clean] / 5

---
### 🔧 12. Create Normalized_Popularity
1. In helper cell W8*:
excel
=MAX([rating_count_clean column])

2. Then in a new column:
excel
=[@rating_count_clean] / $W$8

---
### 🔧 13. Create Combined_Score (equal weight)
excel
=([@Normalized_Rating] + [@Normalized_Popularity]) / 2

---
### ✅ Best Practices
- Use *Excel Tables* (Ctrl + T) for structured references like [@column_name]
- Apply appropriate formatting (Percentage, Currency, etc.)
- Document formulas using Excel comments or a reference sheet
---
## 📊 Dashboard Features
- Slicers for Product category    
- Pivot charts: Rating Distribution, Reviews by Category  
- Price bucket segmentation and many more.

## 💡 Key Insights
- Home improvement and toys&games recoreded the highest and lowest average discount percentage by product category 0f 50% and 0% respectively
- Electronics, computers Accessories and Home & Kitchen lead in revenue potential
-  310 unique products had a <1000 reviews which cut across Electronics, computers Accessories, Home & Kitchen and office Product categories
- Heavily discounted products (50%+) often attract higher review counts  
- Rating distribution clusters around 4.0–4.5 stars
- top 5 most rated products consist of 3 HDMI cables and 2 wireless Earphones of different colours and makeups with rating combined scores range of 0.8-0.9
- Etc.
- ## 📌 Conclusions

### 1. High Revenue Potential in Specific Categories
- Categories like *Electronics, **Home & Kitchen, and **Computers & Accessories* contribute the most to potential revenue.
- These categories have higher product prices and review volumes.

### 2. Positive Correlation Between Discounts and Reviews
- Products with *≥50% discount* tend to attract more reviews, indicating greater visibility and purchase likelihood.

### 3. Most Products Have Ratings Between 3.5 – 4.5
- Suggests generally favorable customer satisfaction but also reflects a narrow quality distribution.

### 4. Underutilized Price Segments
- There is opportunity in the *premium segment (>₹500)*, which has fewer products but high potential revenue per unit.

### 5. Many Products Lack Review Volume
- A considerable number of products have *fewer than 1,000 reviews*, impacting credibility and customer trust.
---

## ✅ Recommendations

### 1. 🎯 Focus Marketing on High-Revenue Categories
- Prioritize advertising and visibility strategies for *Electronics,Computer Accessories* and *Home & Kitchen*, and similar high-performing categories.

### 2. 💸 Use Strategic Discounts to Drive Engagement
- Offer *targeted discounts (e.g., 50% or more)* on selected products to increase visibility and review counts.

### 3. 🌟 Boost Ratings for Mid-Tier Products
- Improve customer experience and follow-up strategies to increase ratings of products rated between *3.5 and 4.0*.

### 4. 🧼 Eliminate or Optimize Underperformers
- Flag and review products with *low ratings and low review counts* for either optimization or removal.

### 5. 📦 Expand into Low-Saturation, High-Price Segments
- Consider introducing high-quality items priced above ₹500 to capture underserved premium segments.

### 6. 📊 Track KPIs Monthly
- Regularly monitor:
  - Total reviews
  - Average discount %
  - Product rating trends
  - Revenue potential by category

## 📷 Dashboard Preview
![Pivot Tables and Dashboard]
