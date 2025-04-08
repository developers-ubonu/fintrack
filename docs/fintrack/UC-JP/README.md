# Use Case: Job Profitability Tracking

## Refined Description

### Overview
Track all income and expenses (including Contractor payments) related to a specific service job to determine profitability, enabling business owners to understand which jobs are most profitable and improve pricing decisions.

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
Business owner gains a clear understanding of each job's financial performance with accurate profit calculation, enabling better business decisions related to pricing, service offerings, and contractor engagement.

### Primary Path
1. Business owner navigates to the job list view in the application
2. Business owner selects a specific job to view its details
3. The system displays job information including the client, service type, status, and dates
4. The system calculates and displays a financial summary for the job, showing:
   - Total revenue (from all recorded payments and invoices)
   - Total expenses (broken down by categories)
   - Total contractor payments (if any)
   - Net profit calculation (Revenue - Expenses - Contractor Payments)
   - Profit margin percentage
5. Business owner can view a detailed breakdown of all financial transactions related to the job
6. Business owner can generate a detailed profitability report for the job
7. Business owner can return to the job list view, which displays profitability indicators for all jobs

### Alternate Paths

#### A1: Profitability Tracking Without Contractor Payments
1. Follow steps 1-3 of the primary path
2. The system calculates and displays a simplified financial summary showing:
   - Total revenue
   - Total expenses
   - Net profit calculation (Revenue - Expenses)
   - Profit margin percentage
3. Continue with steps 5-7 of the primary path

#### A2: Profitability Recalculation After Job Completion
1. Business owner navigates to a completed job in the job list
2. Business owner discovers and records a new expense related to the job
3. System prompts to associate the expense with the completed job
4. System recalculates the job profitability with the new expense included
5. System updates the profitability report and financial summary

#### A3: Profitability Comparison Across Multiple Jobs
1. Business owner navigates to the profitability report section
2. Business owner selects multiple jobs or filters jobs by client, date range, or service type
3. System generates a comparative profitability report for the selected jobs
4. System displays profitability metrics side-by-side for easy comparison

#### A4: Accessing Profitability Data When Offline
1. Business owner attempts to access job details while device is offline
2. System displays cached job information with a notification that data may not be current
3. System shows last-updated timestamp for the profitability data
4. System synchronizes and updates calculations when connectivity is restored

#### A5: Profitability Tracking for Recurring Jobs
1. Business owner identifies a job as recurring in the job details
2. System provides an option to view profitability trends across recurring instances
3. System displays profitability metrics across all instances of the recurring job
4. Business owner can identify profitability trends and variations

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
2. System notifies that detailed reporting is unavailable offline
3. System offers to generate the report when connectivity is restored
4. System queues the report request and generates it automatically once online
5. System notifies the business owner when the report is available

#### E4: Partial Client Payments
1. Business owner records a partial payment for a job invoice
2. System asks whether to calculate profitability based on:
   a. Only received payments (actual cash basis)
   b. Full invoice amount (accrual basis)
3. System calculates profitability according to the selected method
4. System clearly indicates the calculation basis in the profitability report

#### E5: Tax Calculation Impact on Profitability
1. Business owner views profitability for a job that includes GST/QST
2. System detects that tax calculations affect the profitability view
3. System offers to show profitability calculations:
   a. Including tax impact (after tax credits)
   b. Excluding tax considerations (pretax)
4. System displays the selected view with appropriate indicators

## Functional Requirements

### REQ-JP-01: Job Financial Summary Display

**Title:** Job Financial Summary Display

**Description:** The system must calculate and display a financial summary for each job, showing revenue, expenses, contractor payments, and net profit.

**Actors:** Business Owner

**Trigger:** Business owner views a job's details

**Pre-conditions:** 
- Job exists in the system
- Related financial transactions (if any) have been recorded

**Functional Steps (Happy Path):**
1. Retrieve all revenue entries associated with the job
2. Retrieve all expense entries associated with the job
3. Retrieve all contractor payment records associated with the job
4. Calculate total revenue sum
5. Calculate total expense sum
6. Calculate total contractor payment sum
7. Calculate net profit (Revenue - Expenses - Contractor Payments)
8. Calculate profit margin percentage (Net Profit / Revenue × 100%)
9. Display the financial summary prominently in the job details view

**Inputs:**
- Job ID

**Outputs / Expected Results:**
- Total revenue amount (formatted currency)
- Total expense amount (formatted currency)
- Total contractor payments amount (formatted currency)
- Net profit amount (formatted currency)
- Profit margin percentage
- Visual indicator of profitability status (e.g., color coding)

**Error Handling / Alternate Flows:**
- If no financial data exists: Display zeros with a message indicating no financial data has been recorded
- If job is in progress: Display an indicator that profitability is preliminary
- If tax status impacts calculation: Show appropriate tax consideration indicator

**Acceptance Criteria:**
- Given a job with recorded revenue of $1,000, expenses of $300, and contractor payments of $400,
  When the business owner views the job details,
  Then the system displays revenue as $1,000, expenses as $300, contractor payments as $400, net profit as $300, and profit margin as 30%.
  
- Given a job with recorded revenue of $500 and expenses of $600 (no contractor payments),
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

**Description:** The system must generate a detailed profitability report for a specific job, showing all financial components that contribute to its profitability calculation.

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
   - Revenue breakdown (invoices, payments)
   - Expense breakdown (by category)
   - Contractor payment details
   - Profit calculation
   - Comparative metrics (if applicable)
4. System formats the report for viewing
5. System provides export options (PDF, CSV)

**Inputs:**
- Job ID
- Optional: Report parameters (date range, detail level)

**Outputs / Expected Results:**
- Formatted profitability report containing:
  - Job identification and basic details
  - Complete revenue breakdown with dates and sources
  - Itemized expense list with categorization
  - Detailed contractor payment information
  - Clear profit calculation
  - Key metrics (profit margin, cost breakdown percentages)
  - Visual elements (charts/graphs as appropriate)

**Error Handling / Alternate Flows:**
- If offline: Queue report generation for when online
- If insufficient data: Generate report with available data and clearly mark missing components
- If export fails: Provide retry option and alternative export formats

**Acceptance Criteria:**
- Given a completed job with full financial records,
  When the business owner requests a profitability report,
  Then a complete report is generated showing all revenue, expenses, contractor payments, net profit calculation, and profit margin.
  
- Given a job with partial financial records,
  When the business owner requests a profitability report,
  Then a report is generated with available data, clearly indicating which components are incomplete.
  
- Given a request to export the profitability report as PDF,
  When the business owner selects the PDF export option,
  Then the system generates a well-formatted PDF containing all report information.

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
2. For each job, system calculates basic profitability metrics
3. System displays appropriate visual indicators based on profitability status:
   - Profitable jobs: Positive indicator (e.g., green indicator or up arrow)
   - Unprofitable jobs: Negative indicator (e.g., red indicator or down arrow)
   - Break-even jobs: Neutral indicator
   - Incomplete financial data: Information needed indicator
4. System shows profit margin or amount based on user preference setting

**Inputs:**
- None (view initialization)

**Outputs / Expected Results:**
- List of jobs with visual profitability indicators
- Profit amount or percentage displayed for each job (configurable)
- Sort/filter options based on profitability

**Error Handling / Alternate Flows:**
- If profitability cannot be calculated: Display information needed indicator
- If job is in progress: Display preliminary indicator
- If job has no financial data: Display appropriate status indicator

**Acceptance Criteria:**
- Given a list containing profitable and unprofitable jobs,
  When the business owner views the job list,
  Then each job displays an appropriate visual indicator of its profitability status.
  
- Given a job with incomplete financial data,
  When the business owner views the job list,
  Then that job displays an indicator showing financial information is needed.
  
- Given the business owner's preference to view profit margins as percentages,
  When the business owner views the job list,
  Then profit margins are displayed as percentages rather than absolute amounts.

**Dependencies:**
- REQ-JP-01 (Job Financial Summary Display)

### REQ-JP-05: Job Expense Association

**Title:** Job Expense Association

**Description:** The system must enable business owners to associate expenses with specific jobs, either at the time of expense entry or afterward.

**Actors:** Business Owner

**Trigger:**
- Business owner enters a new expense
- Business owner updates an existing expense
- Business owner reviews unassociated expenses

**Pre-conditions:**
- User has an active account
- At least one job exists in the system
- Expense data is available

**Functional Steps (Happy Path):**
1. When entering a new expense, system provides option to associate with a job
2. System displays list of jobs for selection (with search/filter capability)
3. Business owner selects the appropriate job
4. System creates association between expense and selected job
5. System updates job profitability calculations to include the new expense

**Inputs:**
- Expense details (amount, date, category, etc.)
- Selected job ID

**Outputs / Expected Results:**
- Expense record with job association
- Updated job profitability calculation
- Confirmation of successful association

**Error Handling / Alternate Flows:**
- If job list cannot be retrieved (offline): Allow expense entry without job association, flag for later association
- If expense is associated with wrong job: Provide ability to reassign to correct job
- For general business expenses: Allow explicitly marking as non-job specific

**Acceptance Criteria:**
- Given a new expense entry,
  When the business owner associates it with a specific job,
  Then the expense is linked to that job and the job's profitability is recalculated.
  
- Given an existing expense without job association,
  When the business owner later associates it with a job,
  Then the expense is linked to the selected job and profitability is updated accordingly.
  
- Given a list of unassociated expenses,
  When the business owner reviews them from the job details screen,
  Then they can select relevant expenses to associate with the current job.

**Dependencies:**
- UC-ME (Mobile Expense Tracking)
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
5. System updates job profitability calculations to include the new revenue

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
- If revenue needs to be split across multiple jobs: Provide ability to enter multiple entries or split percentage

**Acceptance Criteria:**
- Given a new invoice creation,
  When the business owner associates it with a specific job,
  Then the invoice is linked to that job and the job's profitability is recalculated.
  
- Given a payment receipt,
  When the business owner records it and associates with a job,
  Then the payment is linked to that job and profitability is updated accordingly.
  
- Given an invoice associated with a job,
  When partial payment is received,
  Then the system accurately reflects the partial revenue in the job's profitability calculation.

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

### REQ-JP-08: Profitability Comparison View

**Title:** Profitability Comparison View

**Description:** The system must provide a comparison view that allows business owners to evaluate profitability across multiple jobs based on various criteria.

**Actors:** Business Owner

**Trigger:** Business owner selects option to compare job profitability

**Pre-conditions:**
- Multiple jobs exist in the system
- Financial data exists for jobs

**Functional Steps (Happy Path):**
1. Business owner navigates to job profitability comparison feature
2. System provides filtering options (date range, client, service type, etc.)
3. Business owner selects desired filters and jobs for comparison
4. System retrieves profitability data for selected jobs
5. System presents side-by-side comparison showing key metrics:
   - Revenue totals
   - Expense totals
   - Contractor payment totals
   - Net profit
   - Profit margins
   - Cost breakdowns by category
6. System enables sorting by different profitability metrics
7. System provides option to export comparison data

**Inputs:**
- Filter criteria (date range, client, service type, etc.)
- Selected job IDs for direct comparison

**Outputs / Expected Results:**
- Side-by-side job comparison with key profitability metrics
- Visual indicators highlighting significant differences
- Sorting capabilities by different metrics
- Export options for comparison data

**Error Handling / Alternate Flows:**
- If insufficient data for meaningful comparison: Display appropriate message
- If too many jobs selected: Recommend limiting selection or provide paginated view
- If jobs have vastly different characteristics: Display normalization options (e.g., by job size)

**Acceptance Criteria:**
- Given multiple completed jobs with financial data,
  When the business owner selects them for comparison,
  Then the system displays a side-by-side comparison of key profitability metrics.
  
- Given a filter for "snow removal jobs in January 2025",
  When the business owner applies this filter to the comparison view,
  Then only matching jobs appear in the comparison results.
  
- Given a profitability comparison of 5 jobs,
  When the business owner sorts by profit margin,
  Then the jobs are reordered from highest to lowest profit margin.

**Dependencies:**
- REQ-JP-01 (Job Financial Summary Display)
- REQ-JP-02 (Financial Transaction Retrieval)

### REQ-JP-09: Profitability Data Offline Access

**Title:** Profitability Data Offline Access

**Description:** The system must provide read-only access to job profitability data when the device is offline.

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
4. System displays job profitability information with an indicator showing it's based on cached data
5. System shows timestamp of when the data was last updated
6. System queues synchronization for when connectivity is restored

**Inputs:**
- Job ID
- Offline status detection

**Outputs / Expected Results:**
- Cached job profitability information
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
  Then the system displays the cached profitability data with an offline indicator.
  
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

**Description:** The system must provide options to view job profitability with or without tax considerations (GST/QST) for Quebec businesses.

**Actors:** Business Owner

**Trigger:** Business owner views profitability for a job with tax implications

**Pre-conditions:**
- Job has financial transactions with tax components
- Business profile has tax settings configured

**Functional Steps (Happy Path):**
1. Business owner views job profitability data
2. System detects tax components in the financial data
3. System provides toggle option for viewing profitability:
   - Including tax impact (after input tax credits)
   - Excluding tax considerations (pretax view)
4. Business owner selects desired view
5. System recalculates and displays profitability according to selection
6. System clearly indicates which view is currently displayed

**Inputs:**
- Job ID
- Tax view preference (include/exclude)

**Outputs / Expected Results:**
- Job profitability calculation based on selected tax view
- Clear indicator of which tax view is active
- Proper handling of input tax credits in calculations when applicable

**Error Handling / Alternate Flows:**
- If tax status is unknown/incomplete: Default to pretax view with explanation
- If business is not registered for GST/QST: Show simplified view without tax toggle
- If insufficient tax data exists: Display warning about potentially incomplete tax calculations

**Acceptance Criteria:**
- Given a job with GST/QST collected on revenue and paid on expenses,
  When the business owner toggles to "include tax impact" view,
  Then the profitability calculation includes the net effect of taxes after input tax credits.
  
- Given a job with GST/QST components,
  When the business owner toggles to "exclude tax considerations" view,
  Then the system displays profitability without tax effects.
  
- Given a job with tax implications,
  When viewing profitability reports,
  Then the system clearly indicates which tax perspective is being displayed.

**Dependencies:**
- REQ-JP-01 (Job Financial Summary Display)

## Mockups
[Link to Mockups](./mockups/index.html)