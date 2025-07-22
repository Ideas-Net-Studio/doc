# Project & Folder Structure

This section describes the organizational structure of the Test-Automation repository and how it aligns with the main application codebase.

## Repository Breakdown

- **Main Application Repo**: MAIN
-- Contains the core source code, with Git submodules for APIs and the UI.

- **Test Automation Repo**: Test-Automation
-- Centralized repository for all automated tests.
-- Structured to mirror the MAIN submodules.

## Folder Layout

```
Test-Automation/
├── src/
│   ├── API/
│   ├── Management-API/
│   ├── Userinterface/
│   │   ├── uat/
│   │   │   ├── common/
│   │   │   │   ├── config/
│   │   │   │   ├── fixtures/
│   │   │   │   ├── pages/
│   │   │   │   └── uploads/
│   │   │   ├── features/
│   │   │   ├── reports/
│   │   │   └── steps/
│   └── ...
└── ...
```

## Key Folder Purposes

Key Folder Purposes

- `src/API`, `src/Management-API`: Jest-Cucumber tests for backend APIs, organized by submodule.

- `src/Userinterface/uat/features`: Contains Gherkin .feature files used to define UAT test scenarios for the UI.

- `src/Userinterface/uat/steps`: Step definitions that implement the logic behind the Gherkin steps.

- `src/Userinterface/uat/common/fixtures`: Shared data and utility fixtures used in multiple tests.

- `src/Userinterface/uat/common/pages`: Page Object Models representing UI elements and actions.

- `src/Userinterface/uat/common/config`: Environment configurations, such as base URLs, credentials, or settings.

- `src/Userinterface/uat/common/uploads`: Assets used during tests (e.g., files for upload scenarios).

- `src/Userinterface/uat/reports`: Output artifacts like JSON reports, useful for Xray integration and test validation.

## Naming Conventions

- Folders inside `src/` must match their respective submodules in the Application repo.

- Feature files are grouped by feature or functionality domain.

S- tep definition file names should match the corresponding .feature file whenever possible.

## Test Placement Rules

- Backend API tests → `src/API`, `src/Management-API`

- UI UAT tests → `src/Userinterface/uat/features`

- Shared logic/utilities → `src/Userinterface/uat/common/{fixtures|pages|config|uploads}`

This structure promotes reusability, scalability, and traceability across manual and automated UAT coverage.