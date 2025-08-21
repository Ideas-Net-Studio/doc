# ExceptionsOne Test Automation Strategy

## 1. Introduction

This document describes the Test Automation strategy for the ExceptionsOne project. The application is a central location to handle and track all company exceptions. The test automation effort is divided into two distinct categories:

- **End-to-End Test Automation (E2E-TA)**: Runs automatically in the CI/CD pipeline against the QA environment.

- **User Acceptance Test Automation (UAT-TA)** Runs manually on demand against the UAT environment.

Although ~90% of the steps and fixtures are reusable between both suites, they remain distinct to serve different purposes.

---

## 2. Purpose & Benefits

### E2E-TA (QA)

- Validates that critical UI flows work end-to-end in the QA environment.

- Provides fast feedback during PRs and nightly runs.

- Detects regressions before code is merged.

### UAT-TA (UAT)

- Validates business workflows for sign-off.

- Mapped directly to Jira/XRay tickets for traceability.

- Provides richer evidence (trace, screenshots, video) for stakeholders.

---

## 3. Folder Structure
```
feature/
  ├─ e2e/          # E2E-exclusive .feature files
  ├─ uat/          # UAT-exclusive .feature files
  ├─ E1UAT-113.feature   # Shared .feature files run in both
  ├─ E1UAT-114.feature
  └─ ...
```

- **Shared tests** → in `feature/` root.

- **Exclusive tests** → in `feature/e2e/` or `feature/uat/`.

---

## 4. Naming Convention
- All `.feature` files must be named after the Jira ticket number (e.g., `E1UAT-113.feature`).

- Each file must link to a Jira/XRay test.

- The Jira ticket and the Gherkin file must share suite tags:

  - `@e2e`: E2E-only test.

  - `@uat`: UAT-only test.

  - `No suite tag`: test runs in both.

---

## 5. Tag Taxonomy

### Suite scope

- `@e2e`: CI/CD E2E suite (QA).

- `@uat`: Manual UAT suite (UAT).

### Risk/Priority

- `@critical`: Must pass in PR gate.

- `@smoke`: Fast environment sanity check.

- `@slow`: Excluded from PR, runs nightly.

### Stability

- `@flaky`: Quarantined test (unstable). Excluded from PR, still runs nightly.

- `@quarantine`: Disabled due to known product defect (must reference Jira bug).

---

## 6. Flaky Policy

A **flaky test** is one that passes and fails intermittently without code changes.

### Policy

- #### E2E-TA:

  - Retry once.

  - If it passes on retry → mark/tag as `@flaky`.

  - `@flaky` tests are excluded from PR runs but included in nightly.

  - Weekly review required to fix and remove the tag.

- #### UAT-TA:

  - Retry = 0.

  - Failures treated as potential defects; rerun manually if flakiness is suspected.

---

## 7. Evidence & Reporting

### E2E-TA

- HTML report.

- Trace/screenshots only on failure.

### UAT-TA

- Always record trace, screenshots, and video.

- Evidence is attached to XRay execution.

- Includes build hash and environment info.

___

## 8. Roles & Permissions

- Roles such as `Requester`, `PSPOwner`, `AE`, etc. must be validated.

- **TBD**: Determine how each role will be tested

---

## 9. Execution Rules
| Test               | CLI Filter                          | NPM                     |
| ------------------ | ----------------------------------- | ----------------------- |
| PR Gate (E2E)      | `--grep-invert "@uat|@slow|@flaky"` | `npm run test:e2e:pr`   |
| Nightly (E2E Full) | `--grep-invert "@uat|@flaky"`       | `npm run test:e2e:full` |
| UAT Run            | `--grep-invert "@e2e"`              | `npm run test:uat:full` |

---

## 10. Jenkins Integration

- Jenkins will provide dashboard buttons to trigger specific test suites based on tags.

- Example: UAT team wants to run tests tagged `@utep`. A dedicated button on Jenkins triggers those tests against the main branch in the `QA` environment.

- All runs will execute on the 7PS Test Platform and generate detailed reports.

- Buttons can be configured for common tag sets (e.g., `@uat`, `@release-X.Y`, `@utep`).

___

## 11. Governance

- All tests must be associated with a Jira ticket.

- File name = Jira ticket number.

- Jira/XRay ticket must reflect correct suite tags (`@e2e`, `@uat`).

- Quarantined tests must link to a defect ticket.

- Weekly review of flaky/quarantined tests.
