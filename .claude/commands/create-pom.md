---
description: Create or refactor a Page Object Model class
---

You are creating or refactoring a Page Object Model (POM) class for a UI automation project using Playwright and TypeScript.

## Context

Page Object Model is a design pattern that:
- Encapsulates page elements and interactions
- Improves test maintainability
- Reduces code duplication
- Makes tests more readable
- Centralizes selector management

## Your Task

Create a new POM class or refactor an existing one following these guidelines:

### 1. File Structure
- Place POMs in: `pages/` directory
- Use descriptive names: `[PageName]Page.ts`
- Group related components: `pages/components/` for reusable components
- Example: `HomePage.ts`, `ProductListPage.ts`, `CheckoutPage.ts`

### 2. Class Structure (TypeScript Best Practices)

```typescript
import { Page, Locator, expect } from '@playwright/test';

/**
 * Page Object Model for [Page Name]
 *
 * Represents: [Brief description of the page]
 * URL: [Typical URL pattern]
 *
 * Key features:
 * - [Feature 1]
 * - [Feature 2]
 */
export class [PageName]Page {
  readonly page: Page;

  // Locators - use readonly and descriptive names
  readonly headerLogo: Locator;
  readonly searchInput: Locator;
  readonly searchButton: Locator;

  constructor(page: Page) {
    this.page = page;

    // Initialize locators in constructor
    this.headerLogo = page.locator('[data-testid="header-logo"]');
    this.searchInput = page.locator('input[name="search"]');
    this.searchButton = page.locator('button[type="submit"]');
  }

  /**
   * Navigate to the page
   */
  async goto(): Promise<void> {
    await this.page.goto('/path');
    await this.waitForPageLoad();
  }

  /**
   * Wait for page to be fully loaded
   */
  async waitForPageLoad(): Promise<void> {
    await this.page.waitForLoadState('networkidle');
    await expect(this.headerLogo).toBeVisible();
  }

  /**
   * Perform search operation
   * @param searchTerm - The term to search for
   */
  async search(searchTerm: string): Promise<void> {
    await this.searchInput.fill(searchTerm);
    await this.searchButton.click();
  }
}
```

### 3. Best Practices

**Locator Strategy:**
- Prefer data-testid attributes
- Use role-based selectors when possible
- Avoid XPath unless necessary
- Make selectors resilient to UI changes
- Use text selectors for stable text

**Method Design:**
- Use async/await for all interactions
- Return types should be explicit
- Complex operations should return new page objects
- Include JSDoc comments for all public methods
- Use descriptive parameter names

**Assertions:**
- Keep assertions in test files, not POMs (preferred)
- If adding assertions to POM, use helper methods like `isVisible()`, `hasText()`
- Separate validation methods from action methods

**Error Handling:**
- Let Playwright's built-in waiting handle timing
- Add custom waits only when necessary
- Include meaningful error messages

### 4. Common Patterns

**Navigation:**
```typescript
async navigateToCategory(category: string): Promise<ProductListPage> {
  await this.page.getByRole('link', { name: category }).click();
  return new ProductListPage(this.page);
}
```

**Form Filling:**
```typescript
async fillContactForm(data: ContactFormData): Promise<void> {
  await this.nameInput.fill(data.name);
  await this.emailInput.fill(data.email);
  await this.messageInput.fill(data.message);
}
```

**Conditional Logic:**
```typescript
async closePopupIfVisible(): Promise<void> {
  if (await this.popup.isVisible()) {
    await this.closeButton.click();
  }
}
```

### 5. Component-Based Approach

For reusable components (header, footer, navigation):
```typescript
export class HeaderComponent {
  readonly page: Page;
  readonly cartIcon: Locator;
  readonly accountLink: Locator;

  constructor(page: Page) {
    this.page = page;
    this.cartIcon = page.locator('[data-testid="cart-icon"]');
    this.accountLink = page.locator('[data-testid="account-link"]');
  }

  async openCart(): Promise<void> {
    await this.cartIcon.click();
  }
}
```

Then use in page objects:
```typescript
export class HomePage {
  readonly header: HeaderComponent;

  constructor(page: Page) {
    this.page = page;
    this.header = new HeaderComponent(page);
  }
}
```

## Output

Create or refactor the POM class with:
1. Proper TypeScript types and interfaces
2. Clear documentation
3. Well-organized locators
4. Intuitive method names
5. Reusable patterns
6. Integration with existing codebase

Before implementing, confirm:
- The page/component to model
- Key interactions needed
- Any specific requirements or patterns to follow
