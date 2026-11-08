# PoliSight
## User Acceptance Testing (UAT) Plan

**Document Version:** 1.1  
**Project:** PoliSight – Insurance Policy Intelligence & Analytics Platform  
**Document Type:** User Acceptance Testing Plan  
**Prepared By:** Prathmesh Aghor  
**Project Classification:** Portfolio Demonstration  
**Status:** Draft – Pending Test Execution  
**Date:** 08 November 2026

---

# 1. Introduction

## 1.1 Purpose

This document defines the User Acceptance Testing (UAT) approach for PoliSight, an insurance policy intelligence and analytics platform designed to support business analysis of policy portfolios, premium collections, claims, renewals, and customer retention.

The purpose of UAT is to verify that the platform's outputs and business functionality meet the requirements documented in the Business Requirements Document (BRD).

UAT will focus on business usability, data accuracy, analytical reliability, and whether the platform provides meaningful information for insurance portfolio decision-making.

## 1.2 Project Overview

PoliSight uses structured insurance data and analytical workflows to provide insights into:

- Policy portfolio performance.
- Premium collection and overdue payments.
- Claims frequency and settlement trends.
- Policy renewals and lapse patterns.
- Customer segmentation and retention.
- Business performance indicators.

The platform is intended as a portfolio demonstration of insurance analytics and business analysis capabilities, rather than a production insurance management system.

## 1.3 UAT Objectives

The objectives of UAT are to:

1. Verify that the platform satisfies the approved business requirements.
2. Validate the accuracy and consistency of insurance data.
3. Confirm that key performance indicators are calculated correctly.
4. Verify that policy, premium, claims, and renewal analytics provide meaningful outputs.
5. Identify defects, data inconsistencies, and usability issues.
6. Confirm that the deliverables are suitable for portfolio demonstration.

# 2. UAT Scope

## 2.1 In Scope

| Module | Testing Coverage |
|---|---|
| Policy Analytics | Policy counts, status distribution, sum insured, premium analysis |
| Customer Analytics | Customer distribution, segmentation, demographic analysis |
| Premium Analytics | Premium collection, outstanding amounts, overdue payments |
| Claims Analytics | Claims frequency, claim amounts, settlement and rejection trends |
| Renewal Analytics | Renewal rates, lapse rates, non-renewal analysis |
| KPI Validation | Business metric calculations and consistency |
| Data Validation | Completeness, accuracy, referential integrity, duplicates |
| Dashboard Validation | Filters, visualizations, labels, displayed values |

## 2.2 Out of Scope

The following are excluded from this UAT:

- Live insurance policy issuance.
- Real-time integration with insurance company systems.
- Actual premium payment processing.
- Live claim registration or settlement.
- Regulatory certification or compliance approval.
- Production deployment and security penetration testing.
- Validation against confidential insurer-owned datasets.

# 3. UAT Approach and Methodology

UAT will follow a structured, requirement-based testing approach.

## 3.1 Testing Phases

| Phase | Activity | Expected Output |
|---|---|---|
| 1. Preparation | Review BRD and define test scenarios | Approved test cases |
| 2. Environment Setup | Verify database, datasets, scripts, and dashboard | Ready testing environment |
| 3. Test Execution | Execute test cases using available data | Recorded test results |
| 4. Defect Logging | Record failed tests and inconsistencies | Defect register |
| 5. Retesting | Re-execute corrected test cases | Updated test results |
| 6. UAT Closure | Review results and outstanding issues | UAT summary and sign-off status |

## 3.2 Testing Method

The following testing techniques will be used:

- Requirement-based testing.
- Data validation testing.
- Positive and negative testing.
- Boundary and exception testing.
- Analytical calculation verification.
- Dashboard and usability testing.

# 4. UAT Entry and Exit Criteria

## 4.1 Entry Criteria

Testing may begin when:

- The database schema has been created successfully.
- Required datasets are available.
- Data generation or data-loading scripts have completed successfully.
- Analytical scripts and dashboard components are accessible.
- The BRD and UAT test cases are available.
- The testing environment is operational.

## 4.2 Exit Criteria

UAT may be considered complete when:

- All planned test cases have been executed.
- All critical and high-priority defects have been resolved or formally documented.
- Key business calculations have been verified.
- Data quality issues have been recorded.
- Failed test cases have been retested where applicable.
- Outstanding limitations have been documented.
- The UAT summary has been prepared.

A UAT pass must not be declared solely because the dashboard loads successfully.

# 5. UAT Test Scenarios and Test Cases

**Execution status:** All test cases are initially Not Run.

| Test Case ID | Requirement ID | Module | Test Scenario | Expected Result | Status |
|---|---|---|---|---|---|
| UAT-001 | FR-01 | Database | Verify database connectivity | Application connects to the PoliSight database successfully | Not Run |
| UAT-002 | FR-01 | Data | Verify availability of all eight database tables | All required tables are accessible | Not Run |
| UAT-003 | FR-01 | Data | Validate primary and foreign key relationships | Referential integrity is maintained | Not Run |
| UAT-004 | FR-01 | Data | Check duplicate policy records | Duplicate policy numbers are identified or prevented according to defined rules | Not Run |
| UAT-005 | FR-01 | Policy | Validate total policy count | Displayed count matches the underlying policy records | Not Run |
| UAT-006 | FR-01 | Policy | Validate policy status distribution | Active, Lapsed, Expired, Cancelled, and Renewed counts match source data | Not Run |
| UAT-007 | FR-01 | Policy | Validate total sum insured | Aggregated sum insured matches the database calculation | Not Run |
| UAT-008 | FR-02 | Customer | Validate customer distribution | Customer counts and segmentation match source records | Not Run |
| UAT-009 | FR-05 | Premium | Validate total premium due | Total premium due matches the premium records | Not Run |
| UAT-010 | FR-05 | Premium | Validate total premium collected | Total collected amount matches eligible payment records | Not Run |
| UAT-011 | FR-05 | Premium | Validate overdue premium calculation | Overdue amounts and counts follow the defined business rules | Not Run |
| UAT-012 | FR-06 | Claims | Validate total claims count | Claims count matches the underlying claims records | Not Run |
| UAT-013 | FR-06 | Claims | Validate approved and rejected claims | Status-wise counts and amounts match source data | Not Run |
| UAT-014 | FR-06 | Claims | Validate claims settlement duration | Settlement duration is calculated correctly for eligible settled claims | Not Run |
| UAT-015 | FR-07 | Renewals | Validate total eligible renewal records | Renewal population matches the documented eligibility rules | Not Run |
| UAT-016 | FR-07 | Renewals | Validate renewal rate | Renewal rate matches the approved business formula | Not Run |
| UAT-017 | FR-07 | Renewals | Validate lapse rate | Lapse rate matches the approved business formula | Not Run |
| UAT-018 | FR-09 | Dashboard | Validate dashboard filters | Selected filters update relevant visualizations correctly | Not Run |
| UAT-019 | FR-08 | Dashboard | Validate displayed KPI values | Dashboard values match independently calculated results | Not Run |
| UAT-020 | FR-14 | Dashboard | Validate charts and labels | Charts, legends, labels, and units are understandable and accurate | Not Run |
| UAT-021 | FR-13 | Analytics | Validate product-wise performance | Product-level metrics match the underlying data | Not Run |
| UAT-022 | FR-12 | Analytics | Validate regional performance | Region-level metrics match the underlying data | Not Run |
| UAT-023 | FR-11 | Analytics | Validate date-based filtering | Date selections return the expected reporting period | Not Run |
| UAT-024 | FR-10 | Data Quality | Validate missing values | Missing or invalid values are identified and handled according to documented rules | Not Run |
| UAT-025 | FR-10 | Data Quality | Validate negative and inconsistent financial values | Invalid financial records are flagged or handled according to business rules | Not Run |

*Note: Requirement IDs follow the existing BRD requirement mapping. Database connectivity and structural checks are mapped to FR-01 for this project-level test plan; the mapping should be reviewed against the final functional requirement wording before execution.*

# 6. Detailed Test Case Template

Each test case should be executed and recorded using the following structure.

| Field | Description |
|---|---|
| Test Case ID | Unique test identifier |
| Requirement ID | Related BRD functional requirement |
| Acceptance Criterion ID | Related BRD acceptance criterion, where applicable |
| Test Scenario | Business functionality being tested |
| Preconditions | Conditions required before execution |
| Test Steps | Steps performed by the tester |
| Test Data | Input data used for testing |
| Expected Result | Expected business outcome |
| Actual Result | Observed outcome |
| Status | Pass / Fail / Blocked / Not Run |
| Evidence Reference | Screenshot, query output, or other supporting evidence |
| Defect ID | Reference to a logged defect |
| Remarks | Additional observations |

## 6.1 Example – Premium Collection Validation

**Test Case ID:** UAT-010  
**Requirement Reference:** FR-05 / AC-05  
**Module:** Premium Analytics

**Preconditions:**
- Database is accessible.
- Premium records are available.
- Payment status and amount fields are populated.

**Test Steps:**
1. Open the premium analytics dashboard.
2. Identify the total premium collected KPI.
3. Calculate the collected amount independently using the underlying database records.
4. Compare the calculated amount with the dashboard value.

**Expected Result:**

The dashboard's total premium collected must match the independently calculated amount using the approved definition of collected premium.

**Actual Result:** Pending execution.

**Status:** Not Run.

**Evidence Reference:** Pending execution.

# 7. Business KPI Validation

The following metrics require independent verification against the database and documented business definitions.

| KPI | Validation Approach |
|---|---|
| Total Policies | Count distinct policy records |
| Active Policies | Count policies with Active status |
| Total Sum Insured | Sum eligible policy sum insured |
| Annual Premium | Sum annual premium for the defined policy population |
| Premium Collection | Sum qualifying collected payment amounts |
| Claims Frequency | Claims divided by the defined eligible policy population |
| Claims Settlement Time | Average settlement duration for eligible settled claims |
| Renewal Rate | Renewed policies divided by eligible renewal opportunities |
| Lapse Rate | Lapsed policies divided by the defined eligible policy population |
| Customer Retention | Retained customers divided by the defined eligible customer population |

**Important:** Each KPI must use a documented numerator, denominator, reporting period, and inclusion/exclusion rule. In particular, renewal rate, lapse rate, claims frequency, and customer retention should not be treated as interchangeable metrics.

# 8. Defect Management

All defects identified during UAT should be recorded and tracked until resolution or formal acceptance of the limitation.

## 8.1 Defect Severity

| Severity | Description | Example |
|---|---|---|
| Critical | Core functionality unavailable or major business output incorrect | Database unavailable |
| High | Major analytical result is incorrect | Incorrect premium collection KPI |
| Medium | Limited functionality or data inconsistency | Incorrect chart filtering |
| Low | Cosmetic or minor usability issue | Label alignment issue |

## 8.2 Defect Register

| Defect ID | Test Case ID | Description | Severity | Status | Resolution |
|---|---|---|---|---|---|
| DEF-001 | — | Placeholder – record an actual defect when identified | — | Not Opened | — |
| DEF-002 | — | Placeholder – record an actual defect when identified | — | Not Opened | — |

**Note:** Defects will be recorded here as they are identified during test execution. The current entries are placeholders. No defects are being claimed as identified or resolved at this stage.

# 9. Requirements Traceability

UAT test cases should map back to the requirements documented in the BRD.

| BRD Requirement | UAT Test Cases |
|---|---|
| FR-01 – Policy Data Management | UAT-001, UAT-002, UAT-003, UAT-004, UAT-005, UAT-006, UAT-007 |
| FR-02 – Customer Analytics | UAT-008 |
| FR-03 – Agent Analytics | No dedicated test case currently assigned |
| FR-04 – Product Analytics | No dedicated test case currently assigned |
| FR-05 – Premium Analytics | UAT-009, UAT-010, UAT-011 |
| FR-06 – Claims Analytics | UAT-012, UAT-013, UAT-014 |
| FR-07 – Renewal Analytics | UAT-015, UAT-016, UAT-017 |
| FR-08 – KPI Reporting | UAT-019 |
| FR-09 – Dashboard Filtering | UAT-018 |
| FR-10 – Data Quality Validation | UAT-024, UAT-025 |
| FR-11 – Trend Analysis | UAT-023 |
| FR-12 – Regional Analysis | UAT-022 |
| FR-13 – Product Performance Analysis | UAT-021 |
| FR-14 – Reporting and Visualization | UAT-020 |

The traceability mapping should be checked against the final BRD requirement wording and acceptance criteria before UAT execution. Requirements without dedicated coverage should be addressed if the corresponding functionality is implemented and in scope.

# 10. UAT Execution Summary

The following summary will be completed after actual testing.

| Metric | Result |
|---|---:|
| Total Test Cases | 25 |
| Executed | 0 |
| Passed | 0 |
| Failed | 0 |
| Blocked | 0 |
| Not Run | 25 |
| Pass Percentage | Pending |

**Pass Percentage Formula:**

Pass Percentage = (Passed Test Cases / Executed Test Cases) × 100

Blocked and Not Run cases should be reported separately. A pass percentage should not be presented as meaningful until test execution has started.


# 11. Roles and Responsibilities

| Role | Responsibility |
|---|---|
| Project Author / Business Analyst | Define business scenarios, requirements, and expected results |
| Data Analyst | Validate dataset accuracy, calculations, and analytical outputs |
| QA Reviewer | Execute test cases, document defects, and perform retesting |
| Business Stakeholder | Review business relevance and provide acceptance feedback |

For this portfolio demonstration, Prathmesh Aghor performs the Project Author, Business Analyst, Data Analyst, and QA Reviewer responsibilities.

Independent business stakeholder review and formal organizational approval have not yet been obtained.

# 12. UAT Sign-Off

UAT sign-off should be completed only after execution and review of the test results.

| Approval Role | Name | Status | Date |
|---|---|---|---|
| Project Author | Prathmesh Aghor | Pending | — |
| QA Reviewer | Prathmesh Aghor | Pending | — |
| Business Stakeholder | Not Assigned | Not Obtained | — |

## 12.1 Final UAT Decision

**Current Decision:** Pending Test Execution.

The project cannot be declared UAT-approved until the planned test cases have been executed, results reviewed, and outstanding defects assessed.

# 13. Limitations and Disclaimers

- UAT is based on the project's available datasets and implemented functionality.
- Synthetic or generated data, where used, does not establish real-world insurer performance.
- Business metrics are subject to the definitions documented in the BRD and supporting data dictionary.
- UAT completion does not constitute IRDAI approval, regulatory certification, or production readiness.
- External stakeholder approval is not claimed.

# 14. Related Project Documents

The following paths represent the agreed documentation structure for the repository. They must be checked against the actual repository folders when the files are created.

| Document | Repository Path |
|---|---|
| Business Requirements Document | `docs/BRD.md` |
| Data Dictionary | `docs/data_dictionary.md` |
| Data Governance Framework | `docs/Governance_Checklist.md` |
| UAT Plan | `docs/UAT_Plan.md` |

---

**Document Owner:** Prathmesh Aghor  
**Project:** PoliSight – Insurance Policy Intelligence & Analytics Platform  
**Version:** 1.1  
**Status:** Draft – Pending Test Execution