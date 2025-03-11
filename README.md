# **📊 Superstore Customer Segmentation Using RFM Model (Python - Colab)** #

![image](https://github.com/user-attachments/assets/b90b73a6-aaa6-44ad-9749-a798ebaf4632)

**Author:** Nguyễn Hoàng Đỗ Uyên

**Date:** 07/10/2001

**Tools Used:** Python

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
# Check the general information of df
ecommerce.info()
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
# Filtered UnitPrice <0
print(len(ecommerce_update[ecommerce_update['UnitPrice'] < 0 ]))
ecommerce_update[ecommerce_update['UnitPrice'] < 0 ].head()
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

**🔍 Check duplicate**
[In 16]: 
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

**🔍 Detecting and Handling Duplicate Rows:** 

**1. Detecting Exact Duplicate Rows:**
   - The following code detects rows that are completely duplicated based on `InvoiceNo`, `StockCode`, `InvoiceDate`, `CustomerID`, and `Quantity`.
[In 17]:

```python
# Detect exact duplicate rows based on 'InvoiceNo', 'StockCode', 'InvoiceDate', 'CustomerID', and 'Quantity'
invoice_duplicate_total = ecommerce_update[ecommerce_update.duplicated(subset=['InvoiceNo', 'StockCode', 'InvoiceDate', 'CustomerID', 'Quantity'])]
```

**2. Grouping and Aggregating Data for Exact duplicate:**
The following code groups the data by `InvoiceNo`, `StockCode`, `InvoiceDate`, `CustomerID`, and `Quantity`, and keeps the first occurrence of other columns:

[In 18]:

```python
# Group by 'InvoiceNo', 'StockCode', 'InvoiceDate', 'CustomerID', and 'Quantity' and keep the first occurrence of other columns
ecommerce_update = ecommerce_update.groupby(['InvoiceNo', 'StockCode', 'InvoiceDate', 'CustomerID', 'Quantity'], as_index=False).agg({
    'UnitPrice': 'first',         
    'Description': 'first',       
    'Country': 'first',           
    'Error': 'first',              
    'cancel_invoice': 'first',   
    'Date': 'first',              
    'Month': 'first'               
})
```

**3. Grouping and Summing Quantities for Partial duplicate:**

After filtering out fully duplicated transactions, the remaining duplicates differ in quantity -> Sum Quantity

[In 19]:

```python
ecommerce_update = ecommerce_update.groupby(
    ['InvoiceNo', 'StockCode', 'InvoiceDate', 'CustomerID'], as_index=False
).agg({
    'Quantity': 'sum',
    'UnitPrice': 'first',
    'Description': 'first',
    'Country': 'first',
    'Error': 'first',
    'cancel_invoice': 'first',
    'Date': 'first',
    'Month': 'first'
})

print(len(ecommerce_update))
```

**🔍 Prepare RFM Dataframe for calculating**
[In 20]:

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
[In 21]:

```python
# Check outliers for the 'Recency' column
sns.boxplot(data=RFM_df, x='Recency')

# Check outliers for the 'Monetary' column
sns.boxplot(data=RFM_df, x='Monetary')

# Check outliers for the 'Frequency' column
sns.boxplot(data=RFM_df, x='Frequency')
```
[Out 21]:

![Image](https://github.com/user-attachments/assets/dd08a423-d0da-43a5-bbfe-24ddf6c85bcf)

[In 22]:
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
[In 23]:
```python
# Check for outliers in the 'Recency' column after filtering
sns.boxplot(data=RFM_update, x='Recency')

# Check for outliers in the 'Frequency' column after filtering
sns.boxplot(data=RFM_update, x='Frequency')

# Check for outliers in the 'Monetary' column after filtering
sns.boxplot(data=RFM_update, x='Monetary')
```

[Out 23]:

![Image](https://github.com/user-attachments/assets/80aaab5a-24ec-4cd2-ae78-bbbe90208ae9)

**🔍Assign RFM scores using Qcut** 

[In 24]:
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

[In 25]:
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
[Out 25]:

![Image](https://github.com/user-attachments/assets/e597bac7-f7f6-4cce-baf6-2108d3d2b177)

## 3️⃣ Visualization & Analysis
**1. Contribution by Segmentation**

[In 26]:

```python

# Count the number of customers in each segment
count_segment_by_users = RFM_final[['CustomerID', 'Segment']].groupby(['Segment'])['CustomerID'].count().reset_index().rename(columns={'CustomerID': 'Count'})

# Calculate the percentage of each segment
count_segment_by_users['percent_segment_by_users'] = round(count_segment_by_users['Count'] / count_segment_by_users['Count'].sum() * 100)

# Format segment names to include percentage
count_segment_by_users['Segment'] = count_segment_by_users['Segment'] + ' ' + count_segment_by_users['percent_segment_by_users'].astype(str) + '%'

# Plot a treemap to visualize segment contribution
plt.figure(figsize=(12, 8))
squarify.plot(
    sizes=count_segment_by_users['percent_segment_by_users'], 
    label=count_segment_by_users['Segment'], 
    color=sns.color_palette("Spectral"), 
    alpha=0.8, 
    text_kwargs={'fontsize': 8}
)
plt.title("Contribution by Segment", fontsize=10)
plt.axis('off')  # Hide axes for better visualization
plt.show()
```

[Out 26]:

![image](https://github.com/user-attachments/assets/3ab19206-d207-4783-8dfb-fd9c150295cc)

**2. Segmentation by Spending**

[In 27]:

```python

# Aggregate total spending for each segment
segment_by_spending = RFM_final[RFM_final.Monetary > 0][['Segment', 'Monetary']].groupby('Segment')['Monetary'].sum().reset_index().rename(columns={'Monetary': 'Spending'})

# Calculate the percentage contribution of each segment to total spending
segment_by_spending['percent_segment_by_spending'] = round(segment_by_spending['Spending'] / segment_by_spending['Spending'].sum() * 100)

# Convert percentage values to integers for better readability
segment_by_spending['percent_segment_by_spending'] = segment_by_spending['percent_segment_by_spending'].astype(int)

# Append percentage values to segment labels
segment_by_spending['Segment'] = segment_by_spending['Segment'] + ' ' + segment_by_spending['percent_segment_by_spending'].astype(str) + '%'

# Remove segments with 0% contribution
segment_by_spending = segment_by_spending[segment_by_spending.percent_segment_by_spending > 0]

# Plot a treemap to visualize spending distribution by segment
plt.figure(figsize=(12, 8))
squarify.plot(
    sizes=segment_by_spending['percent_segment_by_spending'], 
    label=segment_by_spending['Segment'], 
    color=sns.color_palette("Set2"), 
    alpha=0.8, 
    text_kwargs={'fontsize': 8}
)
plt.title("Segmentation by Spending", fontsize=10)
plt.axis('off')  # Hide axes for better visualization
plt.show()
```

[Out 27]:
![image](https://github.com/user-attachments/assets/7eddbdd6-271c-4ccf-9fe5-21f615ebee93)

**3. Segmentation by Frequency**

[In 28]:

```python

# Calculate the average frequency of purchases for each segment
segment_by_frequency = RFM_final[RFM_final.Frequency > 0][['Segment', 'Frequency']].groupby('Segment')['Frequency'].mean().reset_index()

# Plot a bar chart to visualize the average frequency per segment
plt.figure(figsize=(12, 8))
sns.barplot(data=segment_by_frequency, x='Frequency', y='Segment')
plt.xlabel('Average Purchase Frequency')
plt.ylabel('Segment')
plt.title('Segmentation by Frequency')
plt.show()
```
[Out 28:

![image](https://github.com/user-attachments/assets/45dd4769-edb2-40d4-9292-08ad1074becc)

**4. Segmentation by Recency**

[In 29]:

```python

# Calculate the average recency (days since last purchase) for each segment
segment_by_recency = RFM_final[RFM_final.Recency > 0][['Segment', 'Recency']].groupby('Segment')['Recency'].mean().reset_index()

# Plot a bar chart to visualize the average recency per segment
plt.figure(figsize=(12, 8))
sns.barplot(data=segment_by_recency, x='Recency', y='Segment')
plt.xlabel('Average Recency (Days)')
plt.ylabel('Segment')
plt.title('Segmentation by Recency')
plt.show()
```

[Out 29]:

![image](https://github.com/user-attachments/assets/98b9e2f0-aa9e-43a0-98b2-0486db1603dd)


### **📊 Observations **
From the four analysis charts on contribution, monetary, recency, and frequency for each segment, we can analyze the behavior of the 11 segments as follows:
| Segment              | R (Recency) | F (Frequency) | M (Monetary) | **Characteristics** |
|----------------------|------------|--------------|-------------|---------------------|
| **Champions (17%)**  | R **very low** (~10-20 days) | F **very high** (~200+ times) | M **highest** (~27% revenue) | The best customer group, **contributing significantly to revenue**. Should be **nurtured continuously**. |
| **Loyal (9%)**  | R **moderate** (~60 days) | F **high** (~180 times) | M **fairly high** (~13% revenue) | **Loyal customers** with a **stable purchasing frequency**. Should be **maintained and cared for**. |
| **Potential Loyalist (12%)**  | R **moderate** (~50 days) | F **moderate** (~100 times) | M **moderate** (~7% revenue) | **Potentially loyal customers** who need **more incentives to convert**. |
| **New Customers (8%)**  | R **moderate** (~40 days) | F **low** (~50 times) | M **low** (~3% revenue) | **Newly acquired customers** who need **retention strategies** to encourage repeat purchases. |
| **Promising (4%)**  | R **moderate** (~60-70 days) | F **moderate** (~50-80 times) | M **low** (~4% revenue) | Customers **showing signs of returning** but **not strongly engaged yet**. Needs **additional push**. |
| **Need Attention (6%)**  | R **high** (~120+ days) | F **moderate/low** (~50 times) | M **low** (~3-4% revenue) | Customers with **past engagement but declining activity**. **May be attracted by competitors**. |
| **At Risk (11%)**  | R **high** (~120 days) | F **moderate** (~100 times) | M **high** (~10-14% revenue) | **Previously high-value customers** who are **gradually disengaging**. **High risk of churn**. |
| **About to Sleep (4%)**  | R **high** (~100 days) | F **low** (~30 times) | M **low** (~3% revenue) | Customers **showing signs of leaving**. Requires **re-engagement strategies** before it's too late. |
| **Cannot Lose Them (3%)**  | R **very high** (~180+ days) | F **moderate** (~100 times) | M **moderate** (~4-5% revenue) | **Previously high-spending customers** who are **drifting away**. **Strong retention efforts needed**. |
| **Hibernating (18%)**  | R **very high** (~200 days) | F **very low** (~10-20 times) | M **very low** (~2% revenue) | Customers who **purchased before but have been inactive for a long time**. |
| **Lost Customers (9%)**  | R **extremely high** (220+ days) | F **extremely low** (~5-10 times) | M **very low** (~1-2% revenue) | **Nearly lost customers** with a **very low chance of returning** without **strong intervention**. |

### **📊 Key Findings**
Based on the above analysis, we can see that some segments share similar characteristics. Therefore, we can group them into segment clusters for easier analysis and to propose suitable strategies as follows:

---

**Group 1: High-Risk Customers (24%)**  

📌 **Includes:** Cannot Lose Them (3%), At Risk (11%), About to Sleep (4%), Need Attention (6%)  

💡 **Reason for grouping:**  
- These customers **previously had high or moderate purchase activity** but are now **showing a significant decline in engagement**.  
- They have a **long time since their last purchase (100 - 150 days)** and previously **contributed significantly to revenue**.  
- Without intervention, they **are likely to leave completely**.  

---

**Group 2: Loyal & High-Value Customers (38%)**  

📌 **Includes:** Champions (17%), Loyal (9%), Potential Loyalist (12%)  

💡 **Reason for grouping:**  
- These are customers with **high and stable purchase frequency**.  
- They **remain highly active**, with **a relatively short time since their last purchase (10 - 50 days)**.  
- Although their **revenue contribution varies**, they all **have long-term potential if nurtured properly**.  

---

**Group 3: New & Potential Customers (25%)**  

📌 **Includes:** New Customers (17%), Promising (8%)  

💡 **Reason for grouping:**  
- This group consists mostly of **new customers or those showing signs of growth**.  
- They have **recent interactions (30 - 50 days)** but **low purchase frequency and revenue contribution**.  
- They **have the potential to become loyal customers if they continue purchasing**.  

---

**Group 4: Inactive & Lost Customers (13%)**  

📌 **Includes:** Hibernating (9%), Lost Customers (4%)  

💡 **Reason for grouping:**  
- These customers are **almost entirely disengaged**, with **a very long time since their last purchase (200+ days)**.  
- **Their purchase frequency and revenue contribution are extremely low**, making them **unlikely to return without strong intervention**.  

**5. Distribution of RFM over Time**

```python
# Merge `RFM_final` & ecommerce_update
RFM_final_merge = RFM_final.merge(ecommerce_update, on='CustomerID', how='left')
```

**5.1 Money**

[In 30]:

```python
# Calculate average RFM grouped by month
RFM_by_month = RFM_final_merge.groupby('Month')['Monetary'].mean().reset_index()

# Plot line chart
plt.figure(figsize=(12,6))
sns.lineplot(data=RFM_by_month, x='Month', y='Monetary', label='Monetary', marker='o')
plt.title('Distribution of Monetary over Time')
plt.xlabel('Month')
plt.ylabel('Average Monetary Value')
plt.grid(True)
plt.show()
```
[Out 30]: 

![image](https://github.com/user-attachments/assets/31f9cf39-bc39-4ae6-9b91-f4e75fda2db3)

[In 31]:

```python
# Calculate average RFM grouped by month
RFM_by_month = RFM_final_merge.groupby('Month')[['Recency', 'Frequency']].mean().reset_index()

# Plot line chart
plt.figure(figsize=(12,6))
sns.lineplot(data=RFM_by_month, x='Month', y='Recency', label='Recency', marker='o')
sns.lineplot(data=RFM_by_month, x='Month', y='Frequency', label='Frequency', marker='o')
plt.title('Distribution of RFM over Time')
plt.xlabel('Month')
plt.ylabel('Average Value')
plt.legend()
plt.grid(True)
plt.show()
```

[Out 31]: 

![image](https://github.com/user-attachments/assets/cc76d31f-142b-4b1d-9e7b-463996cebdc7)

### 📊 Observations:

- **Recency:** This metric shows a **downward trend** over time, which is a **positive sign** since customers are purchasing **more frequently or more recently**.  

- **Frequency:** The purchase frequency appears to be **relatively stable**, but there are **slight fluctuations**. This suggests that customers are maintaining **a certain level of engagement** with the app.  

- **Monetary:** This metric exhibits **significant fluctuations**, with **sharp peaks and dips**. This indicates that the **monetary value spent by customers is not stable**, potentially due to **promotional campaigns, seasonal effects, or changes in purchasing behavior**.  

➡️ **Further analysis is needed** to determine **which segments** are driving these increases and decreases.


**6. Group Segment by Contribution**

[In 32]:
```python
# Classify into Group Segments
RFM_final['Group Segment'] = RFM_final['Segment'].apply(
    lambda x: 'High Risk Customers' if x in high_risk else
              'Loyal & High Value' if x in loyal_high_value else
              'New & Potential' if x in potential else
              'Inactive & Lost' if x in lost else 'Others'
)

# Count the number of customers in each Group Segment
group_counts = RFM_final['Group Segment'].value_counts()

# Calculate the percentage share of each group
group_percentages = (group_counts / len(RFM_final)) * 100

# Plot pie chart
plt.figure(figsize=(8, 8))
plt.pie(group_percentages, labels=group_percentages.index, autopct='%1.1f%%', startangle=140)
plt.axis('equal')
plt.title('Group Segment by Contribution')

plt.show()
```

[Out 32]:

![image](https://github.com/user-attachments/assets/0ce9df4f-60fa-4579-a84c-28972a6573e2)


**7. Segment Distribution Across Countries**
Since **UK contributes significantly to the total**, the overall chart mainly represents the UK market. To gain clearer insights into other countries, we need to exclude UK data.

[In 33]:
```python
# Calculate segment distribution by country
segmentation_by_location = RFM_final_merge.groupby(['Country', 'Group Segment'])['CustomerID'].nunique().unstack()

# Remove 'United Kingdom'
segment_without_UK = segmentation_by_location.drop(index=['United Kingdom'])

# Plot the data
segment_without_UK.plot(kind='barh', stacked=True, figsize=(20, 8))
plt.xlabel('Country')
plt.ylabel('Number of Customers')
plt.title('Distribution of Segment by Country Without UK')
plt.xticks(rotation=45, fontsize=8)
plt.legend(title='Segment')
plt.show()
```

[Out 33]:
![image](https://github.com/user-attachments/assets/efc0d66f-e3e6-4c4a-808b-43c4dce3dff1)

**8. Segmentation Distribution Over Time**

[In 34]:

```python
# Convert Month to correct data type
RFM_final_merge['Month'] = pd.to_datetime(RFM_final_merge['Month'], errors='coerce')

# Count customers in each Group Segment per month
monthly_trend = RFM_final_merge.groupby(['Month', 'Group Segment']).size().reset_index(name='Count')

# Plot the trend for each Group Segment over time
plt.figure(figsize=(12, 6))
for segment in monthly_trend['Group Segment'].unique():
    data = monthly_trend[monthly_trend['Group Segment'] == segment]
    plt.plot(data['Month'], data['Count'], marker='o', label=segment)

plt.xlabel('Month')
plt.ylabel('Number of Customers')
plt.title('Trend of Group Segment')
plt.xticks(rotation=45)
plt.legend(title='Group Segment')
plt.grid(True, linestyle='--', alpha=0.7)
```

[Out 34]:
![image](https://github.com/user-attachments/assets/c9067fb5-d8ff-4dee-9f22-9a4c18d6f887)

**9. Trend of Recency, Frequency, Monetary by Month**

[In 35]:
```python
# Calculate the average RFM values per Group Segment each month
rfm_trend = RFM_final_merge.groupby(['Month', 'Group Segment'])[['Recency', 'Frequency', 'Monetary']].mean().reset_index()

# Plot the trends
plt.figure(figsize=(12, 6))
for metric in ['Recency', 'Frequency', 'Monetary']:
    # Pivot data by Group Segment
    pivot_data = rfm_trend.pivot(index='Month', columns='Group Segment', values=metric)

    # Plot Area Chart
    pivot_data.plot(kind='area', stacked=True, alpha=0.7, figsize=(12, 6))
    plt.title(f'Trend of {metric} by Group Segment')
    plt.ylabel(metric)
    plt.xlabel('Month')
    plt.legend(title='Group Segment')
    plt.show()
```

[Out 35]:

![image](https://github.com/user-attachments/assets/ae538626-3639-40e8-b916-a6dcfccea2ee)

![image](https://github.com/user-attachments/assets/b2bfbe9b-8fe5-4665-9742-09da6211ac69)

![image](https://github.com/user-attachments/assets/2699a1ef-3b76-4a1c-9561-5493acbce2c9)


## **📌 3. Final Conclusion & Recommendations**

###  A. Customer Segmentation Strategy
👉🏻 Based on the insights and findings above, we would recommend the [stakeholder team] to consider the following:

**1. Loyal & High Value Group (38.3%)**  
- This group accounts for **38.3% of total customers** and contributes **the most to revenue**. They are strongly present in **key markets**.  
- Their purchasing behavior is **stable**, but **Recency is decreasing**, indicating a need for retention strategies.  
- **Total spending remains high**, showing their willingness to pay more, especially for **high-value products**.  

**🔹 Recommendation:**  
- **Analyze their preferred products** to develop **premium versions** or **expand the product lineup**.  
- **Test upselling, bundling strategies**, and **exclusive offers** to increase order value.  
- **Implement a long-term loyalty program** to retain this segment.  
- **Encourage reviews & referrals** to expand the loyal customer base.  

---

**2. High-Risk Customers (23.5%)**  
- This segment **used to have high spending but has significantly declined**.  
- Recency is **increasing**, meaning they are **purchasing less frequently**.  
- Revenue from this group is **gradually decreasing**, and without intervention, they may be lost entirely.  

**🔹 Recommendation:**  
- **Launch re-engagement campaigns** with **personalized incentives** to bring them back.  
- **Offer special vouchers or discounts** for their next purchase.  
- **Create targeted marketing content** (emails, push notifications) emphasizing product value.  
- **Reach out directly to VIP customers** to understand their reasons for disengagement and adjust strategies accordingly.  

---

**3. New & Potential Customers (11.7%)**  
- This group has **low spending but potential for growth**.  
- Purchase frequency is **still low**, requiring efforts to encourage repeat purchases.  
- Buying behavior is **increasing slightly but remains unstable**.  

**🔹 Recommendation:**  
- **Develop an onboarding strategy** to help customers explore and buy products easily.  
- **Run nurturing campaigns** to remind them of relevant products.  
- **Leverage reviews & feedback from Loyal customers** to build trust and influence purchasing decisions.  
- **Offer welcome incentives** to encourage their first or repeat purchases.  

---

**4. Inactive & Lost Customers (26.6%)**  
- This group makes up **26.6% of total customers**, but contributes **little to revenue**.  
- Recency is **very high**, meaning they haven’t purchased in a long time.  
- **Revenue from this segment continues to decline**, indicating they are likely to have left the brand.  

**🔹 Recommendation:**  
- **Send win-back emails with strong incentives** to encourage them to return.  
- **Run a "come back" campaign with personalized messaging**, reminding them why they bought before.  
- **Conduct exit surveys** to identify reasons for churn and improve the product or service.  
- **Accept that some of this group is lost** and focus resources on High-Risk or Loyal customers to optimize ROI.  

###  B. Business Recommendation

In SuperStore's retail model, where the RFM (Recency, Frequency, Monetary) model is used for customer segmentation and marketing strategies, the primary **focus should be on Frequency (F)**.

**Why Choose Frequency (F)?**  

**🔹 Increasing Purchase Frequency = Sustainable Revenue Growth**
- If customers **buy more frequently**, revenue will **remain stable and grow**.  
- Retaining existing customers is **cheaper than acquiring new ones** (reducing Customer Acquisition Cost - CAC).  

**🔹 Insights from the Charts: High-Risk Customers & New & Potential Segments Have Low Frequency**  
- **High-Risk Customers**:  
  - Used to be valuable customers but are **buying less frequently**.  
  - Without intervention, they might **transition to the Inactive & Lost segment**.  

- **New & Potential Customers**:  
  - Still in the early stages, **low purchase frequency** means they haven't formed a habit.  
  - If they are not encouraged to buy again, they may **lose interest and churn**.  

**🔹 Even Loyal & High-Value Customers Need Retention Strategies**  
- This group **currently maintains high purchase frequency**, but **if not nurtured**, their engagement may **gradually decline**.  
- Strategies like **loyalty programs, exclusive deals, and personalized offers** can help sustain their buying behavior.  

**🔹 Key Takeaway: Focus on Frequency for Long-Term Revenue Growth**  

✅ **Encouraging repeat purchases** strengthens customer loyalty and increases revenue.  
✅ **Preventing high-risk customers from churning** ensures a stable customer base.  
✅ **Developing purchase habits for new customers** helps convert them into long-term buyers.  

