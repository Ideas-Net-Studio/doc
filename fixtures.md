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
  // UAT-0001: Common Page
  commonPage: async ({ page, request }, use) => {
    await use(new CommonPage(page, request));
  },
  // UAT-0002: Login Page
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
// UAT-0002: Login Page
export class LoginPage {
  constructor(public page: Page, public request: APIRequestContext) {}

  // UAT-0021: Method click Login Button
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

All new fixtures must be associated with a dedicated Jira ticket in the UAT Automation board.

### Ticket Requirements:

- The ticket must remain open permanently and act as a living history of all updates and changes to the fixture.
- Every fixture-related Jira ticket should include the following sections:
  - Description: Brief explanation of what the fixture or method does.
  - Purpose: Why this logic is needed and when it should be used.
  - Implementation Details: Specific logic, wait conditions, config references, or interaction patterns.
  - Example Usage: Code snippet showing how the fixture/method should be called in a test.

### Code Documentation

The corresponding Jira ticket key (e.g., UAT-0000) must be added as a code comment in the fixture or page object:

```JavaScript
// UAT-0000: Method for navigating to the sign-in page
async gotoSignInPage() {
  await this.page.goto(Config.appUrl);
  await this.page.waitForTimeout(1000);
}
```

If the fixture logic is modified, the Jira ticket should be updated with a comment explaining:

- What changed
- Why the change was made
- Who made the change

This approach guarantees traceability, maintainability, and acts as integrated documentation directly tied to the fixture's history.

