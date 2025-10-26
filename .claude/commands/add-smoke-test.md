---
description: Create a new smoke test for critical functionality
---

You are creating a smoke test for a UI automation project using Playwright and TypeScript.

## Context

Smoke tests are quick, critical path tests that verify the basic functionality of the application. They should:
- Execute quickly (ideally < 2 minutes for the entire smoke suite)
- Cover only the most critical user workflows
- Run on every build/commit
- Fail fast if fundamental issues exist

## Your Task

Create a new smoke test based on the user's requirements. Follow these guidelines:

### 1. Test Structure
- Place the test in the appropriate location: `tests/smoke/`
- Use descriptive test names that clearly indicate what is being tested
- Tag the test with `@smoke` for easy filtering
- Keep the test focused on a single critical workflow

### 2. Implementation Requirements
- Use existing Page Object Models from `pages/` directory
- If POM doesn't exist, create it following the established pattern
- Implement proper test isolation (independent of other tests)
- Use proper waiting strategies (no hardcoded waits)
- Include meaningful assertions at each critical step

### 3. Code Quality
- Add TypeScript types for all variables and parameters
- Include JSDoc comments explaining the test purpose
- Follow the project's naming conventions
- Ensure the test can run in parallel with others

### 4. Common Smoke Test Scenarios
Typical smoke tests for web applications include:
- Homepage loads successfully
- Main navigation is accessible
- Search functionality works
- Critical user flows (login, add to cart, etc.)
- Key pages display correctly
- Essential forms submit successfully

### 5. Test Template

```typescript
import { test, expect } from '@playwright/test';

/**
 * Smoke test: [Brief description of what this test validates]
 *
 * Critical workflow: [Describe the user journey]
 * Expected behavior: [What should happen]
 */
test.describe('Smoke Tests - [Feature Name]', () => {
  test('[Test Name] @smoke', async ({ page }) => {
    // Test implementation
  });
});
```

## Output

Create the test file with:
1. Proper imports and setup
2. Clear test description
3. Well-structured test implementation
4. Appropriate Page Objects (create if needed)
5. Meaningful assertions
6. Proper error messages

Ask clarifying questions if the requirements are not clear before implementing.
