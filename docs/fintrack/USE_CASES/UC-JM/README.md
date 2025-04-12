# Use Case: Job Management

## Refined Description

### Overview
The Job Management use case enables business owners to create, view, and manage jobs, associate them with clients, track job status, and view job history. It provides a foundation for tracking profitability and organizing work by client, status, and service type. This use case is core functionality in the FinTrack application. The current implementation focuses on one-time jobs, with future plans to support recurring jobs and on-demand/condition-triggered jobs.

### Actors
- Primary: Business owner

### Trigger(s)
- User accesses Job Management section of the application
- User selects "Add New Job" option
- User selects an existing job to view or edit details
- User needs to search for specific jobs

### Pre-conditions
- User is authenticated in the application
- At least one client exists in the system for job association (for new job creation)

### Primary Path
1. User accesses the Job Management section and views the Job List
2. System displays list of existing jobs with key details (Name/Description, Client, Status, Start Date)
3. User selects "Add New Job" option
4. System presents job creation form
5. User enters job details (Name/Description, Location, Service Type, Start Date)
6. User associates the job with an existing client by selecting from client list
7. User sets initial job status (e.g., Planned, In-Progress)
8. User saves the new job information
9. System confirms job creation and displays updated job list
10. User can select an existing job to view its details
11. User can update job status (e.g., mark as Complete)
12. User can use search/filter function to find specific jobs by client or status

### Alternate Paths

#### A1: Duplicate Job Creation
1. At step 3, user selects an existing job and chooses "Duplicate Job" option
2. System pre-fills job creation form with details from the selected job
3. User modifies any details as needed
4. User saves the new job information
5. Flow continues from step 9 of primary path

#### A2: Quick Job Creation
1. At step 5, user enters only minimum required information (Name, Client)
2. User opts to save with minimal information
3. System creates job with default values for other fields
4. User can update job details later
5. Flow continues from step 9 of primary path

#### A3: Job Service Type Change
1. After job creation, user selects an existing job to edit
2. User changes the service type (e.g., from Landscaping to Snow Removal)
3. System adjusts relevant service-specific fields if applicable
4. User confirms the changes
5. System updates the job records

#### A4: Client Transfer
1. User selects an existing job and chooses "Edit Job" option
2. User changes the client association to a different client
3. User confirms the change
4. System updates the job with new client association

### Exception Paths

#### E1: Offline Job Creation Attempt
1. User attempts to create a new job while offline
2. System notifies user that job creation requires internet connectivity
3. System offers to save job details locally as a draft for later submission
4. When connectivity is restored, system prompts user to complete job creation

#### E2: Missing Required Fields
1. At step 8, system validates that minimum required fields are completed
2. If validation fails, system highlights missing fields and prevents saving
3. User completes required information and attempts to save again

#### E3: Invalid Date Range
1. User enters a job end date that is before the start date
2. System displays an error message and prevents saving
3. User corrects the date information and attempts to save again

#### E4: Search With No Results
1. User enters search criteria that don't match any jobs
2. System displays an appropriate "No Results" message
3. System offers search refinement suggestions
4. User modifies search criteria or returns to the full job list

### Actors
- Business owner

### Trigger(s)
- User navigates to job management section
- User selects "Add New Job" option
- User selects an existing job to view or manage

### Pre-conditions
- User is authenticated in the system
- User has permission to manage jobs
- At least one client exists in the system (for job creation)

### Expected Outcome
Jobs are successfully created and tracked with proper client associations, allowing expenses and income to be correctly allocated for profitability analysis across various service types. Users can easily find, view, and update jobs based on client, status, and other criteria, even with limited connectivity.

## Functional Requirements

### REQ-JM-01: Job List View

- **REQ-ID:** REQ-JM-01
- **Title:** Job List View
- **Description:** System must provide a list view of all jobs with key details and sorting/filtering options
- **Actors:** Business owner
- **Trigger:** User accesses Job Management section
- **Pre-conditions:** User is authenticated
- **Functional Steps (Happy Path):**
  1. System retrieves list of jobs associated with the user's business
  2. System displays jobs in a list format with key details (Name/Description, Client, Status, Dates)
  3. System provides sorting options (by name, date, status, client)
  4. System caches job list data for offline access
- **Inputs:** Optional filter criteria
- **Outputs / Expected Results:** Organized, sortable list of jobs
- **Error Handling / Alternate Flows:**
  - If no jobs exist, show appropriate empty state with easy job creation option
  - If offline, display cached job list with offline indicator
  - If system cannot retrieve jobs, show error message with retry option
- **Acceptance Criteria:**
  - **Given** a business owner with multiple jobs
  - **When** they access the Job Management section
  - **Then** they should see a list of all jobs with key details
  
  - **Given** a business owner viewing the job list
  - **When** they tap a column header or sort control
  - **Then** the list should re-sort based on the selected criterion
  
  - **Given** a business owner in offline mode
  - **When** they access the Job Management section
  - **Then** they should see a cached version of their job list with offline indicator
- **Dependencies:** Authentication system, Data caching mechanism

### REQ-JM-02: Job Creation

- **REQ-ID:** REQ-JM-02
- **Title:** Job Creation
- **Description:** System must allow creation of new jobs with essential details
- **Actors:** Business owner
- **Trigger:** User selects "Add New Job" option
- **Pre-conditions:** User is authenticated and online
- **Functional Steps (Happy Path):**
  1. System displays job creation form
  2. User enters job details (Name/Description, Location, Service Type, Start Date)
  3. User associates job with client (REQ-JM-03)
  4. User sets initial job status
  5. System validates required fields
  6. User submits form
  7. System creates job record and confirms creation
- **Inputs:** Job Name/Description, Location, Service Type, Start Date, End Date (optional), Client association, Initial Status
- **Outputs / Expected Results:** New job record created in system
- **Error Handling / Alternate Flows:**
  - If required fields are missing, highlight them and prevent submission
  - If date validation fails (e.g., end date before start date), show error
  - If offline, offer to save draft locally for later submission
- **Acceptance Criteria:**
  - **Given** a business owner wants to create a new job
  - **When** they complete all required fields and submit the form
  - **Then** the system should create the job and show confirmation
  
  - **Given** a business owner submits incomplete job information
  - **When** they try to save the job
  - **Then** the system should highlight missing required fields and prevent submission
  
  - **Given** a business owner enters an end date before the start date
  - **When** they try to save the job
  - **Then** the system should display an error message and prevent submission
- **Dependencies:** Client Management system (UC-CM), Form validation

### REQ-JM-03: Job-Client Association

- **REQ-ID:** REQ-JM-03
- **Title:** Job-Client Association
- **Description:** System must allow jobs to be associated with existing clients
- **Actors:** Business owner
- **Trigger:** User is creating or editing a job
- **Pre-conditions:** At least one client exists in the system
- **Functional Steps (Happy Path):**
  1. System retrieves list of existing clients
  2. System displays clients in a selection interface (dropdown, searchable list)
  3. User selects a client to associate with the job
  4. System confirms selection and links job to selected client
- **Inputs:** Client selection
- **Outputs / Expected Results:** Job correctly associated with selected client
- **Error Handling / Alternate Flows:**
  - If no clients exist, prompt user to create a client first with link to client creation
  - If client list is large, provide search functionality to easily find clients
- **Acceptance Criteria:**
  - **Given** a business owner is creating a new job
  - **When** they need to associate it with a client
  - **Then** they should see a list of existing clients to select from
  
  - **Given** a business owner is editing a job
  - **When** they change the client association
  - **Then** the system should update the job with the new client association

  - **Given** a business owner with no existing clients
  - **When** they try to create a job
  - **Then** the system should prompt them to create a client first
- **Dependencies:** Client Management system (UC-CM)

### REQ-JM-04: Job Details View

- **REQ-ID:** REQ-JM-04
- **Title:** Job Details View
- **Description:** System must provide a detailed view of individual job information
- **Actors:** Business owner
- **Trigger:** User selects a specific job from the job list
- **Pre-conditions:** User is authenticated and has access to the job
- **Functional Steps (Happy Path):**
  1. User selects a job from the job list
  2. System retrieves comprehensive job details
  3. System displays job details including:
     - Basic info (Name, Description, Service Type)
     - Client information
     - Status and dates
     - Location details
     - Associated expenses (summary)
     - Associated income (summary)
     - Profit calculation
     - Job notes
  4. System provides edit options for relevant fields
- **Inputs:** Job ID/selection
- **Outputs / Expected Results:** Comprehensive view of job details
- **Error Handling / Alternate Flows:**
  - If job details cannot be retrieved, show error with retry option
  - If offline, show cached job details with offline indicator and limited editing
- **Acceptance Criteria:**
  - **Given** a business owner selects a job from the list
  - **When** the job details screen loads
  - **Then** they should see all relevant job information in a well-organized layout
  
  - **Given** a business owner is viewing job details
  - **When** they are in offline mode
  - **Then** they should see cached information with an offline indicator
  
  - **Given** a business owner is viewing job details
  - **When** they need to update job information
  - **Then** they should have access to edit functionality for appropriate fields
- **Dependencies:** Expense tracking system (UC-ME), Income tracking system

### REQ-JM-05: Job Status Management

- **REQ-ID:** REQ-JM-05
- **Title:** Job Status Management
- **Description:** System must allow users to update and track job status
- **Actors:** Business owner
- **Trigger:** User needs to update job status
- **Pre-conditions:** Job exists in the system
- **Functional Steps (Happy Path):**
  1. User accesses job details or selects status update option from list
  2. System displays available status options (Planned, In-Progress, Complete, etc.)
  3. User selects new status
  4. System updates job status and records change timestamp
- **Inputs:** Status selection
- **Outputs / Expected Results:** Job status updated in system
- **Error Handling / Alternate Flows:**
  - If offline, queue status update for sync when connectivity returns
  - If status change requires confirmation (e.g., marking complete), show confirmation dialog
- **Acceptance Criteria:**
  - **Given** a business owner viewing a job
  - **When** they update the job status
  - **Then** the system should save the new status and timestamp
  
  - **Given** a business owner updates job status while offline
  - **When** connectivity is restored
  - **Then** the system should sync the status update
  
  - **Given** a business owner tries to mark a job as complete
  - **When** they select the complete status
  - **Then** the system should request confirmation before finalizing
- **Dependencies:** Offline synchronization system

### REQ-JM-06: Job Search and Filtering

- **REQ-ID:** REQ-JM-06
- **Title:** Job Search and Filtering
- **Description:** System must provide search and filtering functionality for jobs
- **Actors:** Business owner
- **Trigger:** User needs to find specific jobs
- **Pre-conditions:** User is viewing the job list
- **Functional Steps (Happy Path):**
  1. User enters search term or selects filter criteria (client, status, date range, service type)
  2. System applies search/filter to job list
  3. System displays filtered results
  4. User can clear filters/search to return to full list
- **Inputs:** Search term, Filter selections
- **Outputs / Expected Results:** Filtered list of jobs matching criteria
- **Error Handling / Alternate Flows:**
  - If no results match criteria, display appropriate "No Results" message
  - If offline, search only within cached job data
- **Acceptance Criteria:**
  - **Given** a business owner with many jobs
  - **When** they search for a specific job by name
  - **Then** the system should display only jobs matching the search term
  
  - **Given** a business owner needs to view all jobs for a specific client
  - **When** they filter by that client
  - **Then** the system should display only jobs for that client
  
  - **Given** a business owner applies a filter
  - **When** no jobs match the filter criteria
  - **Then** the system should display a meaningful "No Results" message
- **Dependencies:** Search indexing system

### REQ-JM-07: Job Offline Access

- **REQ-ID:** REQ-JM-07
- **Title:** Job Offline Access
- **Description:** System must provide offline access to job information
- **Actors:** Business owner
- **Trigger:** User accesses job information while offline
- **Pre-conditions:** User has previously accessed jobs while online
- **Functional Steps (Happy Path):**
  1. System detects offline status
  2. System displays cached job list and job details
  3. System clearly indicates offline mode
  4. System limits editing capabilities to operations that can be queued
- **Inputs:** None
- **Outputs / Expected Results:** Read access to previously accessed job information
- **Error Handling / Alternate Flows:**
  - If no cached data exists, show appropriate message
  - Queue any allowed offline changes for sync when connectivity returns
  - Clearly indicate which operations are unavailable offline
- **Acceptance Criteria:**
  - **Given** a business owner loses internet connectivity
  - **When** they access the job management section
  - **Then** they should see previously loaded job information
  
  - **Given** a business owner is in offline mode
  - **When** they try to create a new job
  - **Then** the system should explain that job creation requires connectivity
  
  - **Given** a business owner makes allowed changes in offline mode
  - **When** connectivity is restored
  - **Then** the system should automatically sync pending changes
- **Dependencies:** Offline data cache, Synchronization system

## Mockups

[Link to Mockups](./mockups/index.html)
