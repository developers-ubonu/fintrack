# FinTrack: Detailed MVP Feature Scope

## Document Metadata
**Version:** 1.4 *(Updated based on "Ideal Onboarding" requirements)* 
**Status:** Draft
**Last Updated:** April 8, 2025
**Owner:** FinTrack Product Manager
**Reviewers:** Technical Lead, UX Designer, Business Stakeholder

## Purpose
This document defines the detailed feature scope for the FinTrack Minimum Viable Product (MVP), establishing clear boundaries for what will and will not be included in the initial release. The scope is based on user needs analysis, interview findings, technical feasibility assessment, and the decision to incorporate key ease-of-use automation features from the outset.

## MVP Guiding Principles
*(Updated Section)*
The following principles guide our MVP scope decisions:

1.  **Focus on Core Value Proposition:** Prioritize features that directly address job profitability tracking and *effortless* expense management for landscaping businesses.
2.  **Mobile-First & Field Optimized:** Design for field use with reliable offline functionality for critical operations and minimal user input.
3.  **Simplicity & **Effortless Input:** Keep the interface intuitive and workflows streamlined, leveraging automation to minimize manual data entry.
4.  **Quebec Tax Compliance:** Ensure proper handling of GST/QST for Quebec-based businesses, including capturing relevant tax data easily.
5.  **Bilingual Support:** Support both English and French throughout the application.
6.  **Reliability Over Breadth:** Ensure core features, including automation, work reliably in challenging connectivity environments.

## Feature Categories

### 1. Account Settings & Profile

#### Included in MVP:
* User account creation and authentication
* Basic user profile with business information
* Language preference setting (English/French)
* Password reset functionality
* Account security features (2FA optional but available)
* Terms of service and privacy policy acceptance

#### Not Included in MVP:
* Multi-user access (owner + employees)
* Role-based permissions
* Team collaboration features
* User activity logs/audit trails
* Social media login options

### 2. Client Management

#### Included in MVP:
* **Add, Edit, and View Clients:** Manage basic client information including:
    * Name (business and contact person)
    * Contact information (phone, email, address)
    * Language preference
    * Default tax settings (GST/QST applicable or not)
* Client listing with search and filter
* Client data access in offline mode (read-only)
* Client details page with associated jobs and invoices
* Basic client status (active/inactive)

#### Not Included in MVP:
* Client onboarding workflow
* Client portal/access
* Advanced client categorization or tagging
* Client communication history
* Client creation in offline mode
* Custom client fields
* Client document storage
* Automated client communications

### 3. Job Management

#### Included in MVP:
* Job creation with basic details:
    * Client association
    * Job name/description
    * Location
    * Service type (landscaping or snow removal, flexible)
    * Start and expected end dates
    * Job status (upcoming, in-progress, complete)
* Job listing with search and filter by status/client
* Job profitability calculation (revenue - expenses - contractor payments)
* Basic job notes
* Job access in offline mode (read-only)

#### Not Included in MVP:
* Detailed job scheduling
* Job recurrence patterns
* Job templates
* Staff assignment and tracking
* Materials inventory integration
* Job creation in offline mode
* Job checklist or completion criteria
* Job photo gallery
* Job map/route integration
* Advanced job costing (labor rates, equipment rates)
* Job estimation/quoting features

### 4. Expense Tracking *(Revised Section)*

#### Included in MVP:
* **Receipt Capture with Automated Data Extraction (OCR):** Capture receipt images via camera, with the system attempting to automatically extract key details (Vendor, Date, Amount, and GST/QST details). (Note: Basic OCR, user confirms/edits).
* **Manual Expense Entry:** Option for quick manual entry if no receipt or OCR fails.
* **Expense Categorization:** Organize expenses by type (Fuel, Materials, Rentals, Contractor Payments, etc., from predefined list).
* **Context-Aware Job Suggestions:** App suggests likely job associations based on context (e.g., location, calendar, recent activity). User confirms or selects manually.
* **Simple Expense Splitting UI:** Intuitive interface (e.g., sliders, simple amount entry) to allocate a single expense (esp. consumables, contractor pay) across multiple selected jobs.
* **Mark as General Expense:** Easily tag expenses not related to a specific job.
* Offline expense entry capability (manual data, photo capture, basic job selection from cache) with sync. *(Note: OCR/Smart Suggestions may require connectivity)*.
* Expense listing with search and filter.
* Basic expense reports (by category, by job, by date range).

#### Not Included in MVP:
* *Advanced* OCR validation or line-item extraction.
* Recurring expense setup.
* Mileage tracking (though GPS context may be used for suggestions).
* Per diem tracking.
* Expense approval workflows.
* Multiple receipt images per expense.
* Custom expense categories (rely on predefined list initially).
* Advanced expense reports and analytics.
* Bank feed/credit card integration for automatic import.

### 5. Invoice Management

#### Included in MVP:
* Invoice creation with:
    * Client association
    * Job association
    * Line items with descriptions
    * Tax calculations (GST/QST)
    * Due date
    * Payment terms
    * Business logo and basic customization
* PDF invoice generation
* Email invoice sending capability
* Invoice listing with status (draft, sent, paid, overdue)
* Basic invoice templates (1-2 options)
* Mark invoice as paid functionality
* Partial payment recording

#### Not Included in MVP:
* Invoice creation in offline mode
* Recurring invoice setup
* Online payment acceptance
* Advanced invoice customization
* Multiple invoice templates
* Invoice reminders
* Invoice late fees calculation
* Invoice time tracking integration
* Client invoice portal
* Batch invoice operations
* Contract/quote to invoice conversion

### 6. Contractor Management *(Revised Section)*

#### Included in MVP:
* **Add and Edit Contractors:** Ability to create new contractor records and modify existing ones.
* **Contractor Contact Storage:** Store basic contractor contact information (e.g., Name, Phone, Email).
* **Contractor List/View:** View a list of contractors, potentially with search/filter.
* **Contractor Payment Recording:** Record payments made to contractors (date, amount, method), linking payment to the contractor. Includes:
    * **Context-Aware Job Suggestions:** Suggests jobs the contractor is associated with.
    * **Simple Splitting UI:** Use the same intuitive interface as expenses to allocate payments across multiple jobs.

#### Not Included in MVP:
* Advanced contractor details (Service specialization, Tax ID, Insurance docs)
* Contractor-specific contracts or agreements
* Assigning contractors directly to jobs (Association primarily via payments/context)
* Contractor onboarding workflows
* Contractor time tracking
* Contractor communication tools

### 7. Financial Reporting

#### Included in MVP:
* Job profitability report
* Income by client/job report
* Expenses by category report
* Basic cash flow report
* GST/QST summary report for tax filing
* Weekly profit summary view
* Current month vs. previous month comparison
* Export reports to CSV/PDF

#### Not Included in MVP:
* Custom report builder
* Advanced financial analytics
* Seasonal trend analysis
* Benchmark comparisons
* Advanced filtering and report parameters
* Balance sheet and P&L statements
* Dashboard customization
* Profit margin analysis by job type
* Forecasting or budgeting tools
* Graphical/chart visualizations (limited in MVP)

### 8. Tax Features

#### Included in MVP:
* GST/QST calculation on invoices
* Input tax credit tracking on expenses (with data ideally captured via OCR)
* Basic tax summary reports for filing periods
* Tax settings configuration
* Tax information resources specific to Quebec (links to official sources)
* Tax thresholds notification

#### Not Included in MVP:
* Auto-filing integration with tax authorities
* Advanced tax planning features
* Handling of complex tax scenarios
* Multiple tax jurisdictions support
* Tax payment tracking
* Accountant access portal
* Integration with tax preparation software

### 9. Offline Functionality *(Revised Notes)*

#### Included in MVP:
* Offline expense entry (manual data + photo capture)
* Offline access to client/job list (read-only, for basic association)
* Data synchronization when connectivity is restored
* Sync status indicators
* Conflict resolution (simple "newest wins" approach)
* Automatic sync attempts when connectivity detected
* Manual sync trigger option

#### Not Included in MVP (or requires connectivity):
* **OCR processing** (likely requires connectivity unless using on-device models)
* **Smart Job Suggestions** (based on real-time GPS/Calendar likely requires connectivity)
* Offline invoice creation
* Offline client/job/contractor creation or editing
* Offline report generation
* Offline access to historical data beyond recent items
* Complex conflict resolution options
* Background sync in mobile devices (limited reliability)

### 10. Data Utilities

#### Included in MVP:
* Data backup and restore capabilities
* Basic data import (clients, CSV format)
* Data export (expenses, invoices, clients, contractors)
* Storage usage monitoring
* Receipt image compression options

#### Not Included in MVP:
* Advanced data migration tools
* Integration with third-party backup services
* Custom data retention policies
* Data archiving functionality
* Multi-device sync beyond cloud storage

### 11. User Interface/Experience

#### Included in MVP:
* Mobile-optimized responsive design
* Bilingual interface (English and French)
* Quick-access buttons for common tasks (**esp. expense logging**)
* Dark/light mode toggle
* Simplified navigation focused on core tasks
* Basic onboarding guide (**updated to reflect new automated workflows**)
* Accessibility considerations (WCAG 2.1 AA compliance)
* **Intuitive UI for expense splitting/allocation**

#### Not Included in MVP:
* Advanced UI customization
* Keyboard shortcuts
* Power user features
* Custom dashboard configuration
* Advanced help/tutorial system
* Voice input capabilities (Considered for future)

## Priority Features for Initial Development *(Revised Section)*

Based on user needs emphasizing effortless input and core profitability, the following feature development sequence is recommended for the enhanced MVP:

### Phase 1: Core Foundation & Smart Input
1.  Account Settings & Profile
2.  Basic client management (Add, Edit, View)
3.  Core **expense tracking framework** with receipt **photo capture**
4.  **OCR Implementation (Basic)** for key receipt data
5.  Offline storage architecture & basic sync mechanism

### Phase 2: Job Context & Linking
1.  Job management and tracking (including offline list access)
2.  **Context-Aware Job Suggestions** (basic location/recency)
3.  Manual Job-Expense Association (fallback/correction)
4.  Basic Contractor Management (Add, Edit, View, List)
5.  Contractor Payment Recording (manual association initially)

### Phase 3: Profitability & Allocation
1.  **Simple Splitting UI** implementation (for expenses & contractor pay)
2.  Job profitability calculation logic
3.  Weekly financial summary view
4.  Basic Tax Features integration (GST/QST tracking)
5.  Job list profitability indicators

### Phase 4: Invoicing, Reporting & Refinement
1.  Invoice generation with tax calculation
2.  Email sending capability
3.  Core financial reports (Job Profitability, Tax Summary)
4.  Data Utilities (export functionality)
5.  UI refinements, localization, performance optimization, offline robustness improvements.

*(Note: This phasing integrates core automation earlier, potentially extending the overall MVP timeline compared to the previous plan.)*

## Technical Implementation Notes *(Revised Section)*

### Platform Approach
* Progressive Web App (PWA) architecture
* Responsive design for both mobile and desktop use
* Service Worker implementation for offline functionality

### Data Storage Strategy
* Client/Job/Contractor Data: IndexedDB for structured data (read-only offline for Client/Job)
* Expense Data: IndexedDB with timestamped entries for sync; potentially store OCR confidence scores.
* Receipt Images: Cache API with compression before storage.
* Sync Status: Queue maintained in IndexedDB.
* Context Data: Strategy for caching recent locations/calendar info for offline suggestions (TBD).

### Sync Mechanism
* Queue-based synchronization with timestamps.
* Basic conflict resolution using "newest wins" approach.
* Clear status indicators for sync state.
* Handle potential sync issues if OCR occurs server-side after initial offline capture.

### Automation Implementation
* **OCR:** Evaluate on-device vs. cloud-based OCR services (trade-offs: cost, offline capability, privacy, accuracy). Define target fields (Vendor, Date, Amount, GST, QST).
* **Context Suggestions:** Define logic for suggestions (GPS proximity radius, recent job activity window, calendar event matching). Requires user permissions for location/calendar access.
* **Splitting UI:** Design intuitive sliders, percentage inputs, or direct amount entry for allocation.

### Performance Targets
* Initial load time: < 3 seconds on 4G connection.
* Offline expense entry (manual/photo): < 1 second response time.
* Receipt image capture and storage: < 3 seconds.
* **OCR processing time (target): < 5-10 seconds (clarify if sync/background process).**
* Sync operation: Background process with status indicator.

## Success Criteria for MVP *(Revised Section)*

The enhanced MVP will be considered successful if it meets the following criteria:

1.  **User Adoption:** Initial user base of at least 50 active landscaping businesses within 3 months of launch, with positive feedback on ease of input.
2.  **Core Functionality:** Users can successfully:
    * Capture receipts via photo with >80% accuracy on key fields via OCR (target).
    * Quickly associate/split expenses to jobs using smart suggestions and simple UI.
    * Track expenses offline (manual/photo capture, basic association).
    * Add and manage basic client and contractor information.
    * Track payments made to contractors, including splitting costs.
    * Generate invoices with correct tax calculations.
    * View basic profitability reports (including contractor costs).
    * Access the system bilingually (English/French).
3.  **Technical Performance:**
    * 99% successful sync rate.
    * < 1% of users reporting data loss.
    * Average app rating > 4.2 (out of 5), reflecting improved ease of use.
    * < 5% of users requiring support for basic expense logging functions.
4.  **Business Metrics:**
    * Users report spending at least **40%** less time on expense administration (increased target due to automation).
    * 30% conversion from free tier (if applicable) to paid subscriptions.
    * < 10% churn rate after 3 months.
    * Positive user feedback validating the "effortless input" value proposition.

## Product Roadmap Preview (Post-MVP)

While not part of the MVP, the following features are planned for subsequent releases:

### Near-term Additions (3-6 months post-MVP)
* Multi-user access with permissions
* Client portal for invoice access
* Online payment acceptance
* Advanced reporting and analytics
* Mileage tracking (dedicated feature)

### Mid-term Roadmap (6-12 months post-MVP)
* Integration with accounting software (e.g., QuickBooks Online)
* Job scheduling and crew management features
* Expanded offline capabilities (e.g., editing)
* Mobile app versions (iOS/Android native)
* Custom invoice templates

### Long-term Vision (12+ months)
* Industry-specific expansions (pool service, cleaning, etc.)
* Inventory and equipment management
* Client relationship management features
* Predictive analytics for business planning
* Comprehensive business management platform

## Approval and Sign-off

| Role                 | Name | Signature | Date |
| :------------------- | :--- | :-------- | :--- |
| Product Owner        |      |           |      |
| Technical Lead       |      |           |      |
| UX Designer          |      |           |      |
| Business Stakeholder |      |           |      |

## Appendix: Feature Prioritization Matrix *(Revised Section)*

*(Note: Priority score is a combination of the four factors, with 1 being highest priority. This matrix requires significant re-evaluation based on the updated scope emphasizing automation).*

| Feature                           | Business Value | User Value | Implementation Complexity | Risk   | Priority Score (NEW) |
| :-------------------------------- | :------------- | :--------- | :-------------------------- | :----- | :------------------- |
| **Receipt OCR (Basic)** | High           | High       | High                        | High   | **1** |
| **Context-Aware Job Suggestions** | High           | High       | Medium                      | Medium | **2** |
| **Simple Expense Splitting UI** | Medium         | High       | Medium                      | Low    | **3** |
| Expense Tracking Core & Capture   | High           | High       | Medium                      | Medium | **4** |
| Job Profitability Calculation     | High           | High       | Medium                      | Low    | **5** |
| Offline Expense Entry (Core)      | High           | High       | High                        | Medium | **6** |
| Invoice Management                | High           | Medium     | Low                         | Low    | **7** |
| Tax Features (Reporting/Guidance) | Medium         | High       | Medium                      | High   | **8** |
| Contractor Payment Tracking       | Medium         | High       | Low                         | Low    | **9** |
| Client Management                 | Medium         | Medium     | Low                         | Low    | **10** |
| Weekly Financial Summary          | Medium         | High       | Low                         | Low    | **11** |
| Contractor Management (Basic)     | Medium         | High       | Low                         | Low    | **12** |
| Account Settings & Profile        | Medium         | Low        | Low                         | Low    | **13** |
| Data Utilities (Export)           | Low            | Medium     | Low                         | Low    | **14** |
| UI Language Toggle                | Medium         | High       | Low                         | Low    | **15** |

## Change Log
*(Added Entry)*
| Date          | Version | Changed By   | Changes Made                                                                                                                               |
| :------------ | :------ | :----------- | :----------------------------------------------------------------------------------------------------------------------------------------- |
| ...           | ...     | ...          | ...                                                                                                                                        |
| April 8, 2025 | 1.4     | Gemini Model | Major revision: Incorporated "Ideal Onboarding" features (OCR, Smart Suggestions, Easy Splitting) into MVP scope based on stakeholder feedback. Updated Principles, Feature Scope (Expense/Contractor Mgmt), Phasing, Technical Notes, Success Criteria, Prioritization Matrix. Acknowledged increased complexity and potential offline limitations for new features. |