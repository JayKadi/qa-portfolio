# Test Plan — Kadi Thrift E-commerce Platform

**Project:** Kadi Thrift E-commerce Platform  
**Tester:** Jay Kadi  
**Version:** 1.0  
**Date:** May 2026  

---

## 1. Introduction

Kadi Thrift is a full-stack e-commerce platform for buying and selling second-hand clothing. It features product browsing, cart management, Pesapal payment integration (M-Pesa and cards), Google OAuth authentication, and order management. This test plan outlines the strategy for testing the platform's core features to ensure they work correctly in a production environment.

---

## 2. Scope

**In Scope — what will be tested:**
- User authentication (JWT login, registration, Google OAuth)
- Product catalog (browsing, search, filtering by category)
- Shopping cart (add, remove, update quantity)
- Checkout and payment (M-Pesa via Pesapal)
- Order management (order creation, order history)
- Image loading via Cloudinary
- Responsive design on mobile and desktop

**Out of Scope — what will NOT be tested:**
- Pesapal's internal payment processing system (third party)
- Google OAuth infrastructure (third party)
- Cloudinary image storage internals (third party)
- Backend server performance and load testing
- Browser compatibility beyond Chrome and Firefox

---

## 3. Test Objectives

- Verify that users can register, log in, and log out successfully via both JWT and Google OAuth
- Verify that the product catalog displays correctly with accurate search and filtering
- Verify that the shopping cart updates correctly when items are added or removed
- Verify that the checkout flow completes successfully with valid M-Pesa details
- Verify that completed orders appear correctly in the user's order history
- Verify that appropriate error messages display for all invalid user inputs

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
| **Frontend URL** | kadi-thrift.vercel.app |
| **Backend URL** | Railway (Django REST Framework) |
| **Database** | PostgreSQL on Railway |
| **Browser** | Chrome (primary), Firefox (secondary) |
| **Devices** | Desktop (Windows) and Mobile (Android) |
| **Payment** | Pesapal sandbox environment |
| **Image Storage** | Cloudinary |

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
- All core features (auth, cart, checkout) are accessible
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
| Pesapal sandbox unavailable | Medium — payment tests blocked | Document expected behaviour and mark as blocked |
| TikTok/Instagram traffic affects server load | Low | Test during off-peak hours |
| Google OAuth token expiry during testing | Low | Re-authenticate and continue |

---

## 10. Deliverables

By the end of testing the following will be committed to the `qa-portfolio` GitHub repo:

- ✅ This test plan
- ✅ Manual test cases (`/manual-testing/kadi-thrift-test-cases.md`)
- ⏳ Postman collection (`/api-testing/kadi-thrift-postman-collection.json`)
- ⏳ Cypress test suite (`/e2e-testing/cypress/`)
- ⏳ Bug reports (`/bug-reports/kadi-thrift-bugs.md`)
