# Example Workflows

Each workflow below is a question you can ask in plain English, followed by the steps the AI client typically takes to answer it. You don't run the steps yourself. They are listed so you can see where each figure comes from and check it against Sage 100 Contractor.

Every workflow starts the same way: the client calls `company_context` once to learn the fiscal calendar, so "this month" or "year to date" means the same thing it does in your books. That step is left out below.

The examples use the demo company, Ridgeline Mechanical & Plumbing. Tool names are described in [Available Tools](available-tools.md).

## Month-end WIP schedule

> Show me the WIP schedule as of the end of last month. Which jobs are underbilled?

1. `describe_report` for **Over/Under Billings** to see its criteria.
2. `run_report` with `asOf` set to `$lastMonthEnd`. The server resolves that to the real date and returns it with the result.
3. The client sorts the rows by the Under Billings column and explains the largest.

Percent complete is cost to cost (cost to date over estimated cost). The figures match the **Job Performance (WIP)** report for the same date and options, so you can use either one to cross-check.

If your company posts approved change orders into the job budget and contract, say so in the question. The report has an option for it, and without it those change orders are counted twice.

## What we owe one vendor

> How much do we owe Lonestar Pipe & Supply, and how much of it is past due?

1. `find_entity` on `vendors` with a name match. The server returns the closest matches first, with their vendor numbers.
2. `run_report` for **AP Invoice Aging** with that vendor number.
3. The client reports the balance, the aging buckets and the retention held, which is shown separately because it isn't due until the job releases it.

If the name matches more than one vendor, a well-behaved client asks which one you meant before running the report.

## Collections calls

> Which clients are more than 60 days past due? Give me a call list.

1. `run_report` for **AR Collection Call Sheet**, which already includes each client's contact and phone number, the invoice detail and the job notes.
2. The client keeps the 61-90 and Over 90 rows and orders them by balance.

For a summary without contact details, ask for AR aging by client instead, and the client uses **AR Invoice Aging**.

## Subcontractor insurance

> Which subcontractors have insurance or workers' comp certificates that are expired or expire in the next 30 days?

1. `run_report` for **Subcontractor Compliance**, which flags each certificate as expired or expiring.
2. The client lists the vendors affected and the certificate type and date for each.

Federal ID numbers are never returned, even though the Sage report shows them. See [Withheld data](available-tools.md#withheld-data).

## Budget against actual for one job

> How is the Redfern Middle School Chiller job tracking against budget by cost code?

1. `find_entity` on `jobs` with a name match to get the job number.
2. `run_report` for **Budget vs Actual by Cost Code** for that job.
3. The client points out the cost codes with the largest variance and the percent of budget used.

A follow-up such as "what is committed but not yet invoiced on that job?" uses **Committed Costs** for the same job.

## Questions no report answers

> How many AP invoices did we enter each month this year?

There is no report for this, so the client counts records directly:

1. `describe_entity` on `ap-invoices` to find the invoice date field.
2. `summarize_entity` on `ap-invoices`, filtered to this year and grouped by invoice date by month.

The server counts and adds up in one call, so the client doesn't have to page through every invoice. Where a report does exist, the server tells the client to use it instead, because a report applies the same rules as Sage's own printout.

## Checking a figure against Sage

Every report result includes the criteria actually used, with relative dates resolved to real dates, and the date the figures are as of. `describe_report` also explains how each column is calculated and how to tie the report out to the matching Sage report. Ask the client "how was that calculated?" or "which Sage report should I compare this to?" and it will answer from that description.
