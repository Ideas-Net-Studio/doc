# Writing BDD Feature Files

This section outlines standards and best practices for writing BDD-style feature files using Gherkin syntax within the Test-Automation project.

## Purpose

Well-structured feature files ensure tests are:

- Human-readable
- Aligned with business requirements
- Easy to maintain and traceable to Jira tickets and fixtures

## Folder Location

Feature files for UAT tests are stored in:
```
src/Userinterface/uat/features/
```

Each file should focus on a single user scenario or use case.

## File Naming Convention

The feature file name must be the Jira ticket number associated with the test case

**Example**: `UAT-0000.feature`

## Required Structure

Every feature file should follow this format:

```
@UAT-####
Feature: <Descriptive Title>
  As a <user role>
  I want to <achieve something>
  So that <benefit>

  Scenario: <Title of the scenario>
    Given ...
    When ...
    Then ...
```

## Tagging Convention

- Always include the Jira ticket tag on the first line (e.g., @UAT-1149)
- This tag must match a test case in the Xray Test Repository
- Use additional tags for filtering if needed (e.g., @smoke, @regression)

## Linking to Jira (Xray)

- The `@UAT-####` tag is what links the `.feature` file to the corresponding test case in Xray
- When the test runs and results are uploaded (via CI), Xray will automatically associate the results with that test case

## Language Guidelines

- Use present tense
- Avoid technical jargon
- Make steps clear and actionable
- Prefer domain language over implementation details

### Example
```
@UAT-1149 @smoke
Feature: User logs into the dashboard
  As a valid user
  I want to log into the  dashboard using SSO
  So that I can access my account securely

  Scenario: User logs in with valid credentials
    Given the user is on the login page
    When the user enters valid credentials
    And clicks the login button
    Then the user should be redirected to the dashboard
```

Following these standards ensures clarity, maintainability, and traceability across test automation and product requirements.