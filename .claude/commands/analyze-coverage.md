---
description: Analyze test coverage and identify gaps in test automation
---

You are analyzing test coverage for a UI automation project using Playwright and TypeScript.

## Your Task

Perform a comprehensive analysis of test coverage to identify tested areas and gaps in automation.

### 1. Coverage Analysis Areas

**Functional Coverage:**
- Core user journeys
- Feature completeness
- User workflows
- Critical business functions

**Test Level Coverage:**
- Smoke tests (critical path)
- Regression tests (comprehensive scenarios)
- E2E tests (complete user journeys)
- Negative tests (error handling)
- Edge cases and boundary conditions

**Browser Coverage:**
- Chromium-based browsers
- Firefox
- WebKit (Safari)
- Mobile viewports

**Technical Coverage:**
- Page Objects created vs. needed
- Test data management
- Error handling scenarios
- Performance considerations

### 2. Analysis Process

**Step 1: Inventory Existing Tests**
- List all test files and their purpose
- Count tests by level (smoke, regression, e2e)
- Map tests to features/user journeys
- Identify test tags and organization

**Step 2: Identify Feature Coverage**
Based on application functionality:
- Core features and their test coverage
- User workflows and scenarios
- API integrations
- Third-party services
- Authentication and authorization

**Step 3: Calculate Coverage Metrics**
- Percentage of critical paths covered
- Smoke test coverage (should be ~20-30% of features)
- Regression test coverage (should be ~70-80% of features)
- Negative test scenarios coverage

**Step 4: Gap Analysis**
- Features without any tests
- Features with insufficient test coverage
- Missing negative test scenarios
- Untested edge cases
- Missing cross-browser tests

### 3. Coverage Report Format

```markdown
# Test Coverage Analysis Report

## Executive Summary
- Total Tests: [count]
- Smoke Tests: [count]
- Regression Tests: [count]
- E2E Tests: [count]
- Overall Coverage: [percentage]

## Coverage by Feature Area

### 1. [Feature Name]
- Status: ✅ Well Covered / ⚠️ Partial / ❌ Not Covered
- Smoke Tests: [count]
- Regression Tests: [count]
- Gaps: [list of missing scenarios]

## Coverage by Test Level

### Smoke Tests (Critical Path)
**Covered:**
- [Feature 1]
- [Feature 2]

**Missing:**
- [Feature X]
- [Feature Y]

### Regression Tests (Comprehensive)
**Covered:**
- [Feature 1]
- [Feature 2]

**Missing:**
- [Feature X]
- [Feature Y]

## Critical Gaps

### High Priority (P0)
1. [Gap description]
   - Impact: [why this is critical]
   - Recommendation: [what to test]

### Medium Priority (P1)
1. [Gap description]

### Low Priority (P2)
1. [Gap description]

## Page Object Coverage
- POMs Created: [count]
- POMs Needed: [count]
- Missing POMs: [list]

## Recommendations

1. **Immediate Actions**
   - [Action 1]
   - [Action 2]

2. **Short-term Improvements**
   - [Action 1]
   - [Action 2]

3. **Long-term Strategy**
   - [Action 1]
   - [Action 2]

## Test Distribution Analysis
- Smoke: [percentage]% (Target: 20-30%)
- Regression: [percentage]% (Target: 60-70%)
- E2E: [percentage]% (Target: 10-20%)
```

### 4. Key Metrics to Calculate

1. **Feature Coverage Rate**
   ```
   (Features with tests / Total features) × 100
   ```

2. **Critical Path Coverage**
   ```
   (Critical paths tested / Total critical paths) × 100
   ```

3. **Test Level Distribution**
   ```
   Smoke vs Regression vs E2E ratio
   ```

4. **Browser Coverage**
   ```
   Tests running on multiple browsers
   ```

### 5. Analysis Tools

**Manual Analysis:**
- Review test file structure
- Count tests by grep patterns
- Map tests to requirements

**Automated Analysis:**
```bash
# Count tests by tag
npx playwright test --list --grep @smoke
npx playwright test --list --grep @regression

# List all test files
find tests -name "*.spec.ts"

# Count total tests
grep -r "test(" tests/ | wc -l
```

## Output

Provide:
1. Comprehensive coverage report
2. Visual representation (if helpful)
3. Prioritized gap list
4. Specific recommendations with examples
5. Action plan for improving coverage
6. Timeline estimates for filling gaps

Include file references and specific feature areas in your analysis.
