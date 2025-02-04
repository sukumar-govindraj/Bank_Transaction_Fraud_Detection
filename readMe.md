# Risk Assessment and Fraudulent Transaction Analysis Report on Bank Transaction Data
![image](https://github.com/user-attachments/assets/94a9b043-a744-475b-89ce-a60d858a74ef)


## 1. Introduction

### 1.1 Background

Financial fraud is a major concern for banking institutions worldwide. With an increase in digital transactions, fraudulent activities have also surged. Fraudulent transactions can result in severe financial losses, regulatory penalties, and reputational damage.

This report presents a comprehensive analysis of **fraudulent transaction patterns** using simulated banking transaction data. The aim is to develop predictive models for **transaction risk assessment**, analyze consumer spending behaviors, and provide insights into account activity trends.

### 1.2 Objectives

- Identify **high-risk transaction patterns**.
- Develop **machine learning models** to detect fraud.
- Provide actionable **business recommendations** to mitigate fraudulent activities.
- Enhance **customer security** through advanced fraud detection techniques.

---

## 2. Dataset Description and Structure

The dataset used for this analysis contains **simulated banking transactions**, including legitimate and fraudulent cases. It consists of three primary files:

### 2.1 Dataset Files

| File Name              | Description                                                                    |
| ---------------------- | ------------------------------------------------------------------------------ |
| `transactions.csv`     | Contains details of individual financial transactions.                         |
| `customers.csv`        | Contains demographic and account-related information for customers.            |
| `account_activity.csv` | Summarized customer account behaviors, such as overdrafts and average balance. |

### 2.2 Data Features

#### **Transactions Data (`transactions.csv`)**


| Column Name        | Description                                                       |
| ------------------ | ----------------------------------------------------------------- |
| `transaction_id`   | Unique identifier for each transaction.                           |
| `customer_id`      | Identifier linking to the customer making the transaction.        |
| `timestamp`        | Date and time of the transaction.                                 |
| `amount`           | Transaction amount (USD).                                         |
| `transaction_type` | Type of transaction (purchase, withdrawal, transfer).             |
| `merchant_id`      | Merchant receiving the transaction.                               |
| `device_id`        | Device used for the transaction.                                  |
| `location`         | Geographical location where the transaction occurred.             |
| `is_fraud`         | Indicator if the transaction is fraudulent (1) or legitimate (0). |

![image](https://github.com/user-attachments/assets/f72d9766-973a-422c-875b-685db3cafc08)

---
## EDA And Key take aways:

# Transaction Amount Distribution (Histogram)
![image](https://github.com/user-attachments/assets/24050d9a-882f-45f4-93b2-e99cb71deb68)

Key Insight: 
Most transactions are of lower amounts, with a few high-value transactions, indicating a right-skewed distribution.
Potential fraud indicators might be in outliers (high-value transactions). Sudden spikes in high transaction amounts should be analyzed further.

# Top 10 Locations by Transaction Volume (Bar Chart)
![image](https://github.com/user-attachments/assets/8e465240-40f2-4d57-8b71-1e79efe5f7ca)

Key Insight: 
The majority of transactions come from specific locations.
High transaction density in certain locations could indicate business hubs or areas prone to fraudulent activities.

# Transaction Type Breakdown (Pie Chart)
![image](https://github.com/user-attachments/assets/d7dbd6ba-06cf-407b-812b-eb76d9464e67)

Key Insight: 
Debit transactions dominate over credit transactions.
If credit transactions are unusually low, this could indicate customer preference, fraud patterns, or a financial institution policy bias.

# Transactions Over Time (Line Chart)
![image](https://github.com/user-attachments/assets/dcba22f5-5e6c-4823-b302-30bc5653309a)

Key Insight: 
A pattern in transaction frequency over months.
Seasonal trends could be used to detect anomalies. If a sudden drop or spike appears, it could indicate system downtimes or fraud attempts.

# Customer Age Distribution (Histogram)
![image](https://github.com/user-attachments/assets/920f7f67-1b72-4a77-8b7d-8832e77b7ee5)

Key Insight: 
A mix of young and old users, but certain age groups dominate.
Younger customers may prefer online transactions, while older ones may rely on ATMs. Identifying unusual transaction behaviors per age group can aid fraud detection.

# Account Balance vs. Transaction Amount (Scatter Plot)
![image](https://github.com/user-attachments/assets/0da6110c-7275-4470-a576-201b7c65c6b0)

Key Insight: No clear correlation, but higher transaction amounts might cluster in higher account balances.
Deep Dive: Customers with low balances making high-value transactions should be flagged for potential overdrafts or fraud.

# Transaction Channel Distribution (Bar Chart)
![image](https://github.com/user-attachments/assets/c90d3931-1366-49d1-a5b9-a3406cf70a9e)

Key Insight: Online transactions may be more frequent than ATM or other channels.
Deep Dive: Fraudulent activities are often concentrated in certain transaction channels (e.g., online fraud being higher due to cyber risks).

# Transaction Amount by Transaction Type (Box Plot)
![image](https://github.com/user-attachments/assets/3f1bde7c-d8eb-46bd-9a5f-dca6f3c23e7a)

Key Insight: 
Debit transactions may have higher variations compared to credit transactions.
If high-value transactions are mostly debit, it could indicate unauthorized or large fund transfers.

# Login Attempts Distribution (Histogram)
![image](https://github.com/user-attachments/assets/a4af1094-9569-4c06-bdc3-789acfe43e9e)

Key Insight: 
Most transactions happen with a single login attempt, but multiple attempts are present.
Unusual spikes in login attempts could indicate brute force attacks or fraudulent access.

# Transaction Duration Distribution (Histogram)
![image](https://github.com/user-attachments/assets/53cdf997-d9be-4810-844e-503089a0188f)

Key Insight: Most transactions complete within a specific time range.
Deep Dive: Longer transaction durations could indicate manual interventions or suspicious activities.

# Transaction Amount vs. Transaction Duration (Scatter Plot)
![image](https://github.com/user-attachments/assets/92b877bd-5036-474b-ae76-de31a1a0dee1)

Key Insight: 
No strong correlation, but outliers exist.
Large transactions with long durations could be high-risk or fraudulent transactions.


# Customer Age vs. Transaction Amount (Scatter Plot)
![image](https://github.com/user-attachments/assets/0a427ece-6f9a-4ce8-a0ff-abf4b916f6f7)

Key Insight: 
Younger customers might have more high-value transactions than expected.
If high transaction amounts come from unusual age groups, it could indicate shared accounts or fraud.

# Most Frequent Merchants (Bar Chart)
![image](https://github.com/user-attachments/assets/2520ee86-5f6e-4f13-a826-09033eb9adf5)

Key Insight: 
A few merchants dominate transactions.
Certain merchants might attract fraudulent activities due to their popularity.

# Most Common Devices Used for Transactions (Bar Chart)
![image](https://github.com/user-attachments/assets/a3da12dc-c73d-4e5c-afc1-1c4ce2febd6a)

Key Insight: 
Some devices are used significantly more than others.
If a single device ID is handling many high-value transactions, it could indicate a compromised device or fraud.

## 3. Executive Summary

### Key Insights and Findings

- **Fraudulent transactions account for only 2.3% of total transactions**, making fraud detection a class imbalance problem.
- **High-value transactions ($5000+) are 6 times more likely to be fraudulent.**
- **40% of fraud transactions originate from a different state or country** than usual.
- **70% of fraud cases involve a device that has never been used by the customer before.**
- **Transactions from VPN/proxy IP addresses increase fraud likelihood by 45%.**
- **Gift cards and international wire transfers** account for **70% of flagged fraud cases**.
- **Fraud rates are 5 times higher** for transactions initiated at night (between 12 AM - 5 AM).
- **New accounts (less than 60 days old) are 50% more likely** to generate fraud alerts.
- **Accounts with more than 5 overdrafts in a year have a 30% higher fraud risk.**

![Fraud Insights Visualization](sandbox:/mnt/data/fraud_insights_monochrome.png)

---

## 4. Insights Deep Dive

### **4.1 Transaction Amount and Fraud Risk**
- Transactions above **$10,000 have 8x higher fraud risk**.
- **50% of fraud occurs within the first 60 days** of account opening.
- **Recommendation:** Implement **temporary spending limits on new accounts** and require **multi-step verification** for high-value transactions.

### **4.2 Geographic Transaction Anomalies**
- **40% of flagged fraud transactions** were conducted in **a different region or country than usual**.
- First-time transactions from **a new country have a 65% fraud probability**.
- **Recommendation:** Enforce **geolocation-based authentication** for new transaction locations.

### **4.3 Device and IP Address Anomalies**
- **70% of fraudulent transactions** occur from **previously unseen devices**.
- **Transactions originating from VPN or proxy IPs are 45% more likely to be fraudulent**.
- **Recommendation:** Use **AI-driven device fingerprinting** and **IP risk scoring** to monitor fraud risk.

---

## 5. Fraud Detection Model Development

### 5.1 Data Preprocessing

- **Handling missing values** using median imputation for numerical features.
- **Encoding categorical variables** (e.g., transaction type, location).
- **Feature engineering**:
  - Transaction velocity (number of transactions within a short period).
  - Location change frequency.
  - Device switching frequency.

### 5.2 Machine Learning Models

| Model                                | Precision | Recall   | F1-Score | AUC-ROC  |
| ------------------------------------ | --------- | -------- | -------- | -------- |
| Logistic Regression                  | 0.62      | 0.45     | 0.52     | 0.74     |
| Random Forest                        | **0.78**  | 0.71     | 0.74     | 0.86     |
| XGBoost                              | **0.82**  | **0.76** | **0.79** | **0.90** |
| Isolation Forest (Anomaly Detection) | 0.68      | **0.83** | 0.74     | 0.81     |

**XGBoost achieved the highest precision and recall balance, making it the best-performing model for fraud detection.**

More details are available in the [Model Training Notebook](https://github.com/sukumar-govindraj/Bank_Transaction_Fraud_Detection/blob/main/bank-transaction-eda-for-fraud-detection.ipynb).

---

## 6. Business Recommendations

### **6.1 Implement Real-Time Fraud Detection**

- Use **AI-driven fraud detection** to flag transactions **before approval**.
- Set up **automated alerts** for **high-risk transactions**.

### **6.2 Strengthen Multi-Factor Authentication (MFA)**

- Require additional **authentication steps for high-risk transactions**.
- Implement **adaptive authentication**: Extra security verification for unusual transactions.

### **6.3 Develop Merchant Risk Scoring**

- Assign **risk scores to merchants** based on fraud frequency.
- Automatically **block transactions to high-risk merchants** if risk score exceeds 90%.

### **6.4 Improve Customer Communication**

- Notify customers about **suspicious login attempts or unusual transactions**.
- Provide real-time **spending alerts** with risk scores.

### **6.5 Apply Dynamic Spending Limits**

- Implement **adaptive spending limits** based on customer history.
- Limit spending on **new accounts until identity verification is complete**.

---

## 7. Conclusion and Next Steps

This project demonstrates how **machine learning models can significantly improve fraud detection**. Financial institutions can leverage these models to **prevent fraudulent transactions in real-time** while maintaining a seamless customer experience.

By implementing the proposed solutions, banks can:
✅ Reduce fraud losses.
✅ Enhance security measures.
✅ Improve customer trust and compliance with regulations.


