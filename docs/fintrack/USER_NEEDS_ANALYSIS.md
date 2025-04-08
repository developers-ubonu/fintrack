# User Needs Analysis

## Metadata
**Version:** 1.1
**Status:** Draft
**Last Updated:** April 8, 2025
**Owner:** FinTrack Project Manager
**Reviewers:** [To be determined]

## Purpose
To identify and document the needs, goals, and pain points of small landscaping and related service business owners in Quebec, ensuring the FinTrack solution aligns with their financial tracking requirements and operational context.

## Success Criteria
- [ ] Clear identification of primary user personas for small service businesses
- [ ] Comprehensive use cases that reflect real-world financial tracking scenarios
- [ ] User journey maps highlighting key touchpoints and pain points in financial management

## Content Requirements
### 1. User Personas
- **Persona Name:** Solo Operator
  - **Role:** Independent service business owner
  - **Goals:**
    - Track profitability of each job accurately
    - Minimize time spent on financial administration
    - Maintain clear records for tax compliance (GST/QST)
    - Create professional invoices quickly
    - Keep business and personal finances separate
  - **Pain Points:**
    - Difficulty tracking expenses while in the field
    - Time wasted on manual financial record-keeping
    - Confusion about tax obligations and input tax credits
    - Inability to determine which jobs are most profitable
    - Limited connectivity in some work areas
  - **Context:**
    - Works primarily in the field
    - Uses mobile device for most business tasks
    - Has limited financial/accounting knowledge
    - Operates seasonally with fluctuating income
    - Serves the Greater Montreal area with bilingual requirements

- **Persona Name:** Small Business Owner
  - **Role:** Owner of service business potentially engaging 2-10 employees or **Contractors**.
  - **Goals:**
    - Understand profitability across multiple concurrent jobs
    - Track expenses by job and category
    - Track payments to **Contractors** accurately
    - Generate reports for business planning
    - Manage cash flow during seasonal fluctuations
    - Prepare accurate tax documentation
  - **Pain Points:**
    - Complexity of tracking multiple jobs simultaneously
    - Difficulty associating expenses with specific jobs
    - Accurately tracking costs associated with employees vs. **Contractors**.
    - Limited visibility into overall business financial health
    - Cumbersome process for GST/QST reporting
    - Time spent on administration rather than business growth
  - **Context:**
    - Splits time between field work and business management
    - Uses both mobile and desktop devices
    - Operates in both English and French
    - Has basic financial knowledge but no formal training
    - Needs to monitor job costs, including payments to **Contractors** or employee wages.

- **Persona Name:** Prospective/Early-Stage Operator
  - **Role:** Individual planning to start or recently started a small service business
  - **Goals:**
    - Start with proper financial organization from day one
    - Understand basic tax obligations and thresholds (GST/QST)
    - Look professional to clients
    - Track profitability to make informed business decisions
    - Set up a foundation for potential business growth (including potentially engaging **Contractors**)
  - **Pain Points:**
    - Confusion and anxiety about Quebec tax rules and thresholds
    - Uncertainty about which expenses are deductible
    - Lack of affordable guidance on business formalization
    - Overwhelmed by complex accounting software
    - Need to appear professional despite being new
  - **Context:**
    - Works primarily through mobile device (no computer)
    - Limited or no prior business administration experience
    - May offer multiple service types (e.g., landscaping, snow removal, cleaning)
    - Looking to build recurring client base
    - Plans to operate mostly via cash and e-transfers initially

### 2. Use Cases
- **Use Case Name:** Job Profitability Tracking
  - **Description:** Track all income and expenses (including **Contractor** payments) related to a specific service job to determine profitability.
  - **Actors:** Business owner
  - **Steps:**
    1. Create a new job in the system with client details and job specifications.
    2. Record all income/payments for the job.
    3. Track all direct expenses (materials, fuel, etc.) and associate them with the job.
    4. Track payments made to **Contractors** associated with the job.
    5. Generate a profitability report that shows revenue, expenses (incl. **Contractor** payments), and net profit.
  - **Expected Outcome:** Clear understanding of each job's financial performance with accurate profit calculation.

- **Use Case Name:** Mobile Expense Tracking
  - **Description:** Quickly log business expenses (materials, fuel, etc.) while in the field and associate them with specific jobs.
  - **Actors:** Business owner, potentially **Contractor** (if granted permission in future versions for job-specific expenses they incur and bill for)
  - **Steps:**
    1. Open mobile app and select "Add Expense" function.
    2. Enter expense details (amount, vendor, category).
    3. Select the associated job/client.
    4. Take photo of receipt (if applicable).
    5. Save the expense (works offline if needed).
  - **Expected Outcome:** Accurate expense records captured in real-time with minimal effort.

- **Use Case Name:** **Contractor** Payment Tracking
  - **Description:** Record payments made to independent **Contractors** for services rendered on specific jobs.
  - **Actors:** Business owner
  - **Steps:**
    1. Select the relevant **Contractor**.
    2. Enter payment details (amount, date, payment method).
    3. Associate the payment with the specific job(s) the **Contractor** worked on.
    4. Update job costing records.
    5. View payment history per **Contractor**.
  - **Expected Outcome:** Accurate tracking of payments to **Contractors**, contributing to correct job profitability calculations.

- **Use Case Name:** GST/QST Reporting
  - **Description:** Generate a clear summary report for GST/QST filing.
  - **Actors:** Business owner, accountant
  - **Steps:**
    1. Enter sales and expenses with GST/QST details.
    2. Generate a report for a specific period (monthly, quarterly, annually).
    3. Export the report as PDF or CSV for filing or sharing with accountant.
  - **Expected Outcome:** Accurate totals for sales, GST/QST collected, Input Tax Credits (ITCs), and net owed/refundable.

- **Use Case Name:** Invoice Generation
  - **Description:** Create and send professional invoices to clients.
  - **Actors:** Business owner
  - **Steps:**
    1. Select client and associated job(s).
    2. Review job details and pricing.
    3. Generate invoice with appropriate tax calculations.
    4. Send invoice via email or export as PDF.
    5. Track payment status.
  - **Expected Outcome:** Professional invoices delivered promptly with correct tax calculations.

- **Use Case Name:** Cash Payment Tracking (Client)
  - **Description:** Track cash payments received from clients for informal operators.
  - **Actors:** Business owner
  - **Steps:**
    1. Quickly record cash payment received from client.
    2. Associate payment with service provided (minimal details).
    3. Update daily/weekly cash income totals.
    4. Review cash flow summary.
  - **Expected Outcome:** Simple view of cash received with minimal data entry effort, supporting basic income tracking for informal operations.

- **Use Case Name:** Weekly Profit Summary View
  - **Description:** Provide a simple weekly overview of income versus expenses (including **Contractor** payments) for quick business health assessment.
  - **Actors:** Business owner
  - **Steps:**
    1. Access weekly summary dashboard.
    2. View total income for the week across all clients/jobs.
    3. View total expenses by basic category (fuel, materials, **Contractor payments**, etc.).
    4. See calculated weekly profit/loss figure.
    5. Compare to previous weeks (optional).
  - **Expected Outcome:** Clear, at-a-glance understanding of weekly financial performance with minimal complexity.

- **Use Case Name:** Tax Guidance for New Businesses
  - **Description:** Provide basic information and links about Quebec tax obligations and thresholds for new/growing businesses.
  - **Actors:** Business owner, prospective business owner
  - **Steps:**
    1. Access tax information section within the app.
    2. Review GST/QST registration thresholds and requirements (via links/summaries).
    3. Access information about common deductible expenses for the industry (via links/summaries).
    4. Receive notifications when approaching tax thresholds based on tracked income.
    5. Get links to official resources (Revenu Québec, CRA) for further information.
  - **Expected Outcome:** Increased confidence and understanding of tax obligations, reducing anxiety around formalization and compliance.

### 3. User Journey Maps
- **Journey Name:** New Job Financial Lifecycle
  - **Stages:**
    1. Job creation and initial quoting
    2. Material purchasing and expense tracking
    3. Job execution (potentially involving **Contractors**) and additional expense/cost tracking
    4. Job completion, **Contractor** payment processing, and client invoice generation
    5. Payment collection (client) and reconciliation
    6. Profitability analysis (including **Contractor** costs)
  - **Touchpoints:**
    - Mobile app for field expenses
    - Desktop interface for invoicing and reporting
    - Client communications for quotes and invoices
    - Banking integration for payment tracking (Future)
    - **Contractor** payment records
  - **Pain Points:**
    - Disconnection between initial quote and actual expenses (including **Contractor** costs)
    - Forgotten expenses when receipts are lost
    - Manual effort to calculate true profitability
    - Tax implications not considered in profitability analysis
  - **Opportunities:**
    - Streamline quote-to-invoice process
    - Automate tax calculations throughout job lifecycle
    - Provide real-time profitability insights
    - Enable receipt capture and digital storage
    - Simplify tracking of **Contractor** costs per job

- **Journey Name:** Offline Expense Tracking
  - **Stages:**
    1. Purchase materials/supplies at vendor
    2. Log expense offline in the field
    3. Tag expense to a specific job/client
    4. Add receipt documentation
    5. Sync data when back online
    6. Verify expense in financial reports
  - **Touchpoints:**
    - Mobile app (offline mode)
    - Receipt capture functionality
    - Job/client selection interface
    - Sync notification system
  - **Pain Points:**
    - Limited connectivity in remote work areas
    - Need for basic client/job info while offline
    - Risk of data loss if device is damaged
    - Duplicate entries when sync fails
  - **Opportunities:**
    - Enable offline access to client/job info
    - Create quick-entry functionality for common expenses
    - Implement reliable sync mechanism
    - Add quick note addition while offline

- **Journey Name:** Tax Reporting Cycle
  - **Stages:**
    1. Ongoing recording of sales with appropriate GST/QST
    2. Tracking of expenses with input tax credits
    3. Periodic (monthly/quarterly) review of tax status
    4. Tax period filing preparation
    5. Report generation for accountant
    6. Actual filing with tax authorities
  - **Touchpoints:**
    - Expense entry with tax classification
    - Invoice creation with tax calculations
    - Tax summary dashboard
    - Export functionality for reports
  - **Pain Points:**
    - Complexity of GST/QST rules and applications
    - Difficulty tracking input tax credits across many expenses
    - Time-consuming reporting process
    - Risk of errors in manual calculations
  - **Opportunities:**
    - Automate tax calculations on both revenue and expenses
    - Provide clear tax status dashboard
    - Generate compliant reports for filing periods
    - Offer export options compatible with accountant needs

- **Journey Name:** Informal-to-Formal Transition Journey
  - **Stages:**
    1. Initial cash-based income tracking with minimal structure
    2. Gradual addition of expense categories and basic profit tracking
    3. Exploration of tax rules and obligations (GST/QST thresholds)
    4. Decision to formalize business operations
    5. Implementation of invoicing and formal payment tracking (clients and potentially **Contractors**)
    6. First tax filing as a registered business
  - **Touchpoints:**
    - Simple weekly profit dashboard
    - Tax information resources
    - Invoice/quote creation tools
    - Client management transition
    - **Contractor** payment tracking
    - First GST/QST reporting
  - **Pain Points:**
    - Anxiety around tax compliance and registration
    - Uncertainty about when/how to register for GST/QST
    - Need for historical data during formalization
    - Added complexity of formal financial tracking
    - Potential client relationship changes (receipt issuance, tax charging)
    - Potential need to formalize agreements with **Contractors**.
  - **Opportunities:**
    - Provide clear guidance on formalization process
    - Offer simplified tax information resources
    - Create smooth transition between operating models
    - Support gradual feature adoption as business formalizes
    - Support tracking for formalizing **Contractor** relationships (future)

- **Journey Name:** Seasonal Transition Journey
  - **Stages:**
    1. End-of-season financial review for landscaping
    2. Preparation for winter operations (snow removal)
    3. Adaptation to different billing models (per-visit vs monthly/per-storm)
    4. Equipment and material expense tracking changes
    5. Managing different client expectations and service models
    6. End-of-winter financial analysis and landscaping preparation
  - **Touchpoints:**
    - Service type switch in the application
    - Contract management for recurring clients
    - Seasonal profit comparison views
    - Equipment and material inventory changes
    - Storm event tracking (snow operations)
  - **Pain Points:**
    - Different profitability metrics between service types
    - Transitioning clients between service models
    - Managing cash flow during seasonal changes
    - Adapting to reactive vs scheduled service delivery
    - Tracking different expense categories by season
  - **Opportunities:**
    - Provide unified financial view across service types
    - Support different billing/contract models by season
    - Enable service-specific reporting and analysis
    - Simplify year-round financial planning

## Validation Methods
- [ ] User interviews via video calls or phone calls with 5-7 service business owners in the Greater Montreal area
  - Mix of English, French, and bilingual participants
  - Focus on solo operators and small businesses (engaging 1-10 employees/**Contractors**)
  - Key Interview Topics:
    1. Current Software Usage:
       - Accounting/bookkeeping solutions
       - Invoicing tools
       - Expense tracking methods
       - Payment processing systems
       - Job scheduling/**Contractor** management tools
       - Integration points between current tools
    2. Price Sensitivity:
       - Current software expenditure
       - Perceived value of proposed solution
       - Willingness to pay assessment
       - Price point preferences
       - ROI expectations
    3. Seasonal Operations:
       - Winter service offerings (snow removal)
       - Seasonal financial tracking differences
       - Contract structure variations
       - Material usage tracking needs
- [ ] Surveys distributed to broader service business community in Quebec
- [ ] Observational studies of current financial management processes (if feasible)

## Assumptions
- [ ] Target users are comfortable using smartphones for basic business tasks
- [ ] Most target users have limited formal accounting knowledge
- [ ] GST/QST tracking is a significant pain point for Quebec-based businesses
- [ ] Users prioritize simplicity and speed over comprehensive accounting features
- [ ] Offline functionality is essential for field-based expense tracking
- [ ] Bilingual support (English/French) is necessary for the Quebec market
- [ ] Users engaging external help often intend a **Contractor** relationship, even if informal initially.

## Risks
- [ ] Users may resist adoption if the learning curve is too steep
  - Impact: Low user adoption and retention
  - Mitigation: Focus on intuitive UX with minimal training requirements; offer simple onboarding process
- [ ] Incorrect tax calculations could lead to compliance issues
  - Impact: Legal/financial repercussions for users; loss of trust
  - Mitigation: Consult with tax experts; rigorously test tax calculation functions
- [ ] Offline functionality may be technically challenging to implement reliably
  - Impact: User frustration, potential data loss
  - Mitigation: Prioritize robust offline-first architecture; implement reliable sync mechanisms
- [ ] Competition from established financial tools
  - Impact: Difficulty gaining market share
  - Mitigation: Focus on unique value proposition (job costing, QC GST/QST focus, simplicity, **Contractor** tracking)
- [ ] User confusion regarding legal classification of **Contractors** vs. Employees.
  - Impact: Potential misreliance on app terminology, legal risks for users.
  - Mitigation: Clear disclaimers, focus on tracking payments not classification, encourage professional advice.

## Budget Allocation
- [ ] Reserve a portion of the budget for marketing and onboarding post-MVP
  - **Marketing:** Landing page, targeted ads (e.g., Facebook for Quebec service businesses)
  - **Onboarding:** Bilingual help guides and tutorial videos
  - **Initial budget:** Approximately 15-20% of total project budget

## Review Notes
- [ ] Review 1
  - Reviewer:
  - Date:
  - Comments:
  - Status:

## Change Log
| Date | Version | Changed By | Changes Made |
|------|---------|------------|--------------|
| April 4, 2025 | 1.0 | FinTrack PM | Created initial User Needs Analysis |
| April 8, 2025 | 1.1 | FinTrack PM | Standardized terminology: Replaced "helper," "crew member" (where appropriate) with "**Contractor**". Adjusted relevant Personas, Use Cases, Journey Maps, Assumptions, and Risks accordingly. Added specific Use Case for **Contractor** Payment Tracking. |


## Sign-off
- [ ] Technical Review
- [ ] Business Review
- [ ] Stakeholder Review
- [ ] Final Approval

## Next Steps
- [x] Validate user personas through stakeholder interviews
- [x] Schedule user interviews with service business owners
- [x] Review technical feasibility of offline functionality
- [x] Define detailed MVP feature scope based on this analysis
- [ ] Create prototype screens for key use cases (postponed)
