# 🛒 Customer Segmentation Using RFM Analysis

A data analysis project that segments e-commerce customers based on their transaction behavior using **Recency, Frequency, and Monetary (RFM)** analysis — helping businesses identify their most valuable customers and design targeted marketing strategies.

---

## 📌 Project Overview

Every business has different types of customers — some who shop every week, some who spent a lot once and never returned, and some who are slowly drifting away. This project uses RFM Analysis to automatically classify customers into meaningful segments based purely on their purchase history.

| Metric | Question It Answers |
|---|---|
| **Recency** | How recently did this customer make a purchase? |
| **Frequency** | How often do they buy? |
| **Monetary** | How much have they spent in total? |

Each customer receives a score from 1–4 on each dimension, which are then combined into an **RFM Score** (e.g., `444` = Champion customer, `111` = Lost customer).

---

## 📂 Dataset

- **Source File:** `ecommerce_data.csv` (Brazilian E-Commerce Public Dataset by Olist)
- **Original Size:** 541,909 rows
- **After Cleaning:** 406,829 rows
- **Unique Customers:** 4,372
- **Date Range:** January 2010 – December 2011

### Columns Used

| Column | Description |
|---|---|
| `InvoiceNo` | Unique transaction identifier |
| `InvoiceDate` | Date of purchase |
| `CustomerID` | Unique customer identifier |
| `Quantity` | Number of units purchased |
| `UnitPrice` | Price per unit |
| `TotalPrice` | Quantity × UnitPrice (engineered feature) |

---

## 🔧 Project Steps

### Step 1 — Data Cleaning
- Removed rows with missing `CustomerID` values (135,080 rows removed)
- Removed records with non-positive `Quantity` or `UnitPrice`
- Created a `TotalPrice` column = `Quantity × UnitPrice`
- Converted `InvoiceDate` to proper datetime format

### Step 2 — RFM Feature Calculation
- **Reference/Snapshot Date** set to one day after the last transaction date (`2011-12-11`)
- **Recency** = Snapshot Date − Customer's most recent purchase date (in days)
- **Frequency** = Count of unique `InvoiceNo` values per customer
- **Monetary** = Sum of all `TotalPrice` values per customer
- Results aggregated into a new RFM table with one row per customer (4,372 rows)

### Step 3 — RFM Scoring
- Used **quantile-based bucketing (quartiles)** to assign scores of 1–4 on each dimension
- Recency scored in **reverse** (lower days = more recent = higher score)
- Frequency and Monetary scored normally (higher = better)
- Combined into a single `RFM_Score` string (e.g., `"444"`)

### Step 4 — Customer Segmentation & Export
- Mapped RFM scores to business-friendly segment labels
- Exported final dataset as `customer_segments_rfm.csv`

---

## 🏷️ Customer Segments

| RFM Score | Segment | Description |
|---|---|---|
| 444 | **Champions** | Bought recently, buy often, spend the most |
| 334–443 | **Loyal Customers** | Regular, high-value buyers |
| 411–432 | **Potential Loyalists** | Recent with growing frequency |
| 411 | **New Customers** | Bought very recently but only once |
| 311–322 | **Promising** | Recent shoppers, not yet frequent |
| 222–233 | **At Risk** | Used to buy well but haven't recently |
| 111–212 | **Lost / Churned** | Haven't purchased in a long time |

---

## 📁 File Structure

```
📦 rfm-customer-segmentation
 ┣ 📄 ecommerce_data.csv                      # Original raw dataset
 ┣ 📄 cleaned_e_commerce_customer_dataset.xlsx # Cleaned dataset (Step 1 output)
 ┣ 📄 customer_segments_rfm.csv               # Final segmented output
 ┣ 📄 rfm_analysis.ipynb                      # Jupyter Notebook with full analysis
 ┗ 📄 README.md                               # Project documentation
```

---

## 🛠️ Tools & Libraries

- **Python 3**
- **Pandas** — data manipulation and aggregation
- **NumPy** — numerical operations
- **Jupyter Notebook** — interactive analysis environment

---

## 📊 Key Results

- Analysed **4,372 unique customers** across **22,190 unique transactions**
- Customers segmented into **7 distinct groups** for targeted marketing
- Champions (score 444) identified as highest priority for retention campaigns
- Lost/Churned customers identified for win-back campaigns

---

## 🚀 How To Run

1. Clone this repository
   ```bash
   git clone https://github.com/AKABharat/E-Commerce-Customer-Segmentation-using-RFM-Analysis.git
   ```

2. Install required libraries
   ```bash
   pip install pandas numpy openpyxl jupyter
   ```

3. Open the notebook
   ```bash
   jupyter notebook rfm_analysis.ipynb
   ```

4. Run all cells in order — the final `customer_segments_rfm.csv` will be generated automatically

---

## 💡 Business Use Cases

- **Champions** → Reward them, ask for reviews, make them brand ambassadors
- **At Risk** → Send personalised win-back offers before they churn completely
- **New Customers** → Onboard them well, encourage second purchase
- **Lost Customers** → Run reactivation campaigns with strong discounts

---

## 👤 Author

**AKABharat**
- GitHub: [@AKABharat](https://github.com/AKABharat)

---

## 📜 License

This project is open source and available under the [MIT License](LICENSE).
