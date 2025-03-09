# **📊 Project:Superstore Customer Segmentation Using RFM Model (Python - Colab)** #
Author: Nguyễn Hoàng Đỗ Uyên
Date: 07/10/2001
Tools Used: Python

## 📑 Table of Contents ##
- 📌 **Background & Overview**  
- 📂 **Dataset Description & Data Structure**  
- 🔎 **Final Conclusion & Recommendations**  

## 📌 Background & Overview ##
### Objective ###

📖 **What is this project about?**  

- The Marketing team wants to launch personalized campaigns for customer retention and acquisition during the holiday season. However, due to the large dataset, manual segmentation is no longer feasible.  
- To solve this, the **RFM model** is applied using **Python (Colab)** to classify customers into different segments based on their purchasing behavior.  
- This project involves **data preparation, RFM score calculation, segmentation, visualization, and providing actionable recommendations** for the Marketing and Sales teams to optimize their strategies.  

👤 **Who is this project for?**  

✔️ Marketing & Sales Department  
✔️ Decision-makers & stakeholders  

❓ **Business Questions:**  

✔️ How can we segment customers effectively using the RFM model?  
✔️ Which customer groups should be prioritized for retention and promotional campaigns?  
✔️ What actionable insights can help improve marketing strategies and customer engagement?  
✔️ What strategies should be applied to different customer segments to maximize value?  

### RFM Analysis Overview  

**🔎 Why use RFM?**  

RFM (Recency, Frequency, Monetary) is a customer analysis technique based on purchasing behavior.  
- **Recency**: Measures the time elapsed since a customer's last purchase.  
- **Frequency**: Evaluates how often a customer makes transactions.  
- **Monetary**: Calculates the total amount spent by the customer.  
By applying RFM, businesses can segment customers based on their value, allowing them to optimize marketing and customer engagement strategies.  

**🛠️ How does RFM work?**

In RFM analysis, each customer is assigned a score based on these three factors. The data is then used to categorize customers into segments, helping businesses identify key audiences for targeted marketing and sales strategies.  

## 📂 Dataset Description & Data Structure  

### 📌 Data Source  
- **Source**: Provided dataset for E-commerce retail analysis  
- **Size**: 541,910 rows × 8 columns (Sheet 1: E-commerce retail), additional segmentation details in Sheet 2  
- **Format**: .xlsx (Excel file with two sheets)  
## 📊 Data Structure & Relationships  

### 1️⃣ Tables Used  
The dataset consists of **two tables (sheets)**:  
- **Sheet 1: E-commerce Retail** – Contains transaction-level data, including order details, customer IDs, and purchase information.  
- **Sheet 2: Segmentation** – Stores customer segments along with their RFM scores.  

### 2️⃣ Table Schema & Data Snapshot  

#### 📌 Sheet 1: E-commerce Retail  
### 📋 Table Schema: E-commerce Retail  

| Column Name  | Data Type         | Description  |  
|-------------|-----------------|--------------|  
| **InvoiceNo**  | `object`  | Unique invoice number for each transaction (6-digit). If it starts with 'C', it indicates a cancellation. |  
| **StockCode**  | `object`  | Unique product (item) code (5-digit). |  
| **Description**  | `object`  | Product (item) name. |  
| **Quantity**  | `int64`  | The number of units purchased per transaction. |  
| **InvoiceDate**  | `datetime64[ns]`  | Date and time when the transaction occurred. |  
| **UnitPrice**  | `float64`  | Price per unit of the product in sterling. |  
| **CustomerID**  | `float64`  | Unique 5-digit identifier for each customer. |  
| **Country**  | `object`  | Name of the country where the customer resides. |  
- Key columns: `InvoiceNo`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `UnitPrice`, `CustomerID`, `Country`.  

#### 📌 Sheet 2: Segmentation  
### 📊 Customer Segmentation & RFM Scores  

| **Segment**              | **RFM Score**  |  
|-------------------------|-----------------------------------------------------------|  
| **Champions**            | 555, 554, 544, 545, 454, 455, 445  |  
| **Loyal**                | 543, 444, 435, 355, 354, 345, 344, 335  |  
| **Potential Loyalist**   | 553, 551, 552, 541, 542, 533, 532, 531, 452, 451, 442, 441, 431, 453, 433, 432, 423, 353, 352, 351, 342, 341, 333, 323  |  
| **New Customers**        | 512, 511, 422, 421, 412, 411, 311  |  
| **Promising**            | 525, 524, 523, 522, 521, 515, 514, 513, 425, 424, 413, 414, 415, 315, 314, 313  |  
| **Need Attention**       | 535, 534, 443, 434, 343, 334, 325, 324  |  
| **About To Sleep**       | 331, 321, 312, 221, 213, 231, 241, 251  |  
| **At Risk**              | 255, 254, 245, 244, 253, 252, 243, 242, 235, 234, 225, 224, 153, 152, 145, 143, 142, 135, 134, 133, 125, 124  |  
| **Cannot Lose Them**     | 155, 154, 144, 214, 215, 115, 114, 113  |  
| **Hibernating Customers** | 332, 322, 233, 232, 223, 222, 132, 123, 122, 212, 211  |  
| **Lost Customers**       | 111, 112, 121, 131, 141, 151  |  
- Key columns: `Segment`, `RFM Score`.

## ⚒️ **Main Process** ##

### 1️⃣ Data Cleaning & Preprocessing  

**Step 1 : Reading and Understanding Data**

[In 1]:  
```python
# Import required libraries for dataframe and visualization
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
import squarify
```

[In 2]:  
```python
# Load data into Colab  
from google.colab import drive
drive.mount('/content/drive')

# Define the path to the project folder
path = '/content/drive/MyDrive/Python_Nguyễn Hoàng Đỗ Uyên_RFM Project/'

# Load data from Excel file
ecommerce = pd.read_excel(path + 'ecommerce retail.xlsx', sheet_name='ecommerce retail')
segmentation = pd.read_excel(path + 'ecommerce retail.xlsx', sheet_name='Segmentation')

# Convert the files to CSV format
ecommerce.to_csv(path + 'ecommerce.csv', index=False)
segmentation.to_csv(path + 'segmentation.csv', index=False)
```

[In 3]:  
```python
# Print the first five rows of the dataset
ecommerce.head()
```
[Out 3]:  

![Image](https://github.com/user-attachments/assets/91b78596-07a3-4d9d-9fd1-a824b590a0e4)


[In 4]:  
```python
# Print the first five rows of the dataset
ecommerce.head()
```
[Out 4]:  

![Image](https://github.com/user-attachments/assets/deae7032-863a-4694-9229-ac9e649efe18)

[In 5]:
```python
# Check Data Summary
ecommerce.describe()
```
[Out 5]:

![Image](https://github.com/user-attachments/assets/6731170f-672e-4c4b-8493-a9721f239813)

⚡During the initial data exploration, it was observed that the **Quantity** and **Unit Price** columns contain negative values. This is not logically valid and requires further investigation. Possible actions include:
- Checking for data entry errors.
- Identifying whether negative values indicate refunds or cancellations.
- Removing or adjusting incorrect data points to ensure accuracy in analysis.

[In 6]:
```python
# Deeper Analysis on Stock Code and Invoice No
stock_code = ecommerce[['StockCode','InvoiceNo']].groupby('StockCode')['InvoiceNo'].agg('count').reset_index().sort_values(by='InvoiceNo', ascending=False)
print(stock_code.head(5))
print(stock_code.tail(5))
print(len(stock_code))
```
[Out 6]:

![Image](https://github.com/user-attachments/assets/4ee24107-c599-4c7b-86c3-ed09cde6c8b3)

[In 7]:

```python
# Check frequency of each product description. This helps identify the most and least common products in transactions
description_check = ecommerce[['Description','InvoiceNo']].groupby(['Description']).count().reset_index().sort_values(by=['InvoiceNo'], ascending=False)
print(description_check.head())  # Top 5 most common descriptions
print(len(description_check))  # Total unique descriptions
```
[Out 7]:

![Image](https://github.com/user-attachments/assets/9cdb5e74-1ef8-4736-9f6b-8022337e5a55)

### ⚡ Data Quality Insights

During the initial data exploration, a mismatch was identified between **Stock Code** count (4070) and **Description** count (4223). This inconsistency suggests potential data quality issues that require further investigation. Possible reasons include:

- Some products may have multiple descriptions under the same stock code.
- Certain descriptions might not be linked to any valid stock code.
- Data inconsistencies due to missing, du

