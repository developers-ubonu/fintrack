# Use Case: Job Profitability Tracking

**(MVP Version 1.1 - Aligned with Enhanced MVP Scope v1.4/v0.4 & User Needs v1.5)**

## Refined Description

### Overview
Track all income and expenses (including Contractor payments) related to a specific service job to determine profitability, leveraging **automated input features (OCR, suggestions)** for efficiency. This enables business owners to understand which jobs are most profitable with **minimal manual effort** and improve pricing decisions.

**(Non-Functional Requirement Note:** All profitability calculations presented to the user, particularly summary figures and list view indicators (REQ-JP-04), must be displayed quickly and efficiently, even with data linked via automated processes. The system should feel responsive, potentially utilizing strategies like background processing or pre-computation where appropriate to meet performance expectations on mobile devices.)

**(Calculation Basis Note:** For MVP simplicity and alignment with common user cash flows, profitability is calculated on a cash/received basis.)

### Actors
- Primary: Business Owner
- Secondary: None

### Trigger(s)
- Business owner wants to check profitability of a specific job
- Business owner records a new expense or income for a job (**potentially via automated capture**)
- Business owner records and allocates a payment to a contractor for a job (**potentially with smart suggestions/splitting**)
- Business owner generates financial reports for business analysis

### Pre-conditions
- User has an active FinTrack account
- One or more jobs exist in the system
- Client details are available (via UC-CM)
- Any job-related expenses are recorded (**via automated or manual input** - UC-ME v1.5)
- Any contractor payments are tracked and allocated (**via automated suggestions or manual input** - UC-CP v1.5)
- Any job-related income/payments are recorded (via UC-CT or UC-IG)

### Expected Outcome
Business owner gains a clear understanding of each job's financial performance with accurate profit calculation (based on recorded transactions and MVP calculation basis), achieved **with significantly reduced manual effort** due to automation features, enabling better business decisions related to pricing, service offerings, and contractor engagement.

### Primary Path
1. Business owner navigates to the job list view in the application
2. Business owner selects a specific job to view its details
3. The system displays job information including the client, service type, status, and dates
4. The system calculates and displays a **concise financial summary** for the job, focused on quick assessment, showing:
   - Total revenue (based on payments received)
   - Total Costs (Expenses + Contractor Payments - **data potentially captured/allocated via automation**)
   - Net profit calculation (Revenue - Total Costs)
   - Profit margin percentage (or 'N/A')
   - **Breakdown by key cost categories (e.g., Materials, Contractors)**
5. Business owner can view a **detailed list of individual financial transactions** (revenue received, expenses, contractor payments) associated with the job, showing date, description/category, and amount for each transaction. *(Data entry potentially streamlined via automation).*
6. Business owner can generate a basic profitability report for the job.
7. Business owner can return to the job list view, which displays profitability indicators for all jobs.

### Alternate Paths

#### A1: Profitability Tracking Without Contractor Payments
1. Follow steps 1-3 of the primary path.
2. The system calculates and displays a simplified financial summary showing:
   - Total revenue (Received)
   - Total Costs (Expenses only - **data potentially captured/allocated via automation**)
   - Net profit calculation (Revenue - Expenses)
   - Profit margin percentage (or 'N/A')
3. Continue with steps 5-7 of the primary path.

#### A2: Profitability Recalculation After Job Completion / Adjustment
1. Business owner navigates to a completed job in the job list.
2. Business owner adds a newly discovered expense **OR adjusts an existing expense/payment allocation** related to the job (via REQ-JP-11).
3. System prompts to associate/confirm the change with the completed job.
4. System recalculates the job profitability with the updated cost information.
5. System updates the profitability report and financial summary.

#### A4: Accessing Profitability Data When Offline *(Revised)*
1. Business owner attempts to access job details while device is offline.
2. System displays **cached, potentially read-only** job information including basic profitability summary based on *last synced data*.
3. System clearly indicates offline status and that **advanced features (like real-time suggestions/OCR for new entries) are unavailable**.
4. System shows last-updated timestamp for the cached data.
5. System synchronizes and updates calculations when connectivity is restored.

### Exception Paths

#### E1: Missing Expense Data
1. Business owner views a job's profitability report.
2. System detects potential gaps (e.g., low costs for job type - future enhancement) or user identifies missing expenses.
3. System provides an **easy path to add missing expenses** (leveraging UC-ME automation where possible).
4. After adding missing expenses, the system recalculates profitability.

#### E2: Incorrect Expense/Payment Association *(Revised Focus)*
1. Business owner reviews job details or profitability report.
2. Business owner identifies an expense or contractor payment incorrectly associated or allocated to the job (despite smart suggestions).
3. System provides an easy way to **adjust or re-allocate** the cost item (see REQ-JP-11).
4. System recalculates profitability after correction.

#### E3: System Offline When Report Needed
1. Business owner attempts to generate a detailed profitability report while offline.
2. System notifies that detailed reporting (requiring full, up-to-date data) is **unavailable offline**. (Cached summary view may still be available per A4).

#### E4: Partial Client Payments
1. Business owner records a partial payment for a job invoice.
2. System calculates profitability based on the **default MVP cash/received basis**, reflecting actual payments received.
3. System clearly indicates the calculation basis (e.g., "Based on payments received") in the profitability report/summary.

#### E5: Tax Calculation Impact on Profitability
1. Business owner views profitability for a job that includes GST/QST (tax data potentially captured via OCR).
2. System detects that tax calculations affect the profitability view.
3. System displays profitability calculations **based on the default pre-tax view** and shows relevant tax figures (GST/QST collected/paid) separately for informational purposes.

## Functional Requirements *(Revised REQ-JP-01, 05, 07, 09; Added REQ-JP-11)*

### REQ-JP-01: Job Financial Summary Display *(Revised)*

**Title:** Job Financial Summary Display

**Description:** The system must calculate and display a **concise and informative** financial summary for each job, showing key profitability metrics based on recorded transactions (potentially captured/allocated via automation). The summary should highlight major cost components for quick assessment.

**Actors:** Business Owner

**Trigger:** Business owner views a job's details

**Pre-conditions:**
- Job exists in the system
- Related financial transactions (if any) have been recorded (via UC-ME v1.5, UC-CP v1.5, UC-CT, UC-IG)

**Functional Steps (Happy Path):**
1. Retrieve all applicable revenue entries associated with the job.
2. Retrieve all expense entries associated with the job.
3. Retrieve all contractor payment records associated with the job.
4. Calculate total revenue sum (**based on payments received**).
5. Calculate total expense sum (by category).
6. Calculate total contractor payment sum.
7. Calculate **Total Costs** (Total Expenses + Total Contractor Payments).
8. Calculate net profit (Total Revenue - Total Costs).
9. Calculate profit margin percentage (Net Profit / Total Revenue × 100%). If Total Revenue is zero, margin is 'N/A'.
10. Display the core financial summary prominently, **including breakdown by major cost categories (e.g., Materials, Contractors, Other Expenses)**.

**Inputs:**
- Job ID

**Outputs / Expected Results (Core Summary Block):**
- Total revenue amount (formatted currency, indicating basis: '**Received**')
- Total Costs amount (formatted currency)
- **Breakdown of Total Costs by major categories** (e.g., Materials: $X, Contractors: $Y, Other: $Z)
- Net profit amount (formatted currency)
- Profit margin percentage (**or 'N/A' if revenue is zero**)
- Visual indicator of profitability status (e.g., color coding)
- Separate display area for relevant tax totals (GST/QST collected/paid) if applicable.

**Error Handling / Alternate Flows:**
- If no financial data exists: Display zeros with a message indicating no financial data has been recorded
- If job is in progress: Display an indicator that profitability is **preliminary** (calculations reflect data recorded to date and will change).
- If revenue is zero: Display profit margin as 'N/A'.

**Acceptance Criteria:**
- Given a job with recorded payments of $1,000, expenses (Materials $300, Fuel $50), and contractor payments of $400,
  When the business owner views the job details,
  Then the system displays revenue as $1,000 (Received), Total Costs as $750 (broken down by category), net profit as $250, and profit margin as 25% in the main summary block.

- Given a job with recorded payments of $500 and expenses of $600 (no contractor payments),
  When the business owner views the job details,
  Then the system displays a negative profit of -$100 and provides a visual indicator showing the job is unprofitable.

- Given a job with no financial transactions,
  When the business owner views the job details,
  Then the system displays zeros for all financial fields and shows a message indicating no financial data has been recorded.

**Dependencies:**
- REQ-JP-02 (Financial Transaction Retrieval)

### REQ-JP-02: Financial Transaction Retrieval *(Revised)*

**Title:** Financial Transaction Retrieval for Job Profitability

**Description:** The system must retrieve all financial transactions (income, expenses, contractor payments) associated with a specific job, including any relevant metadata (e.g., capture method, allocation details), to enable accurate profitability calculation and display.

**Actors:** System

**Trigger:**
- Job profitability calculation is requested
- Job details page is viewed
- Profitability report is generated

**Pre-conditions:**
- Job exists in the system

**Functional Steps (Happy Path):**
1. Query the database for all income/payment records linked to the job ID.
2. Query the database for all expense records linked to the job ID, including category and allocation details if split.
3. Query the database for all contractor payment records linked to the job ID, including allocation details if split.
4. Organize transactions by type (income, expense, contractor payment).
5. Return the complete transaction dataset including relevant metadata for profitability calculation and display.

**Inputs:**
- Job ID

**Outputs / Expected Results:**
- Comprehensive list of all financial transactions associated with the job, including:
  - Transaction amounts, dates, types, payment methods
  - Categories (for expenses)
  - **Allocation details (if split across jobs)**
  - Tax information (if applicable)
  - **Metadata (e.g., capture method 'OCR'/'Manual' - optional)**

**Error Handling / Alternate Flows:**
- If job ID doesn't exist: Return appropriate error without crashing
- If database connection fails: Display error message and retry option
- If partial data retrieved: Flag incomplete data status in results

**Acceptance Criteria:**
- Given a job with 3 income entries, 5 expense entries (1 split across this and another job), and 2 contractor payment entries (1 split),
  When the system retrieves financial transactions for the job,
  Then all relevant entries *and their specific allocation amounts for this job* are successfully retrieved and categorized.

- Given a job with no financial entries,
  When the system retrieves financial transactions for the job,
  Then an empty result set is returned without errors.

- Given a temporary connectivity issue,
  When the system attempts to retrieve financial transactions for a job,
  Then the system handles the error gracefully and provides retry functionality.

**Dependencies:**
- None

### REQ-JP-03: Job Profitability Report Generation *(Revised)*

**Title:** Job Profitability Report Generation

**Description:** The system must generate a **basic** profitability report for a specific job, showing the core financial components (potentially sourced via automation) and itemized transaction lists, including allocation details.

**Actors:** Business Owner

**Trigger:** Business owner requests a profitability report for a specific job

**Pre-conditions:**
- Job exists in the system
- User has appropriate permissions

**Functional Steps (Happy Path):**
1. User selects option to generate profitability report for a job
2. System retrieves comprehensive financial data for the job (via REQ-JP-02)
3. System organizes data into report sections:
   - Job overview (client, dates, service type)
   - Revenue breakdown (Received basis, itemized)
   - Expense breakdown (by category, itemized, **showing allocated amounts**)
   - Contractor payment details (itemized, **showing allocated amounts**)
   - Profit calculation (clearly stating calculation basis: cash/received)
4. System formats the report for clean viewing
5. System provides basic export options (PDF, CSV)

**Inputs:**
- Job ID

**Outputs / Expected Results:**
- Formatted profitability report containing:
  - Job identification and basic details
  - Itemized Revenue breakdown (Received basis)
  - Itemized expense list with categorization (**reflecting allocations**)
  - Detailed contractor payment information (**reflecting allocations**)
  - Clear profit calculation (indicating calculation basis)
  - Key metrics (profit margin or 'N/A')

**Error Handling / Alternate Flows:**
- If offline: Notify user that reporting is unavailable offline
- If insufficient data: Generate report with available data and clearly mark missing components
- If export fails: Provide retry option and alternative export formats

**Acceptance Criteria:**
- Given a completed job with full financial records, including split expenses/payments,
  When the business owner requests a profitability report,
  Then a basic report is generated showing accurate allocated amounts for expenses and contractor payments contributing to the net profit calculation.

- Given a job with partial financial records,
  When the business owner requests a profitability report,
  Then a report is generated with available data, clearly indicating which components are incomplete.

- Given a request to export the profitability report as PDF,
  When the business owner selects the PDF export option,
  Then the system generates a well-formatted PDF containing the basic report information.

**Dependencies:**
- REQ-JP-02 (Financial Transaction Retrieval)
- REQ-JP-01 (Job Financial Summary Display)

### REQ-JP-04: Job List Profitability Indicators

**Title:** Job List Profitability Indicators

**Description:** The system must display profitability indicators for all jobs in the job list view to provide at-a-glance financial performance visibility, loading efficiently.

**Actors:** Business Owner

**Trigger:** Business owner views the job list

**Pre-conditions:**
- User has at least one job in the system

**Functional Steps (Happy Path):**
1. System loads the job list view.
2. For each job, system retrieves or calculates basic profitability metrics (strategy TBD - e.g., precomputed or efficient on-demand query).
3. System displays appropriate visual indicators based on defined profitability status logic.
4. System shows profit amount or percentage based on user preference setting (defaulting to amount for quick insight).

**Inputs:**
- None (view initialization)

**Outputs / Expected Results:**
- List of jobs with visual profitability indicators
- Profit amount or percentage displayed for each job (configurable, default amount)
- Sort/filter options based on profitability

**Indicator Status Logic:**
* `Profitable:` Net Profit > 0
* `Unprofitable:` Net Profit < 0
* `Break-even:` Net Profit = 0
* `Information Needed:` Job status is 'Completed' AND (Total Revenue = 0 OR Total Costs = 0)
* `Preliminary:` Job Status is 'In Progress' or 'Planned' (calculations reflect data to date)

**Error Handling / Alternate Flows:**
- If profitability cannot be calculated due to errors: Display an error/unknown indicator.
- If job status determines indicator (e.g., 'Preliminary'), use that logic.

**Acceptance Criteria:**
- Given a list containing jobs with positive, negative, and zero net profit,
  When the business owner views the job list,
  Then each job displays an appropriate visual indicator (Profitable, Unprofitable, Break-even) based on the defined logic.

- Given a completed job with revenue recorded but no expenses or contractor payments,
  When the business owner views the job list,
  Then that job displays an 'Information Needed' indicator.

- Given the business owner uses the default setting,
  When the business owner views the job list,
  Then profitability is displayed as absolute amounts (e.g., +$300, -$100).

**Dependencies:**
- REQ-JP-01 (Job Financial Summary Display) - for underlying calculation logic

### REQ-JP-05: Job Expense Association *(Major Revision)*

**Title:** Job Expense Association (Automated & Manual)

**Description:** The system must enable business owners to associate expenses with specific jobs efficiently, leveraging automation (OCR, smart suggestions) and providing intuitive tools for splitting costs. It must also allow for later adjustments.

**Actors:** Business Owner

**Trigger:**
- Business owner enters a new expense (via UC-ME v1.5)
- Business owner updates an existing expense
- Business owner reviews unassociated expenses
- Business owner adjusts allocation via job detail view (REQ-JP-11)

**Pre-conditions:**
- User has an active account
- At least one job exists in the system
- Expense data is being entered or reviewed

**Functional Steps (Ideal Workflow via UC-ME v1.5):**
1. User initiates expense entry (e.g., via photo).
2. App attempts OCR -> User confirms/edits extracted data (Vendor, Date, Amount, Tax). *(Connectivity may be required).*
3. App suggests potential Job(s) based on context -> User confirms suggestion, selects manually, or marks as "General Business Expense". *(Connectivity may be required for suggestions).*
4. If multiple jobs selected or context suggests splitting, App presents simple splitting UI -> User allocates cost.
5. User confirms expense category (may be suggested).
6. System creates association(s) between expense and selected job(s) with allocated amounts.
7. System updates job profitability calculations.
*(Manual entry follows similar association/splitting steps without OCR/suggestions).*

**Inputs:**
- Expense details (via OCR or manual entry)
- User confirmation/selection of Job(s) or "General Expense"
- Allocation details (if split)

**Outputs / Expected Results:**
- Expense record with job association(s) and allocated amounts.
- Updated job profitability calculation(s).
- Confirmation of successful association/allocation.

**Error Handling / Alternate Flows:**
- **Offline:** OCR and Smart Suggestions may be unavailable. User performs manual entry, photo capture, and selects job from *cached list* or marks as general/unassociated. Sync occurs later.
- If incorrect association/allocation made: User can adjust later (see REQ-JP-11).
- Allow explicitly marking as **non-job specific** easily. Non-job specific expenses are excluded from individual job profitability calculations.

**Acceptance Criteria:**
- Given a new expense entry via receipt photo (online),
  When the app successfully performs OCR and suggests the correct job based on GPS context,
  Then the user can confirm the association with minimal interaction (e.g., 1-2 taps).

- Given a fuel expense entered manually (offline),
  When the user needs to split it 50/50 between two jobs selected from the cached list,
  Then the splitting UI is intuitive and the allocation is saved correctly for later syncing.

- Given an expense initially marked as "General",
  When the business owner later identifies the correct job,
  Then they can easily associate the expense via REQ-JP-11.

**Dependencies:**
- UC-ME (Mobile Expense Tracking v1.5)
- REQ-JP-01 (Job Financial Summary Display)
- REQ-JP-11 (Expense/Payment Allocation Adjustment)

### REQ-JP-06: Revenue-Job Association

**Title:** Revenue-Job Association

**Description:** The system must enable associating revenue entries (payments, invoices) with specific jobs to ensure accurate profitability calculation.

**Actors:** Business Owner

**Trigger:**
- Business owner creates an invoice
- Business owner records a payment
- Business owner reviews unassociated revenue

**Pre-conditions:**
- User has an active account
- At least one job exists in the system
- At least one client exists in the system

**Functional Steps (Happy Path):**
1. When creating an invoice or recording a payment, system provides option to associate with a job.
2. System displays list of jobs for selection (with search/filter capability).
3. Business owner selects the appropriate job.
4. System creates association between revenue entry and selected job.
5. System updates job profitability calculations to include the new revenue (based on MVP cash/received basis for payments).

**Inputs:**
- Revenue details (amount, date, type, etc.)
- Selected job ID

**Outputs / Expected Results:**
- Revenue record with job association
- Updated job profitability calculation
- Confirmation of successful association

**(Note:** For MVP, associating a single revenue entry (like one payment received) to multiple jobs is not directly supported. If a payment covers multiple jobs, the user should record separate revenue entries associated with each respective job.)

**Error Handling / Alternate Flows:**
- If job list cannot be retrieved (offline): Allow basic revenue entry without job association, flag for later association
- If revenue is associated with wrong job: Provide ability to reassign to correct job (potentially via REQ-JP-11 concept applied to revenue)

**Acceptance Criteria:**
- Given a new invoice creation,
  When the business owner associates it with a specific job,
  Then the invoice is linked to that job.

- Given a payment receipt,
  When the business owner records it and associates with a job,
  Then the payment is linked to that job and profitability is updated accordingly (based on cash/received basis).

- Given an invoice associated with a job,
  When partial payment is received,
  Then the system accurately reflects the partial revenue in the job's profitability calculation (based on cash/received basis).

**Dependencies:**
- UC-IG (Invoice Generation)
- UC-CT (Cash Payment Tracking)
- REQ-JP-01 (Job Financial Summary Display)

### REQ-JP-07: Contractor Payment-Job Association *(Major Revision)*

**Title:** Contractor Payment-Job Association (Automated & Manual)

**Description:** The system must enable business owners to associate contractor payments with specific jobs efficiently, leveraging smart suggestions and providing intuitive tools for splitting costs. It must also allow for later adjustments.

**Actors:** Business Owner

**Trigger:**
- Business owner records a contractor payment (via UC-CP v1.5)
- Business owner adjusts allocation via job detail view (REQ-JP-11)

**Pre-conditions:**
- User has an active account
- At least one job exists in the system
- At least one contractor exists (UC-CoM)
- Payment details are being entered or reviewed

**Functional Steps (Ideal Workflow via UC-CP v1.5):**
1. User initiates payment recording, selects contractor, enters amount/date/method.
2. App suggests potential Job(s) the contractor worked on based on context -> User confirms suggestion, selects manually, or marks as "General Business Expense". *(Connectivity may be required for suggestions).*
3. If multiple jobs selected or context suggests splitting, App presents simple splitting UI -> User allocates payment amount across jobs.
4. System validates allocation sum matches total payment.
5. System creates association(s) between payment and selected job(s) with allocated amounts.
6. System updates job profitability calculations.

**Inputs:**
- Contractor payment details
- User confirmation/selection of Job(s) or "General Expense"
- Allocation details (if split)

**Outputs / Expected Results:**
- Contractor payment record with job association(s) and allocated amounts.
- Updated job profitability calculation(s).
- Confirmation of successful association/allocation.

**Error Handling / Alternate Flows:**
- **Offline:** Smart Suggestions may be unavailable. User performs manual entry and selects job(s) from *cached list* or marks as general/unassociated. Sync occurs later.
- If incorrect association/allocation made: User can adjust later (see REQ-JP-11).
- Allow explicitly marking as **non-job specific** easily.

**Acceptance Criteria:**
- Given a new contractor payment entry (online),
  When the app suggests the correct job(s) the contractor worked on,
  Then the user can confirm the association/allocation with minimal interaction.

- Given a contractor payment that needs splitting across 3 jobs (offline),
  When the user selects the jobs from the cached list and uses the splitting UI,
  Then the allocation is saved correctly for later syncing.

- Given a payment initially marked as "General",
  When the business owner later identifies the correct job(s),
  Then they can easily associate/allocate the payment via REQ-JP-11.

**Dependencies:**
- UC-CP (Contractor Payment Tracking v1.5)
- UC-CoM (Contractor Management)
- REQ-JP-01 (Job Financial Summary Display)
- REQ-JP-11 (Expense/Payment Allocation Adjustment)

### REQ-JP-09: Profitability Data Offline Access *(Revised)*

**Title:** Profitability Data Offline Access

**Description:** The system must provide read-only access to **cached basic** job profitability summary data when the device is offline. Advanced automation features (OCR, suggestions) require connectivity.

**Actors:** Business Owner

**Trigger:** Business owner attempts to view job profitability while offline

**Pre-conditions:**
- User has previously accessed the job data while online
- Device has cached relevant basic job and summary financial data
- Device is currently offline

**Functional Steps (Happy Path):**
1. Business owner attempts to access job details while offline.
2. System detects offline status.
3. System retrieves cached basic job data and last calculated profitability summary.
4. System displays this cached information **clearly marked as potentially outdated** and **read-only**.
5. System shows timestamp of when the data was last synced/calculated.
6. System **disables or visually indicates unavailability of features requiring connectivity** (e.g., initiating OCR, getting new suggestions).
7. System queues synchronization for when connectivity is restored.

**Inputs:**
- Job ID
- Offline status detection

**Outputs / Expected Results:**
- Cached basic job profitability summary information (**read-only**)
- Visual indicator showing offline/cached status
- Last-updated timestamp
- Clear indication that **advanced input features (OCR, suggestions) are unavailable**.

**Error Handling / Alternate Flows:**
- If no cached data exists: Display message that profitability data is unavailable offline
- If cached data is potentially outdated: Display clear warning about potential inaccuracy
- If partial data is available: Display available metrics with indicators for missing data

**Acceptance Criteria:**
- Given a job previously viewed online with complete profitability data,
  When the business owner views the same job while offline,
  Then the system displays the cached profitability summary with an offline indicator and timestamp, and UI elements for online-only features are disabled/indicated.
- Given an offline status,
  When the user attempts to add an expense via OCR,
  Then the system gracefully informs the user that OCR requires connectivity and offers manual entry + photo capture instead.

**Dependencies:**
- REQ-JP-01 (Job Financial Summary Display)

### REQ-JP-10: Tax Impact on Profitability View *(Revised)*

**Title:** Tax Impact on Profitability View

**Description:** The system must display job profitability based on a default calculation basis (e.g., pre-tax) and provide relevant tax information (GST/QST collected/paid - potentially sourced via OCR) separately for informational context.

**Actors:** Business Owner

**Trigger:** Business owner views profitability for a job with tax implications

**Pre-conditions:**
- Job has financial transactions with tax components
- Business profile has tax settings configured

**Functional Steps (Happy Path):**
1. Business owner views job profitability data.
2. System calculates Net Profit using the default basis (e.g., Revenue Received - Expenses - Contractor Payments).
3. System retrieves total GST/QST collected amounts associated with the job's revenue entries.
4. System retrieves total GST/QST paid amounts associated with the job's expense entries (potential ITCs - potentially identified via OCR).
5. System displays the calculated Net Profit (clearly labeled, e.g., "Net Profit (Pre-Tax)").
6. System separately displays "Total GST/QST Collected: $X" and "Total GST/QST Paid (Potential ITCs): $Y".

**Inputs:**
- Job ID

**Outputs / Expected Results:**
- Job profitability calculation based on default MVP view (e.g., Pre-Tax Profit)
- Separate display of 'Total GST/QST Collected' amount
- Separate display of 'Total GST/QST Paid (Potential ITCs)' amount
- Clear indication of the calculation basis used for the main profit figure

**Error Handling / Alternate Flows:**
- If tax status is unknown/incomplete: Display profit without separate tax figures, potentially with a note.
- If business is not registered for GST/QST: Display simplified view without separate tax figures.
- If insufficient or potentially inaccurate OCR tax data exists: Display warning about potentially incomplete tax information, prompt for review.

**Acceptance Criteria:**
- Given a job where GST/QST on expenses was captured via OCR,
  When the business owner views the job profitability summary,
  Then the system displays the net profit calculated on the default pre-tax basis AND separately shows the total GST/QST collected and the total potential ITCs based on the captured expense data.

- Given a job with tax implications,
  When viewing profitability reports or summaries,
  Then the system clearly indicates the calculation basis for profit and provides separate tax information.

**Dependencies:**
- REQ-JP-01 (Job Financial Summary Display)
- UC-ME (for OCR data source)

### REQ-JP-11: Expense/Payment Allocation Adjustment *(New Requirement)*

**Title:** Expense/Payment Allocation Adjustment

**Description:** The system must allow business owners to easily adjust or re-allocate previously associated expenses or contractor payments from the job detail view or a dedicated review screen.

**Actors:** Business Owner

**Trigger:** Business owner identifies an incorrect expense/payment association or allocation while reviewing a job or financial data.

**Pre-conditions:**
- Expense or contractor payment record exists and is associated with one or more jobs.
- User is viewing job details or a relevant financial review screen.

**Functional Steps (Happy Path):**
1. User identifies an expense/payment needing adjustment within a job's transaction list or a dedicated review interface.
2. User selects the item to adjust.
3. System presents an intuitive interface to:
    - Modify the allocated amount(s) for the current job(s).
    - Re-allocate amounts to different job(s).
    - Unlink the item entirely (mark as "General Expense" or leave unassociated).
4. If splitting/re-allocating, system validates that total allocation matches the original item amount.
5. User confirms the changes.
6. System updates the association/allocation records for all affected items and jobs.
7. System recalculates profitability for all affected jobs.

**Inputs:**
- Identifier for the expense/payment record.
- User input specifying the desired adjustment (new amounts, new job associations, unlink action).

**Outputs / Expected Results:**
- Updated expense/payment association and allocation records.
- Recalculated profitability figures for all affected jobs.
- Confirmation message to the user.

**Error Handling / Alternate Flows:**
- If user tries to allocate more/less than the total item amount: Display validation error.
- If adjustment is attempted offline and requires data not cached: Inform user adjustment requires connectivity.

**Acceptance Criteria:**
- Given an expense of $100 incorrectly linked 100% to Job A,
  When the user accesses the adjustment interface for that expense via Job A's details, selects Job B, and allocates $50 to Job B (leaving $50 for Job A),
  Then the system updates the records, and the profitability for both Job A and Job B is recalculated correctly.

- Given a contractor payment split 50/50 between Job C and Job D,
  When the user decides it should have been 100% for Job C and uses the adjustment interface,
  Then the system updates the allocation, removing the cost from Job D and applying the full amount to Job C, and recalculates profitability for both.

**Dependencies:**
- REQ-JP-01 (Job Financial Summary Display)
- REQ-JP-02 (Financial Transaction Retrieval)
- REQ-JP-05 (Job Expense Association)
- REQ-JP-07 (Contractor Payment-Job Association)

## Mockups
[Link to Mockups](./mockups/index.html)
**(Note: Mockups need significant revision to align with enhanced MVP requirements including automation, splitting UI, and adjustment workflows)**

---

## MVP Exclusions for Job Profitability Tracking *(Revised)*

The following features and paths are explicitly **excluded** from the **enhanced** Minimum Viable Product (MVP) release and are planned for potential future iterations:

* **Advanced Reporting/Comparison:** Dedicated cross-job comparison views, advanced filtering, custom report building, complex visualizations beyond the basic job report/summary. (Excludes original Alternate Path A3).
* **Recurring Job Trend Analysis:** Specific features for analyzing profitability trends across multiple instances of a recurring job. (Excludes original Alternate Path A5).
* **Offline Detailed Reporting:** Generating detailed, fully up-to-date reports while offline. (Excludes original Exception Path E3).
* **Advanced OCR:** Line-item extraction from receipts, high-level validation beyond basic field capture.
* **Advanced Allocation Logic:** Splitting revenue entries, splitting costs based on formulas, time tracking integration, or complex rules beyond simple manual allocation.
* **Profitability Calculation Basis Selection:** User choice between Cash vs. Accrual basis (MVP uses default cash/received).
* **Tax Impact View Selection:** User-selectable toggle for pre-tax vs. after-tax profit views (MVP uses default pre-tax view with separate tax info).

## Change Log
*(Added Entry)*
| Date          | Version | Changed By   | Changes Made                                                                                                                                                                |
| :------------ | :------ | :----------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| April 8, 2025 | 1.0     | Gemini Model | Initial generation based on original documents & refinement feedback.                                                                                                         |
| **April 8, 2025** | **1.1** | **Gemini Model** | **Major Revision: Updated descriptions, paths, and requirements (esp. REQ-JP-01, 05, 07, 09, added 11) to align with enhanced MVP scope (v1.4/v0.4) incorporating automation (OCR, suggestions, splitting) and adjustment capabilities.** |

---