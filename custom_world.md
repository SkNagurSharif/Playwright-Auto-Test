# Custom World in Playwright for Enterprise Automation Testing

## Overview
The custom world in Playwright is a powerful feature that allows you to share state and functionality across your tests. This is particularly useful in enterprise automation testing projects where maintaining a consistent context is crucial.

## Benefits of Using a Custom World

### 1. Shared State
- **User Sessions**: 
  - Maintain user sessions or authentication tokens that need to persist across different tests.
  - This is especially important in scenarios where tests require login functionality.
  - For example, if multiple tests need to verify user actions after logging in, the custom world can store the session information, eliminating the need to log in repeatedly.
  
- **Configuration Management**: 
  - Manage configurations that are needed for different environments (e.g., staging, production) or different test scenarios.
  - This allows you to switch contexts easily without modifying individual test files.

### 2. Common Functions
- **Utility Functions**: 
  - House utility functions that are used across multiple test files, reducing redundancy and improving maintainability.
  - For instance, if you have functions for data setup, API calls, or common assertions, defining them in the custom world allows all tests to access them without duplication.

### 3. Data Management
- **Setup and Teardown**: 
  - Handle setup and teardown of test data, ensuring that tests run in a clean state.
  - This can include creating test data before tests run and cleaning up after tests complete.
  - For example, if your tests require specific database entries, the custom world can manage these entries, ensuring they are present before tests and removed afterward.

- **Database Connections**: 
  - Manage database connections and operations, allowing for seamless integration of database testing within your automation framework.
  - This is particularly useful for tests that require data validation against a database.

### 4. Integration with BDD
- **Scenario Management**: 
  - In a BDD context, the custom world can help manage the state across different scenarios defined in your feature files.
  - This ensures that the context is consistent and that shared data is accessible, making it easier to write and maintain BDD tests.

### 5. Real-Time Implementation
- **Example Usage**: 
  - In your `step_definitions` files, you can access the shared state defined in the custom world to manage user sessions and configurations across different scenarios.
  - For instance, in a login step definition, you can use the user object from the custom world to verify login actions.

### Example: Step Definitions for User Login
```typescript
import { Given, When, Then } from '@cucumber/cucumber';
import { test } from '../custom_world';

Given('I am on the login page', async () => {
    await page.goto('https://example.com/login');
});

When('I enter my username and password', async function () {
    await page.fill('input[name="username"]', this.user.email);
    await page.fill('input[name="password"]', 'password123');
});

When('I click the login button', async () => {
    await page.click('button[type="submit"]');
});

Then('I should be redirected to my dashboard', async () => {
    await expect(page).toHaveURL('https://example.com/dashboard');
});

Then('I should see a welcome message', async () => {
    await expect(page.locator('h1')).toHaveText(`Welcome, ${this.user.name}`);
});


## Conclusion
Implementing a custom world in Playwright enhances the organization and efficiency of your testing framework, making it easier to manage shared state and functionality across your tests. This is particularly beneficial in enterprise automation testing projects, where consistency and maintainability are key.


## Implementation Example
1. **Create a Custom World File**:
   - Create a new file (e.g., `custom_world.ts`) where you define your custom context.

2. **Define the Custom Context**:
   ```typescript
   import { test as base } from '@playwright/test';

   // Define a custom context
   type CustomWorld = {
       user: {
           name: string;
           email: string;
       };
       // Add any other shared properties or methods
   };

   // Extend the base test context
   const test = base.extend<CustomWorld>({
       user: [{ name: 'John Doe', email: 'john@example.com' }, { option: true }],
       // Add any other shared properties or methods
   });

   export { test };
   ```

3. **Using the Custom World**:
   - In your test files, you can now use the custom context defined in your custom world.

## Conclusion
Implementing a custom world in Playwright enhances the organization and efficiency of your testing framework, making it easier to manage shared state and functionality across your tests. This is particularly beneficial in enterprise automation testing projects, where consistency and maintainability are key.
