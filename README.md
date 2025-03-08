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
👉🏻 *(Insert a screenshot of the table schema here)*  
- Key columns: `InvoiceNo`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `UnitPrice`, `CustomerID`, `Country`.  

#### 📌 Sheet 2: Segmentation  
👉🏻 *(Insert a screenshot of the table schema here)*  
- Key columns: `Segment`, `RFM Score`.  
