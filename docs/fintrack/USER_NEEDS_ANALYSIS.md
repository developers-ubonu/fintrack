# User Needs Analysis - FinTrack

## Metadata
**Version:** 1.4 
**Status:** Draft
**Last Updated:** April 8, 2025 
**Owner:** FinTrack Project Manager
**Reviewers:** [To be determined]

## Purpose
To identify and document the needs, goals, and pain points of small landscaping and related service business owners in Quebec, ensuring the FinTrack solution aligns with their financial tracking requirements and operational context.

## Success Criteria
- [ ] Clear identification of primary user personas for small service businesses
- [ ] Comprehensive use cases that reflect real-world financial tracking scenarios and MVP capabilities
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

*(Original Use Cases + Suggested + New UC-CoM + Refinements)*

- **Use Case Name (UC-JP):** Job Profitability Tracking
  - **Description:** Track all income and expenses (including **Contractor** payments) related to a specific service job to determine profitability.
  - **Actors:** Business owner
  - **Steps:**
    1.  Create a new job in the system with client details and job specifications. (See UC-JM)
    2.  Record all income/payments for the job. (See UC-CT or related invoicing payment tracking via UC-IG)
    3.  Track all direct expenses (materials, fuel, etc.) and associate them with the job. (See UC-ME)
    4.  Track payments made to **Contractors** associated with the job. (See UC-CP)
    5.  Generate a profitability report that shows revenue, expenses (incl. **Contractor** payments), and net profit.
  - **Expected Outcome:** Clear understanding of each job's financial performance with accurate profit calculation.

- **Use Case Name (UC-ME):** Mobile Expense Tracking
  - **Description:** Quickly log business expenses (materials, fuel, etc.) while in the field and associate them with specific jobs.
  - **Actors:** Business owner, potentially **Contractor** (if granted permission in future versions for job-specific expenses they incur and bill for)
  - **Steps:**
    1.  Open mobile app and select "Add Expense" function. *(Ensure necessary Client/Job list data is available offline for selection in step 3).*
    2.  Enter expense details (amount, vendor, category - e.g., Fuel, Materials, Tools, Repairs, Contractor Payments).
    3.  Select the associated job/client (requires access to job/client list available offline - See UC-JM, UC-CM).
    4.  Take photo of receipt (if applicable).
    5.  Save the expense (works offline if needed, syncs when online).
  - **Expected Outcome:** Accurate expense records captured in real-time with minimal effort, even when offline.

- **Use Case Name (UC-CoM):** Contractor Management **(New)**
  - **Description:** Add, view, search, and manage basic contractor information necessary for tracking payments.
  - **Actors:** Business owner
  - **Steps:**
    1.  Select option to view Contractor List.
    2.  View list of existing contractors with key details (e.g., Name, Contact).
    3.  Select option to Add New Contractor.
    4.  Enter contractor details (Name - Individual/Business, Contact Info - Phone/Email).
    5.  Save new contractor information.
    6.  Select an existing contractor to view/edit basic details.
    7.  Use search/filter function to find specific contractors in the list.
  - **Expected Outcome:** An organized list of contractors is maintained, enabling efficient selection for payment tracking (UC-CP) and job costing (UC-JP).

- **Use Case Name (UC-CP):** Contractor Payment Tracking
  - **Description:** Record payments made to independent **Contractors** for services rendered on specific jobs or for general services.
  - **Actors:** Business owner
  - **Steps:**
    1.  Ensure the **Contractor** exists in the system (See UC-CoM) and select them.
    2.  Enter payment details (amount, date, payment method).
    3.  Associate the payment with the specific job(s) the **Contractor** worked on. *(This is recommended for accurate job costing via UC-JP, even if technically optional in the system).* (Requires job list access - see UC-JM).
    4.  Update job costing records (if associated with a job - see UC-JP).
    5.  View payment history per **Contractor**.
  - **Expected Outcome:** Accurate tracking of payments to **Contractors**, contributing to correct job profitability calculations and overall expense tracking.

- **Use Case Name (UC-TR):** GST/QST Reporting
  - **Description:** Generate a clear summary report for GST/QST filing preparation.
  - **Actors:** Business owner, accountant
  - **Steps:**
    1.  Ensure sales (via invoices or direct income entry) and expenses are recorded with GST/QST details. (See UC-IG, UC-ME)
    2.  Generate a tax report for a specific period (monthly, quarterly, annually).
    3.  View calculated summary totals for the period: Total Sales, Total GST/QST Collected, Total Input Tax Credits (ITCs) / GST/QST Paid on Expenses, Net Tax Payable/Refundable calculation.
    4.  Export the report as PDF or CSV for filing or sharing with accountant.
  - **Expected Outcome:** Accurate summary totals for key tax figures, simplifying tax preparation.

- **Use Case Name (UC-IG):** Invoice Generation
  - **Description:** Create and send professional invoices to clients.
  - **Actors:** Business owner
  - **Steps:**
    1.  Select client and associated job(s). (See UC-CM, UC-JM)
    2.  Select an invoice template (if multiple basic options exist).
    3.  Review job details and enter line items/pricing.
    4.  Generate invoice preview with appropriate tax calculations (GST/QST if applicable).
    5.  Send invoice via email or export as PDF.
    6.  Track invoice payment status (e.g., Draft, Sent, Paid, Overdue).
    7.  Record payments received against the invoice (including handling of partial payments).
  - **Expected Outcome:** Professional invoices delivered promptly with correct tax calculations, and payment status (including partial payments) tracked accurately.

- **Use Case Name (UC-CT):** Cash Payment Tracking (Client)
  - **Description:** Track cash payments received from clients, especially for informal operators or immediate payments, with extreme simplicity.
  - **Actors:** Business owner
  - **Steps:**
    1.  Quickly record cash payment received (amount, date).
    2.  Optionally associate payment with client and/or a service/job (requires minimal detail entry). (See UC-CM, UC-JM)
    3.  Update daily/weekly cash income totals.
    4.  Review cash flow summary (or contribution to weekly summary).
  - **Expected Outcome:** Simple view of cash received with minimal data entry effort, supporting basic income tracking for informal operations.

- **Use Case Name (UC-WS):** Weekly Profit Summary View
  - **Description:** Provide a simple weekly overview of income versus expenses (including **Contractor** payments) for quick business health assessment.
  - **Actors:** Business owner
  - **Steps:**
    1.  Access weekly summary dashboard/view.
    2.  View total income recorded for the week across all clients/jobs.
    3.  View total expenses recorded by basic category (fuel, materials, **Contractor payments**, etc.).
    4.  See calculated weekly profit/loss figure.
    5.  Optionally compare to previous weeks.
  - **Expected Outcome:** Clear, at-a-glance understanding of weekly financial performance with minimal complexity.

- **Use Case Name (UC-TG):** Tax Guidance Access
  - **Description:** Access basic information and links about Quebec tax obligations and thresholds, particularly for new/growing businesses. (Replaces "Tax Guidance for New Businesses" for clarity).
  - **Actors:** Business owner, prospective business owner
  - **Steps:**
    1.  Access tax information section within the app.
    2.  View informational summaries or links regarding GST/QST registration thresholds and requirements in Quebec.
    3.  Access informational summaries or links about common deductible expense types for the industry in Quebec.
    4.  Receive system notifications when approaching tax thresholds based on tracked income (if feature enabled).
    5.  Access links to official resources (Revenu Québec, CRA) for definitive information. *(Note: The app provides information/links, not financial advice).*
  - **Expected Outcome:** Increased awareness and reduced anxiety regarding tax obligations via curated information and links; facilitates transition to formal compliance.

- **Use Case Name (UC-CM):** Client Management
  - **Description:** Add, view, search, and manage basic client information necessary for job tracking and invoicing.
  - **Actors:** Business owner
  - **Steps:**
    1.  Select option to view Client List.
    2.  View list of existing clients with key details (e.g., Name, Contact).
    3.  Select option to Add New Client.
    4.  Enter client details (Name, Contact Info - Phone/Email/Address).
    5.  Save new client information.
    6.  Select an existing client to view/edit details.
    7.  Use search/filter function to find specific clients in the list.
  - **Expected Outcome:** An organized list of clients is maintained, enabling efficient selection for jobs and invoicing.

- **Use Case Name (UC-JM):** Job Management
  - **Description:** Create new jobs, associate them with clients, track basic job status, and view job history.
  - **Actors:** Business owner
  - **Steps:**
    1.  Select option to view Job List.
    2.  View list of existing jobs with key details (e.g., Name/Description, Client, Status).
    3.  Select option to Add New Job.
    4.  Enter job details (Name/Description, Location, Service Type - e.g., Landscaping, Snow Removal, Cleaning).
    5.  Associate the job with an existing Client (from client list - see UC-CM).
    6.  Set initial job Status (e.g., Planned, In-Progress).
    7.  Save new job information.
    8.  Select an existing job to view details or update status (e.g., mark as Complete).
    9.  Use search/filter function to find specific jobs (e.g., by client, by status).
  - **Expected Outcome:** Jobs are created and tracked, allowing expenses and income to be associated correctly for profitability analysis across various service types.

- **Use Case Name (UC-AM):** Account Management
  - **Description:** Manage user login, profile information, and application settings like language preference. (Corresponds to "Account Settings & Profile" in MVP Scope).
  - **Actors:** Business owner (User)
  - **Steps:**
    1.  User logs into the application using credentials (email/password).
    2.  Access Profile/Settings section.
    3.  View current business profile information.
    4.  Edit basic profile information (e.g., Business Name, Contact Info).
    5.  Select preferred language (English/French) for the application interface.
    6.  Access option to change password or initiate password reset flow.
    7.  Log out of the application.
  - **Expected Outcome:** User can securely access their account, manage basic profile details, set language preference, and maintain account security.

### 3. User Journey Maps

- **Journey Name:** New Job Financial Lifecycle
  - **Stages:**
    1.  Job creation and initial quoting
    2.  Material purchasing and expense tracking
    3.  Job execution (potentially involving **Contractors**) and additional expense/cost tracking
    4.  Job completion, **Contractor** payment processing, and client invoice generation
    5.  Payment collection (client) and reconciliation
    6.  Profitability analysis (including **Contractor** costs)
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
    1.  Purchase materials/supplies at vendor
    2.  Log expense offline in the field (with access to necessary client/job data for tagging)
    3.  Tag expense to a specific job/client
    4.  Add receipt documentation
    5.  Sync data when back online
    6.  Verify expense in financial reports
  - **Touchpoints:**
    - Mobile app (offline mode)
    - Receipt capture functionality
    - Job/client selection interface (with offline data)
    - Sync notification system
  - **Pain Points:**
    - Limited connectivity in remote work areas
    - Need for basic client/job info while offline
    - Risk of data loss if device is damaged
    - Duplicate entries when sync fails
  - **Opportunities:**
    - Enable offline access to essential client/job info for tagging
    - Create quick-entry functionality for common expenses
    - Implement reliable sync mechanism
    - Add quick note addition while offline

- **Journey Name:** Tax Reporting Cycle
  - **Stages:**
    1.  Ongoing recording of sales with appropriate GST/QST
    2.  Tracking of expenses with input tax credits
    3.  Periodic (monthly/quarterly) review of tax status
    4.  Tax period filing preparation
    5.  Report generation for accountant
    6.  Actual filing with tax authorities
  - **Touchpoints:**
    - Expense entry with tax classification
    - Invoice creation with tax calculations
    - Tax summary dashboard (showing key totals: Sales, GST/QST Collected, ITCs, Net Payable/Refundable)
    - Export functionality for reports
  - **Pain Points:**
    - Complexity of GST/QST rules and applications
    - Difficulty tracking input tax credits across many expenses
    - Time-consuming reporting process
    - Risk of errors in manual calculations
  - **Opportunities:**
    - Automate tax calculations on both revenue and expenses
    - Provide clear tax status dashboard with key figures
    - Generate compliant reports for filing periods
    - Offer export options compatible with accountant needs

- **Journey Name:** Informal-to-Formal Transition Journey
  - **Stages:**
    1.  Initial cash-based income tracking with minimal structure (via UC-CT)
    2.  Gradual addition of expense categories and basic profit tracking
    3.  Exploration of tax rules and obligations (GST/QST thresholds via Tax Guidance - UC-TG)
    4.  Decision to formalize business operations
    5.  Implementation of invoicing and formal payment tracking (clients and potentially **Contractors**) (via UC-IG, UC-CP)
    6.  First tax filing as a registered business (using UC-TR)
  - **Touchpoints:**
    - Simple weekly profit dashboard (UC-WS)
    - Tax information resources (UC-TG)
    - Invoice/quote creation tools (UC-IG)
    - Client management transition (UC-CM)
    - **Contractor** management and payment tracking (UC-CoM, UC-CP)
    - First GST/QST reporting (UC-TR)
  - **Pain Points:**
    - Anxiety around tax compliance and registration
    - Uncertainty about when/how to register for GST/QST
    - Need for historical data during formalization
    - Added complexity of formal financial tracking
    - Potential client relationship changes (receipt issuance, tax charging)
    - Potential need to formalize agreements with **Contractors**.
  - **Opportunities:**
    - Provide clear guidance links/info on formalization process via UC-TG
    - Offer simplified tax information resources
    - Create smooth transition between operating models
    - Support gradual feature adoption as business formalizes
    - Support tracking for formalizing **Contractor** relationships (future)

- **Journey Name:** Seasonal Transition Journey
  - **Stages:**
    1.  End-of-season financial review for landscaping
    2.  Preparation for winter operations (snow removal)
    3.  Adaptation to different billing models (per-visit vs monthly/per-storm)
    4.  Equipment and material expense tracking changes
    5.  Managing different client expectations and service models
    6.  End-of-winter financial analysis and landscaping preparation
  - **Touchpoints:**
    - Service type switch in the application (part of UC-JM)
    - Contract management for recurring clients (Future Feature)
    - Seasonal profit comparison views (Reporting Feature)
    - Equipment and material inventory changes (Expense Tracking - UC-ME)
    - Storm event tracking (snow operations) (Future Feature)
  - **Pain Points:**
    - Different profitability metrics between service types
    - Transitioning clients between service models
    - Managing cash flow during seasonal changes
    - Adapting to reactive vs scheduled service delivery
    - Tracking different expense categories by season
  - **Opportunities:**
    - Provide unified financial view across service types
    - Support different billing/contract models by season (Future)
    - Enable service-specific reporting and analysis
    - Simplify year-round financial planning

## Validation Methods
- [ ] User interviews via video calls or phone calls with 5-7 service business owners in the Greater Montreal area
  - Mix of English, French, and bilingual participants
  - Focus on solo operators and small businesses (engaging 1-10 employees/**Contractors**)
  - Key Interview Topics:
    1.  Current Software Usage:
       - Accounting/bookkeeping solutions
       - Invoicing tools
       - Expense tracking methods
       - Payment processing systems
       - Job scheduling/**Contractor** management tools
       - Integration points between current tools
    2.  Price Sensitivity:
       - Current software expenditure
       - Perceived value of proposed solution
       - Willingness to pay assessment
       - Price point preferences
       - ROI expectations
    3.  Seasonal Operations:
       - Winter service offerings (snow removal)
       - Seasonal financial tracking differences
       - Contract structure variations
       - Material usage tracking needs
- [ ] Surveys distributed to broader service business community in Quebec
- [ ] Observational studies of current financial management processes (if feasible)
- [ ] Usability testing of prototypes based on defined Use Cases.

## Assumptions
- [ ] Target users are comfortable using smartphones for basic business tasks
- [ ] Most target users have limited formal accounting knowledge
- [ ] GST/QST tracking is a significant pain point for Quebec-based businesses
- [ ] Users prioritize simplicity and speed over comprehensive accounting features
- [ ] Offline functionality (including access to necessary data for tagging) is essential for field-based expense tracking
- [ ] Bilingual support (English/French) is necessary for the Quebec market
- [ ] Users engaging external help often intend a **Contractor** relationship, even if informal initially.

## Risks
- [ ] Users may resist adoption if the learning curve is too steep
  - Impact: Low user adoption and retention
  - Mitigation: Focus on intuitive UX with minimal training requirements; offer simple onboarding process based on Use Cases.
- [ ] Incorrect tax calculations could lead to compliance issues
  - Impact: Legal/financial repercussions for users; loss of trust
  - Mitigation: Consult with tax experts; rigorously test tax calculation functions (related to UC-TR, UC-IG).
- [ ] Offline functionality (including data sync and offline data access) may be technically challenging to implement reliably
  - Impact: User frustration, potential data loss (related to UC-ME)
  - Mitigation: Prioritize robust offline-first architecture; implement reliable sync mechanisms and ensure necessary lookup data is available offline.
- [ ] Competition from established financial tools
  - Impact: Difficulty gaining market share
  - Mitigation: Focus on unique value proposition (job costing, QC GST/QST focus, simplicity, **Contractor** tracking).
- [ ] User confusion regarding legal classification of **Contractors** vs. Employees.
  - Impact: Potential misreliance on app terminology, legal risks for users.
  - Mitigation: Clear disclaimers, focus on tracking payments (UC-CP) and managing contacts (UC-CoM) not classification, encourage professional advice.
- [ ] Misinterpretation of Tax Guidance information provided via UC-TG.
  - Impact: User makes incorrect tax decisions based on perceived advice.
  - Mitigation: Clearly label guidance as informational links/summaries, not advice; include prominent disclaimers; link only to official government sources.

## Budget Allocation
- [ ] Reserve a portion of the budget for marketing and onboarding post-MVP
  - **Marketing:** Landing page, targeted ads (e.g., Facebook for Quebec service businesses)
  - **Onboarding:** Bilingual help guides and tutorial videos aligned with key Use Cases.
  - **Initial budget:** Approximately 15-20% of total project budget

## Review Notes
- [ ] Review 1
  - Reviewer:
  - Date:
  - Comments:
  - Status:

## Change Log
| Date          | Version | Changed By   | Changes Made                                                                                                                               |
| :------------ | :------ | :----------- | :----------------------------------------------------------------------------------------------------------------------------------------- |
| April 4, 2025 | 1.0     | FinTrack PM  | Created initial User Needs Analysis                                                                                                        |
| April 8, 2025 | 1.1     | FinTrack PM  | Standardized terminology: Replaced "helper," "crew member" with "**Contractor**". Adjusted relevant sections. Added UC for Contractor Payments. |
| April 8, 2025 | 1.2     | Gemini Model | Added suggested Use Cases: UC-CM (Client Management), UC-JM (Job Management), UC-AM (Account Management) based on scope analysis. Renamed UC-TG. Minor adjustments for consistency. |
| April 8, 2025 | 1.3     | Gemini Model | Added **UC-CoM (Contractor Management)** based on dependency analysis. Updated UC-CP step 1 to reference UC-CoM. Updated Next Steps. |
| April 8, 2025 | 1.4     | Gemini Model | Refined steps in UC-ME, UC-CP, UC-TR, UC-IG, UC-CT, UC-TG, UC-JM based on detailed analysis for clarity and alignment with MVP features/interview feedback. Updated version number. Added Risk related to Tax Guidance interpretation. |

## Sign-off
- [ ] Technical Review
- [ ] Business Review
- [ ] Stakeholder Review
- [ ] Final Approval

## Next Steps **(Updated)**
- [x] Validate user personas through stakeholder interviews
- [x] Schedule user interviews with service business owners
- [x] Review technical feasibility of offline functionality (including offline data access needs)
- [x] Define detailed MVP feature scope based on this analysis
- [ ] Create prototype screens for key use cases (postponed)
- [ ] **Begin decomposition of MVP Use Cases (UC-JP, UC-ME, UC-CoM, UC-CP, UC-TR, UC-IG, UC-CT, UC-WS, UC-TG, UC-CM, UC-JM, UC-AM) into detailed Functional Requirements with Acceptance Criteria, incorporating refinements from v1.4.**