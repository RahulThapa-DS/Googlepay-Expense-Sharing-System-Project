# 💳 Google Pay Expense Sharing & Settlement System 

A Python-based data science utility designed to calculate fair-share bill splitting, reconcile group net balances, handle transaction edge cases (like refunds and pending payments), and visualize spending behavior.

---

## 📌 Project Overview
In group expenses, individual contributions are rarely equal, leading to complex settlement calculations. This project automates expense tracking by parsing multi-user split arrangements, calculating individual fair shares, isolating invalid/refunded transactions, and computing final settlement balances.

### Key Objectives
* **Data Cleaning & Filtering:** Exclude refunded transactions dynamically to maintain ledger integrity.
* **Fair-Share Calculation:** Parse multi-payer split strings and divide costs accurately across participants.
* **Net Balance Settlement:** Determine exactly who receives money back vs. who owes money.
* **Data Visualization:** Graphical distribution of expense categories and individual financial status.

---

## 🛠️ Tech Stack & Skills Demonstrated
* **Language:** Python 3.x
* **Data Manipulation & Analytics:** Pandas, NumPy
* **Data Visualization:** Matplotlib, Seaborn
* **Core Concepts:** Data preprocessing, string parsing, grouped aggregation, financial ledger logic

---

## ⚙️ Methodology & Settlement Logic

### 1. Data Cleaning
Transactions with status `Refunded` are removed prior to processing to avoid skewing individual fair share calculations.

### 2. Fair Share Mathematical Logic
For each valid transaction $i$:
$$\text{Individual Share} = \frac{\text{Transaction Amount}_i}{\text{Number of Participants}_i}$$

### 3. Net Balance Formula
$$\text{Net Balance} = \text{Total Amount Paid} - \text{Total Fair Share}$$

* **Positive Balance (+):** Participant overpaid $\rightarrow$ Receives reimbursement.
* **Negative Balance (-):** Participant underpaid $\rightarrow$ Owes money to the pool.

---

## 📊 Analytics & Visual Output

The pipeline generates two core visual insights:
1. **Category Distribution (Pie Chart):** Tracks proportional spending patterns (Food, Fuel, Hotel, Snacks, Cab).
2. **Net Balance Visualizer (Bar Chart):** Displays net visual statuses color-coded in **Green** (Receives) and **Red** (Owes).

---

## 🚀 How to Run Locally

### 1. Clone Repository
```bash
git clone [https://github.com/RahulThapa-DS/Googlepay-Expense-Sharing-System-Project](https://github.com/RahulThapa-DS/Googlepay-Expense-Sharing-System-Project)
cd expense-tracker-python

pip install -r requirements.txt

python main.py

### 1. Clone Repository
```bash
--- Raw Expense Dataset ---
   Transaction_ID  Payer  Amount Category               Split_Among     Status
0             101  Rahul    1200     Food  Rahul, Amit, Priya, Neha  Completed
1             102   Amit     800     Fuel               Rahul, Amit  Completed
2             103  Priya    1500    Hotel  Rahul, Amit, Priya, Neha  Completed
3             104  Rahul     600   Snacks              Rahul, Priya    Pending
4             105   Neha     400      Cab                Neha, Amit   Refunded

--- Final Net Balance Summary ---
       Paid  Fair_Share  Net_Balance
Rahul  1800      1375.0        425.0
Amit    800      1075.0       -275.0
Priya  1500       975.0        525.0
Neha      0       675.0       -675.0

