## Purpose of This Space

This space serves as the central documentation hub for all User Acceptance Testing (UAT) automation efforts within the E1-ExceptionsOne Test Automation project. It provides developers and stakeholders with a clear understanding of the tools, structure, and processes involved in executing automated UAT using Playwright and Jira Xray.

## What Is UAT Testing?

User Acceptance Testing (UAT) is the final phase of testing where end-users validate that the system meets business requirements. It is a critical step before releasing software to production, ensuring real-world workflows behave as expected.

Our UAT process includes both manual and automated test cases, with an emphasis on test traceability and reliability.

## Tools Used

**Playwright-BDD**: A modern end-to-end testing framework that combines Playwright with Cucumber-style step definitions, allowing us to write human-readable automated tests.

**Jira Xray**: A test management plugin for Jira used to organize test cases, plans, executions, and coverage reports.

**GitHub**: Source control for managing test code.

**CI/CD Pipeline**: Automates test execution and reporting to Xray.

## Environments Overview

**UAT**: Main environment for running acceptance tests before release.

**QA**: Used for integration-level validations.

All automated tests run against the UAT environment unless otherwise specified.