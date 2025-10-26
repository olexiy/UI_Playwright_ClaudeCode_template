# Playwright TypeScript UI Test Automation Template

> A professional, reference-quality template for Playwright + TypeScript UI test automation projects with Claude Code integration.

[![Playwright](https://img.shields.io/badge/Playwright-v1.40+-green.svg)](https://playwright.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-v5.0+-blue.svg)](https://www.typescriptlang.org/)
[![Allure](https://img.shields.io/badge/Allure-Reports-orange.svg)](https://allurereport.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Quick Start](#quick-start)
- [Project Structure](#project-structure)
- [Claude Code Integration](#claude-code-integration)
- [Test Levels](#test-levels)
- [Reporting](#reporting)
- [Best Practices](#best-practices)
- [CI/CD Integration](#cicd-integration)
- [Documentation](#documentation)

## 🎯 Overview

This is a **production-ready** template for creating professional UI test automation projects using Playwright and TypeScript. It includes comprehensive Claude Code configuration with slash commands and autonomous agents to accelerate development.

### Purpose

- 🎓 **Production Template**: Ready-to-use template for real projects
- 🏆 **Best Practices**: Industry-standard patterns and conventions
- 🤖 **AI-Enhanced**: Claude Code commands and agents for productivity
- 📚 **Well-Documented**: Comprehensive guides and examples

### Technology Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| Playwright | 1.40+ | Test automation framework |
| TypeScript | 5.0+ | Programming language |
| Node.js | 20+ | Runtime environment |
| Allure | 2.15+ | Advanced test reporting |
| ESLint | 8.50+ | Code linting |
| Prettier | 3.0+ | Code formatting |

## ✨ Features

### Test Automation Features
- ✅ Multi-level testing strategy (Smoke, Regression, E2E)
- ✅ Page Object Model design pattern
- ✅ Component-based architecture
- ✅ Custom test fixtures and builders
- ✅ Data-driven testing support
- ✅ Cross-browser testing (Chromium, Firefox, WebKit)
- ✅ Parallel test execution
- ✅ Screenshot and video capture on failure
- ✅ Test retry mechanism for stability

### Reporting Features
- ✅ Built-in Playwright HTML reporter
- ✅ Allure advanced reporting with:
  - Epic/Feature/Story organization
  - Severity levels
  - Test steps visualization
  - Screenshots and attachments
  - Historical trends
  - Flaky test detection

### Claude Code Integration
- ✅ **9 Slash Commands** for interactive workflows
- ✅ **2 Autonomous Agents** for complex tasks
- ✅ **Playwright MCP integration** for page exploration
- ✅ Automated code reviews
- ✅ Test generation assistance
- ✅ Coverage analysis

### Code Quality Features
- ✅ Full TypeScript type safety
- ✅ ESLint for code quality
- ✅ Prettier for consistent formatting
- ✅ Pre-commit hooks with Husky
- ✅ Comprehensive JSDoc comments

## 🚀 Quick Start

### Prerequisites

- **Node.js** 20+ ([Download](https://nodejs.org/))
- **npm** or **yarn**
- **Git**
- **Claude Code** (optional, for AI-enhanced development)

### Installation

```bash
# Clone this template
git clone <your-repo-url> my-test-project
cd my-test-project

# Install dependencies (create package.json first)
# Use Claude Code command: /setup-project
# Or manually create package.json with Playwright dependencies

npm install

# Install Playwright browsers
npx playwright install

# Verify installation
npx playwright --version
```

### 📚 Code Examples

This template provides a clean foundation without specific application code. **Complete working examples** are available in separate branches:

```bash
# View available example projects
git branch -r | grep examples/

# Checkout a specific example
git checkout examples/e-commerce     # E-commerce testing example
git checkout examples/saas-dashboard # SaaS application example
git checkout examples/basic          # Minimal example
```

**Example branches include:**
- Full Page Object Models
- Complete test suites (smoke, regression, E2E)
- Test data fixtures and utilities
- Working `package.json` and configurations
- Ready-to-run tests

> 💡 **Tip**: Use examples as a reference while building your own tests with Claude Code agents.

### Initial Setup

This template includes pre-configured files to get you started quickly:

**✅ Included configurations:**
- `tsconfig.json` - TypeScript compiler settings
- `.eslintrc.json` - Code quality rules
- `.prettierrc` - Code formatting rules
- `.editorconfig` - Editor settings
- `.vscode/` - VS Code workspace settings
- `.github/workflows/*.disabled` - Example CI/CD workflows

**📝 Files to create:**

1. **Create `package.json`** (use Claude Code agents for latest versions):
   ```bash
   # In Claude Code:
   Launch test-writer agent to setup project with latest Playwright dependencies
   ```

2. **Create `playwright.config.ts`**:
   ```typescript
   import { defineConfig } from '@playwright/test';

   export default defineConfig({
     testDir: './tests',
     use: {
       baseURL: 'https://your-application-url.com',
     },
   });
   ```

3. **Optional: Create `.env` file**:
   ```env
   BASE_URL=https://your-application-url.com
   TEST_ENV=staging
   HEADLESS=true
   ```

### Run Your First Test

```bash
# Run all tests
npm test

# Run smoke tests
npm run test:smoke

# Run in headed mode
npm run test:headed

# View test report
npx playwright show-report
```

## 📁 Project Structure

### Current Template Structure

```
playwright-test-project/
├── .claude/                          # Claude Code configuration
│   ├── commands/                    # 10 interactive slash commands
│   ├── agents/                      # 2 autonomous agents
│   ├── SETUP_GUIDE.md              # Detailed setup instructions
│   ├── PROJECT_PLAN.md             # Project planning guide
│   ├── AGENTS_GUIDE.md             # How to use agents
│   └── MCP_RECOMMENDATIONS.md      # MCP integration guide
│
├── .github/workflows/               # Example CI/CD workflows
│   ├── example-smoke-tests.yml.disabled
│   ├── example-regression-tests.yml.disabled
│   └── example-deploy-reports.yml.disabled
│
├── .vscode/                         # VS Code configuration
│   ├── settings.json               # Workspace settings
│   ├── extensions.json             # Recommended extensions
│   └── launch.json                 # Debug configurations
│
├── .eslintrc.json                  # ESLint rules
├── .prettierrc                     # Prettier formatting
├── .editorconfig                   # Editor configuration
├── tsconfig.json                   # TypeScript settings
├── .gitignore                      # Git ignore rules
├── LICENSE                         # MIT License
└── README.md                       # This file
```

### Recommended Project Structure (After Setup)

```
your-test-project/
├── (all template files above)
├── pages/                     # Page Object Models
│   ├── components/           # Reusable components
│   ├── BasePage.ts          # Base page class
│   └── *.page.ts            # Page classes
│
├── tests/
│   ├── smoke/               # Critical path tests (~20-30%)
│   ├── regression/          # Comprehensive tests (~60-70%)
│   ├── e2e/                 # End-to-end journeys (~10-20%)
│   ├── fixtures/            # Test data & custom fixtures
│   └── utils/               # Helper functions
│
├── playwright.config.ts     # Main configuration
└── package.json            # Dependencies and scripts
```

> 💡 **See example branches** (`examples/*`) for complete working project structures.

## 🤖 Claude Code Integration

### Slash Commands (Interactive)

| Command | Description |
|---------|-------------|
| `/review-tests` | Review test code quality |
| `/add-smoke-test` | Create smoke test |
| `/add-regression-test` | Create regression test |
| `/create-pom` | Create Page Object Model |
| `/run-tests` | Execute tests |
| `/analyze-coverage` | Analyze test coverage |
| `/generate-report` | Generate test reports |
| `/debug-test` | Debug failing tests |
| `/generate-test-data` | Create test fixtures |
| `/setup-ci` | Configure CI/CD |

> 💡 **Tip**: These commands use the latest Playwright versions and best practices automatically.

### Autonomous Agents

**test-writer**: Researches pages, creates POMs, writes professional tests
```
Launch test-writer agent to create smoke tests for user authentication
```

**code-reviewer**: Reviews code, runs tests, provides push/refine verdict
```
Launch code-reviewer agent to review authentication tests
```

### Quick Example

```bash
# In Claude Code:

# Interactive workflow
/create-pom LoginPage
/add-smoke-test

# Autonomous workflow
Launch test-writer agent to create regression tests for checkout flow
Launch code-reviewer agent to review checkout tests
```

## 📊 Test Levels

### Smoke Tests (@smoke)
**When**: Every commit, PR, build
**Duration**: < 5 minutes
**Coverage**: ~20-30% of features

```bash
npm run test:smoke
```

### Regression Tests (@regression)
**When**: Nightly, pre-release
**Duration**: 20-30 minutes
**Coverage**: ~60-70% of features

```bash
npm run test:regression
```

### E2E Tests (@e2e)
**When**: Scheduled (nightly/weekly)
**Duration**: 15-20 minutes
**Coverage**: ~10-20% (complete flows)

```bash
npm run test:e2e
```

## 📈 Reporting

### Playwright HTML Reporter (Built-in)

```bash
# Run tests (auto-generates report)
npx playwright test

# View report
npx playwright show-report
```

### Allure Reporter (Advanced)

```bash
# Run tests
npx playwright test

# Generate Allure report
npm run report:generate

# Open report in browser
npm run report:open
```

### Allure Features

- **Epic/Feature/Story** organization
- **Severity levels** (blocker, critical, normal, minor, trivial)
- **Test steps** visualization
- **Screenshots** and attachments
- **Historical trends**
- **Flaky test** detection
- **Categories** for failure analysis

### Adding Allure Annotations

```typescript
import { test, expect } from '@playwright/test';
import { allure } from 'allure-playwright';

test('user login @smoke', async ({ page }) => {
  // Add metadata
  await allure.epic('Authentication');
  await allure.feature('User Login');
  await allure.story('User can login with valid credentials');
  await allure.severity('critical');
  await allure.owner('QA Team');

  // Add test steps
  await allure.step('Navigate to login page', async () => {
    await page.goto('/login');
  });

  await allure.step('Enter credentials', async () => {
    await page.fill('[data-testid="email"]', 'user@example.com');
    await page.fill('[data-testid="password"]', 'password123');
  });

  await allure.step('Submit login form', async () => {
    await page.click('[data-testid="login-button"]');
  });

  // Assertions
  await expect(page).toHaveURL('/dashboard');
});
```

## ✅ Best Practices

### Test Writing
- ✅ Use descriptive test names
- ✅ One logical assertion per test
- ✅ Test isolation (independent tests)
- ✅ Proper async/await usage
- ✅ No hardcoded waits
- ✅ Use Playwright's auto-waiting

### Page Objects
- ✅ Readonly locators
- ✅ Descriptive method names
- ✅ Return types specified
- ✅ JSDoc comments
- ✅ Single responsibility
- ✅ Component-based for reusable elements

### Code Quality
- ✅ Full TypeScript typing
- ✅ No `any` types
- ✅ ESLint compliant
- ✅ Prettier formatted
- ✅ Comprehensive comments
- ✅ DRY principles

## 🔄 CI/CD Integration

### GitHub Actions

**Example workflows** are included in `.github/workflows/` (with `.disabled` extension):

- `example-smoke-tests.yml.disabled` - PR validation
- `example-regression-tests.yml.disabled` - Nightly runs (multi-browser)
- `example-deploy-reports.yml.disabled` - Deploy to GitHub Pages

**To enable:**
1. Remove `.disabled` extension
2. Update workflow to match your needs
3. Configure GitHub repository settings (Pages, secrets, etc.)

**Example usage:**
```bash
# Rename to activate
mv .github/workflows/example-smoke-tests.yml.disabled .github/workflows/smoke-tests.yml
```

### Other CI Platforms

Templates available for:
- GitLab CI
- Jenkins
- CircleCI
- Azure Pipelines

Use `/setup-ci` command to generate configurations.

## 📚 Documentation

- **[.claude/README.md](.claude/README.md)** - Claude Code configuration overview
- **[.claude/SETUP_GUIDE.md](.claude/SETUP_GUIDE.md)** - Setup instructions
- **[.claude/AGENTS_GUIDE.md](.claude/AGENTS_GUIDE.md)** - Agent usage guide
- **[.claude/PROJECT_PLAN.md](.claude/PROJECT_PLAN.md)** - Project planning template

## 📝 npm Scripts

```json
{
  "test": "playwright test",
  "test:headed": "playwright test --headed",
  "test:debug": "playwright test --debug",
  "test:ui": "playwright test --ui",
  "test:smoke": "playwright test --grep @smoke",
  "test:regression": "playwright test --grep @regression",
  "test:e2e": "playwright test --grep @e2e",
  "report:generate": "allure generate ./allure-results -o ./allure-report --clean",
  "report:open": "allure open ./allure-report",
  "lint": "eslint . --ext .ts",
  "format": "prettier --write \"**/*.{ts,json,md}\"",
  "format:check": "prettier --check \"**/*.{ts,json,md}\""
}
```

## 🤝 Contributing

1. Follow established patterns and conventions
2. Maintain code quality standards
3. Add tests for new features
4. Update documentation
5. Use Claude Code commands for consistency

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

## 🎯 Quick Start Checklist

### Basic Setup
- [ ] Install Node.js 20+
- [ ] Clone template repository
- [ ] Review included configurations (tsconfig, eslint, prettier)
- [ ] Create `package.json` (use Claude Code agents for latest versions)
- [ ] Create `playwright.config.ts`
- [ ] Run `npm install`
- [ ] Run `npx playwright install`

### Claude Code Setup (Optional but Recommended)
- [ ] Install Playwright MCP: `claude mcp add microsoft/playwright-mcp`
- [ ] Try slash commands: `/create-pom`, `/add-smoke-test`
- [ ] Read [.claude/SETUP_GUIDE.md](.claude/SETUP_GUIDE.md)
- [ ] Explore autonomous agents: `Launch test-writer agent`

### Development
- [ ] Check example branches for reference: `git checkout examples/basic`
- [ ] Start building your tests with Claude Code assistance
- [ ] Enable GitHub Actions workflows (remove `.disabled`)
- [ ] Configure VS Code (extensions will be recommended automatically)

---

**Ready to build amazing tests!** 🚀

For detailed guidance, see [.claude/SETUP_GUIDE.md](.claude/SETUP_GUIDE.md) or use Claude Code commands.

---

**Version**: 2.0 - Universal Template
**Last Updated**: 2025-10-26
**Template Status**: ✅ Ready for Production Use

### What's Included

✅ **Configurations**: TypeScript, ESLint, Prettier, EditorConfig
✅ **VS Code**: Workspace settings, recommended extensions, debug configs
✅ **CI/CD**: Example GitHub Actions workflows (disabled by default)
✅ **Claude Code**: 10 slash commands + 2 autonomous agents
✅ **Documentation**: Comprehensive setup guides and best practices
✅ **License**: MIT (free to use)

### What You Need to Add

📝 **package.json** - Use Claude Code agents for latest versions
📝 **playwright.config.ts** - Project-specific configuration
📝 **Tests & Page Objects** - Your application-specific code

💡 **Pro Tip**: Check `examples/*` branches for complete working projects!
