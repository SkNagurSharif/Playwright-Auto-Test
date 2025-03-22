# Playwright Auto Test Requirements

## Prerequisites
- Node.js (version 12 or later)
- npm (Node Package Manager)
- TypeScript (version 4 or later)

## Installation
To install the necessary dependencies for the Playwright auto tests, run the following command:

```bash
npm install
```

## Dependencies
The following packages are required for running Playwright tests:

- `playwright`: The Playwright library for browser automation.
- `@playwright/test`: The Playwright test runner.
- `typescript`: TypeScript for type definitions.
- `cucumber`: For BDD-style testing with Gherkin syntax.
- `pg` or `mysql`: Database client libraries for PostgreSQL or MySQL, depending on your database.

## Playwright Features
- **Cross-Browser Testing**: Supports Chromium, Firefox, and WebKit, allowing you to run tests across different browsers.
- **Headless Mode**: Run tests without a GUI for faster execution.
- **Auto-Waiting**: Automatically waits for elements to be ready before performing actions.
- **Powerful Selectors**: Use CSS and XPath selectors to target elements.

## Common Commands
- **Run All Tests**: Execute all tests in the project.

  ```bash
  npx playwright test
  ```

- **Run Tests in Headless Mode**: By default, tests run in headless mode. To run in headed mode (with a GUI):

  ```bash
  npx playwright test --headed
  ```

- **Run Specific Test File**: To run a specific test file, provide the file path:

  ```bash
  npx playwright test path/to/test.spec.ts
  ```

- **Run Tests with Specific Tags**: To run tests with specific tags:

  ```bash
  npx playwright test --grep @tag
  ```

- **Run Tests with Timeout**: To set a timeout for tests:

  ```bash
  npx playwright test --timeout 30000
  ```

- **Run Tests with Retry**: To retry failed tests:

  ```bash
  npx playwright test --retries 2
  ```

- **Generate HTML Reports**: To generate HTML reports after running tests:

  ```bash
  npx playwright show-report
  ```

- **Run Tests with Custom Configuration**: To run tests with a custom configuration file:

  ```bash
  npx playwright test --config=custom.config.ts
  ```

- **Install Browsers**: To install the necessary browsers for Playwright:

  ```bash
  npx playwright install
  ```

- **List Installed Browsers**: To list the installed browsers:

  ```bash
  npx playwright install --list
  ```

- **Debugging Tests**: To run tests in debug mode, which allows you to pause and inspect the test execution:

  ```bash
  npx playwright test --debug
  ```

- **Trace Tests**: To generate a trace of the test execution for debugging purposes:

  ```bash
  npx playwright test --trace on
  ```

- **Run Tests with Specific Browser**: To specify which browser to run the tests in:

  ```bash
  npx playwright test --browser=firefox
  ```

## BDD Implementation
The requirements for the Playwright auto tests have been implemented in a BDD structure as follows:

### Improved Folder Structure
The folder structure for the Playwright project is organized as follows:
```

Playwright-Auto-Test/
│
├── tests/
│   ├── api/
│   │   ├── document_manager/
│   │   │   ├── documentUpload.spec.ts
│   │   │   ├── documentFetch.spec.ts
│   │   │   └── documentManagerSteps.ts
│   │   ├── linking_documents/
│   │   │   └── linkDocuments.spec.ts
│   │   └── outgoing_documents/
│   │       └── generateOutgoingDocument.spec.ts
│   │
│   ├── ui/
│   │   ├── task_manager/
│   │   │   ├── taskManager.spec.ts
│   │   │   └── taskManagerSteps.ts
│   │   └── checkout/
│   │       └── checkout.spec.ts
│   │
│   ├── integration/
│   │   └── loginIntegration.spec.ts
│   │
│   ├── regression/
│   │   └── regressionTests.spec.ts
│   │
│   ├── smoke/
│   │   └── smokeTests.spec.ts
│   │
│   └── sanity/
│       └── sanityTests.spec.ts
│
├── features/
│   ├── task_manager/
│   │   └── taskManager.feature
│   ├── document_manager/
│   │   └── documentManager.feature
│   ├── linking_documents/
│   │   └── linkDocuments.feature
│   ├── outgoing_documents/
│   │   └── generateOutgoingDocument.feature
│   ├── user/
│   │   └── login.feature
│   └── checkout/
│       └── checkout.feature
│
├── step_definitions/
│   ├── taskManagerSteps.ts
│   ├── documentManagerSteps.ts
│   ├── linkDocumentsSteps.ts
│   ├── generateOutgoingDocumentSteps.ts
│   ├── loginSteps.ts
│   └── checkoutSteps.ts
│
│
├── support/
│   └── hooks.ts
│
├── shared/
│   └── helpers.ts
│
├── pages/
│   ├── loginPage.ts
│   └── checkoutPage.ts
│
├── components/
│   ├── common/
│   │   └── Breadcrumbs.tsx
│   └── specific/
│       └── LoginForm.tsx
│
├── objects/
│   ├── userObject.ts
│   └── productObject.ts
│
├── custom_world/
│
├── failed_screenshots/
│
├── fixtures/
│
├── test_data/
│
├── config/
│   ├── playwright.config.ts
│   └── env.ts
│
├── reports/
│   └── report.html
│
├── data/
│   └── testData.json
│
└── screenshots/

- **Playwright-Auto-Test/**: Root directory for the Playwright tests.
  - **tests/**: Contains all test files organized by type.
    - **ui/**: UI tests for web applications.
      - `login.spec.ts`: Tests for user login functionality.
      - `checkout.spec.ts`: Tests for the checkout process.
    - **api/**: API testing scripts for backend services.
      - `userApi.spec.ts`: Tests for user-related API endpoints.
      - `productApi.spec.ts`: Tests for product-related API endpoints.
    - **integration/**: Integration tests that cover interactions between different components.
      - `loginIntegration.spec.ts`: Tests that verify the login process works with the backend.
    - **database/**: Database testing scripts and utilities.
      - `dbOperations.spec.ts`: Tests for database operations.
  - **features/**: Contains feature files written in Gherkin syntax, organized into subfolders for better categorization.
    - **user/**: User-related features.
      - `login.feature`: Feature file for user login scenarios.
    - **checkout/**: Checkout-related features.
      - `checkout.feature`: Feature file for checkout scenarios.
  - **step_definitions/**: Contains step definitions that map Gherkin steps to Playwright code, organized by feature.
    - `loginSteps.ts`: Step definitions for login scenarios.
    - `checkoutSteps.ts`: Step definitions for checkout scenarios.
  - **support/**: Contains any support files or utilities needed for BDD.
    - `hooks.ts`: Setup and teardown hooks for tests.
  - **shared/**: Contains common utilities and functions that can be reused across different tests and features.
    - `helpers.ts`: Common helper functions for test setup and teardown.
  - **pages/**: Contains page object models representing different pages in the application.
    - `loginPage.ts`: Page object for the login page.
    - `checkoutPage.ts`: Page object for the checkout page.
  - **components/**: Contains UI components used in tests.
    - **common/**: Reusable components used across multiple pages.
      - `Breadcrumbs.tsx`: Common breadcrumb component.
    - **specific/**: Components that are unique to specific pages or features.
      - `LoginForm.tsx`: Login form component.
  - **objects/**: Contains data objects or models that can be used in tests.
    - `userObject.ts`: User data model.
    - `productObject.ts`: Product data model.
  - **custom_world/**: Contains custom world definitions for sharing state and functionality across tests.
  - **failed_screenshots/**: Directory for storing screenshots of failed test cases.
  - **fixtures/**: Directory for test fixtures that can be used to set up the initial state for tests.
  - **test_data/**: Directory for additional test data files.
  - **config/**: Configuration files that manage environment settings.
    - `playwright.config.ts`: Configuration file for Playwright settings, including browser options and test settings.
    - `env.ts`: Environment-specific settings.
  - **reports/**: Directory for storing test reports and logs.
    - `report.html`: HTML report generated after test execution.
  - **data/**: Directory for test data files or fixtures.
    - `testData.json`: JSON file containing test data used in tests.
  - **screenshots/**: Directory for storing screenshots taken during tests.
  - **Requirements.md**: Documentation of requirements and commands for Playwright.

## Database Testing
To handle database testing and operations, follow these guidelines:

### Connecting to the Database
You can establish a connection to your database using the following example for PostgreSQL:

```typescript
import { Client } from 'pg';

const client = new Client({
  user: 'yourUsername',
  host: 'localhost',
  database: 'yourDatabase',
  password: 'yourPassword',
  port: 5432,
});

await client.connect();
```

### Common Database Operations
You can perform common database operations in your tests using the `dbOperations.ts` file:

- **Insert Data**:

```typescript
async function insertData(query: string, values: any[]) {
  await client.query(query, values);
}
```

- **Query Data**:

```typescript
async function queryData(query: string) {
  const res = await client.query(query);
  return res.rows;
}
```

- **Delete Data**:

```typescript
async function deleteData(query: string) {
  await client.query(query);
}
```

### Setup and Teardown
Ensure to set up and tear down your database state before and after tests to maintain isolation:

```typescript
beforeAll(async () => {
  await client.connect();
  // Setup database state
});

afterAll(async () => {
  // Teardown database state
  await client.end();
});
```

## Best Practices for Writing Tests
- **Keep Tests Independent**: Ensure that tests do not depend on each other to avoid cascading failures.
- **Use Descriptive Names**: Name your test files and test cases descriptively to make it clear what they are testing.
- **Organize Tests Logically**: Group related tests together in directories to maintain clarity.

## Troubleshooting Tips
- **Check Browser Installation**: Ensure that the required browsers are installed using `npx playwright install`.
- **Review Console Logs**: Use console logs to debug issues in your tests.
- **Use the Debugger**: Utilize the debug mode to step through your tests and identify problems.

## CI/CD Integration
Playwright can be easily integrated into CI/CD pipelines. Ensure that your CI environment has the necessary dependencies installed and configure your pipeline to run Playwright tests as part of the build process.

## Configuration
You can configure Playwright settings in the `playwright.config.ts` file. This includes options for test retries, timeouts, and browser settings.

## Additional Resources
- [Playwright Documentation](https://playwright.dev/docs/intro)
- [Playwright GitHub Repository](https://github.com/microsoft/playwright)
- [Playwright API Reference](https://playwright.dev/docs/api/class-playwright)
