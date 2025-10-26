# Playwright TypeScript Template - Setup Guide

## Quick Start

### Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** 20+ ([Download](https://nodejs.org/))
- **npm** or **yarn** package manager
- **Git** for version control
- **VS Code** (recommended) or your preferred IDE

### Step 1: Clone the Template

```bash
# Clone this template repository
git clone <your-repo-url> my-test-project
cd my-test-project

# Remove the .git directory to start fresh
rm -rf .git

# Initialize your own git repository
git init
git add .
git commit -m "Initial commit from Playwright template"
```

### Step 2: Install Dependencies

Create a `package.json` file with the following content:

```json
{
  "name": "my-test-project",
  "version": "1.0.0",
  "description": "UI test automation with Playwright and TypeScript",
  "scripts": {
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
  },
  "devDependencies": {
    "@playwright/test": "^1.40.0",
    "@typescript-eslint/eslint-plugin": "^6.0.0",
    "@typescript-eslint/parser": "^6.0.0",
    "allure-commandline": "^2.24.0",
    "allure-playwright": "^2.15.0",
    "eslint": "^8.50.0",
    "prettier": "^3.0.0",
    "typescript": "^5.2.0"
  }
}
```

Then install dependencies:

```bash
npm install

# Install Playwright browsers
npx playwright install

# Verify installation
npx playwright --version
```

### Step 3: Create Playwright Configuration

Create `playwright.config.ts` in your project root:

```typescript
import { defineConfig, devices } from '@playwright/test';

export default defineConfig({
  testDir: './tests',
  fullyParallel: true,
  forbidOnly: !!process.env.CI,
  retries: process.env.CI ? 2 : 0,
  workers: process.env.CI ? 1 : undefined,
  reporter: [
    ['list'],
    ['html', { outputFolder: 'playwright-report' }],
    ['allure-playwright', {
      outputFolder: 'allure-results',
      detail: true,
      suiteTitle: true
    }]
  ],

  use: {
    baseURL: 'https://your-application-url.com', // CHANGE THIS
    trace: 'on-first-retry',
    screenshot: 'only-on-failure',
    video: 'retain-on-failure',
  },

  projects: [
    {
      name: 'chromium',
      use: { ...devices['Desktop Chrome'] },
    },
    {
      name: 'firefox',
      use: { ...devices['Desktop Firefox'] },
    },
    {
      name: 'webkit',
      use: { ...devices['Desktop Safari'] },
    },
  ],
});
```

### Step 4: Create TypeScript Configuration

Create `tsconfig.json`:

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["ES2020"],
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "moduleResolution": "node",
    "types": ["node", "@playwright/test"]
  },
  "include": ["tests/**/*", "pages/**/*"],
  "exclude": ["node_modules"]
}
```

### Step 5: Create Project Structure

```bash
# Create necessary directories
mkdir -p pages/components
mkdir -p tests/{smoke,regression,e2e,fixtures,utils}
mkdir -p reports
```

### Step 6: Configure Claude Code

The template includes Claude Code configuration in `.claude/`:

1. **Install Playwright MCP** (recommended):
   ```bash
   claude mcp add microsoft/playwright-mcp
   ```

2. **Explore available slash commands**:
   - `/create-pom` - Create Page Object Model
   - `/add-smoke-test` - Create smoke test
   - `/add-regression-test` - Create regression test
   - `/review-tests` - Review test code
   - `/run-tests` - Execute tests
   - `/analyze-coverage` - Analyze coverage
   - `/generate-report` - Generate reports
   - `/debug-test` - Debug failing tests
   - `/generate-test-data` - Create test fixtures
   - `/setup-ci` - Setup CI/CD

3. **Use autonomous agents**:
   - `Launch test-writer agent` - Write tests autonomously
   - `Launch code-reviewer agent` - Review code and tests

### Step 7: Create Your First Test

Create a simple test to verify setup:

```typescript
// tests/smoke/example.spec.ts
import { test, expect } from '@playwright/test';

test('homepage loads successfully @smoke', async ({ page }) => {
  await page.goto('/');
  await expect(page).toHaveTitle(/.*/, { timeout: 10000 });
});
```

Run the test:

```bash
npm run test:smoke
```

### Step 8: Optional Configuration

#### ESLint Configuration

Create `.eslintrc.json`:

```json
{
  "parser": "@typescript-eslint/parser",
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended"
  ],
  "plugins": ["@typescript-eslint"],
  "env": {
    "node": true,
    "es6": true
  },
  "rules": {
    "@typescript-eslint/no-explicit-any": "error",
    "@typescript-eslint/explicit-function-return-type": "warn"
  }
}
```

#### Prettier Configuration

Create `.prettierrc`:

```json
{
  "semi": true,
  "trailingComma": "es5",
  "singleQuote": true,
  "printWidth": 100,
  "tabWidth": 2
}
```

#### Environment Variables

Create `.env` (add to .gitignore):

```env
BASE_URL=https://your-application-url.com
TEST_ENV=staging
HEADLESS=true
```

## Next Steps

1. **Update Configuration**:
   - Set your `baseURL` in `playwright.config.ts`
   - Update `package.json` with your project name
   - Configure environment variables

2. **Create Page Objects**:
   - Use `/create-pom` command
   - Follow Page Object Model pattern
   - Add component-based architecture

3. **Write Tests**:
   - Start with smoke tests (@smoke tag)
   - Add regression tests (@regression tag)
   - Create E2E tests (@e2e tag)
   - Use `/add-smoke-test` and `/add-regression-test` commands

4. **Setup CI/CD**:
   - Use `/setup-ci` command
   - Configure GitHub Actions or your preferred CI platform

5. **Review Documentation**:
   - Read [PROJECT_PLAN.md](.claude/PROJECT_PLAN.md) for project structure
   - Check [AGENTS_GUIDE.md](.claude/AGENTS_GUIDE.md) for agent usage
   - Review [MCP_RECOMMENDATIONS.md](.claude/MCP_RECOMMENDATIONS.md) for MCP setup

## Troubleshooting

### Playwright Installation Issues

```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm install
npx playwright install --force
```

### TypeScript Errors

```bash
# Ensure TypeScript is installed
npm install -D typescript @types/node

# Check configuration
npx tsc --showConfig
```

### Claude Code Commands Not Working

1. Ensure `.claude/commands/` directory exists
2. Check command file format (must have frontmatter)
3. Restart Claude Code

### Allure Reports Not Generating

```bash
# Install Allure
npm install -D allure-playwright allure-commandline

# Generate report
npx allure generate ./allure-results -o ./allure-report --clean
npx allure open ./allure-report
```

## Resources

- [Playwright Documentation](https://playwright.dev/)
- [TypeScript Documentation](https://www.typescriptlang.org/)
- [Allure Documentation](https://allurereport.org/)
- [Claude Code Documentation](https://docs.claude.com/claude-code)

## Support

For issues or questions:
1. Check existing documentation
2. Review troubleshooting section
3. Use Claude Code slash commands for guidance
4. Consult Playwright documentation

---

**Ready to start testing!** Use `/create-pom` and `/add-smoke-test` to begin building your test suite.
