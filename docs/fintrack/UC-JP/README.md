# Use Case: Job Profitability Tracking

**(MVP Version 1.0)**

## Refined Description

### Overview
Track all income and expenses (including Contractor payments) related to a specific service job to determine profitability, enabling business owners to understand which jobs are most profitable and improve pricing decisions.

**(Non-Functional Requirement Note:** All profitability calculations presented to the user, particularly summary figures and list view indicators (REQ-JP-04), must be displayed quickly and efficiently. The system should feel responsive, potentially utilizing strategies like background processing or pre-computation where appropriate to meet performance expectations on mobile devices.)

**(Calculation Basis Note:** For MVP simplicity and alignment with common user cash flows, profitability is calculated on a cash/received basis.)

### Actors
- Primary: Business Owner
- Secondary: None

### Trigger(s)
- Business owner wants to check profitability of a specific job
- Business owner records a new expense or income for a job
- Business owner makes a payment to a contractor for a job
- Business owner generates financial reports for business analysis

### Pre-conditions
- User has an active FinTrack account
- One or more jobs exist in the system
- Client details are available (via UC-CM)
- Any job-related expenses are recorded (via UC-ME)
- Any contractor payments are tracked (via UC-CP)
- Any job-related income/payments are recorded (via UC-CT or UC-IG)

### Expected Outcome
Business owner gains a clear understanding of each job's financial performance with accurate profit calculation (based on recorded transactions and MVP calculation basis), enabling better business decisions related to pricing, service offerings, and contractor engagement.

### Primary Path
1. Business owner navigates to the job list view in the application
2. Business owner selects a specific job to view its details
3. The system displays job information including the client, service type, status, and dates
4. The system calculates and displays a **concise financial summary** for the job, focused on quick assessment, showing:
   - Total revenue (based on payments received)
   - Total Costs (Expenses + Contractor Payments)
   - Net profit calculation (Revenue - Total Costs)
   - Profit margin percentage (or 'N/A')
5. Business owner can view a detailed breakdown of all individual financial transactions (revenue, expenses, contractor payments) related to the job
6. Business owner can generate a basic profitability report for the job
7. Business owner can return to the job list view, which displays profitability indicators for all jobs

### Alternate Paths

#### A1: Profitability Tracking Without Contractor Payments
1. Follow steps 1-3 of the primary path
2. The system calculates and displays a simplified financial summary showing:
   - Total revenue (Received)
   - Total Costs (Expenses only in this case)
   - Net profit calculation (Revenue - Expenses)
   - Profit margin percentage (or 'N/A')
3. Continue with steps 5-7 of the primary path

#### A2: Profitability Recalculation After Job Completion
1. Business owner navigates to a completed job in the job list
2. Business owner discovers and records a new expense related to the job
3. System prompts to associate the expense with the completed job
4. System recalculates the job profitability with the new expense included
5. System updates the profitability report and financial summary

#### A4: Accessing Profitability Data When Offline
1. Business owner attempts to access job details while device is offline
2. System displays **cached, potentially read-only** job information with a notification that data may not be current
3. System shows last-updated timestamp for the profitability data
4. System synchronizes and updates calculations when connectivity is restored

### Exception Paths

#### E1: Missing Expense Data
1. Business owner views a job's profitability report
2. System detects that one or more expenses are known but not yet recorded in the system
3. System displays a warning that profitability calculation may be incomplete
4. System provides an option to add missing expenses directly from this view
5. After adding missing expenses, the system recalculates profitability

#### E2: Expenses Without Job Association
1. System detects expenses that could be related to jobs but have no job association
2. System provides a notification in the job profitability view
3. Business owner reviews unassociated expenses
4. Business owner can associate relevant expenses to the job
5. System recalculates profitability with newly associated expenses

#### E3: System Offline When Report Needed
1. Business owner attempts to generate a detailed profitability report while offline
2. System notifies that detailed reporting is **unavailable offline**.

#### E4: Partial Client Payments
1. Business owner records a partial payment for a job invoice
2. System calculates profitability based on the **default MVP cash/received basis**, reflecting actual payments received.
3. System clearly indicates the calculation basis (e.g., "Based on payments received") in the profitability report/summary.

#### E5: Tax Calculation Impact on Profitability
1. Business owner views profitability for a job that includes GST/QST
2. System detects that tax calculations affect the profitability view
3. System displays profitability calculations **based on the default pre-tax view** and shows relevant tax figures (GST/QST collected/paid) separately for informational purposes.

## Functional Requirements

### REQ-JP-01: Job Financial Summary Display

**Title:** Job Financial Summary Display

**Description:** The system must calculate and display a **concise** financial summary for each job, showing key profitability metrics based on recorded transactions. The primary goal of the summary is to provide the business owner with a quick, clear understanding of whether the job made money and identify significant profit deviations, enabling rapid assessment in the field.

**Actors:** Business Owner

**Trigger:** Business owner views a job's details

**Pre-conditions:**
- Job exists in the system
- Related financial transactions (if any) have been recorded

**Functional Steps (Happy Path):**
1. Retrieve all applicable revenue entries associated with the job
2. Retrieve all expense entries associated with the job
3. Retrieve all contractor payment records associated with the job
4. Calculate total revenue sum (**based on payments received** against associated invoices or directly recorded job income).
5. Calculate total expense sum
6. Calculate total contractor payment sum
7. Calculate **Total Costs** (Total Expenses + Total Contractor Payments)
8. Calculate net profit (Total Revenue - Total Costs)
9. Calculate profit margin percentage (Net Profit / Total Revenue × 100%). **If Total Revenue is zero, the margin is considered Not Applicable ('N/A').**
10. Display the core financial summary prominently in the job details view

**Inputs:**
- Job ID

**Outputs / Expected Results (Core Summary Block):**
- Total revenue amount (formatted currency, indicating basis: '**Received**')
- Total Costs amount (formatted currency)
- Net profit amount (formatted currency)
- Profit margin percentage (**or 'N/A' if revenue is zero**)
- Visual indicator of profitability status (e.g., color coding)
- Separate display area for relevant tax totals (GST/QST collected/paid) if applicable.
  **(Note:** Detailed expense breakdowns by category are available via transaction list or basic report).

**Error Handling / Alternate Flows:**
- If no financial data exists: Display zeros with a message indicating no financial data has been recorded
- If job is in progress: Display an indicator that profitability is preliminary
- If revenue is zero: Display profit margin as 'N/A'.

**Acceptance Criteria:**
- Given a job with recorded payments of $1,000, expenses of $300, and contractor payments of $400,
  When the business owner views the job details,
  Then the system displays revenue as $1,000 (Received), Total Costs as $700, net profit as $300, and profit margin as 30% in the main summary block.

- Given a job with recorded payments of $500 and expenses of $600 (no contractor payments),
  When the business owner views the job details,
  Then the system displays a negative profit of -$100 and provides a visual indicator showing the job is unprofitable.

- Given a job with no financial transactions,
  When the business owner views the job details,
  Then the system displays zeros for all financial fields and shows a message indicating no financial data has been recorded.

**Dependencies:**
- REQ-JP-02 (Financial Transaction Retrieval)

### REQ-JP-02: Financial Transaction Retrieval

**Title:** Financial Transaction Retrieval for Job Profitability

**Description:** The system must retrieve all financial transactions (income, expenses, contractor payments) associated with a specific job to enable accurate profitability calculation.

**Actors:** Business Owner

**Trigger:**
- Job profitability calculation is requested
- Job details page is viewed
- Profitability report is generated

**Pre-conditions:**
- Job exists in the system

**Functional Steps (Happy Path):**
1. Query the database for all income/payment records linked to the job ID
2. Query the database for all expense records linked to the job ID
3. Query the database for all contractor payment records linked to the job ID
4. Organize transactions by type (income, expense, contractor payment)
5. Return the complete transaction dataset for profitability calculation

**Inputs:**
- Job ID

**Outputs / Expected Results:**
- Comprehensive list of all financial transactions associated with the job, including:
  - Transaction amounts
  - Transaction dates
  - Transaction types
  - Payment methods
  - Categories (for expenses)
  - Tax information (if applicable)

**Error Handling / Alternate Flows:**
- If job ID doesn't exist: Return appropriate error without crashing
- If database connection fails: Display error message and retry option
- If partial data retrieved: Flag incomplete data status in results

**Acceptance Criteria:**
- Given a job with 3 income entries, 5 expense entries, and 2 contractor payment entries,
  When the system retrieves financial transactions for the job,
  Then all 10 entries are successfully retrieved and categorized by transaction type.

- Given a job with no financial entries,
  When the system retrieves financial transactions for the job,
  Then an empty result set is returned without errors.

- Given a temporary connectivity issue,
  When the system attempts to retrieve financial transactions for a job,
  Then the system handles the error gracefully and provides retry functionality.

**Dependencies:**
- None

### REQ-JP-03: Job Profitability Report Generation

**Title:** Job Profitability Report Generation

**Description:** The system must generate a **basic** profitability report for a specific job, showing the core financial components that contribute to its profitability calculation.

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
   - Revenue breakdown (based on payments received)
   - Expense breakdown (by category)
   - Contractor payment details
   - Profit calculation (clearly stating calculation basis: cash/received)
4. System formats the report for clean viewing
5. System provides basic export options (PDF, CSV)

**Inputs:**
- Job ID

**Outputs / Expected Results:**
- Formatted profitability report containing:
  - Job identification and basic details
  - Revenue breakdown with dates and sources (Received basis)
  - Itemized expense list with categorization
  - Detailed contractor payment information
  - Clear profit calculation (indicating calculation basis)
  - Key metrics (profit margin or 'N/A')

**Error Handling / Alternate Flows:**
- If offline: Notify user that reporting is unavailable offline
- If insufficient data: Generate report with available data and clearly mark missing components
- If export fails: Provide retry option and alternative export formats

**Acceptance Criteria:**
- Given a completed job with full financial records,
  When the business owner requests a profitability report,
  Then a basic report is generated showing core revenue (received), expenses, contractor payments, net profit calculation (indicating basis), and profit margin.

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

**Description:** The system must display profitability indicators for all jobs in the job list view to provide at-a-glance financial performance visibility.

**Actors:** Business Owner

**Trigger:** Business owner views the job list

**Pre-conditions:**
- User has at least one job in the system

**Functional Steps (Happy Path):**
1. System loads the job list view
2. For each job, system retrieves or calculates basic profitability metrics (strategy TBD - e.g., precomputed or on-demand)
3. System displays appropriate visual indicators based on defined profitability status logic (see below).
4. System shows profit margin or amount based on user preference setting (defaulting to amount for quick insight).

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
* `Preliminary:` Job Status is 'In Progress' or 'Planned'

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

### REQ-JP-05: Job Expense Association

**Title:** Job Expense Association

**Description:** The system must enable business owners to associate expenses with specific jobs, either at the time of expense entry or afterward. The process of associating expenses must be optimized for speed and minimal user interaction on a mobile device.

**Actors:** Business Owner

**Trigger:**
- Business owner enters a new expense (via UC-ME)
- Business owner updates an existing expense
- Business owner reviews unassociated expenses (potentially via E2 path)

**Pre-conditions:**
- User has an active account
- At least one job exists in the system
- Expense data is available

**Functional Steps (Happy Path):**
1. When entering a new expense (or reviewing unassociated ones), system provides an efficient option to associate with a job.
2. System displays list of jobs for selection (with effective search/filter/suggestion capability).
3. Business owner quickly selects the appropriate job.
4. System creates association between expense and selected job.
5. System updates job profitability calculations to include the new expense.

**Inputs:**
- Expense details (amount, date, category, etc.)
- Selected job ID

**Outputs / Expected Results:**
- Expense record with job association
- Updated job profitability calculation
- Confirmation of successful association

**Error Handling / Alternate Flows:**
- If job list cannot be retrieved (offline): Allow expense entry without job association, flag for later association using a streamlined process.
- If expense is associated with wrong job: Provide ability to reassign to correct job easily.
- For general business expenses: Allow explicitly marking as non-job specific quickly.

**Acceptance Criteria:**
- Given a new expense entry,
  When the business owner associates it with a specific job using the mobile interface,
  Then the association is completed quickly and the job's profitability is recalculated.

- Given an existing expense without job association,
  When the business owner later associates it with a job via the review screen,
  Then the association process is efficient and profitability is updated accordingly.

- Given a list of unassociated expenses displayed for review,
  When the business owner reviews them from the job details screen,
  Then they can rapidly select and associate relevant expenses with the current job.

**Dependencies:**
- UC-ME (Mobile Expense Tracking) - for initial entry workflow
- REQ-JP-01 (Job Financial Summary Display)

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
1. When creating an invoice or recording a payment, system provides option to associate with a job
2. System displays list of jobs for selection (with search/filter capability)
3. Business owner selects the appropriate job
4. System creates association between revenue entry and selected job
5. System updates job profitability calculations to include the new revenue (based on MVP cash/received basis for payments)

**Inputs:**
- Revenue details (amount, date, type, etc.)
- Selected job ID

**Outputs / Expected Results:**
- Revenue record with job association
- Updated job profitability calculation
- Confirmation of successful association

**Error Handling / Alternate Flows:**
- If job list cannot be retrieved (offline): Allow revenue entry without job association, flag for later association
- If revenue is associated with wrong job: Provide ability to reassign to correct job

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

### REQ-JP-07: Contractor Payment-Job Association

**Title:** Contractor Payment-Job Association

**Description:** The system must enable associating contractor payments with specific jobs to ensure accurate profitability calculation.

**Actors:** Business Owner

**Trigger:**
- Business owner records a contractor payment
- Business owner reviews contractor payment allocation

**Pre-conditions:**
- User has an active account
- At least one job exists in the system
- At least one contractor exists in the system

**Functional Steps (Happy Path):**
1. When recording a contractor payment, system provides option to associate with one or more jobs
2. System displays list of jobs for selection (with search/filter capability)
3. Business owner selects the appropriate job(s)
4. If multiple jobs selected, business owner specifies allocation amount or percentage per job
5. System creates association between contractor payment and selected job(s)
6. System updates job profitability calculations to include the contractor payment expense

**Inputs:**
- Contractor payment details (amount, date, contractor, etc.)
- Selected job ID(s)
- Optional: allocation percentages/amounts for multiple jobs

**Outputs / Expected Results:**
- Contractor payment record with job association(s)
- Updated job profitability calculation(s)
- Confirmation of successful association

**Error Handling / Alternate Flows:**
- If job list cannot be retrieved (offline): Allow payment recording without job association, flag for later association
- If contractor payment is associated with wrong job: Provide ability to reassign to correct job
- For general contractor payments not tied to specific jobs: Allow explicitly marking as non-job specific

**Acceptance Criteria:**
- Given a new contractor payment,
  When the business owner associates it with a specific job,
  Then the payment is linked to that job and the job's profitability is recalculated.

- Given a contractor payment that applies to multiple jobs,
  When the business owner specifies allocation percentages across jobs,
  Then the system distributes the expense accordingly and updates each job's profitability.

- Given a previously recorded contractor payment without job association,
  When the business owner later associates it with a job,
  Then the system updates the job's profitability calculation.

**Dependencies:**
- UC-CP (Contractor Payment Tracking)
- UC-CoM (Contractor Management)
- REQ-JP-01 (Job Financial Summary Display)

### REQ-JP-09: Profitability Data Offline Access

**Title:** Profitability Data Offline Access

**Description:** The system must provide read-only access to **cached** job profitability data when the device is offline.

**Actors:** Business Owner

**Trigger:** Business owner attempts to view job profitability while offline

**Pre-conditions:**
- User has previously accessed the job data while online
- Device has cached relevant job and financial data
- Device is currently offline

**Functional Steps (Happy Path):**
1. Business owner attempts to access job details while offline
2. System detects offline status
3. System retrieves cached job data including profitability information
4. System displays job profitability information with an indicator showing it's based on cached data and may be out of date
5. System shows timestamp of when the data was last updated
6. System queues synchronization for when connectivity is restored

**Inputs:**
- Job ID
- Offline status detection

**Outputs / Expected Results:**
- Cached job profitability information (**potentially read-only**)
- Visual indicator showing offline/cached status
- Last-updated timestamp
- Notification that data will be refreshed when online

**Error Handling / Alternate Flows:**
- If no cached data exists: Display message that profitability data is unavailable offline
- If cached data is potentially outdated: Display clear warning about potential inaccuracy
- If partial data is available: Display available metrics with indicators for missing data

**Acceptance Criteria:**
- Given a job previously viewed online with complete profitability data,
  When the business owner views the same job while offline,
  Then the system displays the cached profitability data with an offline indicator and timestamp.

- Given an offline status and cached profitability data from 3 days ago,
  When the business owner views a job's profitability,
  Then the system displays the data with a clear timestamp indicating when it was last updated.

- Given a return to online status after viewing cached data,
  When the system synchronizes,
  Then it updates any profitability calculations with the latest data.

**Dependencies:**
- REQ-JP-01 (Job Financial Summary Display)

### REQ-JP-10: Tax Impact on Profitability View

**Title:** Tax Impact on Profitability View

**Description:** The system must display job profitability based on a default calculation basis (e.g., pre-tax) and provide relevant tax information (GST/QST collected/paid) separately for informational context. (Note: This approach provides tax context without altering the primary profit figure displayed in the MVP, simplifying the core calculation.)

**Actors:** Business Owner

**Trigger:** Business owner views profitability for a job with tax implications

**Pre-conditions:**
- Job has financial transactions with tax components
- Business profile has tax settings configured

**Functional Steps (Happy Path):**
1. Business owner views job profitability data.
2. System calculates Net Profit using the default basis (e.g., Revenue Received - Expenses - Contractor Payments, without direct tax adjustments).
3. System retrieves total GST/QST collected amounts associated with the job's revenue entries.
4. System retrieves total GST/QST paid amounts associated with the job's expense entries (potential ITCs).
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
- If insufficient tax data exists: Display warning about potentially incomplete tax information.

**Acceptance Criteria:**
- Given a job with GST/QST collected on revenue and paid on expenses,
  When the business owner views the job profitability summary,
  Then the system displays the net profit calculated on the default pre-tax basis AND separately shows the total GST/QST collected and paid figures.

- Given a job with tax implications,
  When viewing profitability reports or summaries,
  Then the system clearly indicates the calculation basis for profit and provides separate tax information.

**Dependencies:**
- REQ-JP-01 (Job Financial Summary Display)

## Mockups
[Link to Mockups](./mockups/index.html)
**(Note: Mockups to be revisited to align with refined MVP requirements)**

---

## MVP Exclusions for Job Profitability Tracking

The following features and paths derived from the initial description are explicitly **excluded** from the initial Minimum Viable Product (MVP) release and are planned for potential future iterations:

* **Alternate Path A3:** Profitability Comparison Across Multiple Jobs.
* **Alternate Path A5:** Profitability Tracking for Recurring Jobs (viewing trends across instances).
* **Exception Path E3:** Generating detailed reports while offline (MVP: reporting unavailable offline).
* **Exception Path E4:** User choice between Cash vs. Accrual basis for profitability calculation (MVP uses a default basis).
* **Exception Path E5:** User-selectable toggle to view profitability including tax impact vs. excluding tax considerations (MVP displays profit based on a default view and shows tax info separately).
* **REQ-JP-03:** Advanced reporting features beyond basic data presentation (e.g., complex visualizations, comparative metrics).
* **REQ-JP-06:** Complex revenue splitting across multiple jobs.
* **REQ-JP-08:** Profitability Comparison View functional requirement.
* **REQ-JP-10:** User-selectable toggle for different tax impact views in profitability calculation.
* **Advanced Expense Association:** Suggestions based on date/location proximity, etc.