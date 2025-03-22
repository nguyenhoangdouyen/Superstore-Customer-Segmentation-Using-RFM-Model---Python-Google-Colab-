# **📊 Superstore Customer Segmentation Using RFM Model (Python - Colab)** #

![image](https://github.com/user-attachments/assets/b90b73a6-aaa6-44ad-9749-a798ebaf4632)

**Author:** Nguyễn Hoàng Đỗ Uyên

**Date:** March 2025

**Tools Used:** Python

## 📑 Table of Contents 

[📌 Background & Overview](#background-and-overview)  
[📂 Dataset Description & Data Structure](#dataset-description-and-data-structure)  
[🧹 Data Cleaning & Preprocessing](#data-cleaning-and-preprocessing)  
[🔍 Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)  
[🧮 Apply RFM Model](#apply-rfm-model)  
[📊 Visualization & Analysis](#visualization-and-analysis)  
[💡 Insight & Recommendation](#insight-and-recommendation)

## 📌 Background & Overview 

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

RFM (Recency, Frequency, Monetary) is a customer analysis technique based on purchasing behavior. In RFM analysis, each customer is assigned a score based on these three factors. The data is then used to categorize customers into segments, helping businesses identify key audiences for targeted marketing and sales strategies.  

- **Recency**: Measures the time elapsed since a customer's last purchase.  
- **Frequency**: Evaluates how often a customer makes transactions.  
- **Monetary**: Calculates the total amount spent by the customer.  
By applying RFM, businesses can segment customers based on their value, allowing them to optimize marketing and customer engagement strategies.  

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

<details>
  <summary>📂 **Dataset Schema** (Click to expand)</summary>

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

</details>

#### 📌 Sheet 2: Segmentation  
### 📊 Customer Segmentation & RFM Scores  

<details>
  <summary>📊 **RFM Segmentation Mapping** (Click to expand)</summary>

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
| **Lost Customers**       | 111, 112, 121, 131, 141, 151   |

</details>

## 🧹 Data Cleaning & Preprocessing

[In 1]:  
```python
# Print the first five rows of the dataset
ecommerce.head()
```
[Out 1]:  

![Image](https://github.com/user-attachments/assets/91b78596-07a3-4d9d-9fd1-a824b590a0e4)

[In 2]:  
```python
# Check the general information of df
ecommerce.info()
```
[Out 2]:  

![Image](https://github.com/user-attachments/assets/deae7032-863a-4694-9229-ac9e649efe18)

[In 3]:
```python
# Check Data Summary
ecommerce.describe()
```
[Out 3]:

![Image](https://github.com/user-attachments/assets/6731170f-672e-4c4b-8493-a9721f239813)

#### Summary:

⚡During the initial data exploration, it was observed that the **Quantity** and **Unit Price** columns contain negative values. This is not logically valid and requires further investigation. Possible actions include:
- Checking for data entry errors.
- Identifying whether negative values indicate refunds or cancellations.
- Removing or adjusting incorrect data points to ensure accuracy in analysis.

#### ⚡ Data Quality Insights

During the initial data exploration, a mismatch was identified between **Stock Code** count (4070) and **Description** count (4223). This inconsistency suggests potential data quality issues that require further investigation. Possible reasons include:

- Some products may have multiple descriptions under the same stock code.
- Certain descriptions might not be linked to any valid stock code.
- Data inconsistencies due to missing, duplicated, or improperly recorded stock codes.

It is recommended to conduct additional validation and data cleaning to ensure consistency and accuracy in analysis.

#### ⚠ Manual Review Required

Some orders contain incorrect **descriptions** → Perform a **manual check** and mark them as **errors** to facilitate further processing.

### 🔎 Data Validation & Error Identification  

- **Flagged Erroneous Orders**: Merged `description_check_update` with `ecommerce` to detect inconsistencies in product descriptions.  
- **Checked Negative Quantities & Cancellations**: Identified if negative **Quantity** values correspond to cancellations by verifying **InvoiceNo** starting with "C".  
-> Review flagged errors and cancellations to ensure data integrity before analysis.  

#### 🚨 Identifying Invalid Transactions

After flagging cancellations, verify if there are any transactions where **Quantity** is negative, but the **InvoiceNo** does not start with "C". These may indicate data inconsistencies.

### ✨ Conclusion:

**Data Types:**
The following columns have inappropriate data types and should be converted to **strings** for easier processing:
- **InvoiceNo**, **StockCode**, **Description**, **CustomerID**, **Country**.

**Data Values:**
- **Quantity < 0 & InvoiceNo starts with 'C'** → These transactions indicate **canceled orders** and should be **removed** from the dataset.
- **Quantity < 0 but InvoiceNo does NOT start with 'C'** → These records contain **incorrect descriptions** and should be **excluded** from the dataset.
- **UnitPrice < 0 & incorrect Description** → These are **invalid transactions** and should also be **removed** from the dataset.

## 🔍 Exploratory Data Analysis (EDA)

### 🛠 Step 1. Convert to correct Data type

[In 4]:
```python
# Convert selected columns to string type
column_list = ["InvoiceNo", "StockCode", "Description", "CustomerID", "Country"]
for c in column_list:
    ecommerce_update[c] = ecommerce_update[c].astype(str)

# Convert InvoiceDate to datetime format
ecommerce_update['InvoiceDate'] = pd.to_datetime(ecommerce_update['InvoiceDate'])
```

### 🛠 Step 2. Removing Invalid Transactions

To ensure data quality, the following steps were taken to remove invalid records:

[In 5]:

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

### 🛠 Step 3. 🛠 Checking Missing Values in CustomerID & Error Columns

[In 6]:

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

[Out 6]:
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

### 🛠 Step 4. Handle duplicate**

[In 7]: 

```python
# Identify duplicate rows based on 'InvoiceNo', 'StockCode', 'InvoiceDate', and 'CustomerID'
ecommerce_duplicate = ecommerce_update[ecommerce_update.duplicated(subset=['InvoiceNo', 'StockCode', 'InvoiceDate', 'CustomerID'])]
```

The result (10038, 12) means there are 10,038 duplicate rows, and they need to be detected and handled in **two cases**: 
1. **Case 1 - Duplicates with the Same Quantity**: 
   - These duplicates are likely caused by system errors (e.g., duplicate entries with the same quantity). 
   - **Action**: Drop the duplicates because they are identical.

2. **Case 2 - Duplicates with Different Quantities**:
   - These duplicates may occur due to system recording issues (e.g., a single order being split into multiple records with different quantities). 
   - **Action**: Sum the quantities of the duplicate entries to correct the data.

## 🧮 Apply RFM Model

#### 🛠 Step 1. Calculate RFM Score

[In 8]:

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

#### 🛠 Step 2. Check outlier

[In 9]:

```python
# Check outliers for the 'Recency' column
sns.boxplot(data=RFM_df, x='Recency')

# Check outliers for the 'Monetary' column
sns.boxplot(data=RFM_df, x='Monetary')

# Check outliers for the 'Frequency' column
sns.boxplot(data=RFM_df, x='Frequency')
```
[Out 9]:

![Image](https://github.com/user-attachments/assets/dd08a423-d0da-43a5-bbfe-24ddf6c85bcf)

**📌 Solution**
We set a 95% threshold for **Recency**, **Frequency**, and **Monetary** to remove extreme values (outliers) from the dataset. This ensures that the analysis focuses on the majority of the data, improving its reliability for further insights.

#### 🛠 Step 3. Assign RFM scores using Qcut

[In 10]:

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

#### 🛠 Step 4. Calculate RFM Score

Process the segmentation table & merge with RFM_df

[In 11]:

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
[Out 11]:

![Image](https://github.com/user-attachments/assets/e597bac7-f7f6-4cce-baf6-2108d3d2b177)


## 📊 Visualization & Analysis

### **1. Contribution by Segmentation

![image](https://github.com/user-attachments/assets/3ab19206-d207-4783-8dfb-fd9c150295cc)

### 2. Segmentation by Spending 

![image](https://github.com/user-attachments/assets/7eddbdd6-271c-4ccf-9fe5-21f615ebee93)

### 3. Segmentation by Frequency

![image](https://github.com/user-attachments/assets/45dd4769-edb2-40d4-9292-08ad1074becc)

### 4. Segmentation by Recency

![image](https://github.com/user-attachments/assets/98b9e2f0-aa9e-43a0-98b2-0486db1603dd)

--- 

### 📊 Observations 

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

---

## 💡 Insight & Recommendation

Based on the above analysis, we can see that some segments share similar characteristics. Therefore, we can group them into segment clusters for easier analysis and to propose suitable strategies as follows:

### Group 1: High-Risk Customers (24%)

📌 **Includes:** Cannot Lose Them (3%), At Risk (11%), About to Sleep (4%), Need Attention (6%)  

💡 **Reason for grouping:**  
- These customers **previously had high or moderate purchase activity** but are now **showing a significant decline in engagement**.  
- They have a **long time since their last purchase (100 - 150 days)** and previously **contributed significantly to revenue**.  
- Without intervention, they **are likely to leave completely**.  


### Group 2: Loyal & High-Value Customers (38%)

📌 **Includes:** Champions (17%), Loyal (9%), Potential Loyalist (12%)  

💡 **Reason for grouping:**  
- These are customers with **high and stable purchase frequency**.  
- They **remain highly active**, with **a relatively short time since their last purchase (10 - 50 days)**.  
- Although their **revenue contribution varies**, they all **have long-term potential if nurtured properly**.  

### Group 3: New & Potential Customers (25%)

📌 **Includes:** New Customers (17%), Promising (8%)  

💡 **Reason for grouping:**  
- This group consists mostly of **new customers or those showing signs of growth**.  
- They have **recent interactions (30 - 50 days)** but **low purchase frequency and revenue contribution**.  
- They **have the potential to become loyal customers if they continue purchasing**.  

### Group 4: Inactive & Lost Customers (13%) 

📌 **Includes:** Hibernating (9%), Lost Customers (4%)  

💡 **Reason for grouping:**  
- These customers are **almost entirely disengaged**, with **a very long time since their last purchase (200+ days)**.  
- **Their purchase frequency and revenue contribution are extremely low**, making them **unlikely to return without strong intervention**.  

### 5. Distribution of RFM over Time

![image](https://github.com/user-attachments/assets/31f9cf39-bc39-4ae6-9b91-f4e75fda2db3)

![image](https://github.com/user-attachments/assets/cc76d31f-142b-4b1d-9e7b-463996cebdc7)

---

### 📊 Observations:

- **Recency:** This metric shows a **downward trend** over time, which is a **positive sign** since customers are purchasing **more frequently or more recently**.  

- **Frequency:** The purchase frequency appears to be **relatively stable**, but there are **slight fluctuations**. This suggests that customers are maintaining **a certain level of engagement** with the app.  

- **Monetary:** This metric exhibits **significant fluctuations**, with **sharp peaks and dips**. This indicates that the **monetary value spent by customers is not stable**, potentially due to **promotional campaigns, seasonal effects, or changes in purchasing behavior**.  

➡️ **Further analysis is needed** to determine **which segments** are driving these increases and decreases.

### 6. Group Segment by Contribution

![image](https://github.com/user-attachments/assets/0ce9df4f-60fa-4579-a84c-28972a6573e2)

### 7. Segment Distribution Across Countries

![image](https://github.com/user-attachments/assets/efc0d66f-e3e6-4c4a-808b-43c4dce3dff1)

### 8. Segmentation Distribution Over Time

![image](https://github.com/user-attachments/assets/c9067fb5-d8ff-4dee-9f22-9a4c18d6f887)

### 9. Trend of Recency, Frequency, Monetary by Month

![image](https://github.com/user-attachments/assets/ae538626-3639-40e8-b916-a6dcfccea2ee)

![image](https://github.com/user-attachments/assets/b2bfbe9b-8fe5-4665-9742-09da6211ac69)

![image](https://github.com/user-attachments/assets/2699a1ef-3b76-4a1c-9561-5493acbce2c9)


## **📌 3. Final Conclusion & Recommendations**

###  A. Customer Segmentation Strategy
👉🏻 Based on the insights above, we recommend the following:

**1. Loyal & High Value Group (38.3%)**  
- **38.3%** of customers, **highest revenue contribution**.  
- Stable purchases but decreasing **Recency**.  
- High willingness to pay for **premium products**.

**🔹 Recommendation:**  
- Analyze preferred products, create **premium versions**.  
- Test **upselling, bundling**, and **exclusive offers**.  
- Implement **loyalty programs**, and encourage **reviews & referrals**.

---

**2. High-Risk Customers (23.5%)**  
- Previously high spending but now declining.  
- **Increasing Recency**, purchasing less frequently.  
- Gradual revenue decrease.

**🔹 Recommendation:**  
- Launch **re-engagement campaigns** with **personalized incentives**.  
- Offer **special discounts** and targeted **marketing content**.  
- Reach out to **VIP customers** to understand disengagement.

---

**3. New & Potential Customers (11.7%)**  
- Low spending, but growth potential.  
- **Increasing** purchase frequency, but still unstable.

**🔹 Recommendation:**  
- Develop **onboarding strategies** to encourage repeat purchases.  
- Run **nurturing campaigns** and offer **welcome incentives**.  
- Leverage **reviews** to build trust and influence purchases.

###  B. Business Recommendation

In SuperStore's retail model, where the RFM (Recency, Frequency, Monetary) model is used for customer segmentation and marketing strategies, the primary **focus should be on Frequency (F)**.

**B. Business Recommendation**

In SuperStore's retail model, the **RFM (Recency, Frequency, Monetary)** model is key for segmentation and marketing strategies, with a primary focus on **Frequency (F)**.

**Why Focus on Frequency (F)?**

🔹 **Increasing Purchase Frequency = Sustainable Revenue Growth**  
- More frequent purchases lead to **stable and growing revenue**.  
- **Retaining customers** is cheaper than acquiring new ones, reducing **Customer Acquisition Cost (CAC)**.

🔹 **Insights from the Charts: High-Risk & New Customers Have Low Frequency**  
- **High-Risk Customers**: Once valuable, but now buying less often. Without action, they may move to the **Inactive** segment.  
- **New & Potential Customers**: Low frequency indicates no buying habit yet. Without encouragement, they may churn.

🔹 **Even Loyal Customers Need Retention**  
- Loyal customers may have high frequency but could decrease without **nurturing**.  
- Use **loyalty programs**, **exclusive deals**, and **personalized offers** to sustain engagement.


