---
description: Set up CI/CD pipeline configuration for Playwright tests
---

You are setting up CI/CD pipeline configuration for a UI automation project using Playwright and TypeScript.

## Your Task

Create or update CI/CD configuration files for automated test execution.

### Supported CI/CD Platforms

1. **GitHub Actions** (`.github/workflows/`)
2. **GitLab CI** (`.gitlab-ci.yml`)
3. **Jenkins** (`Jenkinsfile`)
4. **CircleCI** (`.circleci/config.yml`)
5. **Azure Pipelines** (`azure-pipelines.yml`)

### CI/CD Strategy

**Multi-tier Approach:**

1. **PR Validation (Fast Feedback)**
   - Run smoke tests only
   - Execute on Chromium only
   - Time: < 5 minutes
   - Trigger: Every PR/MR

2. **Nightly Regression (Comprehensive)**
   - Run full regression suite
   - Execute on all browsers
   - Time: < 30 minutes
   - Trigger: Nightly schedule

3. **Pre-Release (Full Validation)**
   - Run all test levels
   - Execute on all browsers and devices
   - Generate comprehensive reports
   - Trigger: Before releases

### GitHub Actions Template

```yaml
name: Playwright Tests

on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main, develop ]
  schedule:
    # Nightly at 2 AM UTC
    - cron: '0 2 * * *'
  workflow_dispatch:

jobs:
  smoke-tests:
    name: Smoke Tests (PR Validation)
    if: github.event_name == 'pull_request'
    timeout-minutes: 10
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Install Playwright Browsers
        run: npx playwright install --with-deps chromium

      - name: Run smoke tests
        run: npx playwright test --grep @smoke --project=chromium

      - name: Upload test results
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: smoke-test-results
          path: |
            playwright-report/
            test-results/
          retention-days: 7

  regression-tests:
    name: Regression Tests (All Browsers)
    if: github.event_name == 'push' || github.event_name == 'schedule'
    timeout-minutes: 60
    runs-on: ubuntu-latest
    strategy:
      fail-fast: false
      matrix:
        browser: [chromium, firefox, webkit]
    steps:
      - uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Install Playwright Browsers
        run: npx playwright install --with-deps ${{ matrix.browser }}

      - name: Run regression tests
        run: npx playwright test --grep @regression --project=${{ matrix.browser }}

      - name: Generate Allure Report
        if: always()
        run: |
          npm install -g allure-commandline
          allure generate ./allure-results -o ./allure-report --clean

      - name: Upload Playwright Report
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: playwright-report-${{ matrix.browser }}
          path: playwright-report/
          retention-days: 30

      - name: Upload Allure Report
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: allure-report-${{ matrix.browser }}
          path: allure-report/
          retention-days: 30

      - name: Upload Test Results
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: test-results-${{ matrix.browser }}
          path: test-results/
          retention-days: 30

  publish-report:
    name: Publish Test Report
    if: always()
    needs: [regression-tests]
    runs-on: ubuntu-latest
    steps:
      - name: Download Allure Reports
        uses: actions/download-artifact@v4
        with:
          pattern: allure-report-*
          merge-multiple: true

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./allure-report
```

### GitLab CI Template

```yaml
stages:
  - test
  - report

variables:
  npm_config_cache: "$CI_PROJECT_DIR/.npm"
  PLAYWRIGHT_BROWSERS_PATH: "$CI_PROJECT_DIR/ms-playwright"

cache:
  paths:
    - .npm
    - node_modules
    - ms-playwright

smoke-tests:
  stage: test
  image: mcr.microsoft.com/playwright:v1.40.0-jammy
  rules:
    - if: '$CI_PIPELINE_SOURCE == "merge_request_event"'
  script:
    - npm ci
    - npx playwright test --grep @smoke --project=chromium
  artifacts:
    when: always
    paths:
      - playwright-report/
      - test-results/
    expire_in: 1 week

regression-chromium:
  stage: test
  image: mcr.microsoft.com/playwright:v1.40.0-jammy
  rules:
    - if: '$CI_PIPELINE_SOURCE == "schedule"'
    - if: '$CI_COMMIT_BRANCH == "main"'
  script:
    - npm ci
    - npx playwright test --grep @regression --project=chromium
  artifacts:
    when: always
    paths:
      - playwright-report/
      - allure-results/
    expire_in: 30 days

regression-firefox:
  stage: test
  image: mcr.microsoft.com/playwright:v1.40.0-jammy
  rules:
    - if: '$CI_PIPELINE_SOURCE == "schedule"'
    - if: '$CI_COMMIT_BRANCH == "main"'
  script:
    - npm ci
    - npx playwright test --grep @regression --project=firefox
  artifacts:
    when: always
    paths:
      - playwright-report/
      - allure-results/
    expire_in: 30 days

generate-report:
  stage: report
  image: node:20
  rules:
    - if: '$CI_PIPELINE_SOURCE == "schedule"'
    - if: '$CI_COMMIT_BRANCH == "main"'
  dependencies:
    - regression-chromium
    - regression-firefox
  script:
    - npm install -g allure-commandline
    - allure generate ./allure-results -o ./allure-report --clean
  artifacts:
    paths:
      - allure-report/
    expire_in: 30 days
```

### Best Practices

1. **Parallel Execution**
   - Use matrix strategy for browsers
   - Run independent tests concurrently
   - Optimize worker count

2. **Caching**
   - Cache node_modules
   - Cache Playwright browsers
   - Cache npm dependencies

3. **Artifact Management**
   - Upload test results
   - Store screenshots and videos
   - Preserve trace files
   - Set appropriate retention

4. **Notifications**
   - Alert on failures
   - Send reports to Slack/Teams
   - Email summaries

5. **Retry Logic**
   - Retry flaky tests (max 2 retries)
   - Don't mask real failures
   - Track retry rates

6. **Security**
   - Use secrets for credentials
   - Don't expose sensitive data
   - Secure environment variables

## Output

Provide:
1. Complete CI/CD configuration file
2. Setup instructions
3. Required secrets/variables list
4. Testing strategy documentation
5. Troubleshooting guide
6. Badge configuration for README

Ask user to specify:
- Which CI/CD platform to use
- Desired test execution strategy
- Report hosting preferences
- Notification requirements
