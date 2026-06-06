# Calculated Fields - SaaS Revenue (Tableau)

---

## 1. `Total Revenue`

```
SUM([Revenue Amount])
```

**What it does:** Aggregates all individual transaction amounts into a single total revenue figure.

**Why it's used:** Base metric for almost every chart in the project. Instead of using `Revenue Amount` directly, this calculated field ensures consistent aggregation across all views.

---

## 2. `ARPPU` - Average Revenue Per Paying User

```
[Total Revenue] / [Paid Users]
```

**What it does:** Divides total revenue by the number of paying users to get the average amount each user brings in.

**Why it's used:** ARPPU is a key SaaS health metric. It shows whether the revenue growth is coming from more users or from users paying more. In this project, ARPPU was declining even as Paid Users grew — a sign of customer base dilution.

---

## 3. `New MRR` - New Monthly Recurring Revenue

```
IF DATETRUNC('month', [Payment Date]) = DATETRUNC('month', [first payment date])
THEN [Revenue Amount]
END
```

**What it does:** Returns the revenue amount only for a user's very first payment month. If the payment was made in any subsequent month, the field returns NULL.

**Why it's used:** Isolates revenue coming from brand-new customers only (not renewals or expansions). This is the standard SaaS definition of New MRR - money from customers who just started paying.

**Logic breakdown:**
- `DATETRUNC('month', [Payment Date])` - truncates the transaction date to the first day of its month
- `DATETRUNC('month', [first payment date])` - truncates the user's first-ever payment to the first day of that month
- If both months match → it's a new customer payment → return the revenue
- If they don't match → it's a returning customer → return NULL

---

## 4. `Payment Month Number`

```
DATEDIFF('month', [first payment month], [payment month])
```

**What it does:** Calculates how many months have passed since a user's first payment. Returns 0 for the first month, 1 for the second month, and so on.

**Why it's used:** This is the column axis of the **Revenue Cohort Table**. It lets you align all customers relative to their own start date, regardless of when they actually joined, making cohort comparison possible.

**Example:**
| User | First Payment | Current Payment | Month Number |
|---|---|---|---|
| A | June 2022 | June 2022 | 0 |
| A | June 2022 | August 2022 | 2 |
| B | October 2022 | November 2022 | 1 |

---

## 5. `First Payment Date`

```
{ FIXED [User Id] : MIN([Payment Date]) }
```

**What it does:** For each unique user, finds their earliest payment date across the entire dataset.

**Why it's used:** Foundation for all cohort logic. Without knowing when each user first paid, you can't calculate `New MRR`, `Payment Month Number`, or assign users to cohorts.

**Key concept — LOD Expression:** `FIXED` is a Level of Detail (LOD) expression. It ignores any filters or dimensions currently in the view and computes the result at the `User Id` level only. This guarantees the first payment date is always correct, no matter how the data is sliced.

---

## 6. `First Payment Month`

```
DATE(DATETRUNC('month', [first payment date]))
```

**What it does:** Takes the `First Payment Date` and truncates it to the first day of that month, then converts it to a DATE format.

**Why it's used:** Used as the **row axis** of the Revenue Cohort Table — each row represents one acquisition cohort (e.g. all users who first paid in June 2022, July 2022, etc.). Truncating to month level groups all users who joined in the same month into one cohort.

**Example:** A user whose first payment was June 14, 2022 → `First Payment Month` = June 1, 2022

---

## 🔗 How the fields connect

```
Payment Date
    └── First Payment Date  (LOD: earliest date per User Id)
            └── First Payment Month  (truncated to month → cohort row)
            └── New MRR  (revenue only in month 0)
            └── Payment Month Number  (months since first payment → cohort column)

Revenue Amount
    └── Total Revenue  (SUM)
            └── ARPPU  (Total Revenue / Paid Users)
```
