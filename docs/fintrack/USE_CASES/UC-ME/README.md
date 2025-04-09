# Use Case: Mobile Expense Tracking

## Refined Description

### Overview
The Mobile Expense Tracking use case enables business owners to quickly and accurately record business expenses while in the field using a combination of manual entry and automated features. The system leverages OCR technology to extract data from receipt images and uses contextual information to suggest relevant job associations. Users can split expenses across multiple jobs with an intuitive interface and optionally track tax details if the tax features are enabled.

### Actors
- Primary: Business owner
- Secondary: None

### Trigger(s)
- User selects "Add Expense" function in the mobile application
- User accesses "Expenses" section and initiates a new expense entry

### Pre-conditions
- User is authenticated in the application
- User has the necessary device permissions granted (camera)
- User has at least one job created in the system for expense association (optional, as expenses can also be marked as general business expenses)

### Primary Path
1. User opens the mobile app and selects "Add Expense" function
2. User photographs a receipt using the device camera
3. System processes the image with OCR and extracts Vendor, Date, and Amount information
4. System displays extracted data for user confirmation/correction
5. System suggests potential job(s) based on contextual information (GPS location, calendar entries, recent activity)
6. User confirms the suggested job(s) or manually selects from a job list
7. If multiple jobs are selected, system displays an expense allocation interface
8. User allocates expense amounts across selected jobs using the interface (sliders, percentages, or direct amounts)
9. User selects or confirms the suggested expense category
10. If tax features are enabled: System attempts to extract and display GST/QST amounts from the receipt
11. If tax features are enabled: User confirms or corrects tax information
12. User saves the expense record
13. System confirms the expense has been recorded and syncs when online

### Alternate Paths

#### A1: Manual Entry Without Receipt
1. At step 2, user selects "Manual Entry" instead of taking a photo
2. User manually inputs expense details (Vendor, Date, Amount)
3. Flow continues from step 5 of primary path

#### A2: Offline Mode Operation
1. System detects no internet connection at any point in the flow
2. System notifies user of offline mode and explains limitations
3. User proceeds with manual entry or photo capture (without real-time OCR processing)
4. Receipt image is stored locally for later processing
5. User can select jobs from cached job list and enter basic information
6. System queues the expense for synchronization when connectivity returns
7. When connectivity is restored, system processes any pending OCR tasks and updates records

#### A3: General Business Expense
1. At step 6, user indicates the expense is not associated with any specific job
2. System marks the expense as a "General Business Expense"
3. Flow continues from step 9 of primary path (skipping allocation steps)

#### A4: Multiple Expense Entry Session
1. After completing one expense entry, user selects "Add Another Expense" option
2. System maintains context from previous entry where applicable (e.g., location for job suggestions)
3. Flow restarts from step 2 of primary path

### Exception Paths

#### E1: OCR Processing Failure
1. At step 3, system fails to extract data from the receipt image
2. System notifies user of the failure and provides troubleshooting tips (e.g., better lighting, different angle)
3. User can retry photo capture or switch to manual entry (A1)

#### E2: Required Data Missing
1. At step 12, system validates that minimum required fields are completed
2. If validation fails, system highlights missing fields and prevents saving
3. User completes required information and attempts to save again

#### E3: Expense Allocation Error
1. At step 8, if the sum of allocated amounts does not equal the total expense amount
2. System displays an error message and prevents proceeding
3. User adjusts allocation until the sum matches the total expense amount

#### E4: Storage Limit Reached
1. System detects local storage limit is approaching or reached
2. System notifies user and suggests sync operation or cleanup options
3. User takes appropriate action or proceeds with limited functionality

### Expected Outcome
Accurate expense records captured with minimal manual effort through automation features; expenses properly allocated to jobs or marked as general; receipt images stored for reference; data synchronized between offline and online environments. If tax features are enabled, tax information is also accurately captured for future reporting.

## Functional Requirements

### REQ-ME-01: Expense Entry Initiation

- **Title:** Expense Entry Initiation
- **Description:** System must provide an easily accessible way to initiate the expense tracking process
- **Actors:** Business owner
- **Trigger:** User selects "Add Expense" function
- **Pre-conditions:** User is authenticated in the application
- **Functional Steps (Happy Path):**
  1. User navigates to expense section or uses quick-access button
  2. System displays expense entry options (photo capture or manual entry)
  3. User selects desired entry method
- **Inputs:** User selection of entry method
- **Outputs / Expected Results:** System activates appropriate entry mode (camera or form)
- **Error Handling / Alternate Flows:** 
  - If camera permissions are missing, prompt user to grant permissions
  - If offline, notify user of limited functionality
- **Acceptance Criteria:**
  - **Given** a logged-in user
  - **When** they select "Add Expense" from any screen
  - **Then** the system should present options for expense entry within 1 second
  
  - **Given** a logged-in user 
  - **When** they access the expense entry flow
  - **Then** both photo capture and manual entry options should be available
  
  - **Given** a logged-in user in offline mode
  - **When** they select "Add Expense"
  - **Then** the system should clearly indicate offline mode and available functions
- **Dependencies:** Authentication system

### REQ-ME-02: Receipt Photo Capture

- **Title:** Receipt Photo Capture
- **Description:** System must enable users to photograph receipts for expense tracking
- **Actors:** Business owner
- **Trigger:** User selects photo capture mode
- **Pre-conditions:** Device has camera access permitted
- **Functional Steps (Happy Path):**
  1. System activates device camera with receipt-optimized settings
  2. User positions receipt and captures photo
  3. System displays preview for confirmation
  4. User confirms or retakes photo
  5. System stores receipt image and prepares for OCR processing
- **Inputs:** Receipt photo captured by device camera
- **Outputs / Expected Results:** High-quality image stored for processing
- **Error Handling / Alternate Flows:**
  - If photo quality is poor, suggest retaking with tips
  - If camera fails, offer manual entry alternative
  - If storage space is limited, warn user before capture
- **Acceptance Criteria:**
  - **Given** a user with camera permissions
  - **When** they select photo capture for expense entry
  - **Then** the camera should activate with receipt-optimized settings
  
  - **Given** a user has taken a receipt photo
  - **When** they confirm the photo
  - **Then** the system should store the image locally and queue for OCR processing
  
  - **Given** the device is offline
  - **When** a user captures a receipt photo
  - **Then** the system should store the image locally for later processing
- **Dependencies:** Device camera API, Local storage system

### REQ-ME-03: Receipt OCR Processing

- **Title:** Receipt OCR Processing
- **Description:** System must analyze receipt images to extract key data (Vendor, Date, Amount) using OCR technology
- **Actors:** Business owner, System OCR service
- **Trigger:** User confirms receipt photo capture
- **Pre-conditions:** Receipt image captured and stored
- **Functional Steps (Happy Path):**
  1. System sends image to OCR processing service (local or cloud-based)
  2. OCR service analyzes image and extracts key data fields
  3. System receives extracted data and prepares for user verification
  4. System displays extracted data fields (Vendor, Date, Amount) to user
- **Inputs:** Receipt image
- **Outputs / Expected Results:** Extracted text data from receipt (Vendor, Date, Amount)
- **Error Handling / Alternate Flows:**
  - If OCR processing fails completely, prompt user for manual entry
  - If OCR processing is partial, pre-fill available fields and prompt for completion
  - If offline, queue OCR processing for when connectivity returns
- **Acceptance Criteria:**
  - **Given** a clear receipt image
  - **When** processed through the OCR service
  - **Then** the system should extract Vendor, Date, and Amount with at least 80% accuracy
  
  - **Given** an OCR-processed receipt
  - **When** displaying results to the user
  - **Then** the system should highlight uncertain results for verification
  
  - **Given** the device is offline
  - **When** a receipt photo is captured
  - **Then** the system should queue the OCR processing and allow manual entry in the interim
- **Dependencies:** OCR service integration, Network connectivity monitoring

### REQ-ME-04: Manual Expense Data Entry

- **Title:** Manual Expense Data Entry
- **Description:** System must provide a form for manual entry of expense data
- **Actors:** Business owner
- **Trigger:** User selects manual entry or OCR fails
- **Pre-conditions:** Expense entry initiated
- **Functional Steps (Happy Path):**
  1. System displays form with fields for Vendor, Date, Amount, and optional notes
  2. User enters expense data
  3. System validates basic format requirements as user types
  4. User submits completed form
- **Inputs:** User-entered expense data (Vendor, Date, Amount, Notes)
- **Outputs / Expected Results:** Validated expense data ready for job association
- **Error Handling / Alternate Flows:**
  - If required fields are missing, highlight and prevent submission
  - If data format is invalid (e.g., numeric amount contains text), show inline error
  - Allow saving with minimal required fields (Amount and Date) if user chooses
- **Acceptance Criteria:**
  - **Given** a user selecting manual entry
  - **When** the form is displayed
  - **Then** all required fields should be clearly marked
  
  - **Given** a user completing the manual entry form
  - **When** they attempt to submit with invalid or missing required data
  - **Then** the system should highlight errors and prevent submission
  
  - **Given** a completed manual entry form
  - **When** the user submits valid data
  - **Then** the system should accept the input and proceed to job association
- **Dependencies:** Form validation system

### REQ-ME-05: Contextual Job Suggestions

- **Title:** Contextual Job Suggestions
- **Description:** System must suggest relevant jobs for expense association based on contextual data
- **Actors:** Business owner, System
- **Trigger:** After expense data capture or entry
- **Pre-conditions:** Expense data confirmed, User has active jobs in the system, Contextual data permissions granted
- **Functional Steps (Happy Path):**
  1. System analyzes available contextual data (GPS location, calendar, recent activity)
  2. System compares contextual data with stored job information
  3. System identifies potentially relevant jobs
  4. System displays suggested job(s) with confidence indicator
  5. User confirms suggestion or manually selects from full job list
- **Inputs:** Contextual data (location, calendar, recent activity), Job database
- **Outputs / Expected Results:** Prioritized list of suggested jobs
- **Error Handling / Alternate Flows:**
  - If no contextual data available or permissions denied, skip suggestions
  - If no strong matches found, show most recent jobs instead
  - If offline, use cached job data and recent selections for suggestions
- **Acceptance Criteria:**
  - **Given** a user with GPS permissions granted
  - **When** they create an expense near a job location
  - **Then** that job should appear in suggestions
  
  - **Given** a user with calendar permissions granted
  - **When** they create an expense on a day with scheduled job(s)
  - **Then** those job(s) should appear in suggestions
  
  - **Given** a user who recently worked on specific jobs
  - **When** they create a new expense
  - **Then** those recent jobs should appear in suggestions
  
  - **Given** contextual job suggestions are displayed
  - **When** the user needs to select a different job
  - **Then** the complete job list should be easily accessible
- **Dependencies:** Location services, Calendar integration, Recent activity tracking, Job database

### REQ-ME-06: Job Selection Interface

- **Title:** Job Selection Interface
- **Description:** System must provide an interface for selecting jobs to associate with an expense
- **Actors:** Business owner
- **Trigger:** After expense data confirmation
- **Pre-conditions:** Expense data confirmed, Jobs exist in the system
- **Functional Steps (Happy Path):**
  1. System displays job selection interface with suggested and recent jobs prominently
  2. User can search or filter job list if needed
  3. User selects one or more jobs or marks as general expense
  4. System confirms selection
- **Inputs:** User job selection
- **Outputs / Expected Results:** Expense associated with selected job(s) or marked as general
- **Error Handling / Alternate Flows:**
  - If no jobs exist, provide guidance for job creation
  - If job list is large, provide search/filter capabilities
  - Allow marking as "General Business Expense" for non-job expenses
- **Acceptance Criteria:**
  - **Given** a user with active jobs
  - **When** they need to associate an expense with job(s)
  - **Then** they should be able to select from a list of all their jobs
  
  - **Given** a user with many jobs
  - **When** they access the job selection interface
  - **Then** they should be able to search or filter the job list
  
  - **Given** a user creating an expense not related to specific jobs
  - **When** they use the job selection interface
  - **Then** they should be able to mark it as a "General Business Expense"
- **Dependencies:** Job database, Search/filter functionality

### REQ-ME-07: Multi-Job Expense Allocation

- **Title:** Multi-Job Expense Allocation
- **Description:** System must provide an interface for allocating portions of an expense across multiple jobs
- **Actors:** Business owner
- **Trigger:** User selects multiple jobs for an expense
- **Pre-conditions:** Expense data confirmed, Multiple jobs selected
- **Functional Steps (Happy Path):**
  1. System displays allocation interface with selected jobs
  2. System presents options for allocation method (equal split, percentage, direct amounts)
  3. User specifies allocation using preferred method
  4. System validates that allocations sum to total expense amount
  5. User confirms final allocation
- **Inputs:** User allocation decisions
- **Outputs / Expected Results:** Expense correctly divided across selected jobs
- **Error Handling / Alternate Flows:**
  - If allocations don't sum to total, highlight discrepancy and prevent proceeding
  - Provide quick options for common scenarios (equal split, 50/50, etc.)
  - Allow adjustment of individual allocations until sum matches total
- **Acceptance Criteria:**
  - **Given** an expense associated with multiple jobs
  - **When** the user accesses the allocation interface
  - **Then** they should be presented with multiple allocation methods
  
  - **Given** a user attempting to allocate an expense across jobs
  - **When** the allocations don't sum to the total expense amount
  - **Then** the system should highlight the discrepancy and prevent proceeding
  
  - **Given** a $100 expense allocated 60% to Job A and 40% to Job B
  - **When** the expense is saved
  - **Then** Job A should be associated with $60 and Job B with $40
- **Dependencies:** Job database, Calculation engine

### REQ-ME-08: Expense Categorization

- **Title:** Expense Categorization
- **Description:** System must allow users to categorize expenses for reporting and analysis
- **Actors:** Business owner
- **Trigger:** During expense creation after job association
- **Pre-conditions:** Expense data and job association confirmed
- **Functional Steps (Happy Path):**
  1. System displays list of expense categories
  2. System may suggest category based on vendor name or previous patterns
  3. User selects appropriate category
  4. System confirms selection
- **Inputs:** User category selection
- **Outputs / Expected Results:** Expense properly categorized
- **Error Handling / Alternate Flows:**
  - Suggest categories based on vendor name from OCR or user history
  - Allow creation of ad-hoc categories if needed (future enhancement)
  - Set default category for quick processing
- **Acceptance Criteria:**
  - **Given** a user creating an expense
  - **When** they reach the categorization step
  - **Then** they should be presented with a list of predefined categories
  
  - **Given** an expense with vendor information
  - **When** the system has historical data for that vendor
  - **Then** it should suggest the most commonly used category
  
  - **Given** a user who frequently categorizes "Shell" as "Fuel"
  - **When** they process a new "Shell" expense
  - **Then** the system should suggest "Fuel" category
- **Dependencies:** Category database, Historical pattern analysis

### REQ-ME-09: Conditional Tax Detail Capture

- **Title:** Conditional Tax Detail Capture
- **Description:** If tax features are enabled, system must capture and process tax-related details from expenses
- **Actors:** Business owner
- **Trigger:** User has tax features enabled and is creating an expense
- **Pre-conditions:** Expense data confirmed, User has enabled tax features via Tax Registration Status
- **Functional Steps (Happy Path):**
  1. System checks if tax features are enabled for user
  2. If enabled, system attempts to extract GST/QST amounts from receipt via OCR
  3. System displays extracted tax information for confirmation
  4. User confirms or corrects tax information
  5. System flags potential Input Tax Credits based on category and tax presence
- **Inputs:** Receipt image (for OCR) or manually entered tax data
- **Outputs / Expected Results:** Correctly captured tax details for the expense
- **Error Handling / Alternate Flows:**
  - If tax extraction fails, prompt for manual tax entry
  - If tax module is not enabled, skip tax capture steps entirely
  - Allow manual tax entry if OCR confidence is low
- **Acceptance Criteria:**
  - **Given** a user with tax features enabled
  - **When** they create an expense
  - **Then** the system should present tax capture fields
  
  - **Given** a receipt with visible tax amounts
  - **When** processed through OCR with tax features enabled
  - **Then** the system should attempt to extract GST/QST amounts
  
  - **Given** a user with tax features disabled
  - **When** they create an expense
  - **Then** no tax capture steps should be presented
- **Dependencies:** OCR service, Tax module activation status, Tax rules database

### REQ-ME-10: Offline Data Handling

- **Title:** Offline Data Handling
- **Description:** System must provide offline capabilities for essential expense tracking functions
- **Actors:** Business owner, System
- **Trigger:** User attempts expense tracking with limited or no connectivity
- **Pre-conditions:** Authentication valid, Basic app data cached
- **Functional Steps (Happy Path):**
  1. System detects limited or no connectivity
  2. System notifies user of offline mode and limitations
  3. User creates expense using manual entry with cached job list
  4. System stores expense data and receipt image locally
  5. System queues record for synchronization
  6. When connectivity returns, system synchronizes data and processes pending tasks
- **Inputs:** Expense data, Receipt image, Connectivity status
- **Outputs / Expected Results:** Local storage of expense data, Successful sync when online
- **Error Handling / Alternate Flows:**
  - Clearly indicate sync status (pending, completed, failed)
  - Handle sync conflicts with appropriate resolution strategy
  - Manage storage constraints for offline image capture
  - Provide manual sync trigger option
- **Acceptance Criteria:**
  - **Given** a user with no internet connection
  - **When** they attempt to create an expense
  - **Then** they should be able to enter basic expense data and capture receipt image
  
  - **Given** expense data created offline
  - **When** internet connectivity is restored
  - **Then** the system should automatically synchronize the pending data
  
  - **Given** a receipt captured offline
  - **When** internet connectivity is restored
  - **Then** the system should process pending OCR tasks
  
  - **Given** a synchronization process
  - **When** conflicts are detected
  - **Then** the system should resolve them using the defined conflict resolution strategy
- **Dependencies:** Offline storage system, Sync queue management, Connectivity detection

### REQ-ME-11: Expense Data Validation

- **Title:** Expense Data Validation
- **Description:** System must validate expense data before saving to ensure data integrity
- **Actors:** Business owner, System
- **Trigger:** User attempts to save expense
- **Pre-conditions:** Expense data entered/confirmed
- **Functional Steps (Happy Path):**
  1. System validates required fields are completed
  2. System validates data formats (date, numeric amount)
  3. System validates business rules (allocation sum matches total)
  4. If all validations pass, system saves the expense
- **Inputs:** Completed expense data
- **Outputs / Expected Results:** Validated expense record
- **Error Handling / Alternate Flows:**
  - For missing required fields, highlight and prevent saving
  - For format errors, show inline guidance
  - For business rule violations, explain the issue clearly
- **Acceptance Criteria:**
  - **Given** an expense with missing required fields
  - **When** the user attempts to save
  - **Then** the system should highlight missing fields and prevent saving
  
  - **Given** an expense with amount entered as text
  - **When** validation occurs
  - **Then** the system should flag the format error
  
  - **Given** a multi-job expense with incorrect allocation total
  - **When** the user attempts to save
  - **Then** the system should alert the user that allocations must equal the total amount
- **Dependencies:** Validation rule engine, Form field mapping

### REQ-ME-12: Expense Confirmation and Feedback

- **Title:** Expense Confirmation and Feedback
- **Description:** System must provide clear confirmation and feedback when expenses are saved
- **Actors:** Business owner
- **Trigger:** Expense is successfully saved
- **Pre-conditions:** All validations passed, Data stored locally or synchronized
- **Functional Steps (Happy Path):**
  1. System saves expense data and confirms success
  2. System displays confirmation message with summary
  3. System offers next action options (add another, view details, return to list)
  4. User selects desired next action
- **Inputs:** User next action selection
- **Outputs / Expected Results:** Appropriate confirmation and navigation
- **Error Handling / Alternate Flows:**
  - If save fails due to technical issues, store locally and retry
  - Provide sync status for expenses saved offline
  - Allow review of saved expense details
- **Acceptance Criteria:**
  - **Given** an expense is successfully saved
  - **When** the save operation completes
  - **Then** the user should see a clear confirmation message with summary information
  
  - **Given** an expense is saved successfully
  - **When** the confirmation is displayed
  - **Then** the user should be presented with logical next action options
  
  - **Given** an expense saved in offline mode
  - **When** the confirmation is displayed
  - **Then** the sync status should be clearly indicated
- **Dependencies:** Notification system, Navigation controller

## Mockups

[Link to Mockups](./mockups/index.html)