# User Needs Analysis - FinTrack

## Metadata
**Version:** 1.5 *(Updated Use Cases for enhanced MVP Scope v1.4/v0.4)*
**Status:** Draft
**Last Updated:** April 8, 2025
**Owner:** FinTrack Project Manager
**Reviewers:** [To be determined]

## Purpose
To identify and document the needs, goals, and pain points of small landscaping and related service business owners in Quebec, ensuring the FinTrack solution aligns with their financial tracking requirements and operational context. This version updates Use Cases to reflect an enhanced MVP scope focused on automation and ease of input.

## Success Criteria
- [ ] Clear identification of primary user personas for small service businesses
- [x] Comprehensive use cases that reflect real-world financial tracking scenarios and **enhanced MVP capabilities (automation)**
- [x] User journey maps highlighting key touchpoints and pain points in financial management, considering automation features

## Content Requirements
### 1. User Personas *(Minor refinements based on automation focus)*
- **Persona Name:** Solo Operator
  - **Role:** Independent service business owner
  - **Goals:**
    - Track profitability of each job accurately
    - **Minimize time spent on financial administration (via automation)**
    - Maintain clear records for tax compliance (GST/QST)
    - Create professional invoices quickly
    - Keep business and personal finances separate
  - **Pain Points:**
    - **Time lost manually entering/allocating field expenses (receipts, etc.)**
    - Manual financial record-keeping feels tedious and error-prone
    - Confusion about tax obligations and input tax credits
    - Inability to determine which jobs are most profitable
    - Limited connectivity potentially hindering advanced automation features
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
    - **Efficiently track expenses by job and category using automation**
    - **Easily track and allocate payments to Contractors**
    - Generate reports for business planning
    - Manage cash flow during seasonal fluctuations
    - Prepare accurate tax documentation
  - **Pain Points:**
    - Complexity of tracking multiple jobs simultaneously
    - Difficulty associating expenses with specific jobs **without significant manual effort**
    - Accurately tracking and **allocating** costs associated with employees vs. **Contractors**.
    - Limited visibility into overall business financial health
    - Cumbersome process for GST/QST reporting
    - Time spent on administration rather than business growth

- **Persona Name:** Prospective/Early-Stage Operator
  - **Role:** Individual planning to start or recently started a small service business
  - **Goals:**
    - Start with proper, **easy** financial organization from day one
    * Understand basic tax obligations and thresholds (GST/QST) **with guidance**
    - Look professional to clients
    - Track profitability to make informed business decisions
    - Set up a foundation for potential business growth (including potentially engaging **Contractors**)
  - **Pain Points:**
    - Confusion and anxiety about Quebec tax rules and thresholds
    - Uncertainty about which expenses are deductible **and how to track them easily**
    - Lack of affordable guidance on business formalization
    - Overwhelmed by complex accounting software; **needs extreme simplicity**
    - Need to appear professional despite being new
  - **Context:**
    - Works primarily through mobile device (no computer)
    - Limited or no prior business administration experience
    - May offer multiple service types (e.g., landscaping, snow removal, cleaning)
    - Looking to build recurring client base
    - Plans to operate mostly via cash and e-transfers initially

### 2. Use Cases *(Revised UC-ME, UC-CP)*

*(Original Use Cases + Suggested + New UC-CoM + Refinements + Automation Updates)*

- **Use Case Name (UC-JP):** Job Profitability Tracking
  - **Description:** Track all income and expenses (including **Contractor** payments) related to a specific service job to determine profitability. *(Leverages automated inputs from UC-ME/UC-CP for efficiency).*
  - **Actors:** Business owner
  - **Steps:**
    1.  Create a new job in the system with client details and job specifications. (See UC-JM)
    2.  Record all income/payments for the job. (See UC-CT or related invoicing payment tracking via UC-IG)
    3.  Track all direct expenses (materials, fuel, etc.) and associate them with the job **via automated or manual input**. (See UC-ME)
    4.  Track payments made to **Contractors** and associate/allocate them with the job. (See UC-CP)
    5.  Generate a profitability report that shows revenue, expenses (incl. **Contractor** payments), and net profit.
  - **Expected Outcome:** Clear understanding of each job's financial performance with accurate profit calculation, **achieved with reduced manual effort**.

- **Use Case Name (UC-ME):** Mobile Expense Tracking *(Revised Steps for Automation)*
  - **Description:** Quickly log business expenses (materials, fuel, etc.) while in the field using automation features (OCR, suggestions) and associate them with specific jobs, allowing for easy splitting of shared costs.
  - **Actors:** Business owner
  - **Steps:**
    1.  Open mobile app and select "Add Expense" function.
    2.  **Snap photo of receipt.**
    3.  **App performs OCR** to attempt extraction of Vendor, Date, Amount, GST/QST -> User quickly confirms or edits extracted data. *(Note: OCR may require connectivity).*
    4.  (Optional) User manually enters details if no receipt or OCR fails.
    5.  **App suggests potential Job(s)** based on context (GPS location, calendar, recent activity) -> User confirms suggestion or manually selects Job(s) from a list (list available offline). *(Note: Suggestions may require connectivity).*
    6.  **If expense applies to multiple jobs (or suggested), App prompts for allocation** -> User utilizes simple UI (sliders/percentages/amounts) to split the cost across selected jobs.
    7.  User confirms expense category (may be suggested based on vendor/OCR).
    8.  User confirms if expense is "General Business Expense" (not linked to specific jobs).
    9.  Save the expense (basic data capture works offline, syncs when online; advanced features may require sync).
  - **Expected Outcome:** Accurate expense records captured in real-time **with significantly reduced manual effort** via automation; shared costs are easily allocated; basic capture works offline.

- **Use Case Name (UC-CoM):** Contractor Management
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

- **Use Case Name (UC-CP):** Contractor Payment Tracking *(Revised Steps for Automation)*
  - **Description:** Record payments made to independent **Contractors**, leveraging smart suggestions and simple allocation tools to associate payments accurately with specific jobs.
  - **Actors:** Business owner
  - **Steps:**
    1.  Ensure the **Contractor** exists in the system (See UC-CoM) and select them.
    2.  Enter payment details (amount, date, payment method).
    3.  **App suggests Job(s)** the Contractor is associated with or worked on recently -> User confirms suggestion or manually selects Job(s). *(Note: Suggestions may require connectivity).*
    4.  **If payment applies to multiple jobs, App prompts for allocation** -> User utilizes simple UI (sliders/percentages/amounts) to split the payment across selected jobs.
    5.  User confirms if payment is "General Business Expense" (not linked to specific jobs).
    6.  Save the payment record.
    7.  System updates associated job costing records (UC-JP).
    8.  View payment history per **Contractor**.
  - **Expected Outcome:** Accurate tracking and **easy allocation** of payments to **Contractors**, contributing to correct job profitability calculations and overall expense tracking with minimal friction.

- **Use Case Name (UC-TR):** GST/QST Reporting
  - **Description:** Generate a clear summary report for GST/QST filing preparation, leveraging automatically captured tax data where possible.
  - **Actors:** Business owner, accountant
  - **Steps:**
    1.  Ensure sales (via invoices or direct income entry) and expenses are recorded with GST/QST details (potentially auto-captured via OCR in UC-ME). (See UC-IG, UC-ME)
    2.  Generate a tax report for a specific period (monthly, quarterly, annually).
    3.  View calculated summary totals for the period: Total Sales, Total GST/QST Collected, Total Input Tax Credits (ITCs) / GST/QST Paid on Expenses, Net Tax Payable/Refundable calculation.
    4.  Export the report as PDF or CSV for filing or sharing with accountant.
  - **Expected Outcome:** Accurate summary totals for key tax figures, simplifying tax preparation, **with reduced manual tax data entry**.

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
  - **Description:** Access basic information and links about Quebec tax obligations and thresholds, potentially integrated contextually within other workflows. (Replaces "Tax Guidance for New Businesses" for clarity).
  - **Actors:** Business owner, prospective business owner
  - **Steps:**
    1.  Access tax information section within the app OR via contextual links (e.g., from expense categories, profitability views).
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

### 3. User Journey Maps *(Refinements for Automation)*

- **Journey Name:** New Job Financial Lifecycle
  - **Stages:**
    1.  Job creation and initial quoting
    2.  Material purchasing and **automated expense capture (UC-ME)**
    3.  Job execution (potentially involving **Contractors**) and additional expense/cost tracking (**via UC-ME/UC-CP**)
    4.  Job completion, **easy Contractor payment allocation (UC-CP)**, and client invoice generation
    5.  Payment collection (client) and reconciliation
    6.  Profitability analysis (including **Contractor** costs)
  - **Touchpoints:**
    - Mobile app for **automated field expenses (OCR, suggestions)**
    - Desktop interface for invoicing and reporting
    - Client communications for quotes and invoices
    - Banking integration for payment tracking (Future)
    - **Contractor** payment records (simplified entry/allocation)
  - **Pain Points:**
    - Disconnection between initial quote and actual expenses (incl. **Contractor** costs)
    - **Manual effort to log/allocate expenses reduced**
    - Manual effort to calculate true profitability
    - Tax implications not considered in profitability analysis
  - **Opportunities:**
    - Streamline quote-to-invoice process
    * **Leverage OCR/suggestions for near real-time expense data**
    * Automate tax calculations throughout job lifecycle
    * Provide real-time profitability insights
    * **Simplify/automate receipt capture and digital storage**
    * Simplify tracking/allocation of **Contractor** costs per job

- **Journey Name:** Offline Expense Tracking *(Refined for limitations)*
  - **Stages:**
    1.  Purchase materials/supplies at vendor
    2.  Log expense offline in the field (**manual entry + photo capture**; access to cached client/job data for basic tagging)
    3.  Tag expense to a specific job/client (manual selection from cached list)
    4.  Add receipt documentation (photo stored locally)
    5.  Sync data when back online
    6.  **(Online Stage):** OCR processing occurs, smart suggestions may appear for refinement/confirmation.
    7.  Verify expense in financial reports
  - **Touchpoints:**
    - Mobile app (**offline mode: manual entry + photo capture**)
    - Receipt capture functionality (offline storage)
    - Job/client selection interface (with offline data)
    - Sync notification system
    - **(Online Touchpoint):** OCR results review, Smart suggestion review
  - **Pain Points:**
    - Limited connectivity preventing real-time OCR/suggestions
    - Need for basic client/job info while offline
    - Risk of data loss if device is damaged before sync
    - Duplicate entries if sync fails (needs robust handling)
  - **Opportunities:**
    - Enable offline access to essential client/job info for tagging
    - Create quick-entry functionality for common expenses (manual offline)
    - Implement reliable sync mechanism
    - **Provide clear UI indicating which features require connectivity**

- **Journey Name:** Tax Reporting Cycle *(Refined for automation)*
  - **Stages:**
    1.  Ongoing recording of sales with appropriate GST/QST
    2.  Tracking of expenses **with GST/QST data potentially auto-captured via OCR (UC-ME)**, identifying potential input tax credits
    3.  Periodic (monthly/quarterly) review of tax status
    4.  Tax period filing preparation
    5.  Report generation for accountant (leveraging captured data)
    6.  Actual filing with tax authorities
  - **Touchpoints:**
    - Expense entry with **auto-captured/verified** tax classification
    - Invoice creation with tax calculations
    - Tax summary dashboard (showing key totals: Sales, GST/QST Collected, ITCs, Net Payable/Refundable)
    - Export functionality for reports
  - **Pain Points:**
    - Complexity of GST/QST rules and applications
    * **Manual effort to find/enter tax amounts from receipts reduced**
    - Time-consuming reporting process
    - Risk of errors in manual calculations
  - **Opportunities:**
    - Automate tax calculations on both revenue and expenses
    - **Leverage OCR to streamline ITC tracking**
    * Provide clear tax status dashboard with key figures
    * Generate compliant reports for filing periods
    * Offer export options compatible with accountant needs

- **Journey Name:** Informal-to-Formal Transition Journey
  - **Stages:** *(Largely unchanged, but automation makes formal tracking easier)*
    1.  Initial cash-based income tracking with minimal structure (via UC-CT)
    2.  Gradual addition of expense categories and basic profit tracking (**simplified by UC-ME automation**)
    3.  Exploration of tax rules and obligations (GST/QST thresholds via Tax Guidance - UC-TG)
    4.  Decision to formalize business operations
    5.  Implementation of invoicing and formal payment tracking (clients and potentially **Contractors**) (**simplified by UC-IG, UC-CP automation**)
    6.  First tax filing as a registered business (using UC-TR, leveraging captured data)
  - **Touchpoints:** *(Automation improves experience at several points)*
    - Simple weekly profit dashboard (UC-WS)
    - Tax information resources (UC-TG)
    - Invoice/quote creation tools (UC-IG)
    - Client management transition (UC-CM)
    - **Contractor** management and **simplified** payment tracking (UC-CoM, UC-CP)
    - First GST/QST reporting (UC-TR - **data capture streamlined**)
  - **Pain Points:** *(Automation aims to reduce pain around complexity)*
    - Anxiety around tax compliance and registration
    - Uncertainty about when/how to register for GST/QST
    - Need for historical data during formalization
    - Added complexity of formal financial tracking **(reduced by automation)**
    - Potential client relationship changes (receipt issuance, tax charging)
    - Potential need to formalize agreements with **Contractors**.
  - **Opportunities:**
    - Provide clear guidance links/info on formalization process via UC-TG
    - Offer simplified tax information resources
    - Create smooth transition between operating models
    - **Automation features lower barrier to adopting formal tracking**
    - Support tracking for formalizing **Contractor** relationships (future)

- **Journey Name:** Seasonal Transition Journey
  *(No major changes needed based on automation scope)*
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
  - Key Interview Topics: *(Add validation for automation features)*
    1.  Current Software Usage: [...]
    2.  Price Sensitivity: [...]
    3.  Seasonal Operations: [...]
    4.  **Reaction to Automation:** Gauge interest/acceptance of OCR, smart suggestions, potential GPS use, permissions.
    5.  **Offline Needs:** Clarify expectations for offline availability of automated features.
- [ ] Surveys distributed to broader service business community in Quebec
- [ ] Observational studies of current financial management processes (if feasible)
- [ ] Usability testing of prototypes **incorporating automated workflows (OCR, suggestions, splitting)** based on defined Use Cases.

## Assumptions *(Revised Section)*
- [x] Target users are comfortable using smartphones for basic business tasks **and granting typical app permissions (camera, potentially location/calendar for advanced features)**
- [x] Most target users have limited formal accounting knowledge
- [x] GST/QST tracking is a significant pain point for Quebec-based businesses
- [x] Users prioritize **simplicity, speed, and effortless input** over comprehensive accounting features
- [x] **Manual offline** functionality is essential; **advanced automation features requiring connectivity are acceptable if manual offline alternatives exist**.
- [x] Bilingual support (English/French) is necessary for the Quebec market
- [x] Users engaging external help often intend a **Contractor** relationship, even if informal initially.
- [x] **Users will accept ~80-90% OCR accuracy with easy correction.** *(Added from Scope)*
- [x] **Users will grant context permissions (GPS/Calendar) if value is clear.** *(Added from Scope)*

## Risks *(Revised Section)*
- [ ] Risk 1: **Offline limitations of automation features (OCR, suggestions) may cause user confusion or frustration.**
  - Impact: Negative user experience if expectations aren't managed.
  - Mitigation: Clear UI indicators of online/offline status and feature availability; robust manual offline workflows; user education.
- [ ] Risk 2: Incorrect tax calculations (or **incorrect OCR capture of tax info**) could lead to compliance issues.
  - Impact: Legal/financial repercussions for users; loss of trust.
  - Mitigation: Consult with tax experts; rigorously test tax calculation & OCR functions; allow easy user correction of OCR data.
- [ ] Risk 3: Users may resist adoption if **automation feels unreliable (low OCR accuracy)** or intrusive (permissions).
  - Impact: Low user adoption and retention.
  - Mitigation: Focus on reliable OCR tech, provide easy correction tools, clearly explain value of permissions, offer manual fallbacks.
- [ ] Risk 4: Incorrect **automated** job suggestions or expense splitting could lead to inaccurate profitability.
  - Impact: User makes bad decisions based on wrong data; loss of trust.
  - Mitigation: Tune suggestion algorithms; make manual correction/override simple and obvious; allow easy review of allocations.
- [ ] Risk 5: Competition from established financial tools (potentially adding similar automation).
  - Impact: Difficulty gaining market share.
  - Mitigation: Focus on unique value proposition (job costing, QC GST/QST focus, simplicity, tailored automation).
- [ ] Risk 6: User confusion regarding legal classification of **Contractors** vs. Employees.
  - Impact: Potential misreliance on app terminology, legal risks for users.
  - Mitigation: Clear disclaimers, focus on tracking payments (UC-CP) and managing contacts (UC-CoM) not classification, encourage professional advice.
- [ ] Risk 7: Misinterpretation of Tax Guidance information provided via UC-TG.
  - Impact: User makes incorrect tax decisions based on perceived advice.
  - Mitigation: Clearly label guidance as informational links/summaries, not advice; include prominent disclaimers; link only to official government sources.
- [ ] **Risk 8:** **Increased MVP scope (due to automation) impacts timeline/budget.**
    - Impact: Delayed launch, requires more resources.
    - Mitigation: Re-evaluate priorities/timeline/budget; clear stakeholder communication.

## Budget Allocation
- [ ] Reserve a portion of the budget for marketing and onboarding post-MVP
  - **Marketing:** Landing page, targeted ads (e.g., Facebook for Quebec service businesses), **highlighting automation benefits**.
  - **Onboarding:** Bilingual help guides and tutorial videos aligned with key Use Cases, **explaining automated workflows and offline limitations**.
  - **Initial budget:** Approximately 15-20% of total project budget (may need review if MVP scope increases cost).

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
| **April 8, 2025** | **1.5** | **Gemini Model** | **Major Revision: Updated Use Cases (esp. UC-ME, UC-CP) and related sections (Personas, Journeys, Assumptions, Risks) to incorporate automation features (OCR, Smart Suggestions, Splitting) aligning with enhanced MVP Scope (v1.4/v0.4).** |


## Sign-off
- [ ] Technical Review
- [ ] Business Review
- [ ] Stakeholder Review
- [ ] Final Approval

## Next Steps **(Updated)**
- [x] Validate user personas through stakeholder interviews
- [x] Schedule user interviews with service business owners
- [x] **Re-evaluate technical feasibility of automated features (OCR, suggestions) and offline limitations.**
- [x] Define detailed **enhanced** MVP feature scope based on this analysis (Done - v1.4)
- [ ] Create prototype screens for key **automated** use cases
- [ ] **Begin decomposition of enhanced MVP Use Cases (UC-JP, UC-ME, UC-CoM, UC-CP, UC-TR, UC-IG, UC-CT, UC-WS, UC-TG, UC-CM, UC-JM, UC-AM) into detailed Functional Requirements with Acceptance Criteria.**