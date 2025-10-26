---
description: Generate and view test execution reports (HTML and Allure)
---

You are helping generate and manage test execution reports for a Playwright TypeScript automation project.

## Your Task

Generate test reports based on user requirements, using Playwright's built-in HTML reporter and/or Allure reporter.

## Reporting Options

### 1. Playwright HTML Reporter (Built-in)

**Generate Report:**
```bash
# Reports are auto-generated after test run
npx playwright test

# View the report
npx playwright show-report
```

**Features:**
- ✅ Built-in, no extra configuration needed
- ✅ Interactive HTML report
- ✅ Screenshots and videos on failure
- ✅ Trace viewer integration
- ✅ Test duration metrics
- ✅ Filterable results

**Configuration** (`playwright.config.ts`):
```typescript
export default defineConfig({
  reporter: [
    ['html', {
      outputFolder: 'playwright-report',
      open: 'never' // 'always', 'never', 'on-failure'
    }]
  ]
});
```

### 2. Allure Reporter (Recommended for Advanced Reporting)

**Installation:**
```bash
npm install --save-dev allure-playwright allure-commandline
```

**Configuration** (`playwright.config.ts`):
```typescript
export default defineConfig({
  reporter: [
    ['line'], // Console output
    ['html'], // Built-in HTML
    ['allure-playwright', {
      outputFolder: 'allure-results',
      detail: true,
      suiteTitle: true
    }]
  ]
});
```

**Generate and View Report:**
```bash
# Run tests (generates allure-results)
npx playwright test

# Generate HTML report from results
npx allure generate ./allure-results -o ./allure-report --clean

# Open report in browser
npx allure open ./allure-report

# Or generate and open in one command
npx allure serve ./allure-results
```

**Advanced Allure Features:**
```typescript
import { test, expect } from '@playwright/test';
import { allure } from 'allure-playwright';

test('example test with Allure annotations', async ({ page }) => {
  // Add metadata
  await allure.epic('E-commerce');
  await allure.feature('Product Search');
  await allure.story('User searches for products');
  await allure.severity('critical');
  await allure.owner('QA Team');

  // Add steps
  await allure.step('Navigate to homepage', async () => {
    await page.goto('/');
  });

  await allure.step('Perform search', async () => {
    await page.fill('[data-testid="search"]', 'test query');
    await page.click('[data-testid="search-button"]');
  });

  // Attach screenshots
  const screenshot = await page.screenshot();
  await allure.attachment('Search Results', screenshot, 'image/png');
});
```

### 3. Multiple Reporters (Recommended Setup)

**Configuration:**
```typescript
export default defineConfig({
  reporter: [
    ['list'], // Console output during test run
    ['html', { outputFolder: 'html-report' }],
    ['json', { outputFile: 'test-results.json' }],
    ['junit', { outputFile: 'junit-results.xml' }],
    ['allure-playwright', { outputFolder: 'allure-results' }]
  ]
});
```

## Report Analysis Commands

### After Test Execution

**View Built-in HTML Report:**
```bash
npx playwright show-report
```

**Generate Allure Report:**
```bash
# Clean previous reports
rm -rf allure-report

# Generate new report
npx allure generate ./allure-results -o ./allure-report --clean

# Open in browser
npx allure open ./allure-report
```

**Analyze Test Results:**
```bash
# View JSON results
cat test-results.json | jq '.suites[].specs[].tests[]'

# Count passed/failed
cat test-results.json | jq '.stats'

# Find failed tests
cat test-results.json | jq '.suites[].specs[] | select(.tests[].results[].status == "failed")'
```

## CI/CD Report Generation

### GitHub Actions Example

```yaml
- name: Run Playwright tests
  run: npx playwright test

- name: Generate Allure Report
  if: always()
  run: |
    npm install -g allure-commandline
    allure generate ./allure-results -o ./allure-report --clean

- name: Upload HTML Report
  if: always()
  uses: actions/upload-artifact@v4
  with:
    name: playwright-report
    path: playwright-report/

- name: Upload Allure Report
  if: always()
  uses: actions/upload-artifact@v4
  with:
    name: allure-report
    path: allure-report/

- name: Deploy to GitHub Pages
  if: always()
  uses: peaceiris/actions-gh-pages@v3
  with:
    github_token: ${{ secrets.GITHUB_TOKEN }}
    publish_dir: ./allure-report
```

## Report Hosting Options

### 1. GitHub Pages
```bash
# Configure GitHub Pages in repository settings
# Reports auto-deployed via GitHub Actions
# Access at: https://username.github.io/repo-name/
```

### 2. Allure Server (Self-hosted)
```bash
# Install Allure Server
docker pull frankescobar/allure-docker-service

# Run server
docker run -p 5050:5050 \
  -v ${PWD}/allure-results:/app/allure-results \
  frankescobar/allure-docker-service
```

### 3. Local Viewing
```bash
# Playwright HTML
npx playwright show-report

# Allure (temporary server)
npx allure serve ./allure-results
```

## Report Customization

### Custom Allure Categories

Create `allure-results/categories.json`:
```json
[
  {
    "name": "Product defects",
    "matchedStatuses": ["failed"],
    "messageRegex": ".*product.*"
  },
  {
    "name": "Test defects",
    "matchedStatuses": ["broken"]
  },
  {
    "name": "Flaky tests",
    "matchedStatuses": ["passed", "failed"],
    "messageRegex": ".*flaky.*"
  }
]
```

### Custom Playwright HTML Report

Create `playwright.config.ts`:
```typescript
export default defineConfig({
  reporter: [
    ['html', {
      outputFolder: 'custom-report',
      open: 'never',
      host: 'localhost',
      port: 9323,
    }]
  ]
});
```

## Troubleshooting

### Issue: Reports not generating

**Solution:**
```bash
# Check reporter configuration
cat playwright.config.ts | grep reporter

# Ensure output directories exist
mkdir -p playwright-report allure-results allure-report

# Run tests with verbose logging
DEBUG=pw:api npx playwright test
```

### Issue: Allure command not found

**Solution:**
```bash
# Install globally
npm install -g allure-commandline

# Or use npx
npx allure --version

# Or add to package.json scripts
"scripts": {
  "allure:generate": "allure generate ./allure-results -o ./allure-report --clean",
  "allure:open": "allure open ./allure-report"
}
```

### Issue: Old reports showing

**Solution:**
```bash
# Clean all reports
rm -rf playwright-report allure-results allure-report test-results.json

# Re-run tests
npx playwright test

# Generate fresh reports
npx allure generate ./allure-results -o ./allure-report --clean
```

## Best Practices

1. **Multiple Reporters**: Use both HTML and Allure for different purposes
   - HTML for quick local viewing
   - Allure for detailed analysis and sharing

2. **CI/CD Integration**: Always generate reports in CI/CD pipeline
   - Upload as artifacts
   - Host on GitHub Pages or similar

3. **Report Retention**: Configure retention policies
   - Keep recent reports (last 30 days)
   - Archive important releases

4. **Metadata**: Add Allure annotations for better organization
   - Epic, Feature, Story
   - Severity, Owner
   - Links to requirements

5. **Screenshots/Videos**: Configure appropriately
   - on-failure for CI (saves space)
   - on for debugging
   - off for fast smoke tests

## Workflow

When user requests report generation:

1. **Clarify Requirements:**
   - Which reporter? (HTML, Allure, or both)
   - Local or CI/CD?
   - Any specific filters or tests?

2. **Provide Commands:**
   - Exact commands to run
   - Expected output location
   - How to view results

3. **Explain Results:**
   - Where to find reports
   - How to interpret results
   - Next steps if failures found

## Output

Provide:
1. Exact commands to generate reports
2. Location of generated reports
3. How to view/open reports
4. Summary of results (if tests were run)
5. Recommendations for improvements
