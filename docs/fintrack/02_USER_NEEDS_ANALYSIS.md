# User Needs Analysis - FinTrack

## Metadata
**Version:** 1.7 *(Added UC-EL: View and Manage Expense List)*.
**Status:** Draft.
**Last Updated:** April 9, 2025.
**Owner:** FinTrack Project Manager.
**Reviewers:** [To be determined].

## **Guiding Principles**

1.  ***Core Experience Priority:*** The primary user experience focuses on effortless core features (jobs, expenses, profitability), remaining simple and functional independently of conditional modules.
2.  ***Integrated Conditional Design:*** While core workflow is primary, design core components anticipating logical integration points for optional conditional features (like taxes) to ensure smooth user transitions and efficient development.

## Purpose
To identify and document the needs, goals, and pain points of small landscaping and related service business owners in Quebec, ensuring the FinTrack solution aligns with their **core** financial tracking requirements and operational context, while allowing for **optional, conditional tax features**. This version updates Use Cases to reflect an enhanced MVP scope focused on automation and ease of input, framed within the core/conditional structure, and formally defines the interaction with the expense list.

## Success Criteria
- [ ] Clear identification of primary user personas for small service businesses
- [x] Comprehensive use cases that reflect real-world financial tracking scenarios, **prioritizing core workflows and clearly marking conditional tax steps**, including viewing/managing expenses.
- [x] User journey maps highlighting key touchpoints and pain points in financial management, **focusing on core tasks and indicating where conditional tax features might apply**

## Content Requirements
### 1. User Personas *(Refined for Core vs. Conditional Needs)*
- **Persona Name:** Solo Operator
  - **Role:** Independent service business owner
  - **Core Goals:**
    - Track profitability of each job accurately **(core)**
    - **Minimize time spent on financial administration (via core automation)**
    - Create professional invoices quickly **(core)**
    - Keep business and personal finances separate **(core)**
    - Easily view and find past or **Draft Expenses (core)**.
  - **Conditional Goals (If Tax Features Enabled/Applicable):**
    - Maintain clear records for tax compliance (GST/QST)
  - **Core Pain Points:**
    - **Time lost manually entering/allocating field expenses (receipts, etc.)**
    - Manual financial record-keeping feels tedious and error-prone
    - Inability to determine which jobs are most profitable
    - Limited connectivity potentially hindering advanced automation features
    - Difficulty finding specific past expenses.
  - **Conditional Pain Points (If Tax Features Enabled/Applicable):**
    - Confusion about tax obligations and input tax credits
  - **Context:**
    - Works primarily in the field
    - Uses mobile device for most business tasks
    - Has limited financial/accounting knowledge
    - Operates seasonally with fluctuating income
    - Serves the Greater Montreal area with bilingual requirements

- **Persona Name:** Small Business Owner
  - **Role:** Owner of service business potentially engaging 2-10 employees or **Contractors**.
  - **Core Goals:**
    - Understand profitability across multiple concurrent jobs **(core)**
    - **Efficiently track expenses by job and category using automation (core)**
    - **Easily track and allocate payments to Contractors (core)**
    - Generate reports for business planning **(core reporting)**
    - Manage cash flow during seasonal fluctuations **(core)**
    - Quickly access and filter expense history **(core)**.
  - **Conditional Goals (Based on Business Status):**
    - Prepare accurate tax documentation
  - **Core Pain Points:**
    - Complexity of tracking multiple jobs simultaneously
    - Difficulty associating expenses with specific jobs **without significant manual effort**
    - Accurately tracking and **allocating** costs associated with employees vs. **Contractors**.
    - Limited visibility into overall business financial health and specific expense details.
  - **Conditional Pain Points (If Tax Features Enabled):**
    - Cumbersome process for GST/QST reporting
  - **Context:** (Same as Solo Operator)

- **Persona Name:** Prospective/Early-Stage Operator
  - **Role:** Individual planning to start or recently started a small service business
  - **Core Goals:**
    - Start with proper, **easy** financial organization from day one **(core)**
    - Look professional to clients **(core invoicing)**
    - Track profitability to make informed business decisions **(core)**
    - Set up a foundation for potential business growth (including potentially engaging **Contractors**) **(core)**
    - Understand how expenses are organized and tracked **(core)**.
  - **Conditional Goals (If considering registration):**
    * Understand basic tax obligations and thresholds (GST/QST) **with guidance**
  - **Core Pain Points:**
    - Uncertainty about which expenses are deductible **and how to track them easily (core expense tracking)**
    - Overwhelmed by complex accounting software; **needs extreme simplicity (core UI)**
    - Need to appear professional despite being new
    - Finding specific expense records later seems daunting.
  - **Conditional Pain Points (If considering registration):**
    - Confusion and anxiety about Quebec tax rules and thresholds
    - Lack of affordable guidance on business formalization
  - **Context:**
    - Works primarily through mobile device (no computer)
    - Limited or no prior business administration experience
    - May offer multiple service types (e.g., landscaping, snow removal, cleaning)
    - Looking to build recurring client base
    - Plans to operate mostly via cash and e-transfers initially

### 2. Use Cases *(Revised for Core Workflow + Conditional Tax Steps, Added UC-EL)*

- **Use Case Name (UC-JP):** Job Profitability Tracking
  - **Description:** Track all income and expenses (including **Contractor** payments) related to a specific service job to determine profitability. *(Leverages automated inputs from UC-ME/UC-CP for core efficiency and views data potentially summarized via UC-EL or reports).*
  - **Actors:** Business owner
  - **Core Steps:**
    1.  Create a new job in the system with client details and job specifications. (See UC-JM)
    2.  Record all income/payments for the job. (See UC-CT or related invoicing payment tracking via UC-IG)
    3.  Track all direct expenses (materials, fuel, etc.) and associate/allocate them with the job **via automated or manual core input**. (See UC-ME)
    4.  Track payments made to **Contractors** and associate/allocate them with the job. (See UC-CP)
    5.  Generate or view a core profitability report for the job that shows revenue, expenses (incl. **Contractor** payments), and net profit.
  - **Expected Core Outcome:** Clear understanding of each job's financial performance with accurate profit calculation, **achieved with reduced manual effort**.

- **Use Case Name (UC-ME):** Mobile Expense Tracking *(Revised for Core + Conditional Tax + Deferred Processing)*
  - **Description:** Quickly log business expenses (materials, fuel, etc.) while in the field using core automation features (OCR, suggestions) and associate them with specific jobs, allowing for easy splitting of shared costs. Supports **Deferred Processing** to save drafts for later completion. Optionally track tax details if the conditional tax module is enabled.
  - **Actors:** Business owner
  * **Trigger:** User selects "Add Expense" function OR selects a **Draft Expense** from the expense list (UC-EL) to resume processing.
  - **Core Steps (Primary Path):**
    1.  Open mobile app and select "Add Expense" function.
    2.  **Snap photo of receipt.**
    3.  **App performs OCR** to attempt extraction of Vendor, Date, Amount -> User quickly confirms or edits extracted data. *(Note: OCR may require connectivity).*
    4.  (Optional) User manually enters details if no receipt or OCR fails.
    5.  **App suggests potential Job(s)** based on context (GPS location, calendar, recent activity) -> User confirms suggestion or manually selects Job(s) from a list (list available offline). *(Note: Suggestions may require connectivity).*
    6.  **If expense applies to multiple jobs (or suggested), App prompts for allocation** -> User utilizes simple UI (sliders/percentages/amounts) to split the cost across selected jobs.
    7.  User confirms expense category (may be suggested based on vendor/OCR).
    8.  User confirms if expense is "General Business Expense" (not linked to specific jobs).
  - **Conditional Steps (If Tax Features Enabled):**
    9.  **App attempts OCR for GST/QST amounts** -> User confirms or manually enters tax details.
    10. System flags potential Input Tax Credits (ITCs) based on category and tax presence.
  - **Core Steps Continued:**
    11. Save the expense (basic data capture works offline, syncs when online; advanced features may require sync). Status becomes 'pending_sync' or 'synced'.
  - **Alternate Path: Deferred Processing**
    1. User initiates expense capture (e.g., photo) (Step 1-2 of Primary Path).
    2. User opts to defer completion after initial capture/OCR attempt (e.g., selects a "Save Draft" option).
    3. System saves available information (e.g., image link) as an expense record with "Draft" status.
    4. User exits the expense capture flow. *(User later selects this Draft Expense via UC-EL to resume)*.
  - **Expected Outcome:** Accurate expense records captured in real-time **with significantly reduced manual effort** via core automation; shared costs are easily allocated; **Draft Expenses** saved for later completion; basic capture works offline. **Optional tax details captured if relevant/enabled.**

- **Use Case Name (UC-CoM):** Contractor Management
  - **Description:** Add, view, search, and manage basic contractor information necessary for tracking payments. (Core Functionality)
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
  - **Description:** Record payments made to independent **Contractors**, leveraging smart suggestions and simple allocation tools to associate payments accurately with specific jobs. (Core Functionality)
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

- **Use Case Name (UC-TR):** GST/QST Reporting *(Conditional Use Case)*
  - **Description:** Generate a clear summary report for GST/QST filing preparation, leveraging automatically captured tax data where possible. **This use case is only relevant if the conditional tax features are enabled.**
  - **Actors:** Business owner, accountant
  - **Pre-condition:** Conditional Tax Features are enabled (e.g., based on "Tax Registration Status").
  - **Steps:**
    1.  Ensure sales (via invoices or direct income entry) and expenses are recorded with GST/QST details (potentially auto-captured via OCR in UC-ME). (See UC-IG, UC-ME)
    2.  Generate a tax report for a specific period (monthly, quarterly, annually).
    3.  View calculated summary totals for the period: Total Sales, Total GST/QST Collected, Total Input Tax Credits (ITCs) / GST/QST Paid on Expenses, Net Tax Payable/Refundable calculation.
    4.  Export the report as PDF or CSV for filing or sharing with accountant.
  - **Expected Outcome:** Accurate summary totals for key tax figures, simplifying tax preparation, **with reduced manual tax data entry, for users who require it**.

- **Use Case Name (UC-IG):** Invoice Generation *(Revised for Core + Conditional Tax)*
  - **Description:** Create and send professional invoices to clients. Optionally includes tax calculations if conditional tax features are enabled.
  - **Actors:** Business owner
  - **Core Steps:**
    1.  Select client and associated job(s). (See UC-CM, UC-JM)
    2.  Select an invoice template (if multiple basic options exist).
    3.  Review job details and enter line items/pricing.
  - **Conditional Steps (If Tax Features Enabled):**
    4.  System applies appropriate tax calculations (GST/QST) based on business registration status and client settings.
  - **Core Steps Continued:**
    5.  Generate invoice preview.
    6.  Send invoice via email or export as PDF.
    7.  Track invoice payment status (e.g., Draft, Sent, Paid, Overdue).
    8.  Record payments received against the invoice (including handling of partial payments).
  - **Expected Outcome:** Professional invoices delivered promptly (**with correct tax calculations if enabled**), and payment status (including partial payments) tracked accurately.

- **Use Case Name (UC-CT):** Cash Payment Tracking (Client)
  - **Description:** Track cash payments received from clients, especially for informal operators or immediate payments, with extreme simplicity. (Core Functionality)
  - **Actors:** Business owner
  - **Steps:**
    1.  Quickly record cash payment received (amount, date).
    2.  Optionally associate payment with client and/or a service/job (requires minimal detail entry). (See UC-CM, UC-JM)
    3.  Update daily/weekly cash income totals.
    4.  Review cash flow summary (or contribution to weekly summary).
  - **Expected Outcome:** Simple view of cash received with minimal data entry effort, supporting basic income tracking for informal operations.

- **Use Case Name (UC-WS):** Weekly Profit Summary View
  - **Description:** Provide a simple weekly overview of income versus expenses (including **Contractor** payments) for quick business health assessment. (Core Functionality)
  - **Actors:** Business owner
  - **Steps:**
    1.  Access weekly summary dashboard/view.
    2.  View total income recorded for the week across all clients/jobs.
    3.  View total expenses recorded by basic category (fuel, materials, **Contractor payments**, etc.).
    4.  See calculated weekly profit/loss figure.
    5.  Optionally compare to previous weeks.
  - **Expected Outcome:** Clear, at-a-glance understanding of weekly financial performance with minimal complexity.

- **Use Case Name (UC-DS):** Dashboard & Home Screen
  - **Description:** Provide a consolidated starting point showing key business information at a glance, including active jobs, draft expenses requiring attention, and recent financial activity. (Core Functionality)
  - **Actors:** Business owner
  - **Steps:**
    1.  User launches the application and authenticates.
    2.  System displays the dashboard as the default landing page.
    3.  User views Active Jobs section showing current/upcoming jobs with status indicators.
    4.  User views Draft Expenses section highlighting expenses needing completion.
    5.  User views Weekly Financial Summary section showing income vs expenses for current period.
    6.  User can tap on any job to navigate to its details (see UC-JM).
    7.  User can tap on any draft expense to resume processing it (see UC-ME, UC-EL).
    8.  User can tap "Add" buttons for quick access to create new jobs or expenses.
    9.  User can pull to refresh dashboard data when online.
  - **Expected Outcome:** Users gain immediate visibility into their current business state and quick access to the most common actions, reducing navigation time and improving awareness of items needing attention.

- **Use Case Name (UC-TG):** Tax Guidance Access *(Conditional Context)*
  - **Description:** Access basic information and links about Quebec tax obligations and thresholds. Primarily relevant for users considering registration or needing reminders **if tax features are enabled/relevant to their status.**
  - **Actors:** Business owner, prospective business owner
  - **Steps:**
    1.  Access tax information section within the app OR via contextual links (e.g., from expense categories, profitability views).
    2.  View informational summaries or links regarding GST/QST registration thresholds and requirements in Quebec.
    3.  Access informational summaries or links about common deductible expense types for the industry in Quebec.
    4.  **(Conditional Step - If Tax Features Enabled):** Receive system notifications when approaching tax thresholds based on tracked income.
    5.  Access links to official resources (Revenu Québec, CRA) for definitive information. *(Note: The app provides information/links, not financial advice).*
  - **Expected Outcome:** Increased awareness and reduced anxiety regarding tax obligations via curated information and links; facilitates transition to formal compliance **for relevant users**.

- **Use Case Name (UC-CM):** Client Management
  - **Description:** Add, view, search, and manage basic client information necessary for job tracking and invoicing. (Core Functionality)
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
  - **Description:** Create new jobs, associate them with clients, track basic job status, and view job history. Current MVP focuses on one-time jobs, with future support planned for recurring jobs (e.g., weekly lawn care) and on-demand/condition-triggered jobs (e.g., snow removal after snowfall). (Core Functionality)
  - **Actors:** Business owner
  - **Steps:**
    1.  Select option to view Job List.
    2.  View list of existing jobs with key details (e.g., Name/Description, Client, Status).
    3.  Select option to Add New Job (one-time job in MVP).
    4.  Enter job details (Name/Description, Location, Service Type - e.g., Landscaping, Snow Removal, Cleaning).
    5.  Associate the job with an existing Client (from client list - see UC-CM).
    6.  Set initial job Status (e.g., Planned, In-Progress).
    7.  Save new job information.
    8.  Select an existing job to view details or update status (e.g., mark as Complete).
    9.  Use search/filter function to find specific jobs (e.g., by client, by status).
  - **Expected Outcome:** Jobs are created and tracked, allowing expenses and income to be associated correctly for profitability analysis across various service types.
  - **Future Extensions (Post-MVP):**
    - Support for recurring jobs with fixed schedules (e.g., weekly lawn mowing)
    - Support for on-demand/condition-triggered jobs (e.g., snow removal after snowfall)
    - Integration with external job sources/platforms

- **Use Case Name (UC-AM):** Account Management
  - **Description:** Manage user login, profile information, and application settings like language preference. Includes setting the **"Tax Registration Status" which activates conditional tax features.** (Core Functionality + Conditional Trigger)
  - **Actors:** Business owner (User)
  - **Steps:**
    1.  User logs into the application using credentials (email/password).
    2.  Access Profile/Settings section.
    3.  View current business profile information.
    4.  Edit basic profile information (e.g., Business Name, Contact Info).
    5.  Select preferred language (English/French) for the application interface.
    6.  **Set/Update "Tax Registration Status" (e.g., Not Registered, Registered - with fields for numbers if applicable). This setting controls the visibility/activation of conditional tax features.**
    7.  Access option to change password or initiate password reset flow.
    8.  Log out of the application.
  - **Expected Outcome:** User can securely access their account, manage basic profile details, set language preference, **control the activation of conditional tax features via their registration status**, and maintain account security.

- **Use Case Name (UC-EL):** View and Manage Expense List *(New Use Case)*
  - **Description:** View, search, filter, and select expenses from the main expense list, including accessing **Draft Expenses** for completion. (Core Functionality)
  - **Actors:** Business owner, accountant (potential secondary reviewer)
  - **Trigger:** User navigates to the main expense list view (e.g., from dashboard, menu, or via navigation element in UC-ME).
  - **Steps:**
    1. System displays a list of expenses, potentially showing recent or **Draft Expenses** first.
    2. User applies filters if desired (e.g., by status: "Draft", "Completed"; by date range; by category; by job).
    3. User enters keywords into a search bar to find specific expenses (e.g., by vendor name, description).
    4. System updates the list based on applied filters and search terms.
    5. User scrolls through the filtered/searched list.
    6. User selects a specific expense from the list.
    7. If a completed expense is selected, system displays its details.
    8. If a **Draft Expense** is selected, system navigates the user to the appropriate step in the UC-ME workflow to resume processing (e.g., data verification).
  - **Expected Outcome:** User can efficiently find specific past expenses or pending **Draft Expenses**; user can get an overview of expenses based on filters; user can initiate the resumption of a **Draft Expense**.

### 3. User Journey Maps *(Refined for Core/Conditional)*

- **Journey Name:** New Job Financial Lifecycle *(Focus on Core, Tax Conditional)*
  - **Stages:**
    1.  Job creation and initial quoting **(core)**
    2.  Material purchasing and **automated core expense capture (UC-ME)**
    3.  Job execution (potentially involving **Contractors**) and additional core expense/cost tracking (**via UC-ME/UC-CP**)
    4.  Job completion, **easy Contractor payment allocation (UC-CP)**, and **core** client invoice generation
    5.  **(Conditional Step - If Tax Features Enabled):** Ensure invoice includes correct taxes.
    6.  Payment collection (client) and reconciliation **(core)**
    7.  Core Profitability analysis (including **Contractor** costs)
  - **Touchpoints:**
    - Mobile app for **automated core field expenses (OCR, suggestions)**
    - Desktop interface for core invoicing and reporting
    - Client communications for quotes and invoices
    - Banking integration for payment tracking (Future)
    - **Contractor** payment records (simplified entry/allocation)
    - Expense List interface (UC-EL) for reviewing job costs.
    - **(Conditional Touchpoint):** Tax settings/reports view.
  - **Core Pain Points:**
    - Disconnection between initial quote and actual expenses (incl. **Contractor** costs)
    - **Manual effort to log/allocate expenses reduced**
    - Manual effort to calculate true profitability
  - **Conditional Pain Points:**
    - Tax implications not considered in profitability analysis (if not enabled/used)
    - Complexity of tax calculations (if enabled)
  - **Opportunities:**
    - Streamline quote-to-invoice process **(core)**
    * **Leverage OCR/suggestions for near real-time core expense data**
    * **(Conditional Opportunity):** Automate tax calculations throughout job lifecycle (if enabled)
    * Provide real-time core profitability insights
    * **Simplify/automate receipt capture and digital storage (core)**
    * Simplify tracking/allocation of **Contractor** costs per job **(core)**

- **Journey Name:** Offline Expense Tracking *(Focus on Core)*
  - **Stages:**
    1.  Purchase materials/supplies at vendor
    2.  Log core expense offline in the field (**manual entry + photo capture saving as Draft Expense**; access to cached client/job data for basic tagging)
    3.  Tag expense to a specific job/client (manual selection from cached list)
    4.  Add receipt documentation (photo stored locally with draft)
    5.  Sync data when back online
    6.  **(Online Stage - Core):** OCR processing occurs for draft, smart suggestions may appear for refinement/confirmation when user resumes draft via UC-EL.
    7.  **(Online Stage - Conditional, if enabled):** OCR attempts tax details capture when draft is resumed.
    8.  Verify expense in financial reports (after completion)
  - **Touchpoints:**
    - Mobile app (**offline mode: manual entry + photo capture -> Draft Expense**)
    - Receipt capture functionality (offline storage)
    - Job/client selection interface (with offline data)
    - Sync notification system
    - Expense List interface (UC-EL) to find and resume draft.
    - **(Online Touchpoint - Core):** OCR results review (Vendor/Date/Amount), Smart suggestion review within UC-ME flow.
    - **(Online Touchpoint - Conditional):** OCR tax results review within UC-ME flow.
  - **Pain Points:**
    - Limited connectivity preventing real-time OCR/suggestions
    - Need for basic client/job info while offline
    - Risk of data loss if device is damaged before sync
    - Duplicate entries if sync fails (needs robust handling)
    - Forgetting to complete **Draft Expenses**.
  - **Opportunities:**
    - Enable offline access to essential client/job info for tagging **(core)**
    - Create quick-entry functionality saving as **Draft Expense (core)**
    - Implement reliable sync mechanism **(core)**
    * **Provide clear UI indicating which features require connectivity**
    * Make resuming **Draft Expenses** intuitive via UC-EL and potentially the initial screen preview.

- **Journey Name:** Tax Reporting Cycle *(Conditional Journey)*
  - **Stages:** *(This journey only applies if Tax Features are Enabled)*
    1.  Ongoing recording of sales with appropriate GST/QST
    2.  Tracking of expenses **with GST/QST data potentially auto-captured via OCR (UC-ME)**, identifying potential input tax credits
    3.  Periodic (monthly/quarterly) review of tax status
    4.  Tax period filing preparation (reviewing data potentially via UC-EL)
    5.  Report generation for accountant (leveraging captured data via UC-TR)
    6.  Actual filing with tax authorities
  - **Touchpoints:**
    - Expense entry with **auto-captured/verified** tax classification (UC-ME)
    - Invoice creation with tax calculations (UC-IG)
    - Expense List interface (UC-EL) for reviewing tax details on expenses.
    - Tax summary dashboard (showing key totals: Sales, GST/QST Collected, ITCs, Net Payable/Refundable)
    - Export functionality for reports (UC-TR)
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

- **Journey Name:** Informal-to-Formal Transition Journey *(Highlighting Activation)*
  - **Stages:**
    1.  Initial cash-based income tracking with minimal structure (**core** - via UC-CT)
    2.  Gradual addition of expense categories and basic profit tracking (**core - simplified by UC-ME automation and ability to save Draft Expenses**)
    3.  Exploration of tax rules and obligations (GST/QST thresholds via Tax Guidance - UC-TG)
    4.  Decision to formalize business operations -> **Activate Tax Features via "Tax Registration Status" setting.** (UC-AM)
    5.  Implementation of invoicing and formal payment tracking (clients and potentially **Contractors**) (**core functionality enhanced by now-active conditional tax calculations**)
    6.  First tax filing as a registered business (using UC-TR, leveraging captured data potentially reviewed via UC-EL)
  - **Touchpoints:**
    - Simple weekly profit dashboard (**core** - UC-WS)
    - Tax information resources (UC-TG)
    - Invoice/quote creation tools (**core** - UC-IG)
    - Client management transition (**core** - UC-CM)
    - **Contractor** management and **simplified** payment tracking (**core** - UC-CoM, UC-CP)
    - First GST/QST reporting (**conditional** - UC-TR - data capture streamlined)
    - Expense List interface (UC-EL) for managing records.
    - **Account setting for Tax Registration Status (Activation Trigger via UC-AM)**
  - **Pain Points:**
    - Anxiety around tax compliance and registration
    - Uncertainty about when/how to register for GST/QST
    - Need for historical data during formalization (accessible via UC-EL)
    - Added complexity of formal financial tracking **(reduced by core automation, tax features only appear when activated)**
    - Potential client relationship changes (receipt issuance, tax charging)
    - Potential need to formalize agreements with **Contractors**.
  - **Opportunities:**
    - Provide clear guidance links/info on formalization process via UC-TG
    - Offer simplified tax information resources
    - Create smooth transition between operating models via activation trigger
    - **Core automation features lower barrier to adopting formal tracking**
    - Support tracking for formalizing **Contractor** relationships (future)

- **Journey Name:** Seasonal Transition Journey
  - **Stages:**
    1.  End-of-season financial review for landscaping (using reports, potentially UC-EL)
    2.  Preparation for winter operations (snow removal)
    3.  Adaptation to different billing models (per-visit vs monthly/per-storm)
    4.  Equipment and material expense tracking changes (via UC-ME)
    5.  Managing different client expectations and service models
    6.  End-of-winter financial analysis and landscaping preparation
  - **Touchpoints:**
    - Service type switch in the application (part of UC-JM)
    - Contract management for recurring clients (Future Feature)
    - Seasonal profit comparison views (Reporting Feature)
    - Equipment and material inventory changes (Expense Tracking - UC-ME)
    - Storm event tracking (snow operations) (Future Feature)
    - Expense List interface (UC-EL) for filtering by season/service type.
  - **Pain Points:**
    - Different profitability metrics between service types
    - Transitioning clients between service models
    - Managing cash flow during seasonal changes
    - Adapting to reactive vs scheduled service delivery
    - Tracking different expense categories by season
  - **Opportunities:**
    - Provide unified financial view across service types
    - Support different billing/contract models by season (Future)
    - Enable service-specific reporting and analysis (via filtering in UC-EL/reports)
    - Simplify year-round financial planning

### 4. Validation Methods
- [ ] User interviews via video calls or phone calls with 5-7 service business owners in the Greater Montreal area
  - Mix of English, French, and bilingual participants
  - Focus on solo operators and small businesses (engaging 1-10 employees/**Contractors**)
  - Key Interview Topics: *(Add validation for conditional approach & UC-EL)*
    1.  Current Software Usage: [...]
    2.  Price Sensitivity: [...]
    3.  Seasonal Operations: [...]
    4.  **Reaction to Automation:** Gauge interest/acceptance of OCR, smart suggestions, potential GPS use, permissions **for core tasks**.
    5.  **Offline Needs:** Clarify expectations for offline availability of automated features **vs. core manual tasks**.
    6.  **Conditional Tax Needs:** Understand when/if users need tax features and validate the proposed activation trigger approach.
    7.  **Expense List Interaction:** Understand how users currently find/review past expenses and validate the proposed features for UC-EL (search, filter by status/date etc.).
- [ ] Surveys distributed to broader service business community in Quebec
- [ ] Observational studies of current financial management processes (if feasible)
- [ ] Usability testing of prototypes **incorporating core automated workflows (OCR, suggestions, splitting), testing the conditional activation of tax features, and testing the interactions defined in UC-EL (including resuming Draft Expenses).**

### 5. Assumptions *(Revised for Core/Conditional & UC-EL)*
- [x] Target users are comfortable using smartphones for basic business tasks **and granting typical app permissions (camera, potentially location/calendar for core features)**
- [x] Most target users have limited formal accounting knowledge
- [x] GST/QST tracking is a significant pain point for Quebec-based businesses **that are registered or need to be**.
- [x] Users prioritize **simplicity, speed, and effortless input for core tasks** over comprehensive accounting features
- [x] **Manual offline** functionality for core tasks (like saving **Draft Expenses**) is essential; **advanced automation features requiring connectivity are acceptable if core manual offline alternatives exist**.
- [x] Bilingual support (English/French) is necessary for the Quebec market
- [x] Users engaging external help often intend a **Contractor** relationship, even if informal initially.
- [x] **Users will accept ~80-90% OCR accuracy with easy correction.**
- [x] **Users will grant context permissions (GPS/Calendar) if value is clear for core suggestions.**
- [x] Users will understand and accept the concept of enabling conditional tax features based on their registration status.
- [x] Users need and will utilize search and filter capabilities (including filtering by 'Draft' status) within the main expense list (UC-EL).

### 6. Risks *(Revised for Core/Conditional & UC-EL)*
- [ ] Risk 1: **Offline limitations of automation features (OCR, suggestions) may cause user confusion or frustration.**
  - Impact: Negative user experience if expectations aren't managed.
  - Mitigation: Clear UI indicators of online/offline status and feature availability; robust manual offline core workflows (saving Drafts); user education.
- [ ] Risk 2: Incorrect tax calculations (or **incorrect OCR capture of tax info**) **within the conditional module** could lead to compliance issues **for users who enable it**.
  - Impact: Legal/financial repercussions for users; loss of trust.
  - Mitigation: Consult with tax experts; rigorously test tax calculation & OCR functions; allow easy user correction of OCR data; clear disclaimers.
- [ ] Risk 3: Users may resist adoption if **core automation feels unreliable (low OCR accuracy)** or intrusive (permissions).
  - Impact: Low user adoption and retention.
  - Mitigation: Focus on reliable OCR tech for core data, provide easy correction tools, clearly explain value of permissions, offer manual fallbacks.
- [ ] Risk 4: Incorrect **automated** job suggestions or expense splitting **(core features)** could lead to inaccurate profitability.
  - Impact: User makes bad decisions based on wrong data; loss of trust.
  - Mitigation: Tune suggestion algorithms; make manual correction/override simple and obvious; allow easy review of allocations.
- [ ] Risk 5: Competition from established financial tools (potentially adding similar automation or tax features).
  - Impact: Difficulty gaining market share.
  - Mitigation: Focus on unique value proposition (job costing, QC focus, simplicity, tailored core automation, seamless conditional tax integration).
- [ ] Risk 6: User confusion regarding legal classification of **Contractors** vs. Employees.
  - Impact: Potential misreliance on app terminology, legal risks for users.
  - Mitigation: Clear disclaimers, focus on tracking payments (UC-CP) and managing contacts (UC-CoM) not classification, encourage professional advice.
- [ ] Risk 7: Misinterpretation of Tax Guidance information provided via UC-TG **(conditional context)**.
  - Impact: User makes incorrect tax decisions based on perceived advice.
  - Mitigation: Clearly label guidance as informational links/summaries, not advice; include prominent disclaimers; link only to official government sources.
- [ ] **Risk 8:** **Increased Core MVP scope (due to automation) impacts timeline/budget, potentially delaying conditional module availability.**
    - Impact: Delayed launch of full feature set, requires more resources for core.
    - Mitigation: Re-evaluate priorities/timeline/budget for core-first; clear stakeholder communication about phased rollout.
- [ ] **Risk 9:** The expense list (UC-EL) interface becomes cluttered or difficult to navigate if filtering/search options are not well-designed, especially on mobile.
    - Impact: Users struggle to find specific or Draft expenses, negating efficiency gains.
    - Mitigation: Prioritize intuitive filter/search design for mobile; conduct usability testing specifically on UC-EL.

### 7. Budget Allocation
- [ ] Reserve a portion of the budget for marketing and onboarding post-MVP
  - **Marketing:** Landing page, targeted ads (e.g., Facebook for Quebec service businesses), **highlighting core automation benefits**.
  - **Onboarding:** Bilingual help guides and tutorial videos aligned with key **Core** Use Cases (including UC-ME with **Deferred Processing**) and **UC-EL**, **explaining automated workflows, offline limitations, and how/when to activate conditional tax features**.
  - **Initial budget:** Approximately 15-20% of total project budget (may need review if core MVP scope increases cost significantly).

### 8. Review Notes
- [ ] Review 1
  - Reviewer:
  - Date:
  - Comments:
  - Status:

### 9. Change Log
| Date          | Version | Changed By   | Changes Made                                                                                                                                                                                                                                |
| :------------ | :------ | :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| April 4, 2025 | 1.0     | FinTrack PM  | Created initial User Needs Analysis                                                                                                        |
| April 8, 2025 | 1.1     | FinTrack PM  | Standardized terminology: Replaced "helper," "crew member" with "**Contractor**". Adjusted relevant sections. Added UC for Contractor Payments. |
| April 8, 2025 | 1.2     | Gemini Model | Added suggested Use Cases: UC-CM (Client Management), UC-JM (Job Management), UC-AM (Account Management) based on scope analysis. Renamed UC-TG. Minor adjustments for consistency. |
| April 8, 2025 | 1.3     | Gemini Model | Added **UC-CoM (Contractor Management)** based on dependency analysis. Updated UC-CP step 1 to reference UC-CoM. Updated Next Steps. |
| April 8, 2025 | 1.4     | Gemini Model | Refined steps in UC-ME, UC-CP, UC-TR, UC-IG, UC-CT, UC-TG, UC-JM based on detailed analysis for clarity and alignment with MVP features/interview feedback. Updated version number. Added Risk related to Tax Guidance interpretation. |
| April 8, 2025 | 1.5     | Gemini Model | **Major Revision:** Updated Use Cases (esp. UC-ME, UC-CP) and related sections (Personas, Journeys, Assumptions, Risks) to incorporate automation features (OCR, Smart Suggestions, Splitting) aligning with enhanced MVP Scope (v1.4/v0.4). |
| April 9, 2025 | 1.6     | Gemini Model | **Refactored based on core vs. conditional prioritization instructions:** Added Guiding Principles; Refined Use Cases (UC-JP, UC-ME, UC-TR, UC-IG, UC-TG, UC-AM) for core flow + conditional steps/context; Applied conditional language and emphasis in Personas, Journeys, Assumptions, Risks. |
| **April 9, 2025** | **1.7** | **Gemini Model** | **Added UC-EL: View and Manage Expense List.** Updated UC-ME triggers and descriptions to reflect Draft Expenses and Deferred Processing. Ensured terminology consistency ("Draft Expense", "Deferred Processing"). Updated related sections (Personas, Journeys, Risks, Validation Methods, Assumptions) to reflect the existence and purpose of UC-EL. Updated version number. |


### 10. Sign-off
- [ ] Technical Review
- [ ] Business Review
- [ ] Stakeholder Review
- [ ] Final Approval

### 11. Next Steps **(Updated)**
- [x] Validate user personas through stakeholder interviews
- [x] Schedule user interviews with service business owners **(incl. questions on conditional tax needs & UC-EL interactions)**
- [x] **Re-evaluate technical feasibility of core automated features (OCR, suggestions) and offline limitations.**
- [x] Define detailed **enhanced Core MVP** feature scope based on this analysis (Reflected in related docs)
- [ ] Create prototype screens for key **core automated** use cases (UC-ME), **the expense list (UC-EL)**, and the conditional activation flow (UC-AM).
- [ ] **Begin decomposition of enhanced Core MVP Use Cases (including UC-EL) into detailed Functional Requirements with Acceptance Criteria.**
- [ ] **Plan detailed requirements for Conditional Tax Module for later phase.**