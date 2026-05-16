# Test Cases — Kadi Thrift Checkout Flow

**Project:** Kadi Thrift E-commerce Platform  
**Tester:** Jay Kadi  
**Feature:** Checkout & Payment  
**Environment:** Production — kadi-thrift.vercel.app  
**Date:** May 2026  

---

## Test Suite: TC-CHECKOUT

---

### TC-001 — Successful M-Pesa Checkout (Happy Path)

| Field | Details |
|---|---|
| **Feature** | Checkout |
| **Scenario** | Logged-in user completes a purchase using M-Pesa |
| **Priority** | High |
| **Severity** | High |

**Preconditions:**
- User is logged in
- At least 1 item is in the cart
- Valid Safaricom number available

**Steps:**
1. Navigate to cart
2. Click "Proceed to Checkout"
3. Confirm delivery details
4. Select M-Pesa as payment method
5. Enter a valid Safaricom phone number
6. Click "Pay Now"
7. Simulate M-Pesa PIN confirmation

**Expected Result:** Order is created, user is redirected to order confirmation page with order ID and summary

**Status:** [ ] Pass [ ] Fail [ ] Blocked

---

### TC-002 — Checkout with Invalid Phone Number

| Field | Details |
|---|---|
| **Feature** | Checkout — Validation |
| **Scenario** | User enters a non-Safaricom or malformed phone number |
| **Priority** | High |
| **Severity** | Medium |

**Preconditions:**
- User is logged in
- At least 1 item is in the cart

**Steps:**
1. Navigate to cart
2. Click "Proceed to Checkout"
3. Select M-Pesa as payment method
4. Enter an invalid number (e.g. 0700000000 or 123)
5. Click "Pay Now"

**Expected Result:** Error message displayed — "Please enter a valid Safaricom number." Payment is not initiated.

**Status:** [ ] Pass [ ] Fail [ ] Blocked

---

### TC-003 — Checkout with Empty Cart

| Field | Details |
|---|---|
| **Feature** | Cart — Edge Case |
| **Scenario** | User navigates directly to checkout with an empty cart |
| **Priority** | Medium |
| **Severity** | Low |

**Preconditions:**
- User is logged in
- Cart is empty

**Steps:**
1. Navigate directly to /checkout
2. Observe behaviour

**Expected Result:** User is redirected to the cart page with a message — "Your cart is empty."

**Status:** [ ] Pass [ ] Fail [ ] Blocked

---

### TC-004 — Checkout as Guest (Unauthenticated User)

| Field | Details |
|---|---|
| **Feature** | Authentication — Checkout Gate |
| **Scenario** | Unauthenticated user attempts to access checkout |
| **Priority** | High |
| **Severity** | High |

**Preconditions:**
- User is NOT logged in

**Steps:**
1. Add an item to cart
2. Click "Proceed to Checkout"

**Expected Result:** User is redirected to the login page. After login, they are returned to checkout with cart intact.

**Status:** [ ] Pass [ ] Fail [ ] Blocked

---

### TC-005 — M-Pesa Payment Timeout

| Field | Details |
|---|---|
| **Feature** | Payment — Error Handling |
| **Scenario** | User does not confirm M-Pesa prompt within the timeout window |
| **Priority** | High |
| **Severity** | High |

**Preconditions:**
- User is logged in
- At least 1 item in cart
- Valid Safaricom number entered

**Steps:**
1. Proceed to checkout
2. Select M-Pesa and enter valid number
3. Click "Pay Now"
4. Do NOT confirm the M-Pesa prompt — let it expire

**Expected Result:** User sees a timeout error message. Order is NOT created. User can retry payment without losing cart.

**Status:** [ ] Pass [ ] Fail [ ] Blocked

---

### TC-006 — Order History Updated After Successful Purchase

| Field | Details |
|---|---|
| **Feature** | Order Management |
| **Scenario** | Completed order appears in user's order history |
| **Priority** | Medium |
| **Severity** | Medium |

**Preconditions:**
- User has completed a successful checkout (TC-001 passed)

**Steps:**
1. Navigate to Profile → Order History
2. Locate the most recent order

**Expected Result:** Order appears with correct items, total amount, date, and status — "Confirmed"

**Status:** [ ] Pass [ ] Fail [ ] Blocked

---

### TC-007 — Add to Cart — Out of Stock Item

| Field | Details |
|---|---|
| **Feature** | Cart — Inventory |
| **Scenario** | User attempts to add an out-of-stock item to cart |
| **Priority** | Medium |
| **Severity** | Medium |

**Preconditions:**
- An out-of-stock product exists in the catalog

**Steps:**
1. Navigate to an out-of-stock product page
2. Attempt to click "Add to Cart"

**Expected Result:** "Add to Cart" button is disabled or hidden. A message displays — "This item is no longer available."

**Status:** [ ] Pass [ ] Fail [ ] Blocked

---

### TC-008 — Google OAuth Login then Checkout

| Field | Details |
|---|---|
| **Feature** | Authentication + Checkout |
| **Scenario** | User logs in via Google OAuth and proceeds to checkout |
| **Priority** | High |
| **Severity** | High |

**Preconditions:**
- User has a valid Google account
- User is not currently logged in

**Steps:**
1. Click "Login with Google"
2. Complete Google OAuth flow
3. Add an item to cart
4. Proceed to checkout

**Expected Result:** User is authenticated, cart is functional, checkout proceeds normally.

**Status:** [ ] Pass [ ] Fail [ ] Blocked

---

## Bug Reports

---

### BUG-001 — Payment Success Page Loads on M-Pesa Timeout

| Field | Details |
|---|---|
| **Bug ID** | BUG-001 |
| **Feature** | Checkout — Payment |
| **Severity** | High |
| **Priority** | High |
| **Status** | Open |

**Title:** Order confirmation page loads even when M-Pesa payment times out

**Steps to Reproduce:**
1. Add item to cart and proceed to checkout
2. Enter valid M-Pesa number
3. Click "Pay Now"
4. Do NOT confirm the M-Pesa STK push — let it expire
5. Observe the page after timeout

**Expected:** Timeout error message shown. No order created.

**Actual:** Order confirmation page loads as if payment was successful. Order appears in history but payment was never received.

**Impact:** Customer receives confirmation but payment fails — revenue loss and inventory confusion.

---

### BUG-002 — Cart Count Does Not Update After Item Removed

| Field | Details |
|---|---|
| **Bug ID** | BUG-002 |
| **Feature** | Cart — UI |
| **Severity** | Low |
| **Priority** | Medium |
| **Status** | Open |

**Title:** Cart icon count in navbar does not decrease after removing an item

**Steps to Reproduce:**
1. Add 2 items to cart — navbar shows count of 2
2. Open cart and remove 1 item
3. Observe navbar cart icon

**Expected:** Cart count updates to 1

**Actual:** Cart count still shows 2 until page is refreshed

**Impact:** UI inconsistency — confusing for users but no functional data loss.

---

### BUG-003 — Search Returns No Results for Partial Category Names

| Field | Details |
|---|---|
| **Bug ID** | BUG-003 |
| **Feature** | Product Search |
| **Severity** | Medium |
| **Priority** | Medium |
| **Status** | Open |

**Title:** Searching "dress" returns no results despite dresses existing in catalog

**Steps to Reproduce:**
1. Navigate to the product catalog
2. Type "dress" in the search bar
3. Observe results

**Expected:** Products in the "Dresses" category are returned

**Actual:** No results found — search only matches exact category name "Dresses", not partial strings

**Impact:** Users can't find products intuitively — likely affects conversion rate.
