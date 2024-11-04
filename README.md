# Reliance Trends Fashion Sales Analysis

This project analyzes sales data from a dataset containing information on Reliance Trends Fashion products. The analysis covers various aspects, including total sales, sales by category, sales by gender, top-selling brands, and discount analysis.

## Table of Contents

- [Getting Started](#getting-started)
- [Data Cleaning and Preparation](#data-cleaning-and-preparation)
- [Total Sales Analysis](#total-sales-analysis)
- [Sales by Category](#sales-by-category)
- [Sales by Gender](#sales-by-gender)
- [Top Selling Brands](#top-selling-brands)
- [Discount Analysis](#discount-analysis)
- [Libraries Used](#libraries-used)
- [Results](#results)

---

## Getting Started

1. **Clone the repository** or **Download the code**.
2. Ensure you have the required libraries installed:
   ```bash
   pip install pandas matplotlib seaborn
3. Load the dataset (`Reliance Trends Fashion.csv`) to begin analysis. This dataset should contain columns for `Category`, `Category_by_gender`, `Brand`, `Discount_Price (in Rs.)`, and `Original_Price (in Rs.)`
   ```bash
   df = pd.read_csv('Reliance Trends Fashion.csv')

## Data Cleaning and Preparation
1. The data requires some cleaning before analysis, including converting price columns to numeric data types for accurate calculations.
   ```bash
   # Convert price columns to numeric type
    reliance['Discount_Price (in Rs.)'] = reliance['Discount_Price (in Rs.)'].str.replace(',', '').astype(float)
    reliance['Original_Price (in Rs.)'] = reliance['Original_Price (in Rs.)'].str.replace(',', '').astype(float)

## Total Sales Analysis
The analysis calculates the total sales based on discounted price of the product.
```bash
 # Calculate total sales based on discounted prices
  reliance['Total_Sales'] = reliance['Discount_Price (in Rs.)']
  total_sales = reliance['Total_Sales'].sum()
  print(f"Total Sales: {total_sales}")
```
## Sales by Category
Analyzes sales by product category and visualizes them with a bar plot.

```bash
  # Group by category and sum sales to analyze sales by category
  sales_by_category = reliance.groupby('Category')['Total_Sales'].sum().sort_values(ascending=False)
  print(sales_by_category)

  # Plot sales by category
  plt.figure(figsize=(10, 6))
  sns.barplot(x=sales_by_category.index, y=sales_by_category.values)
  plt.xlabel('Category')
  plt.ylabel('Total Sales')
  plt.title('Sales by Category')
  plt.xticks(rotation=45, ha='right')
  plt.show()
```

## Sales by Gender
Shows sales distribution by gender using the `Category_by_gender` column and a pie chart.

```bash

# Group by gender and calculate total sales for each
sales_by_gender = reliance.groupby('Category_by_gender')['Total_Sales'].sum()
print(sales_by_gender)

# Plot sales by gender
plt.figure(figsize=(6, 6))
plt.pie(sales_by_gender, labels=sales_by_gender.index, autopct='%1.1f%%', startangle=90)
plt.title('Sales by Gender')
plt.show()
```

## Top Selling Brands

Identifies the top 10 brands by sales and visualizes them in a bar plot.

```bash
# Group by brand and calculate total sales, then sort to find top 10 brands
sales_by_brand = reliance.groupby('Brand')['Total_Sales'].sum().sort_values(ascending=False)
top_brands = sales_by_brand.head(10)
print(top_brands)

# Plot top 10 selling brands
plt.figure(figsize=(10, 6))
sns.barplot(x=top_brands.index, y=top_brands.values)
plt.xlabel('Brand')
plt.ylabel('Total Sales')
plt.title('Top 10 Selling Brands')
plt.xticks(rotation=45, ha='right')
plt.show()

```

## Discount Analysis

Calculates the average discount percentage and visualizes its distribution

```bash
# Calculate the average discount percentage
reliance['Discount_Percentage'] = ((reliance['Original_Price (in Rs.)'] - reliance['Discount_Price (in Rs.)']) / reliance['Original_Price (in Rs.)']) * 100
average_discount = reliance['Discount_Percentage'].mean()
print(f"Average Discount Percentage: {average_discount}")

# Plot distribution of discount percentages
plt.figure(figsize=(8, 6))
sns.histplot(reliance['Discount_Percentage'], kde=True)
plt.xlabel('Discount Percentage')
plt.ylabel('Frequency')
plt.title('Distribution of Discount Percentages')
plt.show()
```

## Libraries Used

- **pandas**: For data manipulation and cleaning
- **matplotlib**: For plotting graphs
- **seaborn**: For enhanced visualizations

## Results

This analysis provides insights into:

- **Total sales figures** based on discounted prices.
- **Sales performance** by product category and gender.
- **Top-selling brands** based on sales volume.
- **Distribution and average** of discount percentages applied to products.

These insights can help inform future sales and marketing strategies for Reliance Trends.



