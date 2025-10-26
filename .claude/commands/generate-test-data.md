---
description: Generate test data fixtures and helpers for tests
---

You are creating test data fixtures and helper functions for a UI automation project using Playwright and TypeScript.

## Your Task

Create well-structured, reusable test data and fixtures to support test automation.

### 1. Test Data Structure

Create test data in: `tests/fixtures/` directory

**File Organization:**
```
tests/fixtures/
├── users.ts          # User account test data
├── products.ts       # Product-related test data
├── addresses.ts      # Shipping/billing addresses
├── payment.ts        # Payment method test data
└── index.ts          # Export all fixtures
```

### 2. User Test Data

```typescript
// tests/fixtures/users.ts

/**
 * User account test data for different scenarios
 */
export interface UserData {
  email: string;
  password: string;
  firstName: string;
  lastName: string;
  phone?: string;
}

/**
 * Generate unique user email with timestamp
 */
export function generateUniqueEmail(prefix: string = 'test'): string {
  const timestamp = Date.now();
  return `${prefix}-${timestamp}@example.com`;
}

/**
 * Pre-defined test users for different scenarios
 */
export const testUsers = {
  validUser: {
    email: generateUniqueEmail('valid-user'),
    password: 'Test@12345',
    firstName: 'Test',
    lastName: 'User',
    phone: '+49 123 456789'
  } as UserData,

  premiumUser: {
    email: 'premium-user@example.com',
    password: 'Premium@12345',
    firstName: 'Premium',
    lastName: 'Customer',
    phone: '+49 987 654321'
  } as UserData,

  newUser: {
    email: generateUniqueEmail('new-user'),
    password: 'NewUser@12345',
    firstName: 'New',
    lastName: 'Customer',
    phone: '+49 111 222333'
  } as UserData,
};

/**
 * Invalid user data for negative testing
 */
export const invalidUsers = {
  invalidEmail: {
    email: 'invalid-email',
    password: 'Test@12345',
    firstName: 'Test',
    lastName: 'User'
  } as UserData,

  shortPassword: {
    email: generateUniqueEmail('short-pass'),
    password: '123',
    firstName: 'Test',
    lastName: 'User'
  } as UserData,

  emptyFields: {
    email: '',
    password: '',
    firstName: '',
    lastName: ''
  } as UserData,
};
```

### 3. Product Test Data

```typescript
// tests/fixtures/products.ts

export interface ProductData {
  name: string;
  category: string;
  subcategory?: string;
  searchTerm: string;
  expectedPrice?: string;
  sku?: string;
}

export const testProducts = {
  catFood: {
    name: 'Royal Canin Feline Health Nutrition',
    category: 'Katzen',
    subcategory: 'Katzenfutter trocken',
    searchTerm: 'royal canin',
  } as ProductData,

  dogFood: {
    name: 'Rinti Kennerfleisch',
    category: 'Hunde',
    subcategory: 'Hundefutter nass',
    searchTerm: 'rinti',
  } as ProductData,

  catToy: {
    name: 'Katzenspielzeug Maus',
    category: 'Katzen',
    subcategory: 'Spielzeug',
    searchTerm: 'katzenspielzeug maus',
  } as ProductData,
};

/**
 * Generate random quantity for cart tests
 */
export function generateRandomQuantity(min: number = 1, max: number = 5): number {
  return Math.floor(Math.random() * (max - min + 1)) + min;
}
```

### 4. Address Test Data

```typescript
// tests/fixtures/addresses.ts

export interface AddressData {
  firstName: string;
  lastName: string;
  street: string;
  houseNumber: string;
  zipCode: string;
  city: string;
  country: string;
  phone?: string;
}

export const testAddresses = {
  berlinAddress: {
    firstName: 'Max',
    lastName: 'Mustermann',
    street: 'Alexanderplatz',
    houseNumber: '1',
    zipCode: '10178',
    city: 'Berlin',
    country: 'Deutschland',
    phone: '+49 30 12345678'
  } as AddressData,

  munichAddress: {
    firstName: 'Anna',
    lastName: 'Schmidt',
    street: 'Marienplatz',
    houseNumber: '8',
    zipCode: '80331',
    city: 'München',
    country: 'Deutschland',
    phone: '+49 89 87654321'
  } as AddressData,

  hamburgAddress: {
    firstName: 'Peter',
    lastName: 'Weber',
    street: 'Reeperbahn',
    houseNumber: '154',
    zipCode: '20359',
    city: 'Hamburg',
    country: 'Deutschland',
    phone: '+49 40 11223344'
  } as AddressData,
};
```

### 5. Payment Test Data

```typescript
// tests/fixtures/payment.ts

export interface PaymentData {
  method: 'credit_card' | 'paypal' | 'invoice' | 'bank_transfer';
  cardNumber?: string;
  cardHolder?: string;
  expiryDate?: string;
  cvv?: string;
}

export const testPaymentMethods = {
  creditCard: {
    method: 'credit_card',
    cardNumber: '4111111111111111', // Test card number
    cardHolder: 'Test User',
    expiryDate: '12/25',
    cvv: '123'
  } as PaymentData,

  invoice: {
    method: 'invoice'
  } as PaymentData,

  paypal: {
    method: 'paypal'
  } as PaymentData,
};
```

### 6. Playwright Fixtures (Custom)

```typescript
// tests/fixtures/custom-fixtures.ts

import { test as base, Page } from '@playwright/test';
import { HomePage } from '../../pages/HomePage';
import { LoginPage } from '../../pages/LoginPage';
import { testUsers } from './users';

/**
 * Extended test fixtures with pre-configured pages and authentication
 */
type CustomFixtures = {
  homePage: HomePage;
  loginPage: LoginPage;
  authenticatedPage: Page;
};

export const test = base.extend<CustomFixtures>({
  /**
   * Provides HomePage instance
   */
  homePage: async ({ page }, use) => {
    const homePage = new HomePage(page);
    await homePage.goto();
    await use(homePage);
  },

  /**
   * Provides LoginPage instance
   */
  loginPage: async ({ page }, use) => {
    const loginPage = new LoginPage(page);
    await use(loginPage);
  },

  /**
   * Provides authenticated page with logged-in user
   */
  authenticatedPage: async ({ page }, use) => {
    const loginPage = new LoginPage(page);
    await loginPage.goto();
    await loginPage.login(testUsers.validUser.email, testUsers.validUser.password);

    // Wait for successful login
    await page.waitForURL('**/account', { timeout: 10000 });

    await use(page);

    // Cleanup - logout after test
    await page.goto('/logout');
  },
});

export { expect } from '@playwright/test';
```

### 7. Test Data Builders (Advanced)

```typescript
// tests/fixtures/builders/UserBuilder.ts

import { UserData } from '../users';

/**
 * Builder pattern for creating user test data
 */
export class UserBuilder {
  private user: Partial<UserData> = {};

  withEmail(email: string): this {
    this.user.email = email;
    return this;
  }

  withPassword(password: string): this {
    this.user.password = password;
    return this;
  }

  withName(firstName: string, lastName: string): this {
    this.user.firstName = firstName;
    this.user.lastName = lastName;
    return this;
  }

  withPhone(phone: string): this {
    this.user.phone = phone;
    return this;
  }

  withRandomEmail(prefix: string = 'test'): this {
    this.user.email = `${prefix}-${Date.now()}@example.com`;
    return this;
  }

  build(): UserData {
    // Provide defaults
    return {
      email: this.user.email || `test-${Date.now()}@example.com`,
      password: this.user.password || 'Test@12345',
      firstName: this.user.firstName || 'Test',
      lastName: this.user.lastName || 'User',
      phone: this.user.phone
    };
  }
}

// Usage:
// const user = new UserBuilder()
//   .withRandomEmail('premium')
//   .withName('John', 'Doe')
//   .build();
```

### 8. Environment-Specific Data

```typescript
// tests/fixtures/environment.ts

export interface EnvironmentConfig {
  baseUrl: string;
  apiUrl: string;
  timeout: number;
  retries: number;
}

const environments: Record<string, EnvironmentConfig> = {
  production: {
    baseUrl: 'https://your-app-url.com',
    apiUrl: 'https://api.your-app-url.com',
    timeout: 30000,
    retries: 2
  },
  staging: {
    baseUrl: 'https://staging.your-app-url.com',
    apiUrl: 'https://api-staging.your-app-url.com',
    timeout: 45000,
    retries: 3
  },
  local: {
    baseUrl: 'http://localhost:3000',
    apiUrl: 'http://localhost:3001',
    timeout: 60000,
    retries: 0
  }
};

export function getEnvironmentConfig(): EnvironmentConfig {
  const env = process.env.TEST_ENV || 'production';
  return environments[env];
}
```

### 9. Index File for Easy Imports

```typescript
// tests/fixtures/index.ts

export * from './users';
export * from './products';
export * from './addresses';
export * from './payment';
export * from './environment';
export * from './custom-fixtures';
export * from './builders/UserBuilder';
```

### 10. Usage in Tests

```typescript
// Example test using fixtures
import { test, expect } from './fixtures/custom-fixtures';
import { testProducts } from './fixtures';

test.describe('Product Search', () => {
  test('search for cat food @smoke', async ({ homePage }) => {
    // homePage fixture is already initialized and navigated
    await homePage.search(testProducts.catFood.searchTerm);

    // Assertions...
  });

  test('add product to cart @regression', async ({ authenticatedPage }) => {
    // User is already logged in via authenticatedPage fixture
    // Test implementation...
  });
});
```

## Output

Provide:
1. Complete fixture files with TypeScript interfaces
2. Test data for various scenarios
3. Custom Playwright fixtures if needed
4. Builder patterns for complex data
5. Usage examples in tests
6. Documentation on how to extend fixtures

Ask user to specify:
- What type of test data is needed
- Specific scenarios to cover
- Data format preferences
- Any special requirements
