# POLISIGHT
## Business Requirements Document (BRD)

**Project:** Insurance Policy Intelligence & Analytics Platform  
**Document Type:** Business Requirements Document  
**Version:** 1.1  
**Status:** Draft – For Review  
**Prepared By:** Prathmesh Aghor
**Industry:** Insurance / InsurTech  
**Project Category:** Business Intelligence, Data Analytics & Decision Support

---

# 1. Executive Summary

PoliSight is an Insurance Policy Intelligence and Analytics Platform designed to organize insurance portfolio information and provide analytical insights into policy performance, premium collections, claims, renewals, customer risk, and portfolio profitability.

Insurance businesses manage large volumes of information across customers, agents, insurance products, policies, premiums, and claims. When these datasets are fragmented or difficult to analyze, business stakeholders may struggle to monitor policy performance, identify potential customer lapses, understand claims patterns, and evaluate portfolio health.

PoliSight aims to address these challenges through a centralized relational database, Python-based data processing, analytical methodologies, and business intelligence reporting.

The platform focuses on transforming structured insurance data into meaningful business insights that can support operational monitoring and management decision-making.

The proposed solution includes:

- Insurance policy portfolio analysis.
- Premium collection and payment monitoring.
- Claims analysis and settlement tracking.
- Customer risk and policy lapse analysis.
- Policy renewal and customer lifetime value analysis.
- Product and agent performance analysis.
- Business intelligence reporting and KPI monitoring.

The current project implementation includes a PostgreSQL database schema and Python-based synthetic data generation. Further dashboard and analytical functionality must be validated against the implemented project before being represented as completed capabilities.

# 2. Business Background

Insurance organizations require continuous monitoring of their policy portfolios to understand business performance and operational risks.

Important business activities include:

1. Managing customer and policy information.
2. Monitoring premium payments and overdue installments.
3. Tracking claims and settlement outcomes.
4. Monitoring policy renewals and lapses.
5. Evaluating customer and product-level risk.
6. Measuring premium collection and claims-related performance.
7. Understanding customer value and retention.

Without consolidated analytical reporting, these activities can become difficult to evaluate across multiple business dimensions.

## 2.1 Indian Insurance Industry Context

The Indian insurance industry operates within a regulatory framework overseen by the Insurance Regulatory and Development Authority of India (IRDAI). Non-life insurance organizations must monitor important portfolio indicators, including premium performance, claims experience, policyholder servicing, and business sustainability.

These indicators provide important context for insurance portfolio analysis.

PoliSight incorporates insurance-oriented analytical measures such as claims-to-premium ratios, policy lapse rates, premium collection performance, and renewal trends.

For demonstration purposes, the synthetic data-generation methodology may use a 70–110% claims-to-premium ratio as an illustrative calibration range. This is a project assumption, not a representation of an official IRDAI-prescribed benchmark or regulatory compliance threshold.

# 3. Business Problem Statement

The project addresses the following business challenges:

| ID | Business Problem | Business Impact |
|---|---|---|
| BP-01 | Insurance information is distributed across different business entities and records. | Difficulty obtaining a consolidated portfolio view. |
| BP-02 | Premium collection and overdue payments require continuous monitoring. | Limited visibility into collection performance. |
| BP-03 | Claims information is difficult to evaluate alongside policy information. | Reduced visibility into claims patterns and financial exposure. |
| BP-04 | Policy lapses and renewals affect customer retention. | Difficulty identifying retention-related patterns. |
| BP-05 | Customer and product risk characteristics may not be evaluated consistently. | Limited risk-based portfolio analysis. |
| BP-06 | Management requires consolidated business performance indicators. | Slower and less informed decision-making. |

# 4. Business Objectives

| Objective ID | Business Objective | Expected Outcome |
|---|---|---|
| BO-01 | Centralize insurance-related analytical data. | Consistent portfolio-level data structure. |
| BO-02 | Monitor policy distribution and status. | Improved policy portfolio visibility. |
| BO-03 | Analyze premium collections and overdue payments. | Better understanding of payment behavior. |
| BO-04 | Evaluate claims frequency and financial amounts. | Improved claims performance visibility. |
| BO-05 | Analyze renewal and lapse patterns. | Better understanding of retention performance. |
| BO-06 | Develop customer and policy risk indicators. | Support risk-based analysis. |
| BO-07 | Measure customer lifetime value. | Better understanding of customer economics. |
| BO-08 | Provide consolidated business intelligence reporting. | Data-supported management decisions. |

# 5. Project Scope

## 5.1 In Scope

**A. Customer Management Analytics**
- Customer demographic analysis.
- Customer distribution by geography.
- Income and occupation-based segmentation.
- Customer activity analysis.

**B. Insurance Product Analytics**
- Insurance product categorization.
- Product-line analysis.
- Coverage and sum-insured analysis.
- Product-level premium analysis.

**C. Policy Portfolio Analytics**
- Total policy volume.
- Policy status distribution.
- Policy tenure analysis.
- Sum insured and annual premium analysis.
- Policy-level risk scoring.
- Policy lapse analysis.

**D. Premium Analytics**
- Premium installment analysis.
- Payment status monitoring.
- Paid, overdue, waived, and partial payment analysis.
- Payment method distribution.
- Days-to-payment analysis.

**E. Claims Analytics**
- Claims frequency analysis.
- Claims categorization.
- Claims status distribution.
- Approved and rejected claim amounts.
- Settlement time analysis.

**F. Renewal and Customer Value Analytics**
- Renewal performance.
- Premium changes at renewal.
- Non-renewal reason analysis.
- Customer lifetime value estimation.

**G. Business Intelligence**
- KPI monitoring.
- Trend analysis.
- Product, customer, policy, and claims segmentation.
- Management reporting.

## 5.2 Out of Scope

- Actual insurance policy issuance.
- Real-time premium payment processing.
- Integration with banking or payment gateways.
- Automated claim approval or rejection.
- Production insurance underwriting.
- Direct integration with external insurance company systems.
- Regulatory filing or statutory reporting.
- Automated communication with customers.
- Production-grade predictive model deployment.

These capabilities may be considered in future versions.

# 6. Stakeholder Identification

| Stakeholder | Responsibility | Information Required |
|---|---|---|
| Business Management | Monitor overall business performance. | Portfolio KPIs and financial indicators. |
| Insurance Operations Team | Monitor policy and premium operations. | Policy status and payment information. |
| Claims Management Team | Monitor claims activity. | Claims status, amounts, and settlement trends. |
| Sales and Distribution Team | Evaluate sales and agent performance. | Product, agent, and customer distribution. |
| Risk Management Team | Evaluate risk patterns. | Risk scores and lapse indicators. |
| Business Analyst | Gather requirements and validate business outcomes. | Requirements, KPIs, and acceptance criteria. |
| Data Analyst | Prepare and analyze business data. | Structured datasets and analytical results. |
| Technical Team | Develop and maintain the platform. | Database, processing, and reporting requirements. |

# 7. Functional Business Requirements

| Requirement ID | Requirement Description | Priority |
|---|---|---|
| FR-01 | The system shall maintain structured customer information. | High |
| FR-02 | The system shall maintain insurance agent information. | High |
| FR-03 | The system shall maintain insurance product information. | High |
| FR-04 | The system shall maintain policy records linked to customers, products, agents, and dates. | High |
| FR-05 | The system shall record policy status, tenure, sum insured, and annual premium. | High |
| FR-06 | The system shall maintain premium installment and payment information. | High |
| FR-07 | The system shall identify paid, overdue, waived, and partial premium installments. | High |
| FR-08 | The system shall maintain insurance claims and their associated policy records. | High |
| FR-09 | The system shall record claim status, claim amount, approved amount, and rejected amount. | High |
| FR-10 | The system shall maintain policy renewal information. | High |
| FR-11 | The system shall calculate or store policy risk indicators. | Medium |
| FR-12 | The system shall support policy lapse analysis. | High |
| FR-13 | The system shall support customer lifetime value estimation. | Medium |
| FR-14 | The system shall support analytical reporting across business dimensions. | High |

# 8. Non-Functional Business Requirements

| Requirement ID | Requirement | Expected Standard |
|---|---|---|
| NFR-01 | Data Integrity | Referential integrity between related database entities. |
| NFR-02 | Data Quality | Validation of required fields, formats, and business rules. |
| NFR-03 | Performance | Efficient processing of analytical datasets. |
| NFR-04 | Maintainability | Modular and documented Python and SQL implementation. |
| NFR-05 | Scalability | Architecture should support larger analytical datasets. |
| NFR-06 | Security | Database credentials must not be committed to public repositories. |
| NFR-07 | Reliability | Data generation and processing should report execution errors. |
| NFR-08 | Usability | Analytical reports should present understandable business indicators. |
| NFR-09 | Auditability | Data processing and validation activities should be documented. |

# 9. Business Rules

| Rule ID | Business Rule |
|---|---|
| BR-01 | Every policy must be associated with a valid customer. |
| BR-02 | Every policy must reference a valid insurance product. |
| BR-03 | Policy start and end dates must reference valid date records. |
| BR-04 | Policy end date must be later than policy start date. |
| BR-05 | Every premium installment must be associated with a valid policy. |
| BR-06 | Every claim must be associated with a valid policy. |
| BR-07 | Every renewal record must reference an existing policy. |
| BR-08 | Policy statuses must follow the defined database constraints. |
| BR-09 | Premium payment statuses must follow the defined database constraints. |
| BR-10 | Claim statuses must follow the defined database constraints. |
| BR-11 | Approved claim amounts must not be treated as paid claims without an appropriate settlement definition. |
| BR-12 | Financial KPIs must use documented aggregation logic to avoid duplicate counting. |

# 10. Key Performance Indicators (KPIs)

| KPI | Business Definition | Calculation |
|---|---|---|
| Total Policies | Number of policies in the portfolio. | COUNT(policy_id) |
| Active Policies | Number of policies with Active status. | COUNT of Active policies |
| Policy Lapse Rate | Percentage of policies identified as lapsed. | Lapsed policies / Total policies × 100 |
| Premium Collection | Total amount collected from premium payments. | SUM(amount_paid) |
| Overdue Premium Amount | Total unpaid amount for overdue installments. | SUM(amount_due) for Overdue records |
| Claims Frequency | Percentage of policies with at least one claim. | Policies with claims / Eligible policies × 100 |
| Total Claims | Total reported claim amount. | SUM(claim_amount) |
| Approved Claims | Total approved claim amount. | SUM(approved_amount) |
| Renewal Rate | Percentage of eligible policies renewed. | Renewed policies / Eligible policies × 100 |
| Average Customer Lifetime Value | Average estimated customer value. | AVG(clv_at_renewal) |

**Claims-to-Paid-Premium Ratio**

\[
\frac{\text{Total Approved Claim Amount}}{\text{Total Paid Premium Amount}}\times100
\]

This is an analytical ratio for the project, not necessarily an insurer's official actuarial loss ratio. An official loss ratio requires agreed accounting definitions and appropriate earned-premium and incurred-claims treatment.

All KPIs must be independently validated against the database before being presented as verified results.

# 11. Data Requirements

The platform uses a relational data model consisting of eight principal tables.

| Table | Business Purpose |
|---|---|
| dim_date | Calendar and date analysis. |
| dim_customers | Customer demographic and profile information. |
| dim_agents | Agent and distribution information. |
| dim_products | Insurance product information. |
| fact_policies | Policy portfolio information. |
| fact_premiums | Premium installment and payment information. |
| fact_claims | Claims and settlement information. |
| fact_renewals | Policy renewal and customer value information. |

The current project uses PostgreSQL for structured storage and Python libraries for data generation and analytical processing.

Detailed field-level definitions, data types, descriptions, and business meanings should be maintained in `docs/data_dictionary.md`.

**Data assumption:** The current generator creates synthetic insurance records. These records must not be represented as actual customer transactions or real insurance company data.

# 12. Assumptions and Dependencies

## 12.1 Assumptions

1. The project uses synthetic data for development and demonstration.
2. Customer, agent, product, policy, premium, claim, and renewal information follows the defined relational schema.
3. Business KPIs use documented calculation definitions.
4. Analytical outputs are intended for demonstration and decision-support purposes.
5. Risk scores and lapse probabilities are simulated indicators and are not validated underwriting models.

## 12.2 Dependencies

- PostgreSQL database availability.
- Python environment and required dependencies.
- Successful execution of SQL schema scripts.
- Valid data-generation logic.
- Consistent relationships between database tables.
- Availability of reporting and visualization components.

# 13. Risks and Constraints

| Risk ID | Risk | Potential Impact | Mitigation |
|---|---|---|---|
| R-01 | Synthetic data may not reflect real insurance behavior. | Misleading business conclusions. | Clearly label simulated data and document assumptions. |
| R-02 | Incorrect KPI aggregation. | Inaccurate business reporting. | Validate calculations using independent SQL queries. |
| R-03 | Inconsistent policy and transaction dates. | Incorrect lifecycle analysis. | Apply date validation rules. |
| R-04 | Large data volume may affect processing. | Slow execution or memory constraints. | Use batch processing and performance optimization. |
| R-05 | Incorrect relationships between tables. | Data integrity issues. | Validate primary and foreign key relationships. |
| R-06 | Unvalidated risk methodology. | Misinterpretation of risk scores. | Document methodology and limitations. |

# 14. Acceptance Criteria

| Acceptance ID | Acceptance Criteria | Evidence Required |
|---|---|---|
| AC-01 | All eight database tables are created successfully. | Database schema verification. |
| AC-02 | Records are generated and inserted successfully. | Table row counts. |
| AC-03 | Customer and policy relationships are valid. | Foreign key validation. |
| AC-04 | Premium records are correctly associated with policies. | SQL validation queries. |
| AC-05 | Claims records are correctly associated with policies. | SQL validation queries. |
| AC-06 | Renewal records follow documented business rules. | Renewal validation report. |
| AC-07 | KPI calculations reconcile with underlying records. | KPI reconciliation report. |
| AC-08 | Data quality checks are completed. | Data quality report. |
| AC-09 | Business users can interpret analytical outputs. | UAT execution evidence. |
| AC-10 | Critical and high-priority defects are resolved or formally accepted. | Defect log and sign-off. |

Detailed UAT test scenarios, expected results, and actual Pass/Fail records will be maintained in `docs/UAT_Plan.md`.

Acceptance criteria are requirements, not completed test results. Actual acceptance must be established through testing.

# 15. Requirements Traceability Matrix

The following matrix establishes traceability between business objectives, functional requirements, and acceptance criteria.

| Business Objective | Functional Requirements | Acceptance Criteria |
|---|---|---|
| BO-01 – Centralize data | FR-01, FR-02, FR-03, FR-04 | AC-01, AC-02 |
| BO-02 – Monitor policy distribution | FR-05 | AC-03 |
| BO-03 – Analyze premium collections | FR-06, FR-07 | AC-04 |
| BO-04 – Evaluate claims | FR-08, FR-09 | AC-05 |
| BO-05 – Analyze renewal and lapse | FR-10, FR-12 | AC-06 |
| BO-06 – Develop risk indicators | FR-11, FR-12 | AC-03, AC-08 |
| BO-07 – Measure customer value | FR-13 | AC-07 |
| BO-08 – Consolidated business intelligence | FR-14 | AC-07, AC-08, AC-09 |

AC-10 provides an overall quality and defect-acceptance condition applicable across the project.

# 16. Future Enhancements

Potential future enhancements include:

- Predictive customer lapse modeling.
- Advanced claims fraud detection.
- Automated customer segmentation.
- Product recommendation analytics.
- Real-time portfolio monitoring.
- Integration with external insurance systems.
- Advanced predictive underwriting analytics.
- Role-based reporting and access control.
- Automated management reporting.

These are future opportunities and are not claimed as current implemented functionality.

# 17. Business Benefits

The expected business benefits include:

1. **Centralized visibility:** Consolidated access to important insurance portfolio information.
2. **Improved monitoring:** Better visibility into policy status and premium collection.
3. **Claims insights:** Improved understanding of claims distribution and settlement outcomes.
4. **Retention analysis:** Better visibility into renewal and lapse patterns.
5. **Risk awareness:** Structured customer and policy risk indicators.
6. **Data-driven decisions:** Consistent KPIs for analytical and management reporting.
7. **Operational transparency:** Documented data definitions and validation requirements.

# 18. Approval and Sign-Off

| Role | Name | Approval | Date |
|---|---|---|---|
| Business Owner | Not assigned | Pending | Pending |
| Business Analyst | Prathmesh Aghor| Portfolio demonstration | Not applicable |
| Technical Lead | Not assigned | Pending | Pending |
| UAT Representative | Not assigned | Pending | Pending |

**Portfolio Demonstration Note**

For this portfolio demonstration, the Prathmesh Aghor performed the roles of Business Analyst, Data Analyst, and QA Reviewer. External business stakeholder review and formal organizational sign-off have not been obtained.

**Document Status:** Draft – For Review

---

*PoliSight – Insurance Policy Intelligence & Analytics Platform*  
*Business Requirements Document | Version 1.1*