---
description: Debug a failing test and provide troubleshooting guidance
---

You are debugging a failing Playwright test for a UI automation project.

## Your Task

Analyze test failures and provide comprehensive debugging guidance and fixes.

### 1. Initial Analysis

When a test fails, gather the following information:

**Test Information:**
- Test name and file location
- Test type (smoke, regression, e2e)
- Browser and environment
- Failure frequency (always fails, intermittent, flaky)

**Error Information:**
- Error message and stack trace
- Failed assertion or action
- Screenshots and videos if available
- Trace files if enabled

### 2. Common Failure Categories

**Timing Issues:**
- Element not found
- Element not visible/clickable
- Stale element references
- Race conditions

**Selector Issues:**
- Invalid or outdated selectors
- Dynamic IDs or attributes
- Shadow DOM elements
- iframes

**State Issues:**
- Test data conflicts
- Session/cookie problems
- Cache issues
- Previous test contamination

**Environmental Issues:**
- Network problems
- API failures
- Third-party service issues
- Configuration problems

**Logic Issues:**
- Incorrect assertions
- Wrong test flow
- Missing preconditions
- Invalid test data

### 3. Debugging Steps

**Step 1: Reproduce the Failure**
```bash
# Run the specific test
npx playwright test path/to/test.spec.ts --headed

# Run with debug mode
npx playwright test path/to/test.spec.ts --debug

# Run with trace
npx playwright test path/to/test.spec.ts --trace on
```

**Step 2: Analyze Artifacts**
- Review screenshots from failure
- Watch video recording
- Examine trace file
- Check console logs

**Step 3: Isolate the Issue**
- Run test in isolation
- Check if it fails consistently
- Test on different browsers
- Verify test data

**Step 4: Investigate Root Cause**
- Examine the page at failure point
- Check element visibility
- Validate selectors
- Review recent code changes

### 4. Common Fixes

**For Timing Issues:**
```typescript
// ❌ Bad - hardcoded wait
await page.waitForTimeout(5000);

// ✅ Good - wait for specific condition
await page.waitForSelector('[data-testid="element"]', { state: 'visible' });
await expect(page.locator('[data-testid="element"]')).toBeVisible();

// ✅ Better - use Playwright's auto-waiting
await page.click('[data-testid="button"]'); // Auto-waits for actionability
```

**For Selector Issues:**
```typescript
// ❌ Bad - fragile selector
await page.click('#content > div.container > button:nth-child(3)');

// ✅ Good - use data-testid
await page.click('[data-testid="submit-button"]');

// ✅ Better - use role and accessible name
await page.getByRole('button', { name: 'Submit' }).click();

// ✅ For text content
await page.getByText('Add to Cart').click();
```

**For State Issues:**
```typescript
// ✅ Add proper cleanup
test.afterEach(async ({ page, context }) => {
  // Clear cookies
  await context.clearCookies();

  // Clear local storage
  await page.evaluate(() => localStorage.clear());

  // Clear session storage
  await page.evaluate(() => sessionStorage.clear());
});

// ✅ Use unique test data
const uniqueEmail = `test-${Date.now()}@example.com`;
```

**For Flaky Tests:**
```typescript
// ✅ Add retries for specific tests
test.describe('Flaky Feature', () => {
  test.describe.configure({ retries: 2 });

  test('flaky test', async ({ page }) => {
    // Test implementation
  });
});

// ✅ Use test.step for better debugging
test('complex flow', async ({ page }) => {
  await test.step('Step 1: Login', async () => {
    // Login logic
  });

  await test.step('Step 2: Add to cart', async () => {
    // Add to cart logic
  });
});
```

**For Network Issues:**
```typescript
// ✅ Wait for network to be idle
await page.goto('https://your-app-url.com');
await page.waitForLoadState('networkidle');

// ✅ Wait for specific API call
await page.waitForResponse(response =>
  response.url().includes('/api/products') && response.status() === 200
);

// ✅ Mock unstable endpoints
await page.route('**/api/analytics', route => route.fulfill({ status: 200 }));
```

### 5. Advanced Debugging Techniques

**Using Playwright Inspector:**
```bash
npx playwright test --debug
```

**Using Trace Viewer:**
```bash
npx playwright test --trace on
npx playwright show-trace trace.zip
```

**Using Console Logs:**
```typescript
// Add debugging logs
page.on('console', msg => console.log('PAGE LOG:', msg.text()));
page.on('pageerror', error => console.log('PAGE ERROR:', error));

// Log network requests
page.on('request', request => console.log('REQUEST:', request.url()));
page.on('response', response => console.log('RESPONSE:', response.url(), response.status()));
```

**Using Soft Assertions:**
```typescript
// Continue test even if assertion fails
await expect.soft(page.locator('.optional-element')).toBeVisible();
await expect.soft(page.locator('.another-element')).toHaveText('Expected');

// Final assertion to fail the test if any soft assertions failed
await expect(page.locator('.critical-element')).toBeVisible();
```

### 6. Prevention Strategies

1. **Make selectors resilient:**
   - Use data-testid attributes
   - Prefer role-based selectors
   - Avoid CSS nth-child selectors

2. **Ensure test isolation:**
   - Clean up after each test
   - Use unique test data
   - Don't depend on test execution order

3. **Add proper waits:**
   - Use Playwright's auto-waiting
   - Add explicit waits for specific conditions
   - Avoid hardcoded timeouts

4. **Improve error messages:**
   - Use descriptive assertions
   - Add context to failures
   - Include relevant test data

5. **Enable tracing for CI:**
   - Enable trace on first retry
   - Store traces as artifacts
   - Review traces for failures

## Output

Provide:
1. **Root Cause Analysis:** Explain why the test is failing
2. **Fix Implementation:** Provide exact code changes needed
3. **Prevention:** Suggest how to prevent similar issues
4. **Testing:** Explain how to verify the fix works
5. **Documentation:** Update test comments if needed

Include file paths and line numbers for all changes.
