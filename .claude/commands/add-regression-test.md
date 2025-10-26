---
description: Create a new regression test for comprehensive functionality validation
---

You are creating a regression test for a UI automation project using Playwright and TypeScript.

## Context

Regression tests are comprehensive tests that validate existing functionality hasn't been broken by new changes. They should:
- Cover edge cases and various scenarios
- Validate both positive and negative flows
- Include data-driven testing where appropriate
- Run on scheduled intervals (nightly, pre-release)
- Provide detailed validation of features

## Your Task

Create a new regression test based on the user's requirements. Follow these guidelines:

### 1. Test Structure
- Place the test in: `tests/regression/[feature-area]/`
- Use descriptive test names indicating the scenario
- Tag with `@regression` and any additional relevant tags
- Organize related tests in describe blocks

### 2. Implementation Requirements
- Use existing Page Object Models from `pages/` directory
- Create new POMs if needed, following project patterns
- Implement test isolation and cleanup
- Use proper waiting strategies
- Include comprehensive assertions
- Add negative test cases where appropriate

### 3. Test Coverage
- Validate happy path thoroughly
- Test edge cases and boundary conditions
- Include error handling scenarios
- Verify data persistence and state changes
- Check accessibility where relevant

### 4. Code Quality
- Add full TypeScript typing
- Include detailed JSDoc comments
- Use test.step() for complex workflows
- Implement proper error messages
- Follow DRY principles

### 5. Data Management
- Use test fixtures for complex data
- Externalize test data when appropriate
- Clean up test data after execution
- Use unique identifiers to avoid conflicts

### 6. Common Regression Test Areas
For web applications, typical regression tests include:
- Feature variations with different options
- Form validation (positive and negative cases)
- Multi-step workflows
- Data persistence across sessions
- Permission and access control
- Search and filtering with various criteria
- Sorting and pagination
- Error handling and recovery
- Cross-browser compatibility scenarios

### 7. Test Template

```typescript
import { test, expect } from '@playwright/test';

/**
 * Regression test: [Feature name]
 *
 * Test scenarios covered:
 * - [Scenario 1]
 * - [Scenario 2]
 * - [Scenario 3]
 *
 * Prerequisites: [Any setup needed]
 * Test data: [Data requirements]
 */
test.describe('Regression Tests - [Feature Name]', () => {

  test.beforeEach(async ({ page }) => {
    // Setup
  });

  test('[Positive scenario] @regression', async ({ page }) => {
    // Test implementation
  });

  test('[Negative scenario] @regression', async ({ page }) => {
    // Test implementation
  });

  test('[Edge case] @regression', async ({ page }) => {
    // Test implementation
  });

  test.afterEach(async ({ page }) => {
    // Cleanup
  });
});
```

## Output

Create the test file with:
1. Comprehensive test coverage
2. Clear documentation
3. Proper error handling
4. Data-driven approaches where beneficial
5. Reusable helper functions if needed
6. Integration with existing framework

Ask clarifying questions if requirements need elaboration before implementing.
