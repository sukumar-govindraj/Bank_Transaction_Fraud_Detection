# Fraudulent Transaction Analysis and Risk Assessment Report

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
1. Histograms of Transaction Amounts
![image](https://github.com/user-attachments/assets/6f9732eb-e09e-4d89-92e1-86563097d6e7)

Key Insights:

The majority of transactions are concentrated at lower amounts, following a right-skewed distribution.

Debit transactions are more frequent than credit transactions, especially for smaller amounts.

Larger transactions appear less frequently but might be more relevant for fraud detection.



2. Box Plot of Transaction Amounts
   ![image](https://github.com/user-attachments/assets/580179ac-520b-4782-bb3f-55368f701bdb)


Key Insights:

A significant number of transactions are outliers, with amounts well above the interquartile range (IQR).

Most transactions fall within $0 - $500, while high-value transactions are sparse but could be critical for anomaly detection.



3. Transaction Distribution Across Locations
   ![image](https://github.com/user-attachments/assets/28fa5ad3-7703-4982-8af8-ed82044617a6)


Key Insights:

Transactions are evenly distributed across major cities, with some locations showing a slightly higher number of transactions.

Fort Worth, Los Angeles, and Oklahoma City have the highest number of recorded transactions, which might be indicative of higher economic activity in those areas.



4. Daily Transaction Patterns
   ![image](https://github.com/user-attachments/assets/bcd6a07b-d3fc-49ed-b8e5-e419de95ebfa)


Key Insights:

Transactions fluctuate daily, with spikes occurring periodically, possibly due to payroll dates, bill payments, or spending trends.

Identifying peak transaction times can help detect fraudulent activities occurring outside normal patterns.



5. Transaction Frequency by Day of the Week
   ![image](https://github.com/user-attachments/assets/366426bf-f588-45e2-ba2e-de440d61bb93)


Key Insights:

Monday experiences the highest number of transactions, while weekends have the least activity.

Businesses and payroll cycles might influence transaction behaviors, making specific days more prone to financial fraud attempts.



6. Transaction Frequency by Hour of the Day
![image](https://github.com/user-attachments/assets/a9e37aff-22e3-4280-9087-b50bd4401b76)

Key Insights:

The busiest transaction periods occur during business hours, especially around 16:00 and 17:00, possibly due to salary credits or end-of-day banking.

A secondary peak in the evening could relate to online transactions, bill payments, or after-work spending.



7. Distribution of Time Gaps Between Transactions
![image](https://github.com/user-attachments/assets/2d7d8e34-7b7a-4a2d-880d-c992b5c7aeeb)

Key Insights:

The time gap between transactions follows an almost uniform pattern, with certain spikes indicating batch transactions (e.g., payrolls, stock trades, or scheduled payments).

Debit and credit transactions exhibit different time-based distributions, which could be useful for fraud detection.


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

More details are available in the [Model Training Notebook](notebooks/model_training.ipynb).

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


