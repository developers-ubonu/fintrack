# Problem Domain Model - FinTrack

## Metadata
**Version:** 0.3
**Status:** Draft
**Last Updated:** April 8, 2025
**Owner:** FinTrack Project Manager
**Reviewers:** [To be determined]

## Dependencies
**Required Artifacts:**
- Problem Statement Document
- User Needs Analysis
- Interview Findings (P1, P2, P3, P4)

**Dependent Artifacts:**
- Scope Definition Document
- Business Case Document
- Solution Vision Document

## Purpose
This document establishes a clear, shared understanding of the FinTrack problem domain concepts, relationships, and business rules governing financial tracking for small service businesses (initially focusing on landscaping/lawn care) in Quebec. It creates a common vocabulary for all project stakeholders and serves as the foundation for technical design decisions.

## Success Criteria
- [x] All key domain concepts are identified and clearly defined
- [x] Relationships between domain concepts are mapped
- [x] Business rules are documented with clear rationale
- [x] Domain model is validated with subject matter experts
- [x] Model is consistent with findings from user research
- [x] Model is comprehensive enough to support identified use cases

## Content Requirements
1. Domain Glossary
2. Conceptual Data Model
3. Business Rules Catalog
4. Domain Constraints
5. Domain Workflows/Processes

## Validation Methods
- [ ] Review with subject matter experts (service business owners)
- [x] Consistency check with user research findings
- [ ] Walkthrough of model against primary use cases
- [x] Verification that all interview findings are addressed
- [ ] Stakeholder review and sign-off

## Content

### 1. Domain Glossary

| Term | Definition | Notes |
|------|------------|-------|
| Business Owner | An individual who owns and operates a small service business in Quebec. | May be a solo operator or manage employees and/or contractors. |
| Client | A person or business entity that contracts the service business to perform services. | May be one-time or recurring, have different payment methods, and may require GST/QST on invoices. |
| Job | A specific instance of service work performed for a client. | The fundamental unit for tracking profitability; includes materials, labor, contractor costs, and other expenses. |
| Service | A type of work provided by the business (e.g., lawn mowing, gardening, snow removal, cleaning, power washing). | Businesses may offer multiple service types with different seasonal patterns and billing models. |
| Expense | Money spent by the business for materials, equipment, fuel, subcontracting, or other operational costs. | May be associated with specific jobs or general overhead. Payments to Contractors result in expenses but are primarily tracked via the Contractor entity relationship. |
| Receipt | Document showing proof of purchase for an expense. | Critical for tax deductions and job cost tracking. |
| Income | Money received from clients for services performed. | May be received via cash, e-transfer, check, or other methods. |
| Invoice | A formal document requesting payment for services rendered. | May require GST/QST calculation for registered businesses. |
| GST/QST | Goods and Services Tax / Quebec Sales Tax that registered businesses must collect. | A significant pain point for Quebec businesses; thresholds apply. |
| Profit | Income minus expenses (including contractor payments), calculated at the job level or business level. | Key metric for business success and decision-making. |
| Contract | Formal agreement between business and client or business and contractor specifying services and payment terms. | May be per-visit, project-based, monthly, or seasonal for clients. Defines terms for contractors. |
| **Contractor** | An individual or business engaged by the Business Owner to perform specific services, typically on a non-employee basis (independent contractor or subcontractor). | Distinct entity to track involvement, payments, and potentially future interactions (scheduling, communication). Payments made to **Contractors** are tracked. |
| Seasonal Business | Business operation that changes significantly between seasons. | Many businesses offer different services (e.g., landscaping vs. snow removal) with different models. |
| Input Tax Credit (ITC) | GST/QST paid on business expenses that can be claimed back from tax authorities. | Important for tax compliance and business profitability. |
| Tax Threshold | Revenue level (currently $30,000 CAD) at which GST/QST registration becomes mandatory in Quebec. | Important consideration for informal/growing businesses. |
| Tax Guidance | Information or links provided within the application regarding tax obligations (e.g., thresholds, common deductions). | Intended to inform, not replace professional advice. May include user acknowledgements. |

### 2. Conceptual Data Model

#### 2.1 Domain Entities

| Entity | Description | Key Attributes | Relationships |
|--------|-------------|----------------|--------------|
| Business | The service business itself. | Name, Address, Contact Info, Tax Registration Status (GST/QST), Language Preference (EN/FR), Service Types Offered | Has Clients, Services, Jobs, Expenses, Income, **Contractors** |
| Client | Customer who receives services. | Name, Address, Contact Info, Client Type (One-time/Recurring), Payment Preference | Has Jobs, Contracts (Client Contracts), Invoices |
| Job | Specific service instance performed for a client. | Job Date, Service Type, Status (Planned/In-Progress/Complete), Description, Location, Season (Summer/Winter/Other) | Belongs to Client, Has Service Type, Has Expenses, Has Income, Involves **Contractors** |
| Service | Type of work offered. Flexible for diverse types (landscaping, snow, cleaning, etc.). | Name, Description, Default Rate, Category, Season Applicability | Used in Jobs, Offered by Business |
| Expense | Money spent on business costs. Essential categories include Fuel, Materials, Equipment (Rent/Purchase), Repairs/Maintenance, Tools, Dump Fees, Subcontracting (if distinct from Contractor payment), Insurance, Office Supplies. | Amount, Date, Category, Payment Method, GST/QST Paid, Job Association (if applicable), Vendor | Associated with Job (optional), Has Receipt (optional) |
| Receipt | Proof of purchase document. | Image, Date, Vendor, Total Amount, GST/QST Amount | Belongs to Expense |
| Invoice | Payment request document. | Invoice Number, Issue Date, Due Date, Total Amount, GST/QST Amount, Status (Draft/Sent/Paid) | Associated with Client, Contains Job(s) |
| Payment | Money received from client or paid to a Contractor. | Amount, Date, Method (Cash/E-transfer/Check), Status, Direction (In/Out), Associated Invoice/Job/Contractor | Associated with Invoice or Job (Client Payments); Associated with Contractor (Contractor Payments) |
| Contract | Service agreement. Can be between Business-Client or Business-Contractor. | Start Date, End Date, Terms, Service Frequency, Pricing, Contract Type (Per-Visit/Monthly/Seasonal/Project-Based), Associated Parties (Client or Contractor) | Associated with Client or Contractor, Contains Service(s) |
| TaxInfo | GST/QST-related information and guidance tracking. | Registration Numbers, Rates, Collection Status, Reporting Period, Threshold Status, Tax Guidance Acknowledgement Status, Link to Official Resources | Associated with Business, Invoices, Expenses |
| **Contractor** | Individual or business performing services on a contract basis. Treated as distinct entity for tracking and potential future feature expansion. | Name (Individual/Business), Contact Info, Service Specialization, Rate/Payment Terms, Tax ID (if applicable) | Works on Jobs, Receives Payments, Has Contracts (Contractor Contracts) |
| Profit | Calculated financial performance. | Amount, Period (Job/Week/Month/Season), Income Total, Expense Total (incl. Contractor Payments) | Associated with Job(s) or Business |

#### 2.2 Entity Relationship Diagram

```
Business
    |
    |---- TaxInfo (GST/QST config & guidance tracking)
    |
    |---- Client (many)
    |      |
    |      |---- Contract (many) [Client Contracts]
    |      |      |
    |      |      |---- Service (many)
    |      |
    |      |---- Invoice (many)
    |             |
    |             |---- Payment (many) [Client Payments] <-- Also potentially linked directly to Job
    |             |
    |             |---- Job (many)
    |                    |
    |                    |---- Service (one)
    |                    |
    |                    |---- **Contractor** (many) <-- **Contractor** involved in Job
    |                    |
    |                    |---- Expense (many)
    |                    |      |
    |                    |      |---- Receipt (one)
    |                    |
    |                    |---- Profit (calculated)
    |
    |---- Expense (many) [General business expenses]
    |      |
    |      |---- Receipt (one)
    |
    |---- **Contractor** (many) <-- **Contractors** associated with the Business
           |
           |---- Contract (many) [Contractor Contracts]
           |
           |---- Payment (many) [Contractor Payments]
```
*(Note: Cardinality (e.g., 1..*, 0..*) could be added for more formal representation if desired)*

### 3. Business Rules Catalog

| ID | Rule | Description | Rationale | Source |
|----|------|-------------|-----------|--------|
| BR-1 | Job Profit Calculation | Job profit equals total payments received minus sum of expenses associated with that job (including payments made to **Contractors** for that job). | Core business need is to understand profitability at the job level. | Interview P1, P3, P4 |
| BR-2 | Tax Applicability | GST/QST must be applied to invoices if business is registered or annual revenue exceeds the current threshold (e.g., $30,000). | Quebec tax regulation compliance. | Interview P1, P4 |
| BR-3 | Tax Input Credits | GST/QST paid on eligible business expenses can be claimed as input tax credits if business is registered. | Reduces tax burden and impacts profitability calculations. | Interview P1 |
| BR-4 | Offline Capability | Key transaction data (expenses, jobs list view) must be recordable/viewable offline and synchronized when connectivity is restored. | Business often operates in areas with limited connectivity. | Interview P1 |
| BR-5 | Flexible Service Types | Business may offer diverse service types (landscaping, snow removal, cleaning, etc.) with different operational models. | Reflects actual operation and growth plans of service businesses. | Interview P1, P3, P4, User Feedback |
| BR-6 | Receipt Documentation | Expenses should allow for receipt image capture to substantiate tax deductions. | Prevents lost deduction opportunities and supports tax compliance. | Interview P1, P2, P3 |
| BR-7 | Payment Method Tracking | System must track multiple payment methods (cash, e-transfer, check) for both incoming (Client) and outgoing (**Contractor**) payments. | Reflects actual payment methods in the industry. | Interview P1, P2, P3, P4 |
| BR-8 | Contract Type Flexibility | Different contract types (per-visit, project, monthly, seasonal) must be supported with appropriate billing models for Client work. Terms for **Contractors** also need tracking. | Businesses use different contract models for different services and engagements. | Interview P1, P3, P4 |
| BR-9 | Recurring vs. One-time Clients | System must distinguish between one-time and recurring clients for payment tracking and potential future features. | Business treats these client types differently and needs appropriate tracking. | Interview P1 |
| BR-10 | Simplified Informal Mode | System must offer a simplified workflow/view for informal/cash businesses without mandatory complex tax tracking or invoicing initially. | Enables adoption by businesses at early stages or those operating informally. | Interview P2, P3 |
| BR-11 | Tax Threshold Awareness | System should monitor revenue relative to tax thresholds and provide informational alerts. May prompt user acknowledgement of their compliance responsibility if operating informally near/above threshold. | Addresses user confusion/anxiety and promotes responsible use, without giving direct advice. | Interview P3, P4, User Feedback |

### 4. Domain Constraints

| ID | Constraint | Description | Impact | Workarounds |
|----|------------|-------------|--------|------------|
| DC-1 | Mobile-First Access | Primary system interaction will occur on mobile devices in field conditions. | Limits UI complexity and data entry methods. | Offer synced web access for complex tasks when in office. |
| DC-2 | Variable Internet Connectivity | Users frequently work in areas with limited or no internet connectivity. | Requires robust offline functionality and synchronization. | Local storage with queued synchronization when connectivity is restored. |
| DC-3 | Limited Technical Skill | Users have minimal accounting knowledge and limited experience with financial software. | System must be extremely intuitive and use familiar concepts. | Progressive disclosure of complexity, guided workflows, automatic calculations. |
| DC-4 | Quebec Tax Requirements | System must handle Quebec's specific GST/QST rules and reporting requirements accurately. | Increases complexity of tax calculation and tracking. | Separate tax module, clear guidance links, user responsibility acknowledgements. |
| DC-5 | Seasonal Business Pattern | Business operations, income, and expense categories can change significantly between seasons for some service types. | Requires flexible categorization and reporting by season/service type. | Season/Service tagging for jobs, expenses with filtered views. |
| DC-6 | Limited Time for Administration | Users have minimal time for financial tracking due to focus on field work. | Data entry must be extremely efficient. | Quick-entry forms, templates, default values. |
| DC-7 | Price Sensitivity | Target users have limited budget for business software ($10-20/month range confirmed). | Restricts development complexity and support options. | Tiered feature approach with core functionality at lower price points. |
| DC-8 | Bilingual Requirements | System must support both English and French for the Quebec market. | Increases UI/UX complexity and content management. | Standardized translation framework and language toggle. |
| DC-9 | Legal Classification | App terminology ("**Contractor**") does not dictate legal worker status; users are responsible for correct classification based on Quebec law. | Potential user confusion or misreliance on app term. | Clear disclaimers in app/support docs; encourage professional legal advice. |

### 5. Domain Workflows/Processes

#### 5.1 Process: Job Lifecycle Financial Management
1. Step 1: Job Creation
   - Create new job record with client association
   - Specify service type and estimated pricing
   - Optionally create quote/estimate for client approval

2. Step 2: Job Expense & **Contractor** Assignment
   - Record expenses associated with the job (materials, fuel, etc.)
   - Capture receipt images for expenses
   - Categorize expenses appropriately
   - Track GST/QST paid on expenses (if applicable)
   - Assign **Contractors** to job (optional)

3. Step 3: Job Completion & **Contractor** Payment
   - Mark job as complete
   - Record final service details and time spent
   - Track payments made to assigned **Contractors** (if applicable) based on agreed terms/rates
   - Calculate actual cost (expenses + **contractor** payments + other costs)

4. Step 4: Invoicing (Client)
   - Generate invoice based on services performed (if using formal invoicing)
   - Apply appropriate pricing (contract, quoted, or standard rates)
   - Calculate and add GST/QST if applicable
   - Send invoice to client via preferred method

5. Step 5: Payment Collection (Client)
   - Record payment received (full or partial) against Invoice or Job
   - Document payment method (cash, e-transfer, check)
   - Update invoice status accordingly (if applicable)

6. Step 6: Profitability Analysis
   - Calculate job profit (payment received - expenses - **contractor** payments)
   - Add job to weekly/monthly profit reporting
   - Compare profitability against similar jobs/services

#### 5.2 Process: Tax Management for Quebec Businesses
*(No terminology changes needed in this section)*
1. Step 1: Tax Status Tracking
   - Monitor revenue relative to GST/QST thresholds
   - Alert user when approaching registration thresholds (BR-11)
   - Record user acknowledgement of tax responsibility (if applicable)
   - Update tax status when business registers

2. Step 2: GST/QST Collection
   - Apply correct tax rates to invoices based on business status
   - Track collected taxes separately from service revenue
   - Record client tax numbers for business clients (if applicable)

3. Step 3: Input Tax Credit Tracking
   - Record GST/QST paid on eligible business expenses
   - Categorize expenses for appropriate ITC claims
   - Maintain receipt documentation to support claims

4. Step 4: Periodic Tax Reporting
   - Generate summary reports for GST/QST collected
   - Calculate ITCs for the period
   - Determine net tax payable/refundable
   - Export data for filing with Revenu Québec

5. Step 5: Tax Payment/Refund Tracking
   - Record tax payments/refunds
   - Reconcile with period calculations
   - Close tax period when complete

#### 5.3 Process: Seasonal Transition Management
*(No terminology changes needed in this section)*
1. Step 1: End-of-Season Review
   - Generate profitability reports for concluding season/service type
   - Review client list for potential service conversion

2. Step 2: Service Offering Adjustment
   - Activate/deactivate seasonal/other service types
   - Update pricing for new season/service types
   - Adjust expense categories as needed

3. Step 3: Contract Conversion
   - Convert applicable clients to new seasonal/service contracts
   - Set up recurring billing if appropriate
   - Generate new quotes/estimates for recurring clients

4. Step 4: Equipment/Supply Expense Management
   - Track season/service-specific equipment maintenance/purchases
   - Update inventory concepts for materials (if applicable)
   - Adjust expense categories for operational changes

5. Step 5: Seasonal/Service Cash Flow Planning
   - Project income/expenses for the upcoming season/service mix
   - Identify potential cash flow gaps
   - Plan for variations in income/expenses

#### 5.4 Process: Informal-to-Formal Business Transition
1. Step 1: Basic Tracking (Informal Mode)
   - Record cash income and basic expenses (using simplified UI)
   - Track weekly profit/loss
   - Maintain simple client list & job records
   - Optionally track **Contractor** involvement & payments

2. Step 2: Enhanced Financial Visibility
   - Begin tracking per-job profitability more formally
   - Categorize expenses more precisely
   - Monitor business growth toward tax thresholds (receive alerts - BR-11)

3. Step 3: Business Formalization
   - Register business when appropriate (near threshold)
   - Activate GST/QST tracking features within the app
   - Set up formal invoice templates (if desired)

4. Step 4: Professional Client & **Contractor** Management
   - Transition to formal quotes and invoices (optional/as needed)
   - Implement contracts for recurring services and/or **Contractors**
   - Begin collecting GST/QST as required

5. Step 5: Tax Compliance
   - Track tax obligations systematically using app features
   - Prepare for first tax filing period using generated reports
   - Generate reports for accountant review

## Assumptions
*(Confirmed as accurate by user feedback)*
- [x] Business owners have basic smartphone proficiency
- [x] Most expenses can be categorized into common groups (fuel, materials, equipment, etc.)
- [x] Users prioritize simplicity and speed over comprehensive accounting features
- [x] Both formal and informal business operation models exist in the market
- [x] Seasonal transitions or offering diverse services are common
- [x] Basic tax knowledge varies significantly among users

## Risks
- [x] Risk 1: Complex tax calculations may lead to compliance issues
   - Impact: Legal and financial repercussions for users
   - Mitigation: Consult with Quebec tax experts; clear disclaimer that tool assists but does not replace professional advice; use acknowledgements.
- [x] Risk 2: Diverse business models may challenge the unified domain model
   - Impact: Model may not fit all user cases perfectly
   - Mitigation: Design for flexibility with optional components; tiered approach based on business maturity/needs.
- [x] Risk 3: Scope creep due to adjacent service industries or advanced **Contractor** management features
   - Impact: Loss of focus on core MVP needs
   - Mitigation: Ensure model accommodates general service business needs while focusing UX/MVP on primary target users/features.
- [x] Risk 4: Offline functionality technical challenges
   - Impact: Unreliable data or synchronization issues
   - Mitigation: Robust offline-first architecture; clear sync status indicators.
- [x] Risk 5: User confusion regarding legal status of "**Contractors**" despite app terminology.
   - Impact: Misreliance on app, potential legal issues for users.
   - Mitigation: Clear in-app disclaimers, help documentation emphasizing user responsibility for legal classification, strong recommendation for professional advice.

## Review Notes
- [ ] Review 1
   - Reviewer: [Name]
   - Date: [Date]
   - Comments: [Comments]
   - Status: [Status]

## Change Log
| Date | Version | Changed By | Changes Made |
|------|---------|------------|--------------|
| April 7, 2025 | 0.1 | FinTrack PM | Initial creation based on interview findings |
| April 7, 2025 | 0.2 | FinTrack PM | Incorporated user feedback: Added core Expense categories; Confirmed Helper as distinct entity; Added Tax Guidance concept & rule (BR-11); Emphasized Service flexibility; Confirmed Assumptions & Workflows. |
| April 8, 2025 | 0.3 | FinTrack PM | Standardized terminology: Replaced "Helper" with "Contractor" throughout the document for consistency and clarity based on project direction. Added Domain Constraint DC-9 and Risk 5 related to legal classification disclaimer. Adjusted related descriptions (Expense, Payment, Workflows). |

## Sign-off
- [ ] Technical Review
- [ ] Business Review
- [ ] Stakeholder Review
- [ ] Final Approval

## Next Steps
- Complete Scope Definition Document using this updated domain model
- Refine Business Case with insights from domain analysis
- Begin Solution Vision development
- Schedule review with service business owners to validate model updates
- Evaluate technical approach for offline functionality and Tax Guidance features