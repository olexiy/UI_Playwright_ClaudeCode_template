---
description: Run tests with specific configurations and generate reports
---

You are helping run Playwright tests for a UI automation project with specific configurations.

## Your Task

Execute tests based on user requirements, using appropriate Playwright commands and configurations.

### Common Test Execution Scenarios

**1. Run Smoke Tests**
```bash
npx playwright test --grep @smoke
```

**2. Run Regression Tests**
```bash
npx playwright test --grep @regression
```

**3. Run Tests by Feature/Area**
```bash
npx playwright test tests/smoke/
npx playwright test tests/regression/feature-name/
```

**4. Run Specific Browser**
```bash
npx playwright test --project=chromium
npx playwright test --project=firefox
npx playwright test --project=webkit
```

**5. Run in Headed Mode (visible browser)**
```bash
npx playwright test --headed
```

**6. Run in Debug Mode**
```bash
npx playwright test --debug
```

**7. Run with Specific Number of Workers**
```bash
npx playwright test --workers=4
```

**8. Run Failed Tests Only**
```bash
npx playwright test --last-failed
```

**9. Run Tests and Generate Reports**
```bash
# Run tests
npx playwright test

# View HTML report
npx playwright show-report

# Generate Allure report (if configured)
npx allure generate ./allure-results -o ./allure-report --clean
npx allure open ./allure-report
```

**10. Run Tests Multiple Times (for flakiness detection)**
```bash
npx playwright test --repeat-each=3
```

**11. Run with Trace**
```bash
npx playwright test --trace on
```

**12. Run Specific Test File**
```bash
npx playwright test tests/smoke/homepage.spec.ts
```

### CI/CD Execution

**For CI environments:**
```bash
# Full regression suite
npx playwright test --grep @regression --reporter=html,json

# Smoke tests for PR validation
npx playwright test --grep @smoke --workers=2

# With retries for stability
npx playwright test --retries=2
```

### Before Running Tests

1. **Check test files exist:**
   - Verify test directory structure
   - Confirm tagged tests are available

2. **Verify configuration:**
   - Check `playwright.config.ts` settings
   - Validate base URL configuration
   - Confirm reporter settings

3. **Environment setup:**
   - Ensure dependencies are installed
   - Check environment variables
   - Verify test data availability

### After Running Tests

1. **Analyze results:**
   - Review test execution summary
   - Check for failures and flaky tests
   - Examine execution time

2. **Generate reports:**
   - Create HTML report
   - Generate Allure report if configured
   - Export JSON results for analysis

3. **Handle failures:**
   - Review failure screenshots
   - Examine trace files
   - Analyze error messages

### Execution Workflow

When the user requests to run tests:

1. **Clarify requirements:**
   - Which test level? (smoke, regression, e2e)
   - Which browser(s)?
   - Headed or headless?
   - Any specific feature area?

2. **Construct command:**
   - Build appropriate npx command
   - Add necessary flags
   - Set reporter options

3. **Execute and monitor:**
   - Run the command
   - Monitor output for errors
   - Capture execution metrics

4. **Report results:**
   - Summarize pass/fail counts
   - Highlight any failures
   - Suggest next steps

5. **Generate reports if requested:**
   - Create HTML reports
   - Generate Allure reports
   - Share report location

## Output

Provide:
1. The exact command(s) to run
2. Expected execution time estimate
3. Results summary after completion
4. Failure analysis if any tests fail
5. Report generation commands if applicable
