অবশ্যই। এবার **Accounting / Expense Management System**-টা আগের Warehouse, E-commerce, Food Delivery-এর মতো **production-level complete model + fields + relationships + constraints + accounting flow** দিয়ে design করছি।

এটা শুধু Expense Tracker হবে না; বরং **small/medium business accounting system** হিসেবে design করা হবে।

# 💰 Accounting / Expense Management System

আমি মোট **47টি model** রাখছি:

```text
1.  BaseModel

2.  Organization
3.  OrganizationMember
4.  Branch
5.  Department

6.  AccountType
7.  Account
8.  AccountBalance

9.  FiscalYear
10. AccountingPeriod

11. JournalEntry
12. JournalEntryLine

13. Customer
14. CustomerAddress

15. Supplier
16. SupplierContact

17. Invoice
18. InvoiceItem
19. InvoicePayment

20. Bill
21. BillItem
22. BillPayment

23. ExpenseCategory
24. Expense
25. ExpenseItem
26. ExpenseAttachment

27. IncomeCategory
28. Income

29. BankAccount
30. BankTransaction
31. BankReconciliation

32. PaymentMethod
33. PaymentTransaction

34. Tax
35. TaxRate

36. Budget
37. BudgetLine

38. RecurringExpense
39. RecurringInvoice

40. FixedAsset
41. AssetDepreciation

42. Employee
43. Payroll
44. PayrollItem

45. FinancialTransaction
46. AuditLog
47. IdempotencyRecord
```

---

# 🧱 1. BaseModel

সব model-এর common fields:

```text
BaseModel
├── id
├── created_at
├── updated_at
├── is_active
└── deleted_at
```

---

# 🏢 ORGANIZATION

## 2. Organization

Business/company-এর মূল entity।

```text
Organization
├── id
├── name
├── legal_name
├── registration_number
├── tax_number
├── email
├── phone
├── website
├── currency
├── country
├── timezone
├── fiscal_year_start_month
└── is_active
```

Example:

```text
ABC Technologies Ltd.
```

---

# 👥 3. OrganizationMember

একজন User-এর organization access।

```text
OrganizationMember
├── id
├── organization
├── user
├── role
├── joined_at
└── is_active
```

Roles:

```text
owner
admin
accountant
manager
employee
viewer
```

Constraint:

```text
Unique(organization, user)
```

---

# 🏢 4. Branch

Business-এর branches।

```text
Branch
├── id
├── organization
├── name
├── code
├── address
├── city
├── phone
├── manager
└── is_active
```

Constraint:

```text
Unique(organization, code)
```

---

# 🏬 5. Department

```text
Department
├── id
├── organization
├── branch
├── name
├── code
└── is_active
```

Example:

```text
IT
HR
Finance
Marketing
Sales
```

---

# 📚 CHART OF ACCOUNTS

Accounting system-এর সবচেয়ে গুরুত্বপূর্ণ অংশ।

## 6. AccountType

```text
AccountType
├── id
├── name
├── code
├── category
└── normal_balance
```

Categories:

```text
asset
liability
equity
income
expense
```

Normal balance:

```text
debit
credit
```

---

# 7. Account ⭐⭐⭐

Actual Chart of Accounts।

```text
Account
├── id
├── organization
├── parent
├── account_type
├── code
├── name
├── description
├── opening_balance
├── currency
├── is_system
└── is_active
```

Example:

```text
1000 Assets
│
├── 1100 Cash
├── 1200 Bank
└── 1300 Accounts Receivable

2000 Liabilities
│
├── 2100 Accounts Payable
└── 2200 Tax Payable

4000 Income
│
└── 4100 Sales Revenue

5000 Expenses
│
├── 5100 Salary Expense
├── 5200 Rent Expense
└── 5300 Electricity Expense
```

Constraint:

```text
Unique(organization, code)
```

---

# 8. AccountBalance

Account-এর calculated/cached balance।

```text
AccountBalance
├── id
├── account
├── fiscal_year
├── opening_debit
├── opening_credit
├── debit_total
├── credit_total
├── closing_balance
└── updated_at
```

এটা performance-এর জন্য cache/materialized summary হিসেবে ব্যবহার করা যায়।

---

# 📅 ACCOUNTING PERIOD

## 9. FiscalYear

```text
FiscalYear
├── id
├── organization
├── name
├── start_date
├── end_date
├── status
└── is_current
```

Example:

```text
2026-2027
```

Constraint:

```text
Unique(organization, name)
```

---

# 10. AccountingPeriod

Monthly/quarterly period।

```text
AccountingPeriod
├── id
├── fiscal_year
├── name
├── start_date
├── end_date
├── status
└── is_closed
```

Example:

```text
July 2026
August 2026
September 2026
```

---

# 📒 DOUBLE-ENTRY ACCOUNTING

এটাই system-এর heart।

## 11. JournalEntry ⭐⭐⭐

একটি accounting transaction-এর header।

```text
JournalEntry
├── id
├── organization
├── journal_number
├── date
├── description
├── reference_type
├── reference_id
├── branch
├── fiscal_year
├── accounting_period
├── status
├── created_by
└── posted_by
```

Status:

```text
draft
posted
reversed
void
```

---

# 12. JournalEntryLine ⭐⭐⭐

Actual debit/credit।

```text
JournalEntryLine
├── id
├── journal_entry
├── account
├── description
├── debit
├── credit
├── customer
├── supplier
├── department
└── branch
```

### Golden Rule

```text
Total Debit = Total Credit
```

Example:

Company pays office rent 20,000:

```text
Debit:
Rent Expense       20,000

Credit:
Cash               20,000
```

---

# 👤 CUSTOMER

## 13. Customer

```text
Customer
├── id
├── organization
├── name
├── code
├── email
├── phone
├── tax_number
├── credit_limit
├── opening_balance
└── is_active
```

---

# 14. CustomerAddress

```text
CustomerAddress
├── id
├── customer
├── label
├── address_line
├── city
├── country
├── postal_code
└── is_default
```

---

# 🚚 SUPPLIER

## 15. Supplier

```text
Supplier
├── id
├── organization
├── name
├── code
├── company_name
├── email
├── phone
├── tax_number
├── payment_terms
├── credit_limit
└── is_active
```

---

# 16. SupplierContact

```text
SupplierContact
├── id
├── supplier
├── name
├── designation
├── email
├── phone
└── is_primary
```

---

# 🧾 SALES INVOICE

## 17. Invoice

Customer-কে sales invoice।

```text
Invoice
├── id
├── organization
├── customer
├── branch
├── invoice_number
├── invoice_date
├── due_date
├── subtotal
├── discount
├── tax
├── total_amount
├── paid_amount
├── due_amount
├── status
├── notes
└── created_by
```

Status:

```text
draft
issued
partially_paid
paid
overdue
cancelled
```

---

# 18. InvoiceItem

```text
InvoiceItem
├── id
├── invoice
├── description
├── quantity
├── unit_price
├── discount
├── tax
└── total_amount
```

---

# 19. InvoicePayment

```text
InvoicePayment
├── id
├── invoice
├── payment_transaction
├── amount
├── payment_date
└── created_by
```

এক invoice-এ multiple payment হতে পারে।

---

# 📥 PURCHASE BILL

## 20. Bill

Supplier-এর invoice/bill।

```text
Bill
├── id
├── organization
├── supplier
├── branch
├── bill_number
├── bill_date
├── due_date
├── subtotal
├── discount
├── tax
├── total_amount
├── paid_amount
├── due_amount
├── status
└── created_by
```

---

# 21. BillItem

```text
BillItem
├── id
├── bill
├── description
├── quantity
├── unit_price
├── discount
├── tax
└── total_amount
```

---

# 22. BillPayment

```text
BillPayment
├── id
├── bill
├── payment_transaction
├── amount
├── payment_date
└── created_by
```

---

# 💸 EXPENSE

## 23. ExpenseCategory

```text
ExpenseCategory
├── id
├── organization
├── parent
├── name
├── code
└── is_active
```

Example:

```text
Operating Expense
├── Rent
├── Utilities
├── Salary
└── Internet
```

---

# 24. Expense

Expense-এর main record।

```text
Expense
├── id
├── organization
├── branch
├── department
├── category
├── expense_number
├── expense_date
├── description
├── subtotal
├── tax
├── total_amount
├── payment_method
├── paid_from_account
├── status
├── submitted_by
├── approved_by
└── approved_at
```

Status:

```text
draft
submitted
approved
rejected
paid
cancelled
```

---

# 25. ExpenseItem

এক expense-এ multiple items।

```text
ExpenseItem
├── id
├── expense
├── description
├── quantity
├── unit_price
├── amount
└── tax
```

---

# 26. ExpenseAttachment

Receipt/invoice upload।

```text
ExpenseAttachment
├── id
├── expense
├── file
├── filename
├── file_size
└── uploaded_by
```

---

# 💵 INCOME

## 27. IncomeCategory

```text
IncomeCategory
├── id
├── organization
├── name
├── code
└── is_active
```

---

# 28. Income

```text
Income
├── id
├── organization
├── branch
├── category
├── income_number
├── income_date
├── description
├── amount
├── tax
├── total_amount
├── received_into_account
├── payment_method
├── status
└── created_by
```

---

# 🏦 BANKING

## 29. BankAccount

```text
BankAccount
├── id
├── organization
├── account
├── bank_name
├── branch_name
├── account_name
├── account_number
├── routing_number
├── opening_balance
├── current_balance
├── currency
└── is_active
```

Account number sensitive—production system-এ encryption/masking consider করতে হবে।

---

# 30. BankTransaction

Bank statement-এর transaction।

```text
BankTransaction
├── id
├── bank_account
├── transaction_date
├── transaction_type
├── reference
├── description
├── amount
├── balance
├── external_id
├── is_reconciled
└── imported_at
```

Types:

```text
deposit
withdrawal
fee
transfer
interest
```

---

# 31. BankReconciliation

Company records বনাম bank statement match করা।

```text
BankReconciliation
├── id
├── bank_account
├── start_date
├── end_date
├── statement_balance
├── book_balance
├── difference
├── status
├── reconciled_by
└── reconciled_at
```

---

# 💳 PAYMENT

## 32. PaymentMethod

```text
PaymentMethod
├── id
├── organization
├── name
├── method_type
├── account
└── is_active
```

Types:

```text
cash
bank
card
mobile_banking
cheque
wallet
```

---

# 33. PaymentTransaction

Actual payment।

```text
PaymentTransaction
├── id
├── organization
├── transaction_number
├── payment_method
├── transaction_type
├── amount
├── transaction_date
├── reference
├── status
├── customer
├── supplier
├── description
└── created_by
```

Types:

```text
customer_payment
supplier_payment
expense_payment
income_receipt
refund
transfer
```

---

# 🧾 TAX

## 34. Tax

```text
Tax
├── id
├── organization
├── name
├── code
├── description
└── is_active
```

Example:

```text
VAT
AIT
```

---

# 35. TaxRate

```text
TaxRate
├── id
├── tax
├── rate
├── effective_from
├── effective_to
└── is_active
```

---

# 📊 BUDGET

## 36. Budget

Annual/monthly budget।

```text
Budget
├── id
├── organization
├── name
├── fiscal_year
├── start_date
├── end_date
├── total_amount
├── status
└── created_by
```

---

# 37. BudgetLine

```text
BudgetLine
├── id
├── budget
├── account
├── department
├── branch
├── allocated_amount
├── spent_amount
└── remaining_amount
```

Formula:

```text
remaining
=
allocated - spent
```

---

# 🔁 RECURRING

## 38. RecurringExpense

Monthly recurring expenses।

```text
RecurringExpense
├── id
├── organization
├── category
├── description
├── amount
├── frequency
├── start_date
├── end_date
├── next_run_date
├── payment_account
├── auto_create
└── is_active
```

Frequency:

```text
daily
weekly
monthly
quarterly
yearly
```

---

# 39. RecurringInvoice

```text
RecurringInvoice
├── id
├── organization
├── customer
├── description
├── amount
├── frequency
├── start_date
├── end_date
├── next_run_date
├── auto_create
└── is_active
```

---

# 🏗️ FIXED ASSET

## 40. FixedAsset ⭐⭐⭐

Company-এর long-term asset।

```text
FixedAsset
├── id
├── organization
├── account
├── asset_code
├── name
├── category
├── purchase_date
├── purchase_cost
├── salvage_value
├── useful_life_months
├── depreciation_method
├── accumulated_depreciation
├── current_value
├── status
└── disposal_date
```

Methods:

```text
straight_line
declining_balance
```

---

# 41. AssetDepreciation

```text
AssetDepreciation
├── id
├── asset
├── accounting_period
├── depreciation_amount
├── accumulated_amount
├── book_value
└── posted_at
```

---

# 👨‍💼 EMPLOYEE

## 42. Employee

```text
Employee
├── id
├── organization
├── user
├── employee_id
├── department
├── branch
├── designation
├── joining_date
├── salary
└── is_active
```

---

# 💰 PAYROLL

## 43. Payroll

এক মাসের payroll header।

```text
Payroll
├── id
├── organization
├── month
├── year
├── total_gross
├── total_deductions
├── total_net
├── status
├── processed_by
└── processed_at
```

---

# 44. PayrollItem

```text
PayrollItem
├── id
├── payroll
├── employee
├── basic_salary
├── allowances
├── bonus
├── deductions
├── tax
└── net_salary
```

Formula:

```text
Net Salary
=
Basic
+
Allowances
+
Bonus
-
Deductions
-
Tax
```

---

# 🔄 FINANCIAL TRANSACTION

## 45. FinancialTransaction

System-এর high-level transaction reference।

```text
FinancialTransaction
├── id
├── organization
├── transaction_number
├── transaction_type
├── reference_type
├── reference_id
├── amount
├── transaction_date
├── status
└── created_by
```

এটা বিভিন্ন financial operation-এর unified reference হিসেবে কাজ করতে পারে।

---

# 📝 46. AuditLog

```text
AuditLog
├── id
├── organization
├── user
├── action
├── model_name
├── object_id
├── old_data
├── new_data
├── ip_address
└── created_at
```

Accounting system-এ audit trail খুব important।

---

# 🔐 47. IdempotencyRecord

```text
IdempotencyRecord
├── id
├── organization
├── user
├── key
├── endpoint
├── status
├── response_data
└── created_at
```

বিশেষ করে:

```text
POST payment
POST invoice
POST bill
POST expense
POST payroll
POST journal
```

duplicate submission prevent করতে useful।

---

# 🔗 COMPLETE RELATIONSHIP

```text
                         ORGANIZATION
                              │
             ┌────────────────┼─────────────────┐
             │                │                 │
          Branch          Department       Members
             │
             │
       ┌─────┴─────────────────────────────┐
       │                                   │
   CUSTOMERS                           SUPPLIERS
       │                                   │
    Invoice                              Bill
       │                                   │
 InvoiceItem                          BillItem
       │                                   │
 InvoicePayment                       BillPayment
       │                                   │
       └──────────────┬────────────────────┘
                      │
               PaymentTransaction
                      │
               JournalEntry
                      │
              JournalEntryLine
                      │
                  Account
```

---

# 📒 Chart of Accounts Structure

একটা real accounting system-এর core:

```text
1000 ASSETS
│
├── 1100 Cash
├── 1200 Bank
├── 1300 Accounts Receivable
└── 1400 Fixed Assets

2000 LIABILITIES
│
├── 2100 Accounts Payable
├── 2200 Tax Payable
└── 2300 Loan Payable

3000 EQUITY
│
├── 3100 Owner Capital
└── 3200 Retained Earnings

4000 INCOME
│
├── 4100 Sales Revenue
└── 4200 Other Income

5000 EXPENSE
│
├── 5100 Salary
├── 5200 Rent
├── 5300 Electricity
├── 5400 Internet
└── 5500 Marketing
```

---

# ⭐ Double Entry Example

ধরো company **৳20,000 rent** cash দিয়ে দিল।

### JournalEntry

```text
Rent Payment
Date: 2026-09-13
```

### JournalEntryLine

```text
Account              Debit       Credit

Rent Expense         20,000      0
Cash                 0           20,000
```

সবসময়:

```text
TOTAL DEBIT
=
TOTAL CREDIT
```

---

# 💰 Sales Example

Customer-কে ৳50,000-এর service বিক্রি হলো, কিন্তু customer এখনো payment দেয়নি।

```text
Accounts Receivable     Debit   50,000
Sales Revenue           Credit  50,000
```

Customer পরে ৳50,000 দিল:

```text
Bank                    Debit   50,000
Accounts Receivable     Credit  50,000
```

এখানে বুঝতে পারছো কেন `Invoice`, `Payment`, `Account`, `JournalEntry` আলাদা model হওয়া দরকার।

---

# 💸 Expense Flow

```text
Employee
   ↓
Expense
   ↓
Approval
   ↓
Payment
   ↓
JournalEntry
   ↓
Expense Account
```

---

# 🧾 Invoice Flow

```text
Customer
   ↓
Invoice
   ↓
InvoiceItem
   ↓
Issue
   ↓
Payment
   ↓
JournalEntry
   ↓
Accounts Receivable
```

---

# 🚚 Supplier Bill Flow

```text
Supplier
   ↓
Bill
   ↓
BillItem
   ↓
Payment
   ↓
JournalEntry
   ↓
Accounts Payable
```

---

# 🏦 Bank Reconciliation Flow

```text
Bank
 ↓
BankTransaction
 ↓
Compare
 ↓
Book Transaction
 ↓
BankReconciliation
 ↓
Matched / Unmatched
```

---

# 📊 Budget Flow

```text
Budget
   ↓
BudgetLine
   ↓
Expense
   ↓
Actual Spending
   ↓
Budget vs Actual
```

Example:

```text
IT Budget       = 500,000

Actual Expense  = 380,000

Remaining       = 120,000
```

---

# 🏗️ Fixed Asset Flow

```text
Purchase Asset
      ↓
FixedAsset
      ↓
Depreciation
      ↓
AssetDepreciation
      ↓
JournalEntry
```

Example:

```text
Laptop Cost = 120,000
Useful Life = 36 months

Monthly depreciation
≈ 3,333
```

---

# 🚨 Production Accounting Rules

এই project-এ কয়েকটা rule **database/service layer-এ enforce** করবে।

### 1. Debit ≠ Credit হতে পারবে না

```text
SUM(debit) == SUM(credit)
```

### 2. Posted Journal পরিবর্তন করা উচিত না

Instead:

```text
Posted
 ↓
Reverse
 ↓
New Correct Journal
```

### 3. Closed period-এ transaction ঢুকবে না

```text
AccountingPeriod.is_closed = True
```

হলে নতুন journal reject।

### 4. Invoice total server-side calculate করবে

```text
subtotal
+ tax
- discount
=
total
```

Client-এর পাঠানো total blindly trust করবে না।

### 5. Payment duplicate হওয়া prevent করবে

```text
transaction_number UNIQUE
```

এবং idempotency ব্যবহার করবে।

### 6. Account balance manually trust করবে না

Primary source:

```text
JournalEntryLine
```

আর performance-এর জন্য:

```text
AccountBalance
```

cache/summary হিসেবে রাখা যাবে।

---

# 🔥 Important Constraints

```text
Organization
    Unique(registration_number)

OrganizationMember
    Unique(organization, user)

Branch
    Unique(organization, code)

Department
    Unique(organization, code)

Account
    Unique(organization, code)

FiscalYear
    Unique(organization, name)

JournalEntry
    Unique(organization, journal_number)

Invoice
    Unique(organization, invoice_number)

Bill
    Unique(organization, bill_number)

Expense
    Unique(organization, expense_number)

PaymentTransaction
    Unique(organization, transaction_number)

Employee
    Unique(organization, employee_id)

FixedAsset
    Unique(organization, asset_code)
```

---

# 📈 Important Database Indexes

সবচেয়ে বেশি query হবে:

```text
JournalEntry
├── organization + date
├── organization + status
└── fiscal_year + accounting_period
```

```text
JournalEntryLine
├── account + created_at
├── customer + created_at
├── supplier + created_at
└── department + created_at
```

```text
Invoice
├── customer + status
├── due_date + status
└── organization + invoice_date
```

```text
Bill
├── supplier + status
└── due_date + status
```

```text
Expense
├── category + expense_date
├── department + expense_date
└── branch + expense_date
```

---

# 🏗️ Recommended Django Apps

```text
accounting/
│
├── accounts/
│   ├── AccountType
│   ├── Account
│   └── AccountBalance
│
├── organizations/
│
├── branches/
│
├── departments/
│
├── fiscal/
│   ├── FiscalYear
│   └── AccountingPeriod
│
├── journals/
│   ├── JournalEntry
│   └── JournalEntryLine
│
├── customers/
│
├── suppliers/
│
├── invoices/
│
├── bills/
│
├── expenses/
│
├── income/
│
├── banking/
│
├── payments/
│
├── taxes/
│
├── budgets/
│
├── recurring/
│
├── assets/
│
├── payroll/
│
├── reports/
│
├── audit/
│
└── core/
```

---

# 🎯 Project Implementation Phases

### Phase 1 — Organization

```text
Organization
OrganizationMember
Branch
Department
```

### Phase 2 — Accounting Core ⭐

```text
AccountType
Account
FiscalYear
AccountingPeriod
JournalEntry
JournalEntryLine
```

### Phase 3 — Customer/Supplier

```text
Customer
CustomerAddress
Supplier
SupplierContact
```

### Phase 4 — Sales

```text
Invoice
InvoiceItem
InvoicePayment
```

### Phase 5 — Purchase

```text
Bill
BillItem
BillPayment
```

### Phase 6 — Expense

```text
ExpenseCategory
Expense
ExpenseItem
ExpenseAttachment
IncomeCategory
Income
```

### Phase 7 — Banking

```text
BankAccount
BankTransaction
BankReconciliation
PaymentMethod
PaymentTransaction
```

### Phase 8 — Tax + Budget

```text
Tax
TaxRate
Budget
BudgetLine
```

### Phase 9 — Advanced

```text
RecurringExpense
RecurringInvoice
FixedAsset
AssetDepreciation
Employee
Payroll
PayrollItem
```

### Phase 10 — Production

```text
FinancialTransaction
AuditLog
IdempotencyRecord
```

---

## ⭐ সবচেয়ে গুরুত্বপূর্ণ Models

যদি পুরো 47টা একসাথে implement না করে **core accounting system** বানাতে চাও, প্রথমে এই 15টা করো:

```text
1. Organization
2. OrganizationMember
3. AccountType
4. Account
5. FiscalYear
6. AccountingPeriod
7. JournalEntry
8. JournalEntryLine
9. Customer
10. Supplier
11. Invoice
12. InvoiceItem
13. Expense
14. PaymentTransaction
15. AuditLog
```

তারপর ধীরে ধীরে:

```text
Invoice
   ↓
Payment
   ↓
Journal
   ↓
Ledger
   ↓
Trial Balance
   ↓
Profit & Loss
   ↓
Balance Sheet
   ↓
Cash Flow
```

এই project-এর সবচেয়ে valuable অংশ হবে **Double-Entry Accounting + Ledger + Trial Balance + P&L + Balance Sheet**। এগুলো implement করলে এটা সাধারণ CRUD Expense Tracker না থেকে সত্যিকারের **Accounting Software / ERP-style backend project** হয়ে যাবে।


