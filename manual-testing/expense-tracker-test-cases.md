# Test Cases — Expense Tracker

**Project:** Expense Tracker  
**Tester:** Jay Kadi  
**Feature:** Multiple Features  
**Environment:** Production — expense-tracker-kappa-mocha.vercel.app  
**Date:** May 2026  

---

## Test Suite: TC-SEARCH

---

### TC-001 — Successful Transaction Search

| Field | Details |
|---|---|
| **Feature** | Search |
| **Scenario** | Logged-in user finds a transaction added a while ago |
| **Priority** | High |
| **Severity** | High |

**Preconditions:**
- User is logged in
- At least one transaction exists in the account that was added more than 30 days ago

**Steps:**
1. Navigate to the transaction history page
2. Click the search bar
3. Enter the name of an existing transaction
4. Click Search or press Enter

**Expected Result:** The transaction appears in the filtered results showing the correct name, amount, date, and category.

**Status:** [ ] Pass [ ] Fail [ ] Blocked

---

## Test Suite: TC-AUTH

---

### TC-002 — Login with Wrong Password

| Field | Details |
|---|---|
| **Feature** | Authentication |
| **Scenario** | User fails to login when using a wrong password |
| **Priority** | High |
| **Severity** | High |

**Preconditions:**
- User has an existing registered account
- User is on the login page

**Steps:**
1. Enter a valid registered email address
2. Enter an incorrect password
3. Click Login

**Expected Result:** An error message displays — "Invalid email or password." User remains on the login page. No session is created.

**Status:** [ ] Pass [ ] Fail [ ] Blocked

---

## Test Suite: TC-EXPORT

---

### TC-003 — CSV Export with Empty Transaction History

| Field | Details |
|---|---|
| **Feature** | CSV Export |
| **Scenario** | User attempts to export CSV when no transactions exist |
| **Priority** | Medium |
| **Severity** | Medium |

**Preconditions:**
- User is logged in
- User has no transactions in their account

**Steps:**
1. Navigate to transaction history
2. Click "Export CSV"

**Expected Result:** A message displays — "No transactions to export." No CSV file is downloaded.

**Status:** [ ] Pass [ ] Fail [ ] Blocked

---

## Test Suite: TC-TRANSACTIONS

---

### TC-004 — Adding a Transaction with No Amount

| Field | Details |
|---|---|
| **Feature** | Add Transaction |
| **Scenario** | User attempts to submit a transaction without entering an amount |
| **Priority** | High |
| **Severity** | High |

**Preconditions:**
- User is logged in
- User is on the Add Transaction page

**Steps:**
1. Click "Add Transaction"
2. Select the type of transaction (Income or Expense)
3. Enter a transaction name
4. Leave the amount field empty
5. Click Save

**Expected Result:** Form submission is blocked. An error message displays beneath the amount field — "Amount is required." Transaction is not saved to the database.

**Status:** [ ] Pass [ ] Fail [ ] Blocked

---

### TC-005 — Dashboard Pie Chart Updates After Adding a Transaction

| Field | Details |
|---|---|
| **Feature** | Dashboard — Data Visualisation |
| **Scenario** | Pie chart reflects new transaction without page refresh |
| **Priority** | High |
| **Severity** | High |

**Preconditions:**
- User is logged in
- User is on the dashboard
- At least one transaction already exists

**Steps:**
1. Navigate to the dashboard and note the current percentage breakdown on the pie chart
2. Click "Add Transaction"
3. Select type — Expense
4. Enter a name, amount, and category
5. Click Save
6. Return to the dashboard
7. Observe the pie chart

**Expected Result:** The pie chart reflects the new transaction. The percentage for the relevant category increases proportionally. The total expense amount shown on the dashboard also updates without requiring a page refresh.

**Status:** [ ] Pass [ ] Fail [ ] Blocked
