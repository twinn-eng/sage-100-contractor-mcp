# Available Tools

The server exposes nine tools. All of them are read-only: they look up records and run reports, and none can post, edit, or delete anything in Sage 100 Contractor.

You don't call these tools yourself. Your AI client chooses them based on the question you ask. This page explains what each one does so you know what to expect.

## Tools

| Tool | What it does |
|---|---|
| `company_context` | Returns the company's accounting calendar: fiscal year, current period, and which periods are open or closed. The client calls this first so that "this month" or "year to date" match the company's books. |
| `list_reports` | Lists the reports the connection can run, optionally filtered by module or by words in the title. |
| `describe_report` | Shows one report's criteria and defaults, its columns, its groupings, and how it is calculated. |
| `run_report` | Runs a report and returns its columns, totals and the criteria actually used, with relative dates such as "last month end" resolved. |
| `list_entities` | Lists the kinds of record the connection can read (jobs, vendors, ledger accounts and so on) and which of them can be searched by name. |
| `describe_entity` | Lists the fields of one kind of record, with each field's type and meaning. |
| `find_entity` | Reads records with filters, sorting and paging, or finds records by name, closest match first. Returns up to 200 rows per page. |
| `summarize_entity` | Counts records, or sums, finds the minimum or finds the maximum of a field, in total or grouped by up to two fields (a date can be grouped by year, month or fiscal period). |
| `decode` | Turns a status or type stored as a number into its meaning, for example an AP invoice status of 4 is Paid. |

## Reports come first

Where a report answers the question, the server steers the client to use it instead of adding up raw records. Reports compute figures the way Sage 100 Contractor's own reports do, so totals such as aging buckets, WIP and job profitability agree with what your accounting team already sees.

Record lookups are mainly used to find the right job, vendor or client before running a report for it, and to answer questions no report covers.

A typical question runs like this:

1. `company_context` to learn the current period.
2. `find_entity` to turn "the Riverside job" into a job number.
3. `describe_report` to choose the criteria.
4. `run_report` for the answer.

## Reports

The demo connection can run 50 reports.

### Accounts Payable

| Report | What it shows |
|---|---|
| AP Invoice Aging | Open payables by vendor, aged into Current, 1-30, 31-60, 61-90 and Over 90 days. |
| AP Invoice List | Payable invoices with totals, payments, retention and balance. |
| Payment Invoice Details | AP payments and the invoices they paid, by vendor. |
| Set to Pay | Open invoices with the amount set to pay, by job or vendor, with balance, retention, discount and warnings. |
| Lien Waiver Tracking | AP payments by job and vendor for a check date range: which lien waivers to collect, for how much, and what is still unpaid. |
| Subcontractor Pay by Job | Per job and subcontractor: subcontract amount with approved changes, billed to date, paid, retention held and remaining. |
| Subcontractor Compliance | Vendor certificates (insurance, workers' comp, license) with expiry dates, flagged expired or expiring. |
| Use Tax Accrual | AP invoices with use tax, by use tax district and posting period, with the taxable base, rate and tax to remit. |
| 1099 Vendor Payments | Payments to 1099 vendors in a calendar year, checked against Sage's 1099 amounts. |
| Vendor List | Vendors with type, contact, address, phone, 1099 type and status. |
| Vendor Workers Comp Report | Per vendor: each payment in the period as Subject or Exempt, with vendor totals. |

### Accounts Receivable

| Report | What it shows |
|---|---|
| AR Invoice Aging | Open receivables by client and job, aged into Current, 1-30, 31-60, 61-90 and Over 90 days. |
| AR Aging by Job | Open receivables aged by job and optionally by phase. |
| AR Collection Call Sheet | Past-due receivables by client and job, with contact details, invoice detail and job notes. |
| AR Invoice List | Receivable invoices with total, sales tax, paid, retention and balance, and each invoice's receipts. |
| Client Statement | Statement of account per client: every open contract and service invoice, with aging totals. |
| Retention Receivable and Payable by Job | Per job: retention held by the client on open AR invoices, retention held on open subcontractor invoices, and the net. |
| Taxable and Non-taxable Billings by Tax District | AR billings for a period split into taxable, non-taxable and sales tax, by tax district or job city. |

### Cash & General Ledger

| Report | What it shows |
|---|---|
| Balance Sheet | Assets, liabilities and equity by account type as of a period, with an optional comparison column. |
| Income Statement | Income and expenses by account type for the selected periods and year to date, with budget. |
| Income Statement by Department | Income statement with a column per department next to the consolidated total. |
| Statement of Cash Flows | Indirect-method cash flow statement for a period range, grouped into operating, investing and financing activities. |
| Trial Balance | Every GL account with its debit or credit balance as of a period. |
| General Ledger | Beginning balance, every posted line with a running balance, and ending balance per account. |
| General Journal | Posted GL transactions with all their lines and debit and credit totals. |
| GL Transaction Detail | Every posted line on one account for a period range. |
| Cash Receipts | Money received into cash accounts, by account and date, with who it came from. |
| Check Register | Checks written from cash accounts, by account and date. |

### Job Cost

| Report | What it shows |
|---|---|
| Budget vs Actual by Cost Code | Per job, phase and cost code: budget against actual cost and hours, the variance and the percent used. |
| Buy Out Report | For one job: target contract against what has been committed on purchase orders and subcontracts, cost to date, and projected cost. |
| Committed Costs | Open commitments per job and cost code from subcontracts and purchase orders. |
| Job Cost Journal | Job cost records by job, phase and cost code. |
| Job Cost Totals | Per job: budget, cost for a range of periods split by cost type, and cost to date. |
| Job Income Statement | Per job or phase: billing, cost by cost type, gross profit and gross profit percent. |
| Job Performance (WIP) | Per job: original and revised budget and contract, costs and billings to date, percent complete, backlog and over/under billing. |
| Job Profitability | Per job: revenue billed, cost by cost type, gross profit and margin. |
| Job Status Report | Job list with status, type, client, supervisor, key dates, contract, billed and cost to date. |
| Over/Under Billings | The WIP schedule as of a date: earned revenue, billed to date, over- and under-billings and gross profit to date. |
| Pending Change Orders | Prime change orders not yet approved, with days outstanding, requested amount and estimated cost. |

### Project Management

| Report | What it shows |
|---|---|
| Bonding Report | Per job through a period: contract, budget, estimated profit, earned and billed to date, under billing, cost to complete and contract remaining. |
| Current Cost Summary | Per cost code: budget with approved changes, cost to date, cost this period and what remains. |

### Purchasing

| Report | What it shows |
|---|---|
| Purchase Order List | Purchase orders with vendor, job, status, total and remaining balance. |
| Open PO Lines | Purchase order lines by job and vendor: ordered, received, canceled and remaining. |

### Payroll

| Report | What it shows |
|---|---|
| Certified Payroll | WH-347-style certified payroll per job and week. |
| Employee List | Employees with status, position, department, pay type, hire date and tax state. |
| Federal Tax Report | Per employee for a quarter, year or date range: federal wages and withholding, Social Security, Medicare and FUTA. |
| State Tax Report | Per state and employee: state wages and income tax withheld, SUI and other state payroll taxes. |
| Payroll by Check Date | Pay per employee for a check date range, with a column for each withholding and deduction. |
| Payroll Check Register | Payroll checks with hours, gross, taxes and deductions, additions and net. |
| Workers' Comp Report | Hours, wages and premium per workers' comp code, optionally by employee or by job. |

## Records

`find_entity` and `summarize_entity` can read 87 kinds of record across every Sage 100 Contractor module.

| Area | Records |
|---|---|
| Accounts payable | `ap-invoices`, `ap-payments`, `vendors`, `vendor-activities`, `vendor-balances`, `vendor-certificates`, `vendor-contacts`, `vendor-part-prices`, `vendor-remittances`, `vendor-types`, `secondary-payees`, `subcontracts`, `sub-change-order-lines`, `pre-liens` |
| Accounts receivable | `ar-invoices`, `ar-payments`, `clients`, `client-types`, `progress-billings`, `proposals` |
| Cash & general ledger | `ledger-accounts`, `ledger-subaccounts`, `ledger-balances`, `ledger-sub-balances`, `ledger-transactions`, `ledger-setups`, `period-statuses`, `bank-reconciliations`, `banking-transactions`, `credit-card-reconciliations`, `card-issuers`, `transaction-sources`, `departments`, `tax-districts`, `tax-entities` |
| Job cost | `jobs`, `job-phases`, `job-statuses`, `job-types`, `job-costs`, `budgets`, `cost-codes`, `cost-divisions`, `cost-types`, `cost-to-completes`, `hours-to-completes`, `units-completes`, `change-orders`, `change-order-types`, `historical-average-costs` |
| Purchasing & inventory | `purchase-orders`, `purchase-order-types`, `parts`, `part-classes`, `assemblies`, `assembly-classes`, `inventory-allocations`, `inventory-balances`, `inventory-consumed`, `inventory-histories`, `inventory-locations`, `inventory-quantities`, `inventory-serials` |
| Equipment | `equipment`, `equipment-types`, `equipment-costs`, `equipment-revenues` |
| Service | `service-contracts`, `service-equipment`, `service-inventories`, `service-locations`, `service-payments`, `service-schedules`, `service-types` |
| Payroll | `employees`, `employee-earnings`, `benefits`, `daily-payrolls`, `job-paygroups`, `paygroups`, `payroll-calculations`, `payroll-positions`, `payroll-postings`, `payroll-records`, `timecard-calculations`, `timecard-lines`, `workers-comps` |

## Withheld data

Some fields are never returned, whatever the client asks for:

- **Always withheld:** tax identifiers and bank details, such as a vendor's federal ID and bank account.
- **Withheld unless the connection is granted personal data:** people's names, home addresses, phone numbers, email and pay rates.
- **Withheld unless the connection is granted financial data:** amounts, balances and rates on everyday records such as jobs.

Withheld fields are left out of records and report columns, and a request that filters or groups on one is refused. `describe_report` names any withheld columns so the client can explain the gap.
