---
description: Review test code for quality, best practices, and maintainability
---

You are reviewing Playwright TypeScript test code for a UI automation project.

## Your Task

Perform a comprehensive code review of the specified test file(s) or the entire test suite, focusing on:

### 1. Code Quality & Best Practices
- Verify proper use of Page Object Model (POM) pattern
- Check for test isolation and independence
- Ensure proper async/await usage
- Validate TypeScript typing and type safety
- Check for code duplication and suggest refactoring opportunities

### 2. Test Structure
- Verify test organization (smoke, regression, e2e levels)
- Check proper use of test tags (@smoke, @regression, etc.)
- Validate test naming conventions and clarity
- Ensure proper use of beforeEach/afterEach hooks

### 3. Assertions & Reliability
- Check for proper assertions and expectations
- Verify waiting strategies (avoid hardcoded waits)
- Ensure tests are not flaky
- Validate error handling

### 4. Maintainability
- Check for proper comments and documentation
- Verify locator strategies are robust
- Ensure configuration is externalized
- Check test data management

### 5. Performance
- Verify parallel execution compatibility
- Check for unnecessary waits or delays
- Ensure proper test cleanup

## Output Format

Provide your review in the following structure:

1. **Summary**: Overall assessment of the code quality
2. **Strengths**: What is done well
3. **Issues Found**: Categorized by severity (Critical, High, Medium, Low)
4. **Recommendations**: Specific actionable improvements with code examples
5. **Best Practices Applied**: List of best practices already followed
6. **Best Practices Missing**: List of best practices that should be applied

Include file paths and line numbers for all findings.
