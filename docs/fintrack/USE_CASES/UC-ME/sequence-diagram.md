# Mobile Expense Tracking - Sequence Diagram

This document illustrates the sequence of interactions between system components for the core mobile expense tracking workflows.

## Primary Flow: Online Receipt Capture & Processing

```mermaid
sequenceDiagram
    participant User
    participant MobileApp
    participant CameraModule
    participant OCRService
    participant LocalDB
    participant SyncService
    participant CloudAPI
    participant StorageService

    User->>MobileApp: Launch expense capture
    MobileApp->>CameraModule: Initialize camera
    CameraModule->>User: Display camera view with guidance
    User->>CameraModule: Capture receipt
    CameraModule->>MobileApp: Return receipt image
    MobileApp->>MobileApp: Preprocess image (enhance, crop)
    MobileApp->>MobileApp: Display loading indicator
    MobileApp->>OCRService: Submit image for processing
    OCRService-->>MobileApp: Return extracted data with confidence scores
    MobileApp->>MobileApp: Parse OCR results
    MobileApp->>User: Display extracted data for verification
    User->>MobileApp: Edit/confirm data fields
    MobileApp->>MobileApp: Show job suggestions
    User->>MobileApp: Select job(s) for allocation

    alt Multiple jobs selected
        MobileApp->>User: Display allocation interface
        User->>MobileApp: Enter allocation percentages/amounts
        MobileApp->>MobileApp: Validate allocation totals
    end

    MobileApp->>User: Display category selection
    User->>MobileApp: Select expense category

    alt Tax module enabled
        MobileApp->>User: Display tax details screen
        User->>MobileApp: Verify/edit tax information
    end

    MobileApp->>User: Show confirmation screen
    User->>MobileApp: Confirm expense submission
    MobileApp->>LocalDB: Store expense data (status='synced' or 'pending_sync') and receipt image
    MobileApp->>User: Display success message

    MobileApp->>SyncService: Queue expense for synchronization
    SyncService->>CloudAPI: Sync expense metadata
    CloudAPI-->>SyncService: Confirm metadata sync
    SyncService->>StorageService: Upload receipt image
    StorageService-->>SyncService: Confirm image upload
    SyncService->>CloudAPI: Update expense with image reference
    CloudAPI-->>SyncService: Confirm update
    SyncService->>LocalDB: Update sync status
    SyncService->>MobileApp: Notify sync complete
    MobileApp->>User: Update expense status indicator
```

## Alternative Flow: Offline Receipt Capture

```mermaid
sequenceDiagram
    participant User
    participant MobileApp
    participant CameraModule
    participant LocalDB
    participant ConnectivityMonitor
    participant SyncService
    participant OCRService
    participant CloudAPI

    User->>MobileApp: Launch expense capture
    MobileApp->>ConnectivityMonitor: Check connectivity
    ConnectivityMonitor-->>MobileApp: Return offline status
    MobileApp->>User: Show offline mode indicator
    MobileApp->>CameraModule: Initialize camera
    User->>CameraModule: Capture receipt
    CameraModule->>MobileApp: Return receipt image
    MobileApp->>LocalDB: Store receipt image locally
    MobileApp->>User: Display manual data entry form
    User->>MobileApp: Enter expense details manually (if possible/desired)
    MobileApp->>User: Select job (from cache) and category (if possible)
    User->>MobileApp: Complete manual entry or opt to save minimal data
    MobileApp->>LocalDB: Save expense (status='draft' if incomplete, 'pending_sync' if complete)
    MobileApp->>SyncService: Queue for future sync
    MobileApp->>User: Confirm offline save (indicating draft status if applicable)

    Note over ConnectivityMonitor: Later, when connectivity is restored

    ConnectivityMonitor->>SyncService: Notify connectivity restored
    SyncService->>LocalDB: Retrieve pending offline expenses
    loop For each expense needing OCR
        SyncService->>OCRService: Process queued receipt image
        OCRService-->>SyncService: Return OCR results
        SyncService->>LocalDB: Update expense with OCR data (potentially still 'draft' if user interaction needed)
    end
    SyncService->>CloudAPI: Sync expense data (completed or draft needing review)
    CloudAPI-->>SyncService: Confirm sync
    SyncService->>MobileApp: Notify sync complete (may require user action for drafts)
    MobileApp->>User: Show sync completion notification / prompt for draft review
```

## New Flow: Deferred Processing (Online)

```mermaid
sequenceDiagram
    participant User
    participant MobileApp
    participant CameraModule
    participant LocalDB
    participant SyncService
    participant CloudAPI
    participant StorageService
    participant OCRService

    User->>MobileApp: Launch expense capture
    MobileApp->>CameraModule: Initialize camera
    User->>CameraModule: Capture receipt
    CameraModule->>MobileApp: Return receipt image
    MobileApp->>MobileApp: Preprocess image (optional quick enhance)
    MobileApp->>User: Display preview & option to 'Save Draft'
    User->>MobileApp: Select 'Save Draft'
    MobileApp->>LocalDB: Store receipt image
    MobileApp->>LocalDB: Create Expense record (status='draft', minimal data, link to image)
    LocalDB-->>MobileApp: Confirm local save
    MobileApp->>User: Confirm 'Draft Saved' and return to previous screen

    Note over MobileApp, User: Later, User accesses Draft Expense (e.g., via UC-EL)

    User->>MobileApp: Select Draft Expense to resume
    MobileApp->>LocalDB: Retrieve Draft Expense data and image
    LocalDB-->>MobileApp: Return draft data/image
    MobileApp->>MobileApp: Initiate processing (e.g., trigger OCR)
    MobileApp->>OCRService: Submit image for processing (if not done initially)
    OCRService-->>MobileApp: Return extracted data
    MobileApp->>User: Display extracted data for verification (similar to Primary Flow Step 4 onwards)
    User->>MobileApp: Complete verification, allocation, categorization, tax (if applicable)
    User->>MobileApp: Confirm final submission
    MobileApp->>LocalDB: Update Expense record (status changed from 'draft')
    MobileApp->>User: Display success message

    MobileApp->>SyncService: Queue expense for synchronization (standard sync process)
    SyncService->>CloudAPI: Sync updated expense data
    CloudAPI-->>SyncService: Confirm sync
    alt Receipt Image not yet synced
        SyncService->>StorageService: Upload receipt image
        StorageService-->>SyncService: Confirm image upload
        SyncService->>CloudAPI: Update expense with image reference
        CloudAPI-->>SyncService: Confirm update
    end
    SyncService->>LocalDB: Update sync status
    SyncService->>MobileApp: Notify sync complete
```

## Expense Allocation Flow

```mermaid
sequenceDiagram
    participant User
    participant MobileApp
    participant JobService
    participant ExpenseService
    participant LocalDB

    User->>MobileApp: Access job allocation screen
    MobileApp->>JobService: Request active jobs
    JobService->>LocalDB: Query active jobs
    LocalDB-->>JobService: Return job list
    JobService->>MobileApp: Return job data

    MobileApp->>MobileApp: Sort jobs by relevance
    Note over MobileApp: Sort based on location,<br/>recent usage, etc.

    MobileApp->>User: Display job suggestions
    User->>MobileApp: Select multiple jobs
    MobileApp->>User: Display allocation interface

    User->>MobileApp: Enter percentage for Job A
    MobileApp->>ExpenseService: Calculate remaining allocation
    ExpenseService-->>MobileApp: Return updated allocations
    MobileApp->>User: Update allocation display

    User->>MobileApp: Enter amount for Job B
    MobileApp->>ExpenseService: Recalculate allocations
    ExpenseService-->>MobileApp: Return updated values
    MobileApp->>User: Update allocation display

    User->>MobileApp: Confirm final allocation
    MobileApp->>ExpenseService: Validate total allocation

    alt Invalid allocation
        ExpenseService-->>MobileApp: Return validation error
        MobileApp->>User: Display error message
    else Valid allocation
        ExpenseService-->>MobileApp: Confirm valid allocation
        MobileApp->>LocalDB: Store allocation data
        MobileApp->>User: Proceed to next step
    end
```

## Conflict Resolution Flow

```mermaid
sequenceDiagram
    participant UserDeviceA
    participant AppDeviceA
    participant SyncService
    participant CloudAPI
    participant WebApp
    participant UserWeb

    Note over UserDeviceA,UserWeb: Expense created on Device A and synced

    UserDeviceA->>AppDeviceA: Create expense
    AppDeviceA->>SyncService: Sync expense
    SyncService->>CloudAPI: Upload expense
    CloudAPI-->>SyncService: Confirm sync

    Note over AppDeviceA: Device goes offline

    UserWeb->>WebApp: Edit same expense
    WebApp->>CloudAPI: Update expense
    CloudAPI-->>WebApp: Confirm update

    UserDeviceA->>AppDeviceA: Edit expense offline
    AppDeviceA->>AppDeviceA: Store local changes

    Note over AppDeviceA: Device back online

    AppDeviceA->>SyncService: Attempt to sync changes
    SyncService->>CloudAPI: Check for conflicts
    CloudAPI-->>SyncService: Return conflict details
    SyncService->>AppDeviceA: Report sync conflict

    AppDeviceA->>UserDeviceA: Display conflict resolution UI
    UserDeviceA->>AppDeviceA: Select resolution option

    alt Keep device version
        AppDeviceA->>SyncService: Force upload device version
        SyncService->>CloudAPI: Override with local version
    else Keep cloud version
        AppDeviceA->>SyncService: Request cloud version
        SyncService->>CloudAPI: Get latest version
        CloudAPI-->>SyncService: Return cloud version
        SyncService->>AppDeviceA: Update with cloud version
    else Merge changes
        AppDeviceA->>UserDeviceA: Show merge interface
        UserDeviceA->>AppDeviceA: Select fields to keep
        AppDeviceA->>SyncService: Sync merged version
        SyncService->>CloudAPI: Update with merged version
    end

    CloudAPI-->>SyncService: Confirm resolution
    SyncService->>AppDeviceA: Update sync status
    AppDeviceA->>UserDeviceA: Show resolution confirmation
```

## System Component Overview

The sequence diagrams above reference the following key system components:

1.  **MobileApp**: The user-facing mobile application interface
2.  **CameraModule**: Handles camera access and image capture functionality
3.  **OCRService**: Performs optical character recognition on receipt images
4.  **LocalDB**: Local database for offline storage and caching (including Draft Expenses)
5.  **SyncService**: Manages data synchronization between local and cloud storage
6.  **CloudAPI**: Server-side API for data persistence and processing
7.  **StorageService**: Cloud storage service for receipt images
8.  **ConnectivityMonitor**: Monitors network connectivity status
9.  **JobService**: Manages job data and related operations
10. **ExpenseService**: Handles expense-related business logic and operations

These components work together to provide a seamless expense tracking experience for the user, with robust offline capabilities, data synchronization, and support for **Deferred Processing** of expenses.