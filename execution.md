# Test Execution Guide

This section explains how to execute tests within the ExceptionOne-Test-Automation project both locally and through the CI/CD pipeline.

## Local Execution

Use local execution for development, debugging, or validating changes before pushing to the repository.

### Step-by-step

1. Install dependencies (if not done yet):
```
    npm install
```
2. Run all UAT tests:
```
    npx playwright test
```
3. Run a specific feature file:
```
    npx playwright test src/Userinterface/uat/features/UAT-1014.feature
```
4. Run tests by tag:
```
    npx playwright test --grep "@smoke"
```

## Debugging Tests

To run a test in debug mode:
```
  npx playwright test src/Userinterface/uat/features/UAT-1014.feature --debug
```
To pause execution with browser UI:
```
  npx playwright test --ui
```

## CI/CD Execution

Tests are automatically executed via GitHub Actions as part of the CI workflow.

### Common CI Tasks:
- Run all tests in the UAT folder
- Generate Cucumber JSON output
- Upload results to Jira/Xray
- Optionally, fail PRs if any tests fail

## Test Output

Test results are generated in the following folder:
```
src/Userinterface/uat/reports/
```

### The output includes:
- Cucumber JSON for Xray integration
- Trace logs and screenshots (if configured)

## Notes
- CI will only execute tests tagged as @UAT-####
- If you skip tagging or use the wrong file name, the test will not link properly to Xray
- For consistent results, always commit .feature files and fixture updates together

## Best Practices
- Run tests locally before pushing
- Use tagging to filter what you need (e.g., `@smoke`, `@regression`)
- Clean up debug statements before commit

This guide ensures a smooth process for validating and delivering automated UAT scenarios across local and remote environments.