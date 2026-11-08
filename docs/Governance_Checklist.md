# PoliSight – Data Governance Checklist

**Project:** PoliSight – Insurance Policy Intelligence & Analytics Platform  
**Document:** Data Governance Checklist  
**Version:** 1.2  
**Prepared By:** Prathmesh Aghor  
**Status:** Preliminary Review Completed – Further Evidence Required  
**Project Classification:** Portfolio Demonstration  
**Last Updated:** 08 November 2026

---

## 1. Purpose

This checklist establishes the data governance controls and validation activities for PoliSight.

It provides a structured approach to managing insurance-related data throughout its lifecycle, including data collection, storage, processing, validation, access, usage, retention, and disposal.

The checklist supports data quality, consistency, security, accountability, and responsible use of data within the project.

## 2. Governance Status Definitions

| Status | Meaning |
|---|---|
| Not Started | Activity has not been initiated or implementation has not been evidenced |
| In Progress | Activity is currently being implemented |
| Implemented | Control is documented or configured, but verification is incomplete |
| Verified | Supporting evidence has been inspected and the stated control has been confirmed within the documented review scope |
| Not Applicable | Control does not apply to the project, with justification recorded |

**Review qualification:** Verified means the available evidence supports the specific control. It does not automatically mean the complete application is production-ready, independently audited, or compliant with a regulatory framework.

## 3. Data Ownership and Accountability

| ID | Governance Control | Expected Outcome | Status | Evidence / Remarks |
|---|---|---|---|---|
| DG-001 | Identify the project data owner | Data ownership is documented | Not Started | Formal ownership record not established |
| DG-002 | Identify data management responsibilities | Responsibilities are assigned | Not Started | Role responsibilities need formal documentation |
| DG-003 | Document the purpose of each dataset | Business purpose is defined | Implemented | Project purpose documented in BRD |
| DG-004 | Maintain a data inventory | All project datasets are listed | Not Started | Inventory needs to be created |
| DG-005 | Document data sources | Source and origin are identifiable | Implemented | Synthetic data generation approach inspected |
| DG-006 | Define responsibility for data quality | Validation ownership is established | Not Started | Formal responsibility matrix pending |

## 4. Data Classification and Privacy

| ID | Governance Control | Expected Outcome | Status | Evidence / Remarks |
|---|---|---|---|---|
| DG-007 | Classify datasets by sensitivity | Data classification is documented | Not Started | Classification register pending |
| DG-008 | Identify personal and sensitive information fields | Sensitive fields are identified | Not Started | Field-level privacy assessment pending |
| DG-009 | Avoid using real customer personal information without authorization | No unauthorized personal data is used | Not Started | Dataset provenance and authorization review pending |
| DG-010 | Use synthetic or appropriately anonymized data for demonstrations | Portfolio data does not expose real customers | Not Started | Faker-based generator inspected; generated dataset and outputs still require review |
| DG-011 | Remove unnecessary personal identifiers from analytical outputs | Reports minimize personal data exposure | Not Started | Dashboard and report review pending |
| DG-012 | Document applicable privacy and regulatory considerations | Relevant obligations are identified for the intended use | Not Started | Formal applicability assessment pending |

## 5. Data Quality Management

| ID | Governance Control | Expected Outcome | Status | Evidence / Remarks |
|---|---|---|---|---|
| DG-013 | Define data quality dimensions | Completeness, accuracy, consistency, validity, and uniqueness are documented | Not Started | Project-specific quality rules need formal documentation |
| DG-014 | Validate mandatory fields | Required fields are populated | Not Started | Execution evidence pending |
| DG-015 | Identify duplicate records | Duplicate records are detected | Not Started | Duplicate checks pending |
| DG-016 | Validate primary key uniqueness | Primary keys are unique | Not Started | Runtime validation pending |
| DG-017 | Validate foreign key relationships | Referential integrity is maintained | Not Started | Runtime validation pending |
| DG-018 | Validate date fields | Date values and date relationships are valid | Not Started | Data-level validation pending |
| DG-019 | Validate financial values | Premium, claim, and sum insured values follow defined rules | Not Started | Financial validation pending |
| DG-020 | Identify missing and null values | Missing values are measured and documented | Not Started | Missing-value profiling pending |
| DG-021 | Check permitted status values | Status fields use approved values | Not Started | Runtime data validation pending |
| DG-022 | Document data quality exceptions | Identified exceptions are recorded | Not Started | Issue register pending |
| DG-023 | Reconcile dashboard metrics with source data | Analytical outputs match independent calculations | Not Started | KPI reconciliation evidence pending |

## 6. Data Architecture and Integrity

PoliSight uses the following eight database tables:

- `dim_date`
- `dim_customers`
- `dim_agents`
- `dim_products`
- `fact_policies`
- `fact_premiums`
- `fact_claims`
- `fact_renewals`

| ID | Governance Control | Expected Outcome | Status | Evidence / Remarks |
|---|---|---|---|---|
| DG-024 | Maintain database schema documentation | Table structures and relationships are documented | Verified | Reviewed `sql/01_create_schema.sql` |
| DG-025 | Maintain a data dictionary | Field names, types, descriptions, and constraints are documented | Not Started | Data dictionary file not yet reviewed |
| DG-026 | Define primary keys | Each table has an appropriate primary key | Verified | Primary key definitions inspected in schema |
| DG-027 | Define foreign key relationships | Related records are linked correctly | Verified | Foreign key definitions inspected in schema |
| DG-028 | Apply appropriate database constraints | Invalid records are restricted where possible | Verified | Available primary key, unique, check, and foreign key constraints inspected; runtime enforcement not independently tested |
| DG-029 | Document transformation logic | Data processing steps are traceable | Implemented | Data-generation and transformation code inspected |
| DG-030 | Maintain consistent date and currency conventions | Values use consistent formats and units | Not Started | Convention documentation and data validation pending |

**Data Dictionary Reference:** The data dictionary should be maintained at `docs/data_dictionary.md`. It should document table names, column names, data types, definitions, constraints, relationships, and relevant business rules.

**Living Document Requirement:** The data dictionary should be updated whenever the database schema changes. Changes should be reviewed alongside the corresponding SQL and application updates.

## 7. Data Access and Security

| ID | Governance Control | Expected Outcome | Status | Evidence / Remarks |
|---|---|---|---|---|
| DG-031 | Restrict database access to authorized users | Unauthorized access is prevented | Not Started | Access-control review pending |
| DG-032 | Store credentials outside source code | Credentials are not committed to GitHub | Not Started | Repository-wide secret review pending |
| DG-033 | Maintain `.env` in `.gitignore` | Environment secrets are excluded from version control | Not Started | `.gitignore` contents need inspection |
| DG-034 | Use environment-specific database configuration | Local and production settings are separated where applicable | Not Started | Configuration review pending |
| DG-035 | Avoid exposing database credentials in logs | Sensitive configuration values are not logged | Not Started | Log review pending |
| DG-036 | Review repository files before publishing | No secrets or private datasets are uploaded | Not Started | Final repository security review pending |
| DG-037 | Document database backup arrangements | Recovery approach is documented where applicable | Not Started | Backup and recovery procedure pending |

## 8. Data Lifecycle Management

| ID | Governance Control | Expected Outcome | Status | Evidence / Remarks |
|---|---|---|---|---|
| DG-038 | Document data acquisition or generation methods | Dataset origin is recorded | Implemented | Synthetic data-generation methods inspected |
| DG-039 | Document data transformation processes | Transformation steps are traceable | Implemented | Data-generation script inspected; runtime lineage evidence pending |
| DG-040 | Maintain original source data where permitted | Reproducibility is supported | Not Started | Source-data retention approach pending |
| DG-041 | Define data retention expectations | Retention requirements are documented | Not Started | Retention policy pending |
| DG-042 | Define data deletion procedures | Unnecessary data can be securely removed | Not Started | Deletion procedure pending |
| DG-043 | Document backup and recovery procedures | Data recovery expectations are defined | Not Started | Recovery documentation pending |
| DG-044 | Prevent accidental database resets | Destructive operations require deliberate configuration | Not Started | Reset protection code exists, but operational safeguards and test evidence need further review |

## 9. Data Lineage and Auditability

| ID | Governance Control | Expected Outcome | Status | Evidence / Remarks |
|---|---|---|---|---|
| DG-045 | Document source-to-target data flow | Data movement is understandable | Not Started | Lineage diagram pending |
| DG-046 | Record important transformation rules | Analytical processing is reproducible | Not Started | Formal transformation specification pending |
| DG-047 | Maintain version control for SQL and Python scripts | Code changes are traceable | Not Started | Repository history and commit review pending |
| DG-048 | Record dataset generation parameters | Generated datasets can be reproduced | Implemented | Random seed and generation parameters inspected; reproducibility run pending |
| DG-049 | Document KPI calculation logic | Business metrics are explainable | Not Started | KPI specification pending |
| DG-050 | Maintain supporting validation evidence | Data quality and analytical checks can be reviewed | Not Started | Execution evidence repository pending |

## 10. Business Rules and Metric Governance

| ID | Governance Control | Expected Outcome | Status | Evidence / Remarks |
|---|---|---|---|---|
| DG-051 | Document policy status definitions | Policy statuses are interpreted consistently | Not Started | Formal business glossary pending |
| DG-052 | Define premium collection rules | Collected premium calculations are consistent | Not Started | KPI definition pending |
| DG-053 | Define overdue payment rules | Overdue calculations use documented conditions | Not Started | Business rule specification pending |
| DG-054 | Define claims frequency methodology | Claims frequency has a clear numerator and denominator | Not Started | Metric specification pending |
| DG-055 | Define claims settlement duration methodology | Settlement duration excludes ineligible records | Not Started | Metric specification pending |
| DG-056 | Define renewal eligibility | Renewal population is clearly identified | Not Started | Eligibility rule specification pending |
| DG-057 | Define lapse rate methodology | Lapse rate uses an approved project definition | Not Started | Metric specification pending |
| DG-058 | Define customer retention methodology | Retention calculations use a documented customer population | Not Started | Metric specification pending |
| DG-059 | Validate KPI calculations independently | Metrics reconcile with source records | Not Started | Independent calculation evidence pending |
| DG-060 | Document analytical assumptions and limitations | Users understand metric limitations | Implemented | Project limitations and assumptions documented in governance materials |

## 11. Regulatory and Responsible Data Use

The project is designed around an Indian non-life insurance analytics context. Regulatory references and compliance obligations must be evaluated according to the actual data, processing activities, and intended use.

| ID | Governance Control | Expected Outcome | Status | Evidence / Remarks |
|---|---|---|---|---|
| DG-061 | Identify applicable Indian data protection requirements | Relevant privacy obligations are assessed | Not Started | Formal applicability assessment pending |
| DG-062 | Review applicable IRDAI requirements where relevant | Insurance-sector considerations are documented | Not Started | Regulatory review pending |
| DG-063 | Avoid representing synthetic data as real insurer data | Dataset origin is transparently disclosed | Not Started | Final dataset and publication review pending |
| DG-064 | Avoid unsupported regulatory compliance claims | Project documentation accurately describes its status | Implemented | Project-level disclaimers documented |
| DG-065 | Document limitations of analytical recommendations | Outputs are not presented as guaranteed business decisions | Implemented | Limitations and disclaimers documented |
| DG-066 | Ensure portfolio examples do not disclose confidential information | Demonstration materials are appropriately sanitized | Not Started | Final publication review pending |

**International Data Protection Consideration:** For international projects, GDPR and other applicable data protection regulations must also be assessed based on the relevant jurisdictions, individuals, and processing activities.

## 12. Issue Management and Continuous Improvement

| ID | Governance Control | Expected Outcome | Status | Evidence / Remarks |
|---|---|---|---|---|
| DG-067 | Maintain a data quality issue register | Data issues are recorded | Not Started | Issue register not yet established |
| DG-068 | Assign severity to identified data issues | Issues are prioritized | Not Started | Severity assessment process pending |
| DG-069 | Document corrective actions | Resolution steps are traceable | Not Started | Corrective action register pending |
| DG-070 | Revalidate corrected datasets | Corrections do not introduce new inconsistencies | Not Started | Retesting evidence pending |
| DG-071 | Review governance controls periodically | Governance remains aligned with project changes | Not Started | Review cadence and ownership pending |

---

## 13. Governance Review Summary

<text strong>Preliminary evidence-based review – 08 November 2026</text>

| Metric | Reviewed Result |
|---|---:|
| Total Governance Controls | 71 |
| Implemented | 8 |
| Verified | 4 |
| In Progress | 0 |
| Not Started | 59 |
| Not Applicable | 0 |

<text weight="semibold" color="success">4 controls verified</text>

**Control verification percentage:**

\[
\frac{4}{71}\times100 = 5.63\%
\]

**Implementation coverage (Implemented + Verified):**

\[
\frac{8+4}{71}\times100 = 16.90\%
\]

**Interpretation:**

- Four controls have been verified against inspected schema artifacts.
- Eight controls have implementation or documentation evidence but still require verification.
- Fifty-nine controls remain not started or lack sufficient evidence to claim implementation.
- No controls have been marked Not Applicable without a documented justification.
- The figures describe a preliminary review of the available project artifacts, not an independent audit or enterprise compliance assessment.

## 14. Governance Evidence Register

| Evidence ID | Related Control ID | Evidence Description | File / Location | Review Status |
|---|---|---|---|---|
| EVD-001 | DG-025 | Data dictionary | `docs/data_dictionary.md` | Pending – file not yet reviewed |
| EVD-002 | DG-024, DG-026, DG-027, DG-028 | Database schema | `sql/01_create_schema.sql` | Verified – schema definitions inspected |
| EVD-003 | DG-013 to DG-023 | Data quality validation results | To be documented | Pending – execution evidence unavailable |
| EVD-004 | DG-029, DG-038, DG-039, DG-048 | Data generation and transformation scripts | `notebooks/03_generate_data_v3_final.py` | Verified – code inspected; runtime outputs not verified |
| EVD-005 | DG-049, DG-059 | KPI calculation and reconciliation evidence | To be documented | Pending – independent reconciliation not supplied |
| EVD-006 | DG-032 to DG-036 | Repository security review | `.gitignore` and repository review | Pending – review not completed |
| EVD-007 | DG-067 to DG-070 | Data quality issue register | To be created if issues are identified | Pending – register not established |

**Evidence review note:** Verified in this register means the referenced artifact was inspected for the stated scope. It does not imply that the generated data, runtime behavior, or all associated governance controls have passed testing.

## 15. Roles and Responsibilities

| Role | Responsibility |
|---|---|
| Project Author | Owns project documentation and governance checklist |
| Business Analyst | Defines business rules, data requirements, and ownership expectations |
| Data Analyst | Validates data quality, transformations, and KPI calculations |
| QA Reviewer | Reviews evidence and verifies applicable controls |
| Business Stakeholder | Provides independent review where applicable |

For this portfolio demonstration, Prathmesh Aghor performs the Project Author, Business Analyst, Data Analyst, and QA Reviewer responsibilities.

Independent organizational governance approval has not been obtained.

## 16. Governance Limitations, Version Control and Disclaimer

- This checklist represents a project-level data governance framework, not a certified enterprise governance program.
- Controls must be verified against actual implementation and supporting evidence.
- Synthetic data must be clearly identified and must not be represented as actual insurer customer or policy records.
- Regulatory references do not imply IRDAI approval or compliance certification.
- GDPR and other international requirements must be assessed where applicable; this checklist does not establish compliance with them.
- Privacy and security controls should be reassessed before any use of real personal or financial information.
- Formal organizational approval and independent stakeholder validation remain pending.
- **Version Control:** This checklist should be version-controlled alongside the codebase, and changes should be documented in a change log.

### Change Log

| Version | Date | Author | Change Description |
|---|---|---|---|
| 1.0 | 08 November 2026 | Prathmesh Aghor | Initial governance checklist |
| 1.1 | 08 November 2026 | Prathmesh Aghor | Added GDPR consideration and data dictionary reference |
| 1.2 | 08 November 2026 | Prathmesh Aghor | Added preliminary evidence-based control statuses, evidence review results, living-document guidance, and version-control requirements |

---

**Document Owner:** Prathmesh Aghor  
**Project:** PoliSight – Insurance Policy Intelligence & Analytics Platform  
**Version:** 1.2  
**Status:** Preliminary Review Completed – Further Evidence Required