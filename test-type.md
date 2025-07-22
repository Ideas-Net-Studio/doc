## Test Types & Scope
### What Is Covered in UAT

UAT focuses on testing high-value user workflows that reflect real-world usage scenarios. These tests are based on business requirements and user stories, and they validate that the system performs correctly from an end-user perspective.

#### Examples include:

- Login and authentication flows

- Dashboard access and user roles

- Data submission and processing

- Error handling and validation messages

### Manual vs Automated UAT Tests

UAT includes both manual and automated test cases:

- **Manual Tests** are typically exploratory or require human judgment (e.g., UI aesthetics, vague acceptance criteria).

- **Automated Tests** are implemented using Playwright-BDD and are triggered to validate business-critical workflows reliably and repeatedly.

## How Test Scenarios Are Selected

UAT scenarios are selected based on:

- Business-criticality of the feature

- Frequency of use

- Risk level and potential impact

- Regression sensitivity

Each scenario is documented in Jira Xray and linked to its corresponding manual and/or automated test case for full traceability.