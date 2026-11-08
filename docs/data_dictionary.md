# PoliSight – Insurance Policy Intelligence & Analytics Platform

# Data Dictionary

**Document Version:** 1.1  
**Prepared By:** Prathmesh Aghor  
**Project:** PoliSight – Insurance Policy Intelligence & Analytics Platform  
**Database:** PostgreSQL  
**Schema:** public  
**Document Status:** Draft – Schema-Based Documentation

---

## 1. Purpose

This document defines the database structure, fields, data types, business meanings, constraints, and relationships used in the PoliSight insurance analytics platform.

It serves as a reference for:

- Business Analysts understanding business data requirements.
- Data Analysts developing SQL queries, reports, and KPIs.
- Developers maintaining database structures and application logic.
- QA reviewers validating data integrity and business rules.
- Stakeholders understanding the information used for insurance policy analysis.

## 2. Database Overview

PoliSight uses a relational database design consisting of eight tables.

| Table | Category | Description |
|---|---|---|
| `dim_date` | Dimension | Calendar and reporting attributes |
| `dim_customers` | Dimension | Customer demographic and profile information |
| `dim_agents` | Dimension | Insurance agent and distribution channel information |
| `dim_products` | Dimension | Insurance product and coverage information |
| `fact_policies` | Fact | Insurance policy and policyholder information |
| `fact_premiums` | Fact | Premium installments and payment information |
| `fact_claims` | Fact | Insurance claims and settlement information |
| `fact_renewals` | Fact | Policy renewal and customer lifetime value information |

### 2.1 Database Design

The database follows a dimensional modelling approach:

- Dimension tables store descriptive information.
- Fact tables store insurance-related transactional and analytical information.
- Primary keys uniquely identify records.
- Foreign keys establish relationships between fact and dimension tables.

## 3. Data Type and Key Conventions

| Convention | Meaning |
|---|---|
| PK | Primary Key |
| FK | Foreign Key |
| UNIQUE | Unique constraint |
| NOT NULL | Value is mandatory |
| NULL | Value may be missing |
| DEFAULT | Database-provided default value |
| UUID | Universally Unique Identifier |
| DECIMAL(p,s) | Exact numeric value with precision and scale |
| SMALLINT | Small-range integer |
| BOOLEAN | True or false |
| DATE | Calendar date |
| TIMESTAMP | Date and time |

---

# 4. Dimension Tables

## 4.1 dim_date

**Business Purpose:** Stores calendar attributes used for time-based insurance analysis, reporting, and trend comparisons.

| Column | Data Type | Key | Nullable | Description |
|---|---|---|---|---|
| `date_id` | INTEGER | PK | No | Unique numeric identifier for a calendar date, represented in YYYYMMDD format. |
| `full_date` | DATE | UNIQUE | No | Actual calendar date. |
| `year` | SMALLINT | — | No | Calendar year. |
| `quarter` | SMALLINT | — | No | Calendar quarter, from 1 to 4. |
| `month` | SMALLINT | — | No | Numeric month, from 1 to 12. |
| `month_name` | VARCHAR(15) | — | Yes | Name of the month. |
| `week_of_year` | SMALLINT | — | Yes | Week number within the year. |
| `day_of_week` | SMALLINT | — | Yes | Numeric weekday representation. |
| `is_weekday` | BOOLEAN | — | Yes | Indicates whether the date falls on a weekday. |
| `is_fiscal_year_end` | BOOLEAN | — | Yes | Indicates whether the date is marked as fiscal year-end. Defaults to FALSE. |

**Primary Key:** `date_id`

**Unique Constraint:** `full_date`

**Business Applications:**
- Monthly and quarterly premium analysis.
- Year-over-year policy comparisons.
- Claims trend analysis.
- Policy issuance and renewal reporting.
- Fiscal-year reporting.

**Fiscal Year Convention:** The fiscal year convention used in the project should be explicitly documented. For Indian insurance reporting, an April–March financial year may be appropriate. The exact convention and fiscal year-end flag generation logic must be confirmed against the date-generation script before treating this field as validated.

**Implementation Note:** The generator creates calendar dates from 2015 through 2024. The `day_of_week` value uses Python's weekday convention: Monday = 0 and Sunday = 6.

## 4.2 dim_customers

**Business Purpose:** Stores customer profile information to support customer segmentation, demographic analysis, and insurance portfolio insights.

| Column | Data Type | Key | Nullable | Description |
|---|---|---|---|---|
| `customer_id` | UUID | PK | No | Unique identifier for each customer. Generated using `gen_random_uuid()`. |
| `first_name` | VARCHAR(100) | — | No | Customer's first name. |
| `last_name` | VARCHAR(100) | — | No | Customer's last name. |
| `date_of_birth` | DATE | — | No | Customer's date of birth. |
| `gender` | VARCHAR(20) | — | Yes | Customer gender category. |
| `education_level` | VARCHAR(50) | — | Yes | Highest recorded education category. |
| `marital_status` | VARCHAR(30) | — | Yes | Customer marital status. |
| `occupation` | VARCHAR(100) | — | Yes | Customer's occupation. |
| `income_bracket` | VARCHAR(30) | — | Yes | Categorized customer income range. |
| `city` | VARCHAR(100) | — | Yes | Customer's city. |
| `state` | VARCHAR(100) | — | Yes | Customer's state. |
| `customer_since` | DATE | — | No | Date from which the customer relationship is recorded. |
| `is_active` | BOOLEAN | — | Yes | Indicates whether the customer is active. Defaults to TRUE. |

**Primary Key:** `customer_id`

**Check Constraint:** `chk_gender`

Permitted gender values:
- Male
- Female
- Other

**Business Applications:**
- Customer segmentation.
- Demographic analysis.
- Income-based portfolio analysis.
- Customer retention analysis.
- Customer lifetime value assessment.

**Data Governance Consideration:** Customer names, dates of birth, income brackets, and location information should be handled as potentially sensitive personal information. Access should be restricted according to the project's data governance and security requirements.

## 4.3 dim_agents

**Business Purpose:** Stores insurance agent and agency information to support distribution channel and agent performance analysis.

| Column | Data Type | Key | Nullable | Description |
|---|---|---|---|---|
| `agent_id` | UUID | PK | No | Unique identifier for each insurance agent. |
| `agent_name` | VARCHAR(150) | — | No | Name of the insurance agent. |
| `agency_name` | VARCHAR(150) | — | Yes | Name of the associated agency. |
| `region` | VARCHAR(100) | — | Yes | Geographic region assigned to the agent. |
| `channel` | VARCHAR(50) | — | Yes | Distribution channel through which policies are sold. |
| `hire_date` | DATE | — | Yes | Agent's hiring or joining date. |
| `is_active` | BOOLEAN | — | Yes | Indicates whether the agent is currently active. Defaults to TRUE. |

**Primary Key:** `agent_id`

**Business Applications:**
- Agent-wise policy distribution.
- Regional performance analysis.
- Distribution channel comparisons.
- Agent productivity analysis.
- Policy acquisition reporting.

## 4.4 dim_products

**Business Purpose:** Stores insurance product information, including product categories, coverage types, and sum-insured limits.

| Column | Data Type | Key | Nullable | Description |
|---|---|---|---|---|
| `product_id` | UUID | PK | No | Unique identifier for each insurance product. |
| `product_name` | VARCHAR(150) | — | No | Name of the insurance product. |
| `product_line` | VARCHAR(50) | — | No | Broad insurance category, such as Motor, Health, Life, or Travel. |
| `coverage_type` | VARCHAR(100) | — | Yes | Type or scope of insurance coverage. |
| `vehicle_category` | VARCHAR(50) | — | Yes | Vehicle category, where applicable. |
| `base_premium_rate` | DECIMAL(8,4) | — | Yes | Configured base premium rate for the product. |
| `min_sum_insured` | DECIMAL(15,2) | — | Yes | Minimum configured sum-insured amount. |
| `max_sum_insured` | DECIMAL(15,2) | — | Yes | Maximum configured sum-insured amount. |
| `is_active` | BOOLEAN | — | Yes | Indicates whether the product is active. Defaults to TRUE. |

**Primary Key:** `product_id`

**Business Applications:**
- Product portfolio analysis.
- Product-line performance.
- Coverage-based segmentation.
- Sum-insured distribution.
- Product-level premium analysis.

**Data Quality Consideration:** Product configuration should be reviewed to ensure that minimum sum insured does not exceed maximum sum insured. The current schema does not enforce this rule through a CHECK constraint.

---

# 5. Fact Tables

## 5.1 fact_policies

**Business Purpose:** Stores insurance policy records and associated customer, product, agent, coverage, premium, and risk information.

| Column | Data Type | Key | Nullable | Description |
|---|---|---|---|---|
| `policy_id` | UUID | PK | No | Unique identifier for each insurance policy. |
| `customer_id` | UUID | FK | No | References the customer who owns the policy. |
| `product_id` | UUID | FK | No | References the insurance product associated with the policy. |
| `agent_id` | UUID | FK | Yes | References the agent associated with the policy. |
| `policy_start_date_id` | INTEGER | FK | No | References the policy start date in `dim_date`. |
| `policy_end_date_id` | INTEGER | FK | No | References the policy end date in `dim_date`. |
| `policy_number` | VARCHAR(50) | UNIQUE | No | Business-facing unique policy reference number. |
| `policy_status` | VARCHAR(30) | — | No | Current recorded policy status. |
| `sum_insured` | DECIMAL(15,2) | — | No | Maximum insured coverage amount recorded for the policy. |
| `annual_premium` | DECIMAL(10,2) | — | No | Annual premium amount associated with the policy. |
| `risk_score` | DECIMAL(5,2) | — | Yes | Simulated or calculated policy risk indicator. |
| `policy_tenure_months` | SMALLINT | — | Yes | Policy duration in months. |
| `is_renewed` | BOOLEAN | — | Yes | Indicates whether the policy is marked as renewed. Defaults to FALSE. |
| `is_lapsed` | BOOLEAN | — | Yes | Indicates whether the policy is marked as lapsed. Defaults to FALSE. |
| `lapse_reason_code` | SMALLINT | — | Yes | Numeric code representing the reason for policy lapse. |
| `created_at` | TIMESTAMP | — | Yes | Timestamp when the record is created. Defaults to NOW(). |
| `updated_at` | TIMESTAMP | — | Yes | Timestamp when the record is updated. Defaults to NOW(). |

**Primary Key:** `policy_id`

**Foreign Keys:**
- `customer_id` → `dim_customers.customer_id`
- `product_id` → `dim_products.product_id`
- `agent_id` → `dim_agents.agent_id`
- `policy_start_date_id` → `dim_date.date_id`
- `policy_end_date_id` → `dim_date.date_id`

**Unique Constraint:** `policy_number`

**Check Constraints:**

`chk_policy_status`

Permitted values:
- Active
- Lapsed
- Expired
- Cancelled
- Renewed

`chk_dates`

The policy end date identifier must be greater than the policy start date identifier.

**Business Applications:**
- Total policy count.
- Active, expired, cancelled, and lapsed policy analysis.
- Policy renewal analysis.
- Risk segmentation.
- Sum-insured and premium distribution.
- Customer and agent portfolio analysis.

**Risk Score Interpretation:** The risk score range and calculation methodology should be documented alongside the model or business logic that generates it. The current generator uses a simulated score; it is not a validated underwriting model. It should not be interpreted as an actual insurer's underwriting decision or validated risk assessment.

## 5.2 fact_premiums

**Business Purpose:** Stores premium installment and payment information associated with insurance policies.

| Column | Data Type | Key | Nullable | Description |
|---|---|---|---|---|
| `premium_id` | UUID | PK | No | Unique identifier for each premium installment record. |
| `policy_id` | UUID | FK | No | References the associated insurance policy. |
| `due_date_id` | INTEGER | FK | No | References the premium installment due date in `dim_date`. |
| `paid_date_id` | INTEGER | FK | Yes | References the date on which payment was recorded. |
| `installment_type` | VARCHAR(20) | — | No | Premium payment frequency or installment category. |
| `amount_due` | DECIMAL(10,2) | — | No | Amount payable for the installment. |
| `amount_paid` | DECIMAL(10,2) | — | Yes | Amount received against the installment. Defaults to 0. |
| `days_to_payment` | SMALLINT | — | Yes | Recorded number of days associated with payment timing. |
| `payment_method` | VARCHAR(50) | — | Yes | Payment method used by the customer. |
| `payment_status` | VARCHAR(20) | — | No | Payment status of the installment. |
| `is_overdue` | BOOLEAN | — | Yes | Indicates whether the installment is marked overdue. Defaults to FALSE. |

**Primary Key:** `premium_id`

**Foreign Keys:**
- `policy_id` → `fact_policies.policy_id`
- `due_date_id` → `dim_date.date_id`
- `paid_date_id` → `dim_date.date_id`

**Check Constraint:** `chk_payment_status`

Permitted values:
- Paid
- Overdue
- Waived
- Partial

**Generator Reference Values:**

Installment types:
- Annual
- Semi-Annual
- Quarterly
- Monthly

Payment methods:
- UPI
- NEFT
- Credit Card
- Cheque
- Cash

These are generator reference values, not database-enforced CHECK constraints.

**Business Applications:**
- Premium collection analysis.
- Outstanding premium analysis.
- Overdue installment monitoring.
- Payment method analysis.
- Payment frequency comparisons.
- Collection efficiency reporting.

## 5.3 fact_claims

**Business Purpose:** Stores insurance claim information, including claim amount, status, approval, rejection, and settlement details.

| Column | Data Type | Key | Nullable | Description |
|---|---|---|---|---|
| `claim_id` | UUID | PK | No | Unique identifier for each insurance claim. |
| `policy_id` | UUID | FK | No | References the insurance policy associated with the claim. |
| `incident_date_id` | INTEGER | FK | No | References the date on which the incident occurred. |
| `filed_date_id` | INTEGER | FK | No | References the date on which the claim was filed. |
| `settled_date_id` | INTEGER | FK | Yes | References the claim settlement date, where applicable. |
| `claim_type` | VARCHAR(50) | — | Yes | Category or type of insurance claim. |
| `claim_status` | VARCHAR(30) | — | No | Current recorded status of the claim. |
| `claim_amount` | DECIMAL(15,2) | — | No | Total amount submitted or recorded for the claim. |
| `approved_amount` | DECIMAL(15,2) | — | Yes | Amount approved for the claim. Defaults to 0. |
| `rejected_amount` | DECIMAL(15,2) | — | Yes | Amount rejected for the claim. Defaults to 0. |
| `days_to_settlement` | SMALLINT | — | Yes | Recorded number of days taken for settlement. |
| `rejection_reason` | VARCHAR(200) | — | Yes | Reason recorded when a claim is rejected. |

**Primary Key:** `claim_id`

**Foreign Keys:**
- `policy_id` → `fact_policies.policy_id`
- `incident_date_id` → `dim_date.date_id`
- `filed_date_id` → `dim_date.date_id`
- `settled_date_id` → `dim_date.date_id`

**Check Constraint:** `chk_claim_status`

Permitted values:
- Filed
- Under Review
- Approved
- Rejected
- Settled

**Business Applications:**
- Claim frequency analysis.
- Claim approval and rejection rates.
- Claims amount analysis.
- Average settlement time.
- Claims by product and region.
- Portfolio loss ratio analysis.

**Data Quality Considerations:**
- Incident dates should logically precede or equal filing dates.
- Settlement dates should be populated only when appropriate to the claim status.
- Approved and rejected amounts should be reconciled against the claim amount according to defined business rules.
- The current schema does not enforce these conditions through CHECK constraints.

## 5.4 fact_renewals

**Business Purpose:** Stores policy renewal information and associated premium changes, renewal decisions, and customer lifetime value estimates.

| Column | Data Type | Key | Nullable | Description |
|---|---|---|---|---|
| `renewal_id` | UUID | PK | No | Unique identifier for each renewal record. |
| `policy_id` | UUID | FK | No | References the original insurance policy. |
| `new_policy_id` | UUID | FK | Yes | References the new policy created through renewal, if available. |
| `renewal_date_id` | INTEGER | FK | No | References the renewal date in `dim_date`. |
| `original_start_date_id` | INTEGER | FK | No | References the original policy start date in `dim_date`. |
| `renewal_number` | SMALLINT | — | No | Sequential renewal number. Defaults to 1. |
| `previous_premium` | DECIMAL(10,2) | — | No | Premium amount before renewal. |
| `new_premium` | DECIMAL(10,2) | — | Yes | Premium amount after renewal, where applicable. |
| `premium_change_pct` | DECIMAL(6,2) | — | Yes | Percentage change between previous and new premium. |
| `renewed` | BOOLEAN | — | No | Indicates whether the policy was renewed. Defaults to FALSE. |
| `non_renewal_reason` | VARCHAR(100) | — | Yes | Recorded reason when a policy is not renewed. |
| `clv_at_renewal` | DECIMAL(12,2) | — | Yes | Estimated customer lifetime value recorded at renewal. |

**Primary Key:** `renewal_id`

**Foreign Keys:**
- `policy_id` → `fact_policies.policy_id`
- `new_policy_id` → `fact_policies.policy_id`
- `renewal_date_id` → `dim_date.date_id`
- `original_start_date_id` → `dim_date.date_id`

**Business Applications:**
- Policy renewal rate.
- Non-renewal analysis.
- Premium change analysis.
- Customer retention analysis.
- Customer lifetime value estimation.
- Renewal trends by product and region.

**Data Interpretation Note:** In the current generator, `new_policy_id` is populated as NULL. The field is available in the schema for linking a subsequent policy but is not currently populated by the generation logic.

The current CLV calculation is an estimate based on collected premium assumptions, approved claim amounts, and an assumed acquisition cost. It should not be interpreted as an audited financial or actuarial valuation.

---

# 6. Table Relationships

The following relationships define how records are connected across the PoliSight database.

| Parent Table | Parent Column | Child Table | Child Column | Relationship |
|---|---|---|---|---|
| `dim_customers` | customer_id | `fact_policies` | customer_id | One-to-Many |
| `dim_products` | product_id | `fact_policies` | product_id | One-to-Many |
| `dim_agents` | agent_id | `fact_policies` | agent_id | One-to-Many |
| `dim_date` | date_id | `fact_policies` | policy_start_date_id | One-to-Many |
| `dim_date` | date_id | `fact_policies` | policy_end_date_id | One-to-Many |
| `fact_policies` | policy_id | `fact_premiums` | policy_id | One-to-Many |
| `fact_policies` | policy_id | `fact_claims` | policy_id | One-to-Many |
| `fact_policies` | policy_id | `fact_renewals` | policy_id | One-to-Many |
| `fact_policies` | policy_id | `fact_renewals` | new_policy_id | One-to-Many |
| `dim_date` | date_id | `fact_premiums` | due_date_id | One-to-Many |
| `dim_date` | date_id | `fact_premiums` | paid_date_id | One-to-Many |
| `dim_date` | date_id | `fact_claims` | incident_date_id | One-to-Many |
| `dim_date` | date_id | `fact_claims` | filed_date_id | One-to-Many |
| `dim_date` | date_id | `fact_claims` | settled_date_id | One-to-Many |
| `dim_date` | date_id | `fact_renewals` | renewal_date_id | One-to-Many |
| `dim_date` | date_id | `fact_renewals` | original_start_date_id | One-to-Many |

## 6.1 Logical Relationship Summary

- One customer can have multiple insurance policies.
- One product can be associated with multiple policies.
- One agent can manage multiple policies.
- One policy can have multiple premium installment records.
- One policy can have multiple claims.
- One policy can have multiple renewal records.
- The date dimension supports multiple date roles across insurance transactions.

---

# 7. Important Business Terms

| Business Term | Definition |
|---|---|
| Policy | An insurance contract recorded in the system. |
| Premium | Amount payable by the policyholder for insurance coverage. |
| Sum Insured | Maximum insured coverage amount recorded for a policy. |
| Claim | A request for compensation under an insurance policy. |
| Approved Amount | Amount approved for a claim. |
| Rejected Amount | Amount rejected for a claim. |
| Policy Lapse | A policy marked as lapsed due to non-continuation or another recorded reason. |
| Renewal | Continuation of an existing insurance policy for a subsequent term. |
| Premium Change | Difference between the previous and new premium amounts. |
| Risk Score | Numeric indicator used to represent a policy's risk level. |
| Customer Lifetime Value (CLV) | Estimated value associated with a customer relationship over a defined period. |
| Distribution Channel | Method through which an insurance product is sold. |
| Loss Ratio | A claims-to-premium measure whose exact numerator and denominator must be defined consistently. |

# 8. Data Quality and Validation Rules

The following rules are recommended for data validation. The `Enforced by Schema?` column indicates whether the current SQL schema directly enforces the stated rule. A No indicates that the rule requires separate business logic, application validation, or data-quality testing.

| Rule ID | Validation Rule | Relevant Table | Enforced by Schema? | Priority |
|---|---|---|---|---|
| DQ-001 | Policy number must be unique. | fact_policies | Yes – UNIQUE | High |
| DQ-002 | Every policy must reference an existing customer. | fact_policies | Yes – FK | High |
| DQ-003 | Every policy must reference an existing product. | fact_policies | Yes – FK | High |
| DQ-004 | Policy end date must be after policy start date. | fact_policies | Yes – CHECK | High |
| DQ-005 | Annual premium must be greater than zero. | fact_policies | No | High |
| DQ-006 | Sum insured must be greater than zero. | fact_policies | No | High |
| DQ-007 | Amount paid should not exceed amount due unless an approved business exception exists. | fact_premiums | No | Medium |
| DQ-008 | Paid installments should have a valid paid date. | fact_premiums | No | High |
| DQ-009 | Claim amount must be non-negative. | fact_claims | No | High |
| DQ-010 | Approved and rejected amounts should be reconciled with claim amount. | fact_claims | No | High |
| DQ-011 | Claim filing date should not precede incident date. | fact_claims | No | High |
| DQ-012 | Settled claims should have a valid settlement date. | fact_claims | No | High |
| DQ-013 | Renewal premium change percentage should reconcile with previous and new premiums. | fact_renewals | No | Medium |
| DQ-014 | Renewed policies should have a valid new premium. | fact_renewals | No | High |
| DQ-015 | Product minimum sum insured should not exceed maximum sum insured. | dim_products | No | Medium |
| DQ-016 | Customer date of birth should be earlier than customer_since. | dim_customers | No | Medium |

**Important:** Schema enforcement does not prove that existing records are valid. Foreign keys and CHECK constraints must also be tested against the actual database. Rules marked No require separate implementation and execution evidence before being considered verified controls.

---

# 9. Data Security and Governance Considerations

The following controls are recommended for responsible data handling:

1. Restrict access to customer-level personal information.
2. Avoid publishing real customer names, dates of birth, or financial details in public repositories.
3. Use synthetic or appropriately anonymized data for portfolio demonstrations.
4. Store database credentials in environment variables and exclude `.env` files from version control.
5. Apply role-based access control when deploying the database in a shared environment.
6. Maintain appropriate backups and recovery procedures.
7. Document data sources, transformations, and assumptions.
8. Validate data quality before using data for dashboards or analytical models.
9. Review retention and deletion requirements before using real customer information.
10. Do not represent a synthetic demonstration dataset as actual insurer or policyholder data.

# 10. Known Schema Limitations and Future Improvements

The following items are identified from the current schema and generator design. Priorities indicate recommended improvement order, not completed implementation status.

| Area | Current Limitation | Recommended Improvement | Priority |
|---|---|---|---|
| Policy dates | Date validation relies on date identifiers. | Add explicit date-role validation and reporting checks. | High |
| Customer data | Personal information is stored directly. | Apply access restrictions and masking where appropriate. | High |
| Product limits | Minimum and maximum sum insured are not checked against each other. | Add a CHECK constraint. | Medium |
| Premium payments | Payment amount and payment date consistency are not enforced. | Add business validation rules. | High |
| Claims | Amount reconciliation is not enforced. | Add claim amount validation. | High |
| Claims | Claim date sequence is not enforced. | Validate incident, filing, and settlement chronology. | High |
| Renewals | `new_policy_id` is currently not populated by the generator. | Link renewed records to newly created policy records when implemented. | Medium |
| Renewal history | Renewal number defaults to 1. | Validate sequential renewal numbering. | Medium |
| Audit fields | `updated_at` has a default but no automatic update mechanism is defined in this schema. | Add an update trigger or application-level timestamp handling. | Low |
| Data lineage | Source and transformation metadata are not stored in the schema. | Maintain separate data lineage documentation. | Medium |

# 11. Source and Documentation References

| Reference | Location | Purpose |
|---|---|---|
| Database Schema | `sql/01_create_schema.sql` | Source of table definitions, columns, constraints, and indexes. |
| Data Generator | `notebooks/03_generate_data_v3_final.py` | Source of synthetic data generation logic and generator reference values. |
| Business Requirements Document | `docs/BRD.md` | Business requirements and expected platform capabilities. |
| UAT Plan | `docs/UAT_Plan.md` | Functional testing and acceptance criteria. |
| Data Governance Checklist | `docs/Governance_Checklist.md` | Governance control tracking and evidence status. |

# 12. Document Maintenance

This document must be updated whenever:

- A table is added or removed.
- A column is added, modified, or removed.
- A data type or nullability rule changes.
- A primary key, foreign key, index, or constraint changes.
- Business definitions or transformation logic change.
- New data validation rules are introduced.

The data dictionary should be reviewed alongside the Data Governance Checklist, particularly control **DG-025**, and updated whenever the database schema changes.

All changes should be recorded in the document change history and reviewed against the actual database schema.

# 13. Change History

| Version | Date | Author | Description |
|---|---|---|---|
| 1.0 | 08-Nov-2026 | Prathmesh Aghor | Initial data dictionary prepared from the PoliSight PostgreSQL schema and generator definitions. |
| 1.1 | 08-Nov-2026 | Prathmesh Aghor | Added fiscal-year convention note, risk-score methodology disclaimer, schema enforcement indicators for data quality rules, improvement priorities, and DG-025 governance cross-reference. |

---

**Document Owner:** Prathmesh Aghor  
**Project:** PoliSight – Insurance Policy Intelligence & Analytics Platform  
**Status:** Draft – Pending database and data-quality validation
