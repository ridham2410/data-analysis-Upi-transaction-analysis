# UPI-Transactions-Dashboard

### Dashboard Link : https://app.powerbi.com/groups/me/reports/3b1b637f-5d11-42de-9868-f2f4aa3d4861/e88f8848046b8a6da7ab?experience=power-bi

## Problem Statement

This dashboard helps to understand UPI (Unified Payments Interface) transactions in one place. It shows how much money was transacted each quarter and month, how the remaining account balance moves over time, and lets the user slice the data by sending bank, receiving bank, device, city, gender, age group, merchant, payment method, purpose and transaction type.

Using the slicers, a bank or payment company can see which cities, merchants, devices and customer groups drive transaction volume, and can look at them month by month in a matrix.

Since 20 % of all transactions (4,000 out of 20,000) have the status "Failed", worth about 4.00 million of the 19.87 million transacted, the failure rate is something that should be investigated and reduced.

### Steps followed

- Step 1 : Load data into Power BI Desktop. The data is in a single table named `UPI transactions` (20,000 rows, 20 columns, one row per transaction).
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that none of the columns has errors or empty values, and all 20,000 transaction IDs are unique.
- Step 5 : Date hierarchy (Year, Quarter, Month, Day) was used on the `TransactionDate` column.
- Step 6 : A calculated column was created in which customers were grouped into three age groups.

  For creating the new column following DAX expression was written;

        Age Groups =
        IF('UPI transactions'[CustomerAge] <= 25, "A1",
            IF('UPI transactions'[CustomerAge] <= 35, "A2", "A3"))

  A1 = age 25 or below, A2 = age 26 to 35, A3 = age 36 and above.

- Step 7 : A theme was selected from the View tab in the report view.
- Step 8 : **Page 1** was built with ten slicers on the left & four charts.

  Slicers were added for the fields,

  (a) Bank Name Sent

  (b) Bank Name Received

  (c) Device Type

  (d) City

  (e) Gender

  (f) Age Groups

  (g) Merchant Name

  (h) Payment Method

  (i) Purpose

  (j) Transaction Type

  Charts (each one uses quarter and month of `TransactionDate`, in a drill down hierarchy, on the axis),

  (a) Line chart : Sum of Amount

  (b) Column chart : Sum of Amount

  (c) Column chart : Sum of Remaining Balance

  (d) Line chart : Sum of Remaining Balance

  A bookmark navigator was also added so that the user can switch between saved views of the report.

- Step 9 : **Page 2** was built with the same ten slicers and a matrix visual. The matrix shows Sum of Amount and Sum of Remaining Balance, with the month in rows and city and currency in columns.
- Step 10 : The report was then published to Power BI Service.

# Snapshot of Dashboard (Power BI Service)

<img width="1917" height="1016" alt="Image" src="https://github.com/user-attachments/assets/0755427f-d277-45a4-aede-830bc60e7ed0" />

# Report Snapshot (Power BI DESKTOP)

<img width="1917" height="1015" alt="Image" src="https://github.com/user-attachments/assets/bae7c68b-4b4b-41ee-a594-2b96669d89cc" />

<img width="1917" height="1015" alt="Image" src="https://github.com/user-attachments/assets/7db8c54b-2fb4-4f43-86a6-0ec8e9f22c64" />

# Insights

A two page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard. All figures are calculated from the 20,000 transactions in the data model (01 Jan 2024 to 30 Dec 2024).

### [1] Overall

   Total number of transactions = 20,000

   Total transaction amount = 19,872,274.03

   Average transaction amount = 993.61 (smallest 0.05, largest 1,999.87)

   Average remaining balance = 5,020.54 (smallest 0.53, largest 9,999.47)

### [2] Transaction Status

   Successful transactions = 16,000 (80 %), amount = 15,875,486.95

   Failed transactions = 4,000 (20 %), amount = 3,996,787.08

           thus, 1 in every 5 transactions fails, and every city has the same failure rate (1,000 failed and 4,000 successful transactions in each).

### [3] Amount by Quarter

   | Quarter | Transactions | Amount |
   |---|---|---|
   | Q1 2024 | 5,000 | 4,995,165.77 |
   | Q2 2024 | 5,001 | 5,022,281.17 |
   | Q3 2024 | 5,001 | 4,875,586.14 |
   | Q4 2024 | 4,998 | 4,979,240.95 |

           thus, Q2 has the highest amount & Q3 has the lowest, but the difference between the quarters is less than 3 %.

   Month with the highest amount = May (1,706,785.86)

   Month with the lowest amount = August (1,598,708.63)

   Each month has about 1,666 transactions, so changes in the monthly amount come from the transaction amount & not from the number of transactions.

### [4] City

   | City | Transactions | Amount |
   |---|---|---|
   | Mumbai | 5,000 | 5,052,564.92 |
   | Delhi | 5,000 | 5,036,738.71 |
   | Hyderabad | 5,000 | 4,907,634.17 |
   | Bangalore | 5,000 | 4,875,336.23 |

           thus, Mumbai has the highest amount & Bangalore has the lowest, with exactly 25 % of transactions in each city.

### [5] Merchant & Purpose

   Each merchant has 4,000 transactions (20 %).

   | Merchant | Purpose | Amount |
   |---|---|---|
   | Zomato | Travel | 3,998,155.96 |
   | Flipkart | Shopping | 3,996,787.08 |
   | IRCTC | Others | 3,986,338.75 |
   | Swiggy | Bill Payment | 3,945,853.73 |
   | Amazon | Food | 3,945,138.51 |

   Merchant and purpose are linked one to one in this data (for example, every Zomato transaction has the purpose "Travel", and every Amazon transaction has the purpose "Food"), so they give the same split.

### [6] Payment Method & Device

   | Payment method | Device | Transactions | Amount |
   |---|---|---|---|
   | Phone Number | Tablet | 6,667 (33.34 %) | 6,640,042.16 |
   | UPI ID | Mobile | 6,666 (33.33 %) | 6,642,887.48 |
   | QR Code | Laptop | 6,667 (33.34 %) | 6,589,344.39 |

           thus, all three payment methods are used almost equally.

### [7] Transaction Type, Gender & Payment Mode

   Transfer = 10,000 (50 %), amount = 9,944,372.88

   Payment = 10,000 (50 %), amount = 9,927,901.15

   Gender : 10,000 male (50 %) & 10,000 female (50 %).

   Payment mode : 10,000 instant & 10,000 scheduled.

### [8] Age Group

   | Age group | Age | Transactions | Amount |
   |---|---|---|---|
   | A1 | 25 and below | 3,000 (15 %) | 2,946,355.93 |
   | A2 | 26 to 35 | 5,000 (25 %) | 4,989,280.09 |
   | A3 | 36 and above (up to 59) | 12,000 (60 %) | 11,936,638.01 |

           thus, maximum transactions come from the A3 age group. Customer ages in the data range from 20 to 59, and A3 covers 24 age values against 6 for A1, so it is the largest group.

### [9] Currency

   | Currency | Transactions | Amount |
   |---|---|---|
   | INR | 5,000 | 5,052,564.92 |
   | USD | 5,000 | 5,036,738.71 |
   | GBP | 5,000 | 4,907,634.17 |
   | EUR | 5,000 | 4,875,336.23 |

   The charts on Page 1 add up amounts in different currencies without conversion. Page 2 shows currency as a column in the matrix, so the amounts can be read per currency.

### [10] Data Observations

1. **Sum of Remaining Balance is not meaningful** : remaining balance is a balance after each transaction, so adding it across rows (about 100.4 million in total, about 8.4 million per month) does not give a real balance. An average, or the last balance per account, should be used instead.
2. **Mixed currencies** : INR, USD, GBP and EUR amounts are added together in the totals, so the totals are not in one currency.
3. **Several columns move together** : city, currency, sending bank and receiving bank are linked one to one (for example, every Mumbai transaction is in INR and is sent from an HDFC Bank account). The same is true for gender, transaction type and payment mode, for device type and payment method, and for merchant and purpose. Slicing by one of these also filters the others, so combining slicers can give blank results.
4. **Very even distribution** : most categories have exactly 25 % or 50 % of the transactions, which suggests that this is sample (synthetic) data and real trends should not be expected from it.
5. **Every transaction has a different account number** : there are 20,000 different customer account numbers and 20,000 merchant account numbers, so customer level analysis (repeat customers, top customers) is not possible with this data.
