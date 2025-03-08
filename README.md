![image](https://github.com/user-attachments/assets/4316057d-2721-4134-b25b-634cc0a30bfe)# **📊 Project:Superstore Customer Segmentation Using RFM Model (Python - Colab)** #
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
```python
# Import required libraries for dataframe and visualization
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
import squarify
