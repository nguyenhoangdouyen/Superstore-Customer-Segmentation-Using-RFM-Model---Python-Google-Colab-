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

#### ⚡ Data Quality Insights

During the initial data exploration, a mismatch was identified between **Stock Code** count (4070) and **Description** count (4223). This inconsistency suggests potential data quality issues that require further investigation. Possible reasons include:

- Some products may have multiple descriptions under the same stock code.
- Certain descriptions might not be linked to any valid stock code.
- Data inconsistencies due to missing, duplicated, or improperly recorded stock codes.

It is recommended to conduct additional validation and data cleaning to ensure consistency and accuracy in analysis.

[In 8]:
To validate and review the processed data, export the **description_check** dataframe to an Excel file.

```python
# Export Data for Double-Checking Orders
description_check.to_excel(path + 'description_check.xlsx')
```

[Out 8]:
![Image](https://github.com/user-attachments/assets/73a60e98-6a2a-4925-8e38-7bd9e1a1e1bc)

#### ⚠ Manual Review Required

Some orders contain incorrect **descriptions** → Perform a **manual check** and mark them as **errors** to facilitate further processing.

[In 9]:
To obtain a complete dataset with flagged erroneous orders, merge the **description_check_update** file with the **ecommerce** dataset.

```python
#Merging Data for Error Identification
ecommerce_update = ecommerce.merge(description_check_update[['Description','Error']], how='left', on='Description')
```
#### 🔍 Checking If Negative Quantities Indicate Cancellations

[In 10]:
To verify whether transactions with negative **Quantity** values are due to order cancellations (indicated by **InvoiceNo** starting with "C"), apply the following condition:

```python
ecommerce_update['InvoiceNo'] = ecommerce_update['InvoiceNo'].astype(str)
ecommerce_update['cancel_invoice'] = ecommerce_update.apply(
    lambda x: True if x['Quantity'] < 0 and x['InvoiceNo'].startswith('C') else False, axis=1)
```

#### 🚨 Identifying Invalid Transactions

After flagging cancellations, verify if there are any transactions where **Quantity** is negative, but the **InvoiceNo** does not start with "C". These may indicate data inconsistencies.

[In 11]:
After flagging cancellations, verify if there are any transactions where **Quantity** is negative, but the **InvoiceNo** does not start with "C". These may indicate data inconsistencies.

```python
check_invalid_invoice = ecommerce_update[(ecommerce_update['cancel_invoice'] == False) & (ecommerce_update['Quantity'] < 0)]
print(len(check_invalid_invoice))  # Number of inconsistent records
check_invalid_invoice.head()  # Preview of invalid records
```
[Out 11]:

![Image](https://github.com/user-attachments/assets/f6708de9-d4fb-45a7-be28-ca4dfb886f99)

#### ⚠ Further Investigation: Negative Quantity Without Cancellation

After checking, it was found that some orders **do not have "C" in InvoiceNo** but still have **negative Quantity**. To analyze the cause, export the file for further review.

[In 12 ]:

```python
# Check for Negative Unit Prices
print(len(ecommerce_update[ecommerce_update['UnitPrice'] < 0 ]))  # Number of invalid records
print(ecommerce_update[ecommerce_update['UnitPrice'] < 0 ].head())  # Preview of invalid records
print(len(ecommerce_update[ecommerce_update['UnitPrice'] < 0 ]))  # Number of invalid records
ecommerce_update[ecommerce_update['UnitPrice'] < 0 ].head()  # Preview of invalid records
```

[Out 12 ]:

![Image](https://github.com/user-attachments/assets/32e6169f-c53e-472a-a6df-88863817444a)

#### ✨ General Observations

**Data Types:**
The following columns have inappropriate data types and should be converted to **strings** for easier processing:
- **InvoiceNo**, **StockCode**, **Description**, **CustomerID**, **Country**.

**Data Values:**
- **Quantity < 0 & InvoiceNo starts with 'C'** → These transactions indicate **canceled orders** and should be **removed** from the dataset.
- **Quantity < 0 but InvoiceNo does NOT start with 'C'** → These records contain **incorrect descriptions** and should be **excluded** from the dataset.
- **UnitPrice < 0 & incorrect Description** → These are **invalid transactions** and should also be **removed** from the dataset.

### **2️⃣ Exploratory Data Analysis (EDA)**

🛠 To ensure proper data processing, we need to convert specific columns to the appropriate data types:

[In 13]:
```python
# Convert selected columns to string type
column_list = ["InvoiceNo", "StockCode", "Description", "CustomerID", "Country"]
for c in column_list:
    ecommerce_update[c] = ecommerce_update[c].astype(str)

# Convert InvoiceDate to datetime format
ecommerce_update['InvoiceDate'] = pd.to_datetime(ecommerce_update['InvoiceDate'])
```

🛠 Data Cleaning: Removing Invalid Transactions

To ensure data quality, the following steps were taken to remove invalid records:

[In 14]:

```python
# 1. Remove canceled orders (InvoiceNo starting with 'C')
ecommerce_update = ecommerce_update[~ecommerce_update['InvoiceNo'].str.startswith("C")]

# 2. Remove transactions with Quantity < 0 where InvoiceNo does not start with 'C' (due to incorrect descriptions)
ecommerce_update = ecommerce_update[ecommerce_update['Quantity'] > 0]

# 3. Remove transactions marked as Error = 1 (due to incorrect descriptions)
ecommerce_update = ecommerce_update[ecommerce_update['Error'] != 1]

# 4. Remove transactions with UnitPrice < 0
ecommerce_update = ecommerce_update[ecommerce_update['UnitPrice'] > 0]
```

🛠 Checking Missing Values in CustomerID & Error Columns

[In 15]:

```python
import missingno as msno
import numpy as np

# Visualizing missing data
msno.matrix(ecommerce_update)

# Handling missing values in CustomerID
ecommerce_update['CustomerID'] = ecommerce_update['CustomerID'].replace(["nan", "", " "], np.nan)

# Creating a dictionary with missing value counts and percentages
missing_dict = {
    'volume': ecommerce_update.isnull().sum(),
    '%': (ecommerce_update.isnull().sum() / ecommerce_update.shape[0]) * 100
}
missing_ecommerce = pd.DataFrame.from_dict(missing_dict)

# Display missing values summary
print(missing_ecommerce)
```

[Out 15]:
![Image](https://github.com/user-attachments/assets/35e54952-05be-4430-8115-45d1337d7b0b)

![Image](https://github.com/user-attachments/assets/184f9ea7-024a-497b-90ec-58a849535aee)

#### 🔍 Investigating Missing CustomerID

Before executing the code: It is important to check if the missing **CustomerID** is concentrated in specific countries or time periods before deciding how to handle it.

**🧐 Key Findings:**
- **Missing CustomerID** values are **spread across all months & countries**, not just a specific region or time period.
- Likely due to **human errors** (e.g., incomplete updates) or **system recording issues**.

**Hypothesis:**
- **Missing CustomerID** might be concentrated in the **United Kingdom** or could be **distributed evenly** across all countries.
- These missing **CustomerID** values could be limited to specific **time periods** or may be **spread evenly** across the months.

**✅ Solution:**
Since **CustomerID is essential**, drop missing values to maintain data integrity.

```python
# Remove transactions with missing CustomerID
ecommerce_update = ecommerce_update.dropna(subset=['CustomerID'])
```

[In 16]: 
🔍 Check duplicate**
```python
# Identify duplicate rows based on 'InvoiceNo', 'StockCode', 'InvoiceDate', and 'CustomerID'
ecommerce_duplicate = ecommerce_update[ecommerce_update.duplicated(subset=['InvoiceNo', 'StockCode', 'InvoiceDate', 'CustomerID'])]

# Print the number of duplicate rows found
print(ecommerce_duplicate.shape)
```

The result (10038, 12) means there are 10,038 duplicate rows, and they need to be detected and handled in **two cases**: 
1. **Case 1 - Duplicates with the Same Quantity**: 
   - These duplicates are likely caused by system errors (e.g., duplicate entries with the same quantity). 
   - **Action**: Drop the duplicates because they are identical.

2. **Case 2 - Duplicates with Different Quantities**:
   - These duplicates may occur due to system recording issues (e.g., a single order being split into multiple records with different quantities). 
   - **Action**: Sum the quantities of the duplicate entries to correct the data.

[In 16]:

**Detecting and Handling Duplicate Rows:** 

**1. Detecting Exact Duplicate Rows:**
   - The following code detects rows that are completely duplicated based on `InvoiceNo`, `StockCode`, `InvoiceDate`, `CustomerID`, and `Quantity`.
   
```python
# Detect exact duplicate rows based on 'InvoiceNo', 'StockCode', 'InvoiceDate', 'CustomerID', and 'Quantity'
invoice_duplicate_total = ecommerce_update[ecommerce_update.duplicated(subset=['InvoiceNo', 'StockCode', 'InvoiceDate', 'CustomerID', 'Quantity'])]
```
[In 17]:

**2. Grouping and Aggregating Data for Exact duplicate:**
The following code groups the data by `InvoiceNo`, `StockCode`, `InvoiceDate`, `CustomerID`, and `Quantity`, and keeps the first occurrence of other columns:

```python
# Group by 'InvoiceNo', 'StockCode', 'InvoiceDate', 'CustomerID', and 'Quantity' and keep the first occurrence of other columns
ecommerce_update = ecommerce_update.groupby(['InvoiceNo', 'StockCode', 'InvoiceDate', 'CustomerID', 'Quantity'], as_index=False).agg({
    'UnitPrice': 'first',          # Keep the first 'UnitPrice'
    'Description': 'first',        # Keep the first 'Description'
    'Country': 'first',            # Keep the first 'Country'
    'Error': 'first',              # Keep the first 'Error'
    'cancel_invoice': 'first',     # Keep the first 'cancel_invoice'
    'Date': 'first',               # Keep the first 'Date'
    'Month': 'first'               # Keep the first 'Month'
})
```
[In 18]:

**3. Grouping and Summing Quantities for Partial duplicate:**

The following code groups the data by `InvoiceNo`, `StockCode`, `InvoiceDate`, and `CustomerID`, sums the `Quantity`, and keeps the first occurrence of other columns:

```python
# Group by 'InvoiceNo', 'StockCode', 'InvoiceDate', 'CustomerID' and sum the 'Quantity', keeping the first occurrence of other columns
ecommerce_update = ecommerce_update.groupby(['InvoiceNo', 'StockCode', 'InvoiceDate', 'CustomerID'], as_index=False).agg({
    'Quantity': 'sum',            # Sum 'Quantity' for each group
    'UnitPrice': 'first',         # Keep the first 'UnitPrice'
    'Description': 'first',       # Keep the first 'Description'
    'Country': 'first',           # Keep the first 'Country'
    'Error': 'first',             # Keep the first 'Error'
    'cancel_invoice': 'first',    # Keep the first 'cancel_invoice'
    'Date': 'first',              # Keep the first 'Date'
    'Month': 'first'              # Keep the first 'Month'
})
```

**🔍 Prepare RFM Dataframe for calculating**
[In 19]:

```python
#Calculate the last transaction date  
last_day = ecommerce_update['Date'].max()

# Create revenue column 
ecommerce_update['revenue'] = ecommerce_update['Quantity'] * ecommerce_update['UnitPrice']  

# Create RFM df
RFM_df = ecommerce_update.groupby('CustomerID').agg(  
    Recency=('Date', lambda x: (last_day - x.max()).days),  # Calculate the number of days since the last purchase  
    Frequency=('InvoiceNo', 'count'),  # Count the number of transactions per customer  
    Monetary=('revenue', 'sum')  # Sum the total revenue per customer  
).reset_index()

RFM_df
```

**🔍 Check outlier**
[In 20]:

```python
# Check outliers for the 'Recency' column
sns.boxplot(data=RFM_df, x='Recency')

# Check outliers for the 'Monetary' column
sns.boxplot(data=RFM_df, x='Monetary')

# Check outliers for the 'Frequency' column
sns.boxplot(data=RFM_df, x='Frequency')
```
[Out 20]:

![Image](https://github.com/user-attachments/assets/dd08a423-d0da-43a5-bbfe-24ddf6c85bcf)

[In 21]:
**🔍 Drop outlier**
```python
# Set the 95th percentile threshold for 'Recency'
R_update = RFM_df['Recency'].quantile(0.95)

# Set the 95th percentile threshold for 'Frequency'
F_update = RFM_df['Frequency'].quantile(0.95)

# Set the 95th percentile threshold for 'Monetary'
M_update = RFM_df['Monetary'].quantile(0.95)

# Filter out rows where any column exceeds the 95th percentile threshold
RFM_update = RFM_df[(RFM_df['Recency'] <= R_update) & 
                     (RFM_df['Frequency'] <= F_update) & 
                     (RFM_df['Monetary'] <= M_update)]
```
[In 22]:
```python
# Check for outliers in the 'Recency' column after filtering
sns.boxplot(data=RFM_update, x='Recency')

# Check for outliers in the 'Frequency' column after filtering
sns.boxplot(data=RFM_update, x='Frequency')

# Check for outliers in the 'Monetary' column after filtering
sns.boxplot(data=RFM_update, x='Monetary')
```

[Out 22]:

![Image](https://github.com/user-attachments/assets/80aaab5a-24ec-4cd2-ae78-bbbe90208ae9)

**🔍Assign RFM scores using Qcut** 

[In 23]:
```python
# Recency score: Lower values indicate more recent purchases, so assign higher scores to lower recency values  
RFM_update['R_score'] = pd.qcut(RFM_update['Recency'], 5, labels=range(5, 0, -1), duplicates='drop').astype(int)  

# Frequency score: Higher values indicate more frequent purchases, so assign higher scores to higher frequency values  
RFM_update['F_score'] = pd.qcut(RFM_update['Frequency'], 5, labels=range(1, 6), duplicates='drop').astype(int)  

# Monetary score: Higher values indicate higher spending, so assign higher scores to higher monetary values  
RFM_update['M_score'] = pd.qcut(RFM_update['Monetary'], 5, labels=range(1, 6), duplicates='drop').astype(int)  

# Combine RFM scores into a single string to create the RFM segment  
RFM_update['RFM'] = (
    RFM_update['R_score'].astype(str) +
    RFM_update['F_score'].astype(str) +
    RFM_update['M_score'].astype(str)
)
```

**🔍Process the segmentation table & merge with RFM_df**

[In 24]:
```python
# Flatten the segmentation table by splitting the 'RFM Score' column  
segmentation['RFM Score'] = segmentation['RFM Score'].astype(str).str.split(',')
segmentation = segmentation.explode('RFM Score').reset_index(drop=True)

# Trim spaces in the 'RFM Score' column to ensure proper merging  
segmentation['RFM Score'] = segmentation['RFM Score'].str.strip()

# Merge the segmentation table with the RFM table based on the 'RFM Score'  
RFM_final = RFM_update.merge(segmentation, how='left', left_on='RFM', right_on='RFM Score')

# Display the final RFM segmentation table  
RFM_final
```
[Out 24]:

![Image](https://github.com/user-attachments/assets/e597bac7-f7f6-4cce-baf6-2108d3d2b177)
