---
date: 2025-05-31T16:42:07+08:00
# description: ""
# image: ""
lastmod: 2025-05-31
showTableOfContents: false
tags: ["Ai Prompts",]
title: "Shared CC Prompts"
type: "post"
---

```
# Bank Statement Transaction Extraction Prompt

## Task Overview
Analyze the uploaded PDF bank statement and extract credit card transaction data from all relevant pages in a format suitable for Excel import.

## Instructions

### 1. Page Selection
- **First, scan through all pages** to identify which pages contain credit card transactions
- Look for sections labeled "Credit Card Transactions", "Card Purchases", "Credit Card Activity", or similar headings
- Focus exclusively on pages that contain individual credit card transaction entries
- Ignore pages with only account summaries, payment totals, interest charges, or footer content
- Extract only individual credit card transaction entries (purchases, payments, fees, etc.)

### 2. Data Extraction Requirements
For each credit card transaction, extract the following fields in this exact order:
1. **Transaction Description** (merchant name/transaction details)
2. **Transaction Date** (format: YYYY-MM-DD or DD/MM/YYYY - maintain consistency)
3. **Transaction Amount** (use negative for purchases; if "CR" suffix is present, make the numerical value negative and retain the "CR" suffix; other payments/credits positive)
4. **WHO** (determined by analyzing the transaction - see WHO Assignment Rules below)
5. **Check List**
6. **eStatements**

### 3. WHO Assignment Rules
**CRITICAL**: Analyze each transaction to determine who it belongs to:
- If the **Transaction Amount has suffix "CR"** (credit amount) → assign **"MINUS"**
- If the **Transaction Description contains "PETRON"** (case-insensitive) → assign **"KAMIL"**
- If the **Transaction Amount equals "15.90"** (exactly) → assign **"KAMIL"**
- For all other transactions → leave **WHO field blank** or assign based on other patterns you identify

**Priority Order**: Check for "CR" suffix first, then apply other rules if no "CR" is found.

### 4. Output Format
Present the data as a **Markdown table** with these exact column headers:

    ```markdown
    | Transaction Description | Transaction Date | Transaction Amount | WHO   | Check List | eStatements |
    |-------------------------|------------------|--------------------|-------|------------|-------------|
    | PETRON GAS STATION      | 2024-01-15       | 45.20              | KAMIL |            |             |
    | WALMART SUPERCENTER     | 2024-01-16       | 127.45             |       |            |             |
    | COFFEE SHOP DOWNTOWN    | 2024-01-17       | 15.90              | KAMIL |            |             |
    | PAYMENT RECEIVED        | 2024-01-18       | -500.00 CR         | MINUS |            |             |
    | PETRON FUEL STOP        | 2024-01-19       | 52.30              | KAMIL |            |             |
    | REFUND PROCESSING       | 2024-01-20       | -25.75 CR          | MINUS |            |             |
    ```

**Important**:
- Format as a standard Markdown table.

### 5. Data Cleaning Instructions
- Remove currency symbols but **PRESERVE "CR" suffix** in transaction amounts
- Ensure consistent date formatting throughout
- If the **Transaction Amount has a 'CR' suffix**, convert its numerical value to negative but **PRESERVE the 'CR' suffix**.
- Trim extra spaces from transaction descriptions
- If amounts are in parentheses (), treat as negative/debit amounts
- **Apply WHO assignment rules consistently to every transaction**
- **Keep "CR" suffix visible** in the Transaction Amount column for identification
- Preserve original transaction descriptions but clean up formatting

### 6. Quality Checks
- Verify that all credit card transaction pages have been identified and processed
- Check that transaction amounts and dates are consistent with credit card statement logic
- **Verify WHO assignments**: Double-check that all amounts with "CR" suffix are marked as MINUS
- **Verify WHO assignments**: Double-check that all PETRON transactions are marked as KAMIL
- **Verify WHO assignments**: Double-check that all 15.90 amount transactions are marked as KAMIL
- Flag any unclear or partially visible transactions
- Note any pages that may be cut off or illegible

### 7. Special Handling
- If a credit card transaction spans multiple lines, combine into single row
- For recurring charges (subscriptions, etc.), maintain individual entries with dates
- If page contains sub-totals, interest charges, or fees, include these as separate transaction types
- Handle different transaction types (Purchase, Payment, Fee, Interest, Credit, etc.) consistently
- Look for both current month transactions and any pending/recent transactions
- **Priority**: Always apply WHO assignment rules before finalizing each transaction row

## Expected Output Structure

Please provide:
1. **Summary**: "Found credit card transactions on pages [X, Y, Z] - Extracted [N] total transactions"
2. **Markdown table format**
3. **Notes**: Any irregularities, unclear entries, formatting issues, or pages that contained credit card data

## Additional Notes
- The output should be immediately copy-pasteable into Excel
- Use **tabs** between columns for proper Excel formatting
- If any transaction data is unclear or partially visible, note this separately
- Maintain chronological order as shown in the original statement