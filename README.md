# E-commerce Sales Analysis

## 📌 Project Overview

This project analyzes an online retail transaction dataset to understand sales performance, customer and product contribution, geographic concentration, time trends, and data-quality issues.

The original business question was:

> **“Sales are growing, but are we actually becoming more profitable?”**

The analysis found that the available dataset does not contain product cost/COGS data. Therefore, true profit and profit margin cannot be calculated reliably. Instead, the project focuses on transaction-value analysis and identifies the additional data required for profitability analysis.

---

## 🎯 Business Questions

The analysis addresses:

* How much transaction value was generated?
* How many units and invoices were recorded?
* Which countries contribute most to transaction value?
* Which products contribute most?
* Which customers contribute most?
* How did transaction value change over time?
* Are there unusually large transactions?
* How concentrated is the business geographically and across customers?
* What data-quality issues could affect the analysis?
* What additional data is required to measure profitability?

---

## 📊 Dataset

**Dataset:** Online Retail transactional data

Original dataset size:

* 541,909 rows
* 8 original columns

Main fields:

* InvoiceNo
* StockCode
* Description
* Quantity
* InvoiceDate
* UnitPrice
* CustomerID
* Country

A calculated `LineValue` field was created:

```python
LineValue = Quantity * UnitPrice
```

---

## 🧹 Data Quality Investigation

Before performing business analysis, the dataset was investigated for:

* Missing CustomerID
* Missing Description
* Negative quantities
* Zero-price transactions
* Negative prices
* Duplicate records
* Postage transactions
* Accounting adjustments
* Manual/fee-related records
* Inconsistent StockCode/Description combinations

### Key findings

| Issue                |      Finding | Treatment                                              |
| -------------------- | -----------: | ------------------------------------------------------ |
| Missing CustomerID   | 135,080 rows | Retained and treated as a customer-analysis limitation |
| Missing Description  |   1,454 rows | Investigated/flagged                                   |
| Negative Quantity    |  10,624 rows | Classified primarily as returns/cancellations          |
| Zero UnitPrice       |   2,515 rows | Classified separately                                  |
| Negative UnitPrice   |       2 rows | Classified as accounting adjustments                   |
| Extra duplicate rows |        5,225 | Flagged; not automatically deleted                     |
| Postage records      |        1,256 | Classified separately                                  |
| Missing InvoiceNo    |            0 | No issue                                               |
| Missing StockCode    |            0 | No issue                                               |
| Missing InvoiceDate  |            0 | No issue                                               |
| Missing Country      |            0 | No issue                                               |

---

## 📈 Analytical Dataset

After transaction classification:

**Normal transaction records:** 528,978

Analytical transaction value:

**£10.59M**

Other key metrics:

| KPI                   |   Value |
| --------------------- | ------: |
| Transaction Value     | £10.59M |
| Units                 |   5.59M |
| Invoices              |  19,884 |
| Identified Customers  |   4,338 |
| Products/StockCodes   |   3,921 |
| Average Invoice Value | £532.52 |

Because duplicates were flagged rather than automatically deleted and the dataset contains special transaction types, the £10.59M figure is treated as **analytical transaction value rather than audited revenue**.

---

## 🌍 Geographic Analysis

The UK contributed approximately:

**£9.02M / 85.15%**

of analytical transaction value.

The top five countries together contributed approximately **93.3%**.

This indicates significant geographic concentration.

The analysis also identified markets where relatively high transaction value came from a small number of customers, creating opportunities for further customer-level investigation.

---

## 📦 Product Analysis

Product-level analysis was performed using:

* Transaction value
* Units
* Invoice count
* Customer count
* Revenue share

Operational/non-product records such as postage, manual transactions and fees were separated from ordinary product analysis where appropriate.

The analysis also identified unusually large transactions requiring validation.

---

## ⚠️ Anomaly Investigation

Two particularly large transactions stood out:

### Transaction 1

* StockCode: `23843`
* Quantity: 80,995
* Unit Price: £2.08
* Transaction Value: £168,469.60

### Transaction 2

* StockCode: `23166`
* Quantity: 74,215
* Unit Price: £1.04
* Transaction Value: £77,183.60

These records were not automatically removed.

They should be validated against the source/business system to determine whether they represent legitimate bulk transactions or data-quality issues.

---

## 👥 Customer Analysis

The top 10 identified customers contributed approximately:

**14.44%**

of transaction value.

The top 50 contributed:

**27.85%**.

However, customer-level analysis is limited because 135,080 transactions do not contain CustomerID.

---

## 📅 Time Analysis

Transaction value increased strongly during September–November 2011:

| Month     | Transaction Value |
| --------- | ----------------: |
| September |           £1.053M |
| October   |           £1.147M |
| November  |           £1.499M |

November was the highest complete month in the dataset.

December 2011 was not directly compared with full months because the dataset ends on **December 9, 2011**.

---

## 📊 Statistical Analysis

The project also investigates the relationship between:

* Unit price
* Quantity sold

Both Pearson and Spearman correlation are used, along with a sensitivity check for extreme values.

The purpose is to identify association rather than claim causation.

---

## 🗄️ SQL Analysis

The analysis is reproduced using SQL for:

* Overall KPIs
* Country performance
* Monthly trends
* Customer contribution
* Large transactions
* Missing CustomerID impact

---

## 📊 Power BI Dashboard

The planned executive dashboard contains:

* KPI cards
* Monthly transaction-value trend
* Country contribution
* Top products
* Customer contribution
* High-value transaction table
* Key business findings
* Data limitations

---

## 💡 Key Business Findings

1. The business is highly concentrated in the UK, which contributes 85.15% of analytical transaction value.
2. Transaction value increased substantially during September–November 2011.
3. Several unusually large transactions can materially influence aggregate metrics.
4. Customer analysis is constrained by missing CustomerIDs.
5. Operational records such as postage, fees and manual transactions should not be treated as ordinary product sales.
6. The dataset does not contain cost/COGS information, so profitability cannot be calculated reliably.

---

## 📌 Recommendations

* Validate unusually large transactions with the source system.
* Separate product sales from operational and adjustment records in reporting.
* Monitor geographic concentration.
* Improve customer identification.
* Add product cost/COGS data to enable genuine profit and margin analysis.

---

## 🛠️ Tools Used

* Python
* Pandas
* NumPy
* Matplotlib
* SciPy
* SQL
* Power BI

---

## 🎓 What This Project Demonstrates

This project focuses not only on technical data manipulation but also on the analytical process:

**Business Problem → Data Quality → Data Preparation → Exploration → Statistical Analysis → Business Insights → Recommendations → Dashboard**

It demonstrates the ability to question the data, identify limitations, investigate anomalies and translate analysis into business-focused conclusions.
