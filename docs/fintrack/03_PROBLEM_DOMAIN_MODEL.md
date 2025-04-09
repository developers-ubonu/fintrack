# Problem Domain Model - FinTrack

## Metadata
**Version:** 0.4 *(Updated for Enhanced MVP Scope v1.4/v0.4)*
**Status:** Draft
**Last Updated:** April 8, 2025
**Owner:** FinTrack Project Manager
**Reviewers:** [To be determined]

## Dependencies
**Required Artifacts:**
- Problem Statement Document *(Reflecting enhanced MVP)*
- User Needs Analysis *(v1.5 or later)*
- Interview Findings (P1, P2, P3, P4)

**Dependent Artifacts:**
- Scope Definition Document *(v0.4 or later)*
- Business Case Document
- Solution Vision Document

## Purpose
This document establishes a clear, shared understanding of the FinTrack problem domain concepts, relationships, and business rules governing financial tracking for small service businesses (initially focusing on landscaping/lawn care) in Quebec, **incorporating automated data capture and allocation concepts**. It creates a common vocabulary for all project stakeholders and serves as the foundation for technical design decisions.

## Success Criteria
- [x] All key domain concepts are identified and clearly defined
- [x] Relationships between domain concepts are mapped
- [x] Business rules **(including automation)** are documented with clear rationale
- [x] Domain model is validated with subject matter experts
- [x] Model is consistent with findings from user research **and enhanced scope**
- [x] Model is comprehensive enough to support identified use cases **(including automated workflows)**

## Content Requirements
1. Domain Glossary
2. Conceptual Data Model
3. Business Rules Catalog
4. Domain Constraints
5. Domain Workflows/Processes

## Validation Methods
- [ ] Review with subject matter experts (service business owners)
- [x] Consistency check with user research findings and **enhanced MVP scope**
- [ ] Walkthrough of model against primary use cases (**including automated paths**)
- [x] Verification that all interview findings are addressed
- [ ] Stakeholder review and sign-off

## Content

### 1. Domain Glossary *(Minor Refinements)*

| Term | Definition | Notes |
|------|------------|-------|
| Business Owner | An individual who owns and operates a small service business in Quebec. | May be a solo operator or manage employees and/or contractors. |
| Client | A person or business entity that contracts the service business to perform services. | May be one-time or recurring, have different payment methods, and may require GST/QST on invoices. |
| Job | A specific instance of service work performed for a client. | The fundamental unit for tracking profitability; includes materials, labor, contractor costs, and other expenses. |
| Service | A type of work provided by the business (e.g., lawn mowing, gardening, snow removal, cleaning). | Businesses may offer multiple service types with different seasonal patterns and billing models. |
| Expense | Money spent by the business for materials, equipment, fuel, subcontracting, or other operational costs. | May be associated with specific jobs (potentially split/allocated) or general overhead. **Input may be automated via OCR.** Payments to Contractors result in expenses but are primarily tracked via the Contractor entity relationship. |
| Receipt | Document showing proof of purchase for an expense. | Critical for tax deductions and job cost tracking. **Can be captured via photo, potentially enabling automated data extraction (OCR).** |
| Income | Money received from clients for services performed. | May be received via cash, e-transfer, check, or other methods. |
| Invoice | A formal document requesting payment for services rendered. | May require GST/QST calculation for registered businesses. |
| GST/QST | Goods and Services Tax / Quebec Sales Tax that registered businesses must collect. | A significant pain point for Quebec businesses; thresholds apply. **Tax amounts on expenses may be auto-captured via OCR.** |
| Profit | Income minus **allocated** expenses (including **allocated** contractor payments), calculated at the job level or business level. | Key metric for business success and decision-making. |
| Contract | Formal agreement between business and client or business and contractor specifying services and payment terms. | May be per-visit, project-based, monthly, or seasonal for clients. Defines terms for contractors. |
| **Contractor** | An individual or business engaged by the Business Owner to perform specific services, typically on a non-employee basis (independent contractor or subcontractor). | Distinct entity to track involvement, payments, and potentially future interactions. Payments made require allocation to jobs. |
| Seasonal Business | Business operation that changes significantly between seasons. | Many businesses offer different services (e.g., landscaping vs. snow removal) with different models. |
| Input Tax Credit (ITC) | GST/QST paid on business expenses that can be claimed back from tax authorities. | Important for tax compliance and business profitability. **Identification potentially aided by OCR.** |
| Tax Threshold | Revenue level (currently $30,000 CAD) at which GST/QST registration becomes mandatory in Quebec. | Important consideration for informal/growing businesses. |
| Tax Guidance | Information or links provided within the application regarding tax obligations (e.g., thresholds, common deductions). | Intended to inform, not replace professional advice. May include user acknowledgements. |
| **Allocation** | The process of distributing the cost of a single Expense or Contractor Payment across multiple Jobs. | Crucial for accurate job costing of shared resources (e.g., fuel, bulk materials, contractor time). |
| **OCR (Optical Character Recognition)** | Technology used to automatically extract text data (vendor, date, amount, taxes) from receipt images. | Key enabler for effortless expense input. |
| **Smart Suggestion** | Context-aware recommendations provided by the app (e.g., suggesting which job an expense belongs to based on location/calendar). | Aims to reduce manual selection effort. |


### 2. Conceptual Data Model *(Revised Section)*

#### 2.1 Domain Entities

| Entity | Description | Key Attributes | Relationships |
|--------|-------------|----------------|--------------|
| Business | The service business itself. | Name, Address, Contact Info, Tax Registration Status (GST/QST), Language Preference (EN/FR), Service Types Offered | Has Clients, Services, Jobs, Expenses, Income, **Contractors** |
| Client | Customer who receives services. | Name, Address, Contact Info, Client Type (One-time/Recurring), Payment Preference | Has Jobs, Contracts (Client Contracts), Invoices |
| Job | Specific service instance performed for a client. | Job Date, Service Type, Status (Planned/In-Progress/Complete), Description, Location, Season (Summer/Winter/Other) | Belongs to Client, Has Service Type, **Has Expense Allocations**, Has Income, Involves **Contractors** |
| Service | Type of work offered. | Name, Description, Default Rate, Category, Season Applicability | Used in Jobs, Offered by Business |
| **Expense** | Money spent on business costs. | Amount, Date, Category, Payment Method, GST/QST Paid, Vendor, **CaptureMethod ('OCR', 'Manual')**, **IsSplit** (Boolean), **IsGeneralExpense** (Boolean) | **Has Expense Allocations (one or many)**, Has Receipt (optional) |
| **ExpenseAllocation** | Links an Expense to a Job and specifies the allocated amount. | AllocatedAmount, GSTQSTAllocated | Belongs to Expense, Belongs to Job |
| **Receipt** | Proof of purchase document. | Image, Date, Vendor, Total Amount, GST/QST Amount, **OCRStatus** ('Pending', 'Complete', 'Failed'), **RawOCRData** (optional) | Belongs to Expense |
| Invoice | Payment request document. | Invoice Number, Issue Date, Due Date, Total Amount, GST/QST Amount, Status (Draft/Sent/Paid) | Associated with Client, Contains Job(s) |
| **Payment** | Money received from client or paid to a Contractor. | Amount, Date, Method (Cash/E-transfer/Check), Status, Direction (In/Out), Associated Invoice/Job (Client Payments); Associated Contractor (Contractor Payments), **IsSplit** (Boolean), **IsGeneralExpense** (Boolean) | **Has Payment Allocations (one or many, for Contractor Payments)** |
| **PaymentAllocation** | Links a Contractor Payment to a Job and specifies the allocated amount. | AllocatedAmount | Belongs to Payment (Contractor), Belongs to Job |
| Contract | Service agreement. | Start Date, End Date, Terms, Service Frequency, Pricing, Contract Type (Per-Visit/Monthly/Seasonal/Project-Based), Associated Parties (Client or Contractor) | Associated with Client or Contractor, Contains Service(s) |
| TaxInfo | GST/QST-related information and guidance tracking. | Registration Numbers, Rates, Collection Status, Reporting Period, Threshold Status, Tax Guidance Acknowledgement Status, Link to Official Resources | Associated with Business, Invoices, Expenses |
| **Contractor** | Individual or business performing services on a contract basis. | Name (Individual/Business), Contact Info, Service Specialization, Rate/Payment Terms, Tax ID (if applicable) | Works on Jobs, Receives Payments, Has Contracts (Contractor Contracts) |
| Profit | Calculated financial performance. | Amount, Period (Job/Week/Month/Season), Income Total, **Total Allocated Expenses**, **Total Allocated Contractor Payments** | Associated with Job(s) or Business |

#### 2.2 Entity Relationship Diagram *(Conceptual Update)*

```
Business
    |
    |---- TaxInfo
    |
    |---- Client (many)
    |      |
    |      |---- Contract (many) [Client Contracts]
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
    |                    |---- **Contractor** (many) <-- Involved in Job
    |                    |
    |                    |---- ExpenseAllocation (many) ----> Expense (one) --> Receipt (optional, one)
    |                    |
    |                    |---- PaymentAllocation (many) ----> Payment (one) [Contractor Payment]
    |                    |
    |                    |---- Profit (calculated)
    |
    |---- Expense (many) [General business expenses - linked via IsGeneralExpense flag, not Allocation]
    |      |
    |      |---- Receipt (one)
    |
    |---- **Contractor** (many) <-- Associated with the Business
           |
           |---- Contract (many) [Contractor Contracts]
           |
           |---- Payment (many) [Contractor Payments - potentially split via PaymentAllocation]
```
*(Note: Introduced Allocation entities to explicitly model splitting. General expenses bypass allocation.)*

### 3. Business Rules Catalog *(Revised Section)*

| ID | Rule | Description | Rationale | Source |
|----|------|-------------|-----------|--------|
| BR-1 | Job Profit Calculation | Job profit equals total payments received minus sum of **allocated** expenses and **allocated** contractor payments associated with that job. | Core business need, requires accurate allocation. | Interview P1, P3, P4 |
| BR-2 | Tax Applicability | GST/QST must be applied to invoices if business is registered or annual revenue exceeds the current threshold. | Quebec tax regulation compliance. | Interview P1, P4 |
| BR-3 | Tax Input Credits | GST/QST paid on eligible business expenses can be claimed as input tax credits if business is registered. **App aids identification via OCR/categorization.** | Reduces tax burden and impacts profitability calculations. | Interview P1 |
| BR-4 | Offline Capability | Key **manual** transaction data (expenses, payments) must be recordable/viewable offline (with basic job selection) and synchronized later. **Automated features (OCR, suggestions) may require connectivity.** | Business often operates in areas with limited connectivity; manage expectations for advanced features. | Interview P1, Feasibility Analysis |
| BR-5 | Flexible Service Types | Business may offer diverse service types with different operational models. | Reflects actual operation and growth plans. | Interview P1, P3, P4, User Feedback |
| BR-6 | Receipt Documentation | Expenses should allow for receipt image capture **with OCR attempt** to substantiate tax deductions and streamline input. | Prevents lost deductions, reduces manual entry. | Interview P1, P2, P3, User Feedback |
| BR-7 | Payment Method Tracking | System must track multiple payment methods for both incoming (Client) and outgoing (**Contractor**) payments. | Reflects actual payment methods. | Interview P1, P2, P3, P4 |
| BR-8 | Contract Type Flexibility | Different contract types must be supported with appropriate billing models for Client work. Terms for **Contractors** also need tracking. | Businesses use different contract models. | Interview P1, P3, P4 |
| BR-9 | Recurring vs. One-time Clients | System must distinguish between one-time and recurring clients. | Business treats these client types differently. | Interview P1 |
| BR-10 | Simplified Informal Mode | System must offer a simplified workflow/view for informal/cash businesses without mandatory complex tax tracking or invoicing initially. | Enables adoption by businesses at early stages. | Interview P2, P3 |
| BR-11 | Tax Threshold Awareness | System should monitor revenue relative to tax thresholds and provide informational alerts. | Addresses user confusion/anxiety and promotes responsible use. | Interview P3, P4, User Feedback |
| **BR-12** | **Automated Data Capture (OCR)** | System attempts OCR on receipt images; **user must confirm/correct extracted data before saving.** | Streamlines input but requires user validation for accuracy. | Enhanced MVP Scope |
| **BR-13** | **Contextual Job Suggestions** | System suggests job associations based on context (GPS, Calendar, Recency); **user confirms or manually selects/overrides.** | Speeds up allocation but relies on user confirmation. | Enhanced MVP Scope |
| **BR-14** | **Cost Allocation & Validation** | Expenses/Contractor Payments can be split across multiple jobs via an allocation mechanism. **Total allocated amount must equal the original item amount.** | Ensures accurate costing for shared resources without creating/losing money. | Enhanced MVP Scope |
| **BR-15** | **Allocation Adjustment** | Users must be able to easily modify or re-allocate previous expense/payment allocations to correct errors. | Provides flexibility and ensures data accuracy over time. | Enhanced MVP Scope |
| **BR-16** | **General Expense Marking** | Users must be able to easily mark expenses/payments as non-job specific (general overhead). | Ensures overhead is tracked but excluded from individual job profit calculations. | Enhanced MVP Scope |


### 4. Domain Constraints *(Revised Section)*

| ID | Constraint | Description | Impact | Workarounds |
|----|------------|-------------|--------|------------|
| DC-1 | Mobile-First Access | Primary system interaction will occur on mobile devices in field conditions. | Limits UI complexity; requires intuitive design for automation features. | Offer synced web access for complex tasks/review. |
| DC-2 | Variable Internet Connectivity | Users frequently work in areas with limited or no internet connectivity. | Requires robust **offline capability for manual entry/capture**; **OCR/suggestions may be unavailable offline.** | Local storage with queued synchronization; clear UI indication of online/offline feature availability. |
| DC-3 | Limited Technical Skill | Users have minimal accounting knowledge and limited experience with financial software. | System must be extremely intuitive; automation must be easy to understand and correct. | Progressive disclosure, guided workflows, simple correction mechanisms. |
| DC-4 | Quebec Tax Requirements | System must handle Quebec's specific GST/QST rules accurately. **OCR must handle tax fields correctly.** | Increases complexity of tax calculation/capture validation. | Separate tax module, clear guidance links, user responsibility acknowledgements, OCR validation/correction step. |
| DC-5 | Seasonal Business Pattern | Business operations, income, and expense categories can change significantly between seasons. | Requires flexible categorization and reporting by season/service type. | Season/Service tagging for jobs, expenses with filtered views. |
| DC-6 | Limited Time for Administration | Users have minimal time for financial tracking due to focus on field work. | Data entry must be extremely efficient; **automation is key.** | Quick-entry via OCR/suggestions, templates, default values. |
| DC-7 | Price Sensitivity | Target users have limited budget for business software ($10-20/month range confirmed). | Restricts development complexity and support options; **value of automation must justify cost.** | Tiered feature approach with automation in paid tiers. |
| DC-8 | Bilingual Requirements | System must support both English and French. | Increases UI/UX complexity and content management. | Standardized translation framework and language toggle. |
| DC-9 | Legal Classification | App terminology ("**Contractor**") does not dictate legal worker status; users are responsible for correct classification. | Potential user confusion or misreliance on app term. | Clear disclaimers; encourage professional legal advice. |
| **DC-10** | **OCR Accuracy Dependence** | System usability heavily relies on acceptable OCR accuracy. **Errors require user correction.** | **Low accuracy leads to frustration, negating time savings.** | **Easy correction UI; set realistic user expectations; choose reliable OCR tech.** |
| **DC-11** | **Context Data Permissions** | Smart suggestions rely on user granting permissions (GPS/Calendar). **Feature is less useful without permissions.** | **Appears less "smart" if permissions denied.** | **Clear value explanation; robust manual selection fallback.** |

### 5. Domain Workflows/Processes *(Revised Section)*

#### 5.1 Process: Job Lifecycle Financial Management *(Automation Added)*
1. Step 1: Job Creation
   - Create new job record with client association
   - Specify service type and estimated pricing

2. Step 2: Job Expense Capture & Allocation
   - **Capture expenses via OCR/manual entry (UC-ME)**
   - **Confirm/correct OCR data**
   - **Confirm/select/split job allocation using smart suggestions or manual choice (REQ-JP-05)**
   - Categorize expenses appropriately
   - Track GST/QST paid (potentially via OCR)

3. Step 3: Job Completion & **Contractor** Payment Allocation
   - Mark job as complete
   - Record final service details and time spent (if tracked)
   - **Record contractor payments (UC-CP)**
   - **Confirm/select/split job allocation for payment using suggestions or manual choice (REQ-JP-07)**
   - Calculate actual cost (**sum of allocated expenses & payments**)

4. Step 4: Invoicing (Client)
   - Generate invoice based on services performed
   - Apply appropriate pricing
   - Calculate and add GST/QST if applicable
   - Send invoice to client

5. Step 5: Payment Collection (Client)
   - Record payment received against Invoice or Job
   - Document payment method
   - Update invoice status

6. Step 6: Profitability Analysis & Adjustment
   - Calculate job profit (payment received - allocated expenses - allocated contractor payments)
   - Review job profitability details
   - **Adjust allocations if necessary (REQ-JP-11)**
   - Add job to weekly/monthly profit reporting

#### 5.2 Process: Tax Management for Quebec Businesses *(Leveraging OCR)*
1. Step 1: Tax Status Tracking
   - Monitor revenue relative to GST/QST thresholds
   - Alert user when approaching registration thresholds (BR-11)
   - Record user acknowledgement of tax responsibility
   - Update tax status when business registers

2. Step 2: GST/QST Collection
   - Apply correct tax rates to invoices based on business status
   - Track collected taxes separately from service revenue

3. Step 3: Input Tax Credit Tracking
   - Record GST/QST paid on eligible business expenses (**potentially auto-captured via OCR**)
   - User confirms/corrects captured tax amounts
   - Categorize expenses for appropriate ITC claims
   - Maintain receipt documentation (digital image) to support claims

4. Step 4: Periodic Tax Reporting
   - Generate summary reports for GST/QST collected
   - Calculate ITCs for the period (based on confirmed expense data)
   - Determine net tax payable/refundable
   - Export data for filing with Revenu Québec

5. Step 5: Tax Payment/Refund Tracking
   - Record tax payments/refunds
   - Reconcile with period calculations
   - Close tax period when complete

#### 5.3 Process: Seasonal Transition Management
*(No major changes needed based on automation scope)*
1. Step 1: End-of-Season Review
2. Step 2: Service Offering Adjustment
3. Step 3: Contract Conversion
4. Step 4: Equipment/Supply Expense Management
5. Step 5: Seasonal/Service Cash Flow Planning

#### 5.4 Process: Informal-to-Formal Business Transition *(Automation Impact)*
1. Step 1: Basic Tracking (Informal Mode)
   - Record cash income and basic expenses (**using simplified automated capture - UC-ME**)
   - Track weekly profit/loss
   - Maintain simple client list & job records
   - Optionally track **Contractor** involvement & payments (**via simplified UC-CP**)

2. Step 2: Enhanced Financial Visibility
   - Begin tracking per-job profitability more formally (**data capture easier via automation**)
   - Categorize expenses more precisely (**aided by OCR/suggestions**)
   - Monitor business growth toward tax thresholds (receive alerts - BR-11)

3. Step 3: Business Formalization
   - Register business when appropriate
   - Activate GST/QST tracking features within the app (**data capture already supported**)
   - Set up formal invoice templates (if desired)

4. Step 4: Professional Client & **Contractor** Management
   - Transition to formal quotes and invoices (optional/as needed)
   - Implement contracts for recurring services and/or **Contractors**
   - Begin collecting GST/QST as required

5. Step 5: Tax Compliance
   - Track tax obligations systematically using app features (**leveraging captured data**)
   - Prepare for first tax filing period using generated reports
   - Generate reports for accountant review

## Assumptions *(Confirmed as accurate by user feedback)*
- [x] Business owners have basic smartphone proficiency
- [x] Most expenses can be categorized into common groups (fuel, materials, equipment, etc.)
- [x] Users prioritize **simplicity, speed, and effortless input** over comprehensive accounting features
- [x] Both formal and informal business operation models exist in the market
- [x] Seasonal transitions or offering diverse services are common
- [x] Basic tax knowledge varies significantly among users

## Risks *(Revised Section)*
- [x] Risk 1: **Complex tax calculations/OCR capture may lead to compliance issues if not accurate and easily correctable.**
   - Impact: Legal and financial repercussions for users
   - Mitigation: Consult with Quebec tax experts; clear disclaimer; user validation/correction step for OCR tax data.
- [x] Risk 2: Diverse business models may challenge the unified domain model.
   - Impact: Model may not fit all user cases perfectly.
   - Mitigation: Design for flexibility with optional components; tiered approach.
- [x] Risk 3: Scope creep due to adjacent service industries or advanced features beyond enhanced MVP.
   - Impact: Loss of focus on core MVP needs.
   - Mitigation: Strict scope management against enhanced MVP definition.
- [x] Risk 4: **Offline functionality technical challenges, especially differentiating manual core vs. online automation.**
   - Impact: Unreliable data, synchronization issues, user confusion.
   - Mitigation: Robust offline-first architecture *for manual core*; clear UI indicators for online features; thorough testing.
- [x] Risk 5: User confusion regarding legal status of "**Contractors**" despite app terminology.
   - Impact: Misreliance on app, potential legal issues for users.
   - Mitigation: Clear in-app disclaimers, help documentation, encourage professional advice.
- [x] **Risk 6: OCR Accuracy may not meet expectations.**
    - Impact: Frustration, manual correction negates benefit.
    - Mitigation: Set realistic targets, use reliable tech, provide easy correction UI.
- [x] **Risk 7: Smart suggestions may be inaccurate or unhelpful.**
    - Impact: User ignores feature or makes incorrect allocations.
    - Mitigation: Algorithm tuning, allow easy manual override/selection, gather user feedback.

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
| April 8, 2025 | 0.3 | FinTrack PM | Standardized terminology: Replaced "Helper" with "Contractor" throughout. Added Domain Constraint DC-9 and Risk 5 related to legal classification disclaimer. Adjusted related descriptions. |
| **April 8, 2025** | **0.4** | **Gemini Model** | **Major Revision: Updated Glossary, Entities (Expense, Payment, added Allocation), Relationships, Business Rules (added BR-12 to BR-16), Constraints (added DC-10, DC-11), and Workflows to incorporate automation features (OCR, Suggestions, Splitting, Adjustment) aligning with enhanced MVP Scope (v1.4/v0.4).** |


## Sign-off
- [ ] Technical Review
- [ ] Business Review
- [ ] Stakeholder Review
- [ ] Final Approval

## Next Steps
- Complete Scope Definition Document (v0.4) using this updated domain model (Done)
- Refine Business Case with insights from domain analysis
- Begin Solution Vision development
- Schedule review with service business owners to validate model updates **(including automation concepts)**
- Evaluate technical approach for **OCR, suggestions, offline limitations**
