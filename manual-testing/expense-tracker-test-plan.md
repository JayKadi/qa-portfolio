# Test Plan — Expense Tracker Platform

**Project:** Expense Tracker  
**Tester:** Jay Kadi  
**Version:** 1.0  
**Date:** May 2026  

---

## 1. Introduction

Expense Tracker is a full-stack personal finance application that enables users to track their expenses versus income. Features include transaction search, addition of transactions, deletion of transactions, Google authentication, CSV export of transaction history, and pie charts for data visualisation. This test plan outlines the strategy for testing the platform's core features to ensure they work correctly in a production environment.

---

## 2. Scope

**In Scope — what will be tested:**
- User authentication (JWT login, registration, Google OAuth)
- Addition of transactions (income and expense)
- Deletion of transactions
- Transaction export via CSV
- Search for previously added transactions
- Dashboard pie chart updates after adding transactions

**Out of Scope — what will NOT be tested:**
- Google OAuth infrastructure (third party)
- Backend server performance and load testing
- Browser compatibility beyond Chrome and Firefox
- CSV export file compatibility with third party spreadsheet software (e.g. Excel, Google Sheets)

---

## 3. Test Objectives

- Verify that users can register, log in, and log out successfully via both JWT and Google OAuth
- Verify that a user can add a transaction whether it is an expense or income
- Verify that a user can delete a transaction
- Verify that a user can search a previously added transaction
- Verify that a user can export transaction history as a CSV file
- Verify that the dashboard pie chart updates correctly after a transaction is added

---

## 4. Test Types

| Test Type | Description |
|---|---|
| **Functional Testing** | Verify each feature works as expected |
| **Negative Testing** | Verify the app handles invalid inputs and edge cases gracefully |
| **Smoke Testing** | Quick check that core flows work after any deployment |
| **UI Testing** | Verify layout is correct and responsive on mobile and desktop |
| **Regression Testing** | Re-test existing features after new changes are made |

---

## 5. Test Environment

| Field | Details |
|---|---|
| **Frontend URL** | expense-tracker-kappa-mocha.vercel.app |
| **Backend URL** | Railway (Django REST Framework) |
| **Database** | PostgreSQL on Railway |
| **Browser** | Chrome (primary), Firefox (secondary) |
| **Devices** | Desktop (Windows) and Mobile (Android) |

---

## 6. Test Schedule

| Phase | Activity | Duration |
|---|---|---|
| Week 1 | Write all manual test cases | 3 days |
| Week 2 | Execute manual test cases and log bugs | 3 days |
| Week 3 | API testing with Postman | 4 days |
| Week 4 | E2E testing with Cypress | 5 days |
| Week 5 | Regression testing and final bug review | 3 days |

---

## 7. Resources

| Resource | Details |
|---|---|
| **Tester** | Jay Kadi |
| **Test Management** | GitHub (qa-portfolio repo) |
| **Manual Testing** | Browser + documented test cases |
| **API Testing** | Postman |
| **E2E Testing** | Cypress |
| **Bug Tracking** | GitHub Issues or documented bug reports |

---

## 8. Entry and Exit Criteria

**Entry Criteria — testing begins when:**
- Application is successfully deployed to production
- All core features (auth, transactions, CSV export) are accessible
- Test cases have been written and reviewed

**Exit Criteria — testing is complete when:**
- All test cases have been executed
- All High severity bugs have been fixed and re-tested
- All Medium severity bugs have been documented
- Test results have been committed to the qa-portfolio repo

---

## 9. Risks

| Risk | Impact | Mitigation |
|---|---|---|
| Railway backend goes down during testing | High — API tests cannot run | Run tests locally against local backend |
| Google OAuth token expiry during testing | Low | Re-authenticate and continue |
| CSV export produces incorrect data after new transactions | Medium | Cross-check exported data against dashboard totals |
| Pie chart not updating without page refresh | Medium | Document as bug if confirmed |

---

## 10. Deliverables

By the end of testing the following will be committed to the `qa-portfolio` GitHub repo:

- ✅ This test plan
- ✅ Manual test cases (`/manual-testing/expense-tracker-test-cases.md`)
- ⏳ Postman collection (`/api-testing/expense-tracker-postman-collection.json`)
- ⏳ Cypress test suite (`/e2e-testing/cypress/`)
- ⏳ Bug reports (`/bug-reports/expense-tracker-bugs.md`)
