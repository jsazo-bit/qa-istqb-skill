# Generate Test Cases - QA Senior ISTQB (Efficient Mode)

## Critical Constraint

Generate the **MINIMUM number of test cases** needed for complete coverage. QA teams need to validate quickly and move to the next project.

**Target:** 3-7 test cases for most features (not 15-20).

---

## Instructions
Using the **QA Senior ISTQB skill**, analyze the provided input and generate **consolidated, efficient test cases** that validate multiple related behaviors per case.

---

## Input Types Accepted

Provide ONE or MORE of:
- ✅ Source code (functions, classes, APIs)
- ✅ Acceptance criteria (user stories, BDD scenarios)
- ✅ Feature specifications
- ✅ UI mockups or wireframes description
- ✅ API documentation
- ✅ Business rules

---

## Output Format

Generate test cases following this structure:

```
**TC-[ID]**: [Clear title covering all validations]
**Priority**: [Critical/High/Medium/Low]
**Validates**: [List 2-4 things this case covers]
**Preconditions**: [If needed]
**Test Data**: [Specific values]
**Steps**:
1. [Specific action]
2. [Specific action]
**Expected Result**: [All observable outcomes]
```

---

## Consolidation Rules

### ✅ Consolidate When Possible:
- Related validations in same flow
- Multiple assertions on same operation
- Sequential operations (Create → Read → Update → Delete)
- Boundary values that share similar behavior

### Example:
Instead of 3 separate cases for login validation:
- **1 case**: Login validates credentials + creates session + redirects + shows welcome message

---

## Coverage Requirements (Prioritized)

Generate cases covering:
1. **Critical happy path** (1-2 cases) - Main user flow end-to-end
2. **Top 3 negative scenarios** (1-3 cases) - Likely + high-impact failures only
3. **Boundaries** (consolidate in 1-2 cases) - Min/max together when possible
4. **Edge cases** (1-2 cases max) - Only real production risks

**Skip:**
- Obvious validations (standard email format, required fields with clear validation)
- Low-probability scenarios
- Redundant negative cases

---

## Efficiency Targets by Complexity

- **Simple feature**: 2-3 test cases
- **Medium feature**: 3-5 test cases
- **Complex feature**: 5-8 test cases
- **Critical system**: 8-12 test cases

---

## Examples

### Example 1: Efficient Password Validation

**Input:**
```javascript
function validatePassword(password) {
  if (!password || password.length < 8 || password.length > 50) {
    return { valid: false, error: 'Invalid length' };
  }
  if (!/[A-Z]/.test(password) || !/[a-z]/.test(password) || 
      !/[0-9]/.test(password) || !/[!@#$%^&*]/.test(password)) {
    return { valid: false, error: 'Missing character type' };
  }
  return { valid: true };
}
```

**Output (Consolidated - 4 cases instead of 15):**

```
**TC-PASS-001**: Validate password with all requirements met
**Priority**: High
**Validates**: Valid password acceptance, all character types, length within bounds
**Test Data**: 
- password = "Test123!"
- password = "Valid1Pass!" (10 chars)
- password = "LongPassword123!..." (50 chars)
**Steps**: Call validatePassword() with each test data
**Expected Result**: All return { valid: true }

**TC-PASS-002**: Reject password with length violations
**Priority**: High
**Validates**: Below minimum (< 8), above maximum (> 50)
**Test Data**:
- password = "Test12!" (7 chars)
- password = [51-character valid password]
**Steps**: Call validatePassword() with each test data
**Expected Result**: Both return { valid: false, error: 'Invalid length' }

**TC-PASS-003**: Reject password missing character types
**Priority**: High
**Validates**: Missing uppercase, lowercase, number, or special char
**Test Data**:
- password = "test123!" (no uppercase)
- password = "TEST123!" (no lowercase)
- password = "TestAbc!" (no number)
- password = "Test1234" (no special)
**Steps**: Call validatePassword() with each test data
**Expected Result**: All return { valid: false, error: 'Missing character type' }

**TC-PASS-004**: Handle null/empty edge cases
**Priority**: Critical
**Validates**: Null, undefined, empty string handling
**Test Data**: password = null, undefined, ""
**Steps**: Call validatePassword() with each test data
**Expected Result**: All return { valid: false, error: 'Invalid length' }
```

**Result:** 4 consolidated cases covering full functionality.

---

### Example 2: E-commerce Checkout Flow

**Input:**
```
Feature: Checkout
- User can review cart
- Apply discount code
- Enter shipping address
- Select payment method
- Confirm order
- Receive confirmation email
```

**Output (Consolidated - 3 cases instead of 10+):**

```
**TC-CHECKOUT-001**: Complete successful checkout flow
**Priority**: Critical
**Validates**: Cart review, discount application, address entry, payment, order creation, email
**Preconditions**: Cart has 2 items ($50 total), valid discount code "SAVE10"
**Test Data**:
- Discount: "SAVE10" (10% off)
- Address: "123 Main St, City, 12345"
- Payment: Card ending 4242, CVV 123
**Steps**:
1. Navigate to /checkout
2. Review cart items and total
3. Apply discount code "SAVE10"
4. Enter shipping address
5. Select credit card payment
6. Click "Confirm Order"
**Expected Result**: 
- Discount applied ($5 off, total $45)
- Order created with status "Confirmed"
- Confirmation email sent to user
- Redirected to /order/[id] page

**TC-CHECKOUT-002**: Validate required fields and invalid inputs
**Priority**: High
**Validates**: Missing address, invalid discount, payment validation
**Test Data**:
- Discount: "EXPIRED10"
- Address: empty
- Card: invalid CVV "12"
**Steps**:
1. Go to /checkout
2. Try to apply expired discount "EXPIRED10"
3. Leave address empty
4. Enter invalid CVV "12"
5. Click "Confirm Order"
**Expected Result**:
- Error: "Discount code invalid or expired"
- Error: "Shipping address required"
- Error: "Invalid CVV"
- Order not created

**TC-CHECKOUT-003**: Handle empty cart and payment failures
**Priority**: High
**Validates**: Empty cart prevention, payment gateway rejection
**Test Data**: 
- Scenario 1: Empty cart
- Scenario 2: Payment decline (card 4000000000000002)
**Steps**:
1. Scenario 1: Navigate to /checkout with empty cart
2. Scenario 2: Complete checkout with declined card
**Expected Result**:
- Scenario 1: Redirect to /cart with message "Cart is empty"
- Scenario 2: Error "Payment declined", order status "Failed", email not sent
```

**Result:** 3 cases covering 12+ individual validations.

---

## Constraints (CRITICAL)

- **Minimum cases**: Generate the fewest possible while maintaining coverage
- **Consolidate**: Group related validations (2-4 per case)
- **Prioritize**: Focus on high-risk, high-frequency scenarios
- **No fluff**: No ISTQB explanations, no intros, no conclusions
- **Few questions**: Maximum 2 clarifications, only if blocking

---

## What You'll Get

✅ 3-7 test cases for typical features (not 15-20)
✅ Each case validates 2-4 related behaviors
✅ Fast to execute - QA team can complete in minutes
✅ Full coverage of critical paths
✅ Skips obvious/low-value scenarios
✅ Prioritized by business risk

---

## What You Won't Get

❌ One test case per validation (too granular)
❌ Exhaustive combinatorial testing
❌ Edge cases with low production probability
❌ Duplicate or redundant scenarios
❌ Unnecessary explanations