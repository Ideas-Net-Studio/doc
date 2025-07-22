# Fixtures & Test Utilities

This section documents how we structure and use shared test utilities, data builders, and fixtures within the Test-Automation repository.

## What Are Fixtures?

Fixtures are reusable components that provide setup, configuration, and logic to tests in a structured and centralized way. They are essential in UAT automation for maintaining reusable Page Object Models, consistent test context setup, and shared helper functions.

## Folder Location and Structure

In our UI automation framework, we use a single `fixtures.ts` file to declare and initialize all commonly used page objects. This file acts as a manifest that binds test lifecycle methods with Playwright’s `base.extend()` method.

```
src/Userinterface/uat/common/
├── config/      → Application config and test users
├── fixtures.ts  → Declares and binds Page Object Models for test usage
├── pages/       → Contains the actual logic for each Page Object (e.g., LoginPage, CommonPage)
├── uploads/     → Files and assets used during testing (e.g., attachments, documents)
```

## Real Fixture Usage Pattern

In `fixtures.ts`, we bind objects like `LoginPage` and `CommonPage` to the Playwright test context:
```JavaScript
const testPages = base.extend<Pages>({
  commonPage: async ({ page, request }, use) => {
    await use(new CommonPage(page, request));
  },
  loginPage: async ({ page, request }, use) => {
    await use(new LoginPage(page, request));
  }
});

export const test = testPages;
export const { Given, When, Then, Before, After } = createBdd(testPages);
```

This allows the usage of `loginPage` or `commonPage` directly in step definition files without needing manual setup.

## Page Object Model (POM)

The logic lives in individual `.ts` files inside `pages/`. Each class represents a specific section or component of the UI (e.g., LoginPage):

```JavaScript
export class LoginPage {
  constructor(public page: Page, public request: APIRequestContext) {}

  async clickLoginButton() {
    await this.page.locator('#login-button').click();
  }
}
```

## Best Practices

- Keep fixture declarations simple and focused on registration/binding
- Place all logic inside individual Page Object classes under `pages/`
- Group actions and elements by domain (e.g., Login, Dashboard, Forms)
- Only add a fixture to `fixtures.ts` if it is used across multiple features or has setup logic

## Requesting New Fixtures

If a shared fixture does not yet exist:

- Implement its logic inside the appropriate Page Object class in `pages/`
- Add a fixture binding in `fixtures.ts`
- If unsure, submit a Jira ticket under the UAT Automation board with:
  - Feature file or scenario
  - Suggested fixture name and purpose
  - Related POM if already implemented

This ensures reusable components are discoverable, centralized, and consistent.