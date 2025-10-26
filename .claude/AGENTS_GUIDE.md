# Agents Usage Guide

## 🤖 Available Agents

This project includes two specialized autonomous agents that work together to create and maintain high-quality test code.

---

## 1. Test Writer Agent (`test-writer`)

### Purpose
Autonomously researches pages and writes professional, clean Playwright tests using UI testing patterns.

### Capabilities
- ✅ Independent page research using Playwright MCP
- ✅ Creates Page Object Models following best practices
- ✅ Writes comprehensive test suites
- ✅ Generates test fixtures and data
- ✅ Uses slash commands when appropriate
- ✅ Follows project patterns and conventions

### When to Use
- Creating new smoke tests
- Implementing regression test suites
- Building E2E test scenarios
- Generating POMs for new pages
- Researching and documenting page structures

### How to Invoke

In Claude Code:

```
Use the test-writer agent to create smoke tests for product search functionality
```

Or more specifically:

```
Launch test-writer agent to:
1. Research the search functionality
2. Create necessary Page Object Models
3. Write comprehensive smoke tests for search
4. Include edge cases and error handling
```

### What the Agent Will Do

1. **Research Phase**
   - Explores target page using Playwright MCP
   - Identifies elements and interactions
   - Documents findings
   - Plans test scenarios

2. **Implementation Phase**
   - Creates or updates Page Object Models
   - Writes test files with proper structure
   - Generates test data/fixtures if needed
   - Follows all best practices

3. **Reporting Phase**
   - Provides summary of work completed
   - Lists files created/modified
   - Documents research findings
   - Suggests next steps

### Expected Output

```
📝 Test Writing Summary

Target: Product Search Functionality
Test Level: Smoke
Files Created:
- pages/HomePage.ts (MODIFIED)
- pages/SearchResultsPage.ts (NEW)
- tests/smoke/product-search.spec.ts (NEW)

Test Scenarios Covered:
1. Basic product search with valid term
2. Search with no results
3. Search with special characters

Selectors Used:
- Search input: [data-testid="search-input"] (stable, recommended)
- Search button: getByRole('button', { name: 'Search' }) (accessible)

✅ Ready for code review by code-reviewer agent
```

---

## 2. Code Reviewer Agent (`code-reviewer`)

### Purpose
Reviews test code for quality, functionality, and best practices, providing clear recommendations to refine or push to git.

### Capabilities
- ✅ Runs tests to verify functionality
- ✅ Checks code quality and adherence to standards
- ✅ Identifies unnecessary redundancy
- ✅ Validates best practices
- ✅ Provides actionable recommendations
- ✅ Makes push/refine decisions

### When to Use
- After test-writer agent completes work
- Before pushing code to git
- For periodic code quality checks
- When refactoring existing tests
- To validate manual code changes

### How to Invoke

In Claude Code:

```
Use the code-reviewer agent to review the recently created search tests
```

Or more specifically:

```
Launch code-reviewer agent to:
1. Review tests/smoke/product-search.spec.ts
2. Review pages/SearchResultsPage.ts
3. Run the tests to verify functionality
4. Provide push/refine recommendation
```

### What the Agent Will Do

1. **Discovery Phase**
   - Identifies files to review
   - Gathers context from project
   - Understands test level and purpose

2. **Analysis Phase**
   - Reviews functionality and correctness
   - Checks code quality
   - Analyzes redundancy
   - Validates best practices
   - Runs tests

3. **Reporting Phase**
   - Categorizes issues by severity
   - Provides specific fixes
   - Acknowledges strengths
   - Gives clear recommendation

### Expected Output

```
# 🔍 Code Review Report

## 📊 Overview
- **Files Reviewed**: 2
- **Overall Status**: ✅ READY TO PUSH

### Files Reviewed:
1. `pages/SearchResultsPage.ts` - POM
2. `tests/smoke/product-search.spec.ts` - Test

## ✅ Test Execution Results
- **Total Tests**: 3
- **Passed**: 3
- **Duration**: 8.5s
✅ All tests executed successfully

## 💪 Strengths
1. ✅ Excellent selector strategies using data-testid
2. ✅ Comprehensive JSDoc documentation
3. ✅ Proper async/await usage
4. ✅ Clean Page Object Model implementation

## 🐛 Issues Found
### 💡 Medium Priority (Recommended):
1. **Missing edge case** - `tests/smoke/product-search.spec.ts:45`
   - Consider testing search with very long input

## 🎯 Final Recommendation

### Status: ✅ READY TO PUSH TO GIT

**Verdict**: Code meets all quality standards and is production-ready.

**Next Steps**:
```bash
git add pages/SearchResultsPage.ts tests/smoke/product-search.spec.ts
git commit -m "feat: add smoke tests for product search functionality"
git push origin feature/search-tests
```
```

---

## 🔄 Recommended Workflow

### Complete Test Development Workflow

```
┌─────────────────────────────────────┐
│  1. User defines requirements       │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│  2. Launch test-writer agent        │
│     - Research page                 │
│     - Create POMs                   │
│     - Write tests                   │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│  3. test-writer completes work      │
│     Returns: Summary + files        │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│  4. Launch code-reviewer agent      │
│     - Review code quality           │
│     - Run tests                     │
│     - Check best practices          │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│  5. code-reviewer provides verdict  │
│     ✅ Push | ⚠️ Refine | ❌ Fix    │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│  6. Take action based on verdict    │
│     - Push to git (if approved)     │
│     - Refine code (if needed)       │
│     - Fix issues (if critical)      │
└─────────────────────────────────────┘
```

---

## 📋 Usage Examples

### Example 1: Creating Smoke Tests

**User Request:**
```
I need smoke tests for the homepage - navigation, search, and basic layout verification
```

**Step 1: Launch test-writer**
```
Launch test-writer agent to create smoke tests for the homepage covering:
- Navigation menu accessibility
- Search functionality
- Layout and key elements verification
```

**Step 2: Wait for completion**
Agent will:
- Research homepage
- Create/update HomePage POM
- Write smoke tests
- Provide summary

**Step 3: Launch code-reviewer**
```
Launch code-reviewer agent to review the homepage smoke tests
```

**Step 4: Follow recommendation**
Based on verdict, either push to git or refine code.

---

### Example 2: Building Regression Suite

**User Request:**
```
Create comprehensive regression tests for the checkout flow
```

**Step 1: Launch test-writer**
```
Launch test-writer agent to create regression tests for checkout flow:
- Guest checkout
- Registered user checkout
- Multiple payment methods
- Shipping options
- Edge cases and error handling
```

**Step 2: Review**
```
Launch code-reviewer agent to review the checkout regression tests
```

---

### Example 3: Refactoring Existing Tests

**User Request:**
```
Review and refactor the existing product listing tests
```

**Step 1: Direct code-reviewer**
```
Launch code-reviewer agent to:
1. Review tests/regression/products/product-listing.spec.ts
2. Identify refactoring opportunities
3. Check for redundancy
4. Suggest improvements
```

**Step 2: Apply fixes (manual or test-writer)**
Based on recommendations, either:
- Fix manually
- Or launch test-writer to implement recommended changes

---

## 🎯 Agent Collaboration

### Scenario: Complete Feature Testing

**Goal**: Create and validate tests for shopping cart functionality

**Workflow:**

```bash
# Phase 1: Test Creation
User → test-writer agent:
"Create regression tests for shopping cart:
 - Add items
 - Update quantities
 - Remove items
 - Calculate totals
 - Persist cart state"

# test-writer works autonomously:
# ✅ Researches cart page
# ✅ Creates CartPage POM
# ✅ Writes comprehensive tests
# ✅ Creates test fixtures
# ✅ Returns summary

# Phase 2: Code Review
User → code-reviewer agent:
"Review the cart tests created by test-writer"

# code-reviewer works autonomously:
# ✅ Reads all related files
# ✅ Runs the tests
# ✅ Checks quality
# ✅ Provides verdict

# Phase 3: Action
If ✅ READY TO PUSH:
  → Push to git
  → Move to next feature

If ⚠️ NEEDS REFINEMENT:
  → Apply minor fixes
  → Push to git

If ❌ REQUIRES FIXES:
  → Fix critical issues
  → Re-run code-reviewer
```

---

## 🔧 Customization

### Modifying Agent Behavior

Both agents are configured via markdown files in `.claude/agents/`:

- `test-writer.md` - Test writing agent configuration
- `code-reviewer.md` - Code review agent configuration

You can customize:
- Agent instructions
- Quality standards
- Code patterns
- Review criteria
- Output format

**To modify:**
1. Edit the agent file
2. Update instructions
3. Test with agent invocation
4. Iterate as needed

---

## 💡 Best Practices

### Using test-writer Agent

**DO:**
- ✅ Provide clear requirements
- ✅ Specify test level (smoke/regression/e2e)
- ✅ Mention specific features to cover
- ✅ Let agent research independently
- ✅ Review agent's research findings

**DON'T:**
- ❌ Micromanage the research process
- ❌ Skip the code review step
- ❌ Push code without review
- ❌ Provide vague requirements

### Using code-reviewer Agent

**DO:**
- ✅ Always review after test-writer
- ✅ Review before pushing to git
- ✅ Follow the recommendations
- ✅ Use for periodic quality checks
- ✅ Trust the agent's verdict

**DON'T:**
- ❌ Skip the review step
- ❌ Push without addressing critical issues
- ❌ Ignore recommendations
- ❌ Review too frequently (after every tiny change)

---

## 🚀 Quick Start

### First Time Using Agents

1. **Ensure Prerequisites:**
   ```bash
   # MCP server should be installed
   claude mcp list
   # Should show: microsoft/playwright-mcp
   ```

2. **Try test-writer:**
   ```
   Launch test-writer agent to create a simple smoke test for homepage navigation
   ```

3. **Review the output:**
   - Check created files
   - Review research findings
   - Understand the test structure

4. **Try code-reviewer:**
   ```
   Launch code-reviewer agent to review the homepage navigation test
   ```

5. **Follow recommendations:**
   - If approved, push to git
   - If issues found, fix them

---

## 📊 Agent Output Comparison

### test-writer Output Focus
- ✅ What was researched
- ✅ What was created
- ✅ Selectors and strategies used
- ✅ Test scenarios covered
- ✅ Files created/modified

### code-reviewer Output Focus
- ✅ Test execution results
- ✅ Issues found (categorized)
- ✅ Code quality assessment
- ✅ Redundancy analysis
- ✅ Clear recommendation (push/refine/fix)

---

## ⚙️ Advanced Usage

### Parallel Agent Workflow

You can work on multiple features simultaneously:

```bash
# Terminal 1 (Claude Code instance 1)
Launch test-writer agent for search functionality

# Terminal 2 (Claude Code instance 2)
Launch test-writer agent for cart functionality

# Later, review both:
Launch code-reviewer agent to review all recently created tests
```

### Iterative Refinement

```bash
# Iteration 1
test-writer → creates tests
code-reviewer → finds issues
↓
# Iteration 2
test-writer → fixes issues based on review
code-reviewer → re-reviews
↓
# Iteration 3 (if needed)
Manual fixes → specific adjustments
code-reviewer → final review
↓
✅ Push to git
```

---

## 🎓 Learning from Agents

Both agents are educational:

**From test-writer, learn:**
- How to research pages systematically
- Proper POM structure
- Test organization patterns
- Selector strategies
- Code documentation

**From code-reviewer, learn:**
- What makes code high-quality
- Common mistakes to avoid
- Best practices to follow
- When redundancy is beneficial
- How to write maintainable tests

---

## 📞 Troubleshooting

### Agent Not Responding

**Issue**: Agent doesn't start or respond

**Solutions:**
1. Check agent file exists: `.claude/agents/test-writer.md`
2. Verify file format (frontmatter required)
3. Check Claude Code version
4. Restart Claude Code

### Agent Output Incomplete

**Issue**: Agent stops mid-task

**Solutions:**
1. Check for errors in agent output
2. Simplify the request
3. Break into smaller tasks
4. Check available tokens/context

### MCP Server Issues

**Issue**: test-writer can't access Playwright MCP

**Solutions:**
```bash
# Verify MCP installation
claude mcp list

# Reinstall if needed
claude mcp remove microsoft/playwright-mcp
claude mcp add microsoft/playwright-mcp

# Test MCP connection
"Navigate to https://your-app-url.com"
```

---

## ✅ Success Checklist

You're successfully using agents when:

- [ ] test-writer creates comprehensive tests
- [ ] POMs follow project patterns
- [ ] Tests pass on first run
- [ ] code-reviewer provides detailed feedback
- [ ] Clear recommendations are given
- [ ] Code quality improves over time
- [ ] You understand the agent decisions
- [ ] Workflow is efficient and productive

---

## 🎯 Next Steps

1. **Try the agents:**
   ```
   Launch test-writer agent to create your first smoke test
   ```

2. **Review the work:**
   ```
   Launch code-reviewer agent to review what was created
   ```

3. **Iterate and learn:**
   - Observe how agents work
   - Learn from their code
   - Adapt to the workflow

4. **Scale up:**
   - Use for larger features
   - Build complete test suites
   - Maintain high quality standards

---

**Happy testing with autonomous agents!** 🤖✨

---

**Version**: 1.0
**Last Updated**: 2025-10-25
**Maintained by**: Reference Project Template
