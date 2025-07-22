# Jira & Xray Integration

This section documents how automated tests are linked to Jira using the Xray plugin, and how we maintain traceability between test cases, feature files, and execution results.

## Purpose

To ensure:

- Every automated test is traceable to a business requirement
- Test coverage is centralized and visible in Jira
- Test execution results are reported back to Jira automatically

## Xray Test Repository

Our Xray repository is organized by type:

```
Xray Test Repository
├── Manual
├── Automation
│   ├── Login
│   ├── Dashboard
│   └── ...
```

Each automated test case is stored under the Automation folder and tagged as `Cucumber` / `Automated`.

## Feature File Linking

To link an automated `.feature` file to an Xray test case:

1. Create a test case in Xray under the appropriate Automation folder
2. Add the tag `@UAT-####` at the top of the `.feature` file
3. Name the `.feature` file exactly as the Jira test key (e.g., `UAT-1014.feature`)

Xray uses this tag to match the test case with the test execution result.

## Uploading Test Results

When tests run via CI/CD pipeline (e.g., GitHub Actions), the output is converted to a Cucumber JSON report and uploaded to Xray.

Example:
```
POST /api/v2/import/execution/cucumber
```

This creates a Test Execution in Jira and links results to each individual test case.

## Traceability Workflow

1. **Story/Requirement** `→` Linked to one or more Xray test cases
2. **Xray Test Case** `→` Linked to .feature file via @E1UAT-####
3. **Feature File** `→` Executes in CI and uploads result to Xray
4. **Test Execution** `→` Automatically associated with the linked Jira test

## Best Practices

- Always link tests to Jira tickets via tags and file naming
- Use Xray’s built-in traceability reports to validate coverage
- Use Test Execution issues in Jira to view pass/fail history
- Keep Xray tickets open for automated test cases to log changes and rework history

Maintaining tight integration between Playwright tests and Xray ensures visibility, accountability, and consistent reporting across UAT automation.

