# FinTrack: Detailed MVP Feature Scope

## Document Metadata
**Version:** 1.6 *(Updated for Standardized Terminology)*.
**Status:** Draft.
**Last Updated:** April 9, 2025.
**Owner:** FinTrack Product Manager.
**Reviewers:** Technical Lead, UX Designer, Business Stakeholder.

## **Guiding Principles**

1.  ***Core Experience Priority:*** The primary user experience focuses on effortless core features (jobs, expenses, profitability), remaining simple and functional independently of conditional modules.
2.  ***Integrated Conditional Design:*** While core workflow is primary, design core components anticipating logical integration points for optional conditional features (like taxes) to ensure smooth user transitions and efficient development.

## Purpose
This document defines the detailed feature scope for the FinTrack Minimum Viable Product (MVP), establishing clear boundaries for what will and will not be included in the initial release. The scope prioritizes the **Core MVP Workflow** while defining the **Conditional Tax Module** features activated by user choice. The scope is based on user needs analysis, interview findings, technical feasibility assessment, and the decision to incorporate key ease-of-use automation features within the core framework from the outset.

## MVP Guiding Principles

The following principles guide our MVP scope decisions:

1.  **Focus on Core Value Proposition:** Prioritize features that directly address job profitability tracking and *effortless* expense management for landscaping businesses **as part of the core, standalone workflow**.
2.  **Mobile-First & Field Optimized:** Design **core features** for field use with reliable offline functionality for critical **core** operations and minimal user input.
3.  **Simplicity & **Effortless Input (Core):** Keep the **core** interface intuitive and workflows streamlined, leveraging automation to minimize manual data entry for essential tasks.
4.  **Quebec Tax Compliance (Conditional):** Ensure proper handling of GST/QST for Quebec-based businesses **via the optional, conditional tax module activated by user setting**.
5.  **Bilingual Support:** Support both English and French throughout the application **(core requirement)**.
6.  **Reliability Over Breadth:** Ensure **core features**, including automation, work reliably in challenging connectivity environments. The **conditional module** must also be reliable when activated.

## Feature Categories & MVP Scope Definition

*(This section defines the features included in the Core MVP and the Conditional Tax Module Add-on)*

### **A. Core MVP Features (Always Active)**

These features constitute the standalone, always-available functionality providing core value.

#### 1. Account Settings & Profile (Core)

* User account creation and authentication
* Basic user profile with business information
* **Tax Registration Status Setting:** (e.g., Not Registered / Registered) - This setting acts as the **activation trigger** for the Conditional Tax Module.
* Language preference setting (English/French)
* Password reset functionality
* Account security features (2FA optional but available)
* Terms of service and privacy policy acceptance

#### 2. Client Management (Core)

* **Add, Edit, and View Clients:** Manage basic client information including:
    * Name (business and contact person)
    * Contact information (phone, email, address)
    * Language preference
* Client listing with search and filter
* Client data access in offline mode (read-only)
* Client details page with associated jobs and invoices
* Basic client status (active/inactive)

#### 3. Job Management (Core)

* Job creation with basic details:
    * Client association
    * Job name/description
    * Location
    * Service type (landscaping or snow removal, flexible)
    * Start and expected end dates
    * Job status (upcoming, in-progress, complete)
* Job listing with search and filter by status/client
* Job profitability calculation (revenue - expenses - contractor payments, **core basis**)
* Basic job notes
* Job access in offline mode (read-only)

#### 4. Expense Tracking (Core)

* **Receipt Capture with Automated Data Extraction (OCR - Core Data):** Capture receipt images via camera, with the system attempting to automatically extract key **core** details (Vendor, Date, Amount). (Note: Basic OCR, user confirms/edits).
* **Manual Expense Entry:** Option for quick manual entry if no receipt or OCR fails.
* **Deferred Processing Support:** Ability to save a captured receipt image as a **Draft Expense** for later completion of details (verification, allocation, categorization).
* **Expense Categorization:** Organize expenses by type (Fuel, Materials, Rentals, Contractor Payments, etc., from predefined list).
* **Context-Aware Job Suggestions:** App suggests likely job associations based on context (e.g., location, calendar, recent activity). User confirms or selects manually.
* **Simple Expense Splitting UI:** Intuitive interface (e.g., sliders, simple amount entry) to allocate a single expense (esp. consumables, contractor pay) across multiple selected jobs.
* **Mark as General Expense:** Easily tag expenses not related to a specific job.
* Offline expense entry capability (**core manual data**, photo capture, basic job selection from cache, saving as **Draft Expense**) with sync. *(Note: OCR/Smart Suggestions may require connectivity)*.
* Expense listing with search and filter (including ability to filter/view **Draft Expenses**).
* Basic expense reports (by category, by job, by date range - **core data**).

#### 5. Invoice Management (Core)

* Invoice creation with:
    * Client association
    * Job association
    * Line items with descriptions
    * Due date
    * Payment terms
    * Business logo and basic customization
* PDF invoice generation
* Email invoice sending capability
* Invoice listing with status (draft, sent, paid, overdue)
* Basic invoice templates (1-2 options)
* Mark invoice as paid functionality
* Partial payment recording

#### 6. Contractor Management (Core)

* **Add and Edit Contractors:** Ability to create new contractor records and modify existing ones.
* **Contractor Contact Storage:** Store basic contractor contact information (e.g., Name, Phone, Email).
* **Contractor List/View:** View a list of contractors, potentially with search/filter.
* **Contractor Payment Recording:** Record payments made to contractors (date, amount, method), linking payment to the contractor. Includes:
    * **Context-Aware Job Suggestions:** Suggests jobs the contractor is associated with.
    * **Simple Splitting UI:** Use the same intuitive interface as expenses to allocate payments across multiple jobs.

#### 7. Financial Reporting (Core)

* Job profitability report (**core basis**)
* Income by client/job report (**core basis**)
* Expenses by category report (**core data**, includes completed expenses, not drafts)
* Basic cash flow report (**core basis**)
* Weekly profit summary view (**core basis**)
* Current month vs. previous month comparison (**core basis**)
* Export **core** reports to CSV/PDF

#### 8. Offline Functionality (Core Focus)

* Offline **core** expense entry (manual data + photo capture, saving as **Draft Expense**)
* Offline access to client/job list (read-only, for basic association)
* Data synchronization when connectivity is restored (including **Draft Expenses** needing processing)
* Sync status indicators
* Conflict resolution (simple "newest wins" approach)
* Automatic sync attempts when connectivity detected
* Manual sync trigger option

#### 9. Data Utilities (Core)

* Data backup and restore capabilities
* Basic data import (clients, CSV format)
* Data export (**core** expenses [completed], invoices, clients, contractors)
* Storage usage monitoring
* Receipt image compression options

#### 10. User Interface/Experience (Core)

* Mobile-optimized responsive design
* Bilingual interface (English and French)
* Quick-access buttons for common **core** tasks (**esp. expense logging**)
* Interface for accessing and resuming **Draft Expenses**.
* Dark/light mode toggle
* Simplified navigation focused on **core** tasks
* Basic onboarding guide (**updated to reflect new core automated workflows & Deferred Processing**)
* Accessibility considerations (WCAG 2.1 AA compliance)
* **Intuitive UI for core expense splitting/allocation**

### **B. Conditional Tax Module Features (MVP Add-on)**

These features are activated only when the user sets their "Tax Registration Status" to 'Registered' (or similar) in their Business Profile.

#### 11. Tax Features (Conditional)

* **GST/QST Calculation & Tracking:** Monitor collected and paid taxes accurately (**if enabled**; OCR potentially enhanced for tax fields).
* **Tax Status Monitoring & Guidance:** Track revenue against tax thresholds; provide informational alerts & links to official resources (**if enabled**).
* **Tax Filing Reports:** Generate basic summary reports for tax filing preparation (**if enabled**).
* Tax settings configuration (within Business Profile, including registration numbers **if enabled**).

#### 12. Invoice Management (Conditional Enhancement)

* **Tax Calculations on Invoices:** Apply appropriate taxes (GST/QST) based on registration status and client settings **when tax features are enabled**.

#### 13. Expense Tracking (Conditional Enhancement)

* **Tax Detail Capture on Expenses:** Capture/track GST/QST paid on expenses (via OCR enhancement or manual input) **when tax features are enabled and expense is processed (not Draft)**. Enable Input Tax Credit (ITC) identification support.

### **C. Features Not Included in MVP (Core or Conditional)**

* **Advanced Accounting:** Full Accounting Suite, Depreciation Tracking.
* **Financial Management:** Payroll Processing, Personal Finance, Bank Integration.
* **Operations:** Detailed Crew/Contractor Scheduling, Route Optimization, Equipment Tracking.
* **Client Management:** CRM Features, Client Portal, Client creation offline, Custom client fields, Client document storage, Automated client communications.
* **Invoice Management:** Invoice creation offline, Recurring invoices, Online payment acceptance, Advanced customization, Reminders, Late fees, Time tracking integration, Batch operations, Quote conversion.
* **Contractor Management:** Advanced contractor details (Tax ID, Insurance), Contracts, Assigning to jobs directly, Onboarding, Time tracking, Communication tools.
* **Expense Tracking:** *Advanced* OCR validation/line items, Recurring expenses, Mileage tracking, Per diems, Approvals, Multiple receipts/expense, Custom categories, Advanced reports, Bank feed import.
* **Financial Reporting:** Custom report builder, Advanced analytics, Seasonal trend analysis, Benchmarking, Advanced filtering, Balance sheet/P&L, Dashboard customization, Profit margin by job type, Forecasting/budgeting.
* **Tax Features:** Auto-filing, Advanced planning, Complex scenarios, Multiple jurisdictions, Tax payment tracking, Accountant portal, Tax prep software integration.
* **Offline Functionality:** *Complex* offline operations (OCR, suggestions, conditional features), Offline creation/editing (beyond core expense draft), Offline reporting.
* **Data Utilities:** Advanced migration, Third-party backup integration, Custom retention, Archiving.
* **UI/Experience:** Advanced UI customization, Keyboard shortcuts, Power user features, Custom dashboard, Advanced help, Voice input.

## Priority Features for Initial Development

Based on user needs emphasizing effortless core input and core profitability, the following feature development sequence is recommended, delivering the **Core MVP** first, followed by the **Conditional Tax Module**.

### Phase 1: Core Foundation & Smart Input
1.  Account Settings & Profile (**Incl. Tax Status Trigger**)
2.  Basic client management (Add, Edit, View)
3.  Core **expense tracking framework** with receipt **photo capture**
4.  **OCR Implementation (Basic Core Data)** for key receipt data
5.  Offline storage architecture & basic sync mechanism (supporting saving **Draft Expenses**)

### Phase 2: Core Job Context & Linking
1.  Job management and tracking (including offline list access)
2.  **Context-Aware Job Suggestions** (basic location/recency)
3.  Manual Job-Expense Association (fallback/correction)
4.  Basic Contractor Management (Add, Edit, View, List)
5.  Contractor Payment Recording (manual association initially)

### Phase 3: Core Profitability & Allocation
1.  **Simple Splitting UI** implementation (for expenses & contractor pay)
2.  Job profitability calculation logic (**core basis**)
3.  Weekly financial summary view (**core basis**)
4.  Interface for accessing and resuming **Draft Expenses**.
5.  *Design/Prep:* Define data points needed for conditional tax module integration (e.g., tax fields in expense/invoice).
6.  Job list profitability indicators (**core basis**)

### Phase 4: Core Invoicing, Reporting & Refinement
1.  Core Invoice generation (**no tax initially**)
2.  Email sending capability
3.  Core financial reports (Job Profitability - core basis, Expense lists including **Drafts**)
4.  Data Utilities (export core data functionality)
5.  UI refinements, localization, performance optimization, offline robustness improvements.

### Phase 5 (Post-Core Validation): Conditional Tax Module Build & Test
1.  Implement GST/QST calculation logic for invoices **(conditional)**.
2.  Implement GST/QST capture/tracking for expenses (incl. OCR enhancements for tax fields) **(conditional)**.
3.  Build Tax Reporting features (Tax Summary) **(conditional)**.
4.  Implement Tax Settings display & Guidance features **(conditional)**.
5.  Integrate conditional features into UI, controlled by activation trigger.
6.  End-to-end testing of Core + Conditional workflows.

*(Note: This phasing explicitly validates the core automated workflow before building the conditional tax features.)*

## Technical Implementation Notes

### Platform Approach
* Progressive Web App (PWA) architecture
* Responsive design for both mobile and desktop use
* Service Worker implementation for offline functionality **(core focus)**

### Data Storage Strategy
* Client/Job/Contractor Data: IndexedDB for structured data (read-only offline for Client/Job)
* Expense Data: IndexedDB with timestamped entries for sync; includes status field (e.g., 'draft', 'synced'); potentially store OCR confidence scores. **Tax fields populated only if module enabled.**
* Receipt Images: Cache API with compression before storage.
* Sync Status: Queue maintained in IndexedDB.
* Context Data: Strategy for caching recent locations/calendar info for offline core suggestions (TBD).
* **Conditional Data:** Tax-related fields in core entities (Expense, Invoice) may be null/unused if module is inactive. TaxInfo entity linked only if active.

### Sync Mechanism
* Queue-based synchronization with timestamps **for core data, including Draft Expenses**.
* Basic conflict resolution using "newest wins" approach.
* Clear status indicators for sync state.
* Handle potential sync issues if OCR occurs server-side after initial offline capture. Sync logic needs awareness of conditional module status.

### Automation Implementation (Core)
* **OCR:** Evaluate on-device vs. cloud-based OCR services. Define target **core** fields (Vendor, Date, Amount). **Conditional enhancement:** OCR for GST/QST fields if module enabled.
* **Context Suggestions:** Define logic for core suggestions (GPS proximity, recent job activity, calendar). Requires user permissions for location/calendar access.
* **Splitting UI:** Design intuitive sliders, percentage inputs, or direct amount entry for core allocation.

### Performance Targets (Core Focus)
* Initial load time: < 3 seconds on 4G connection.
* Offline core expense entry (manual/photo capture of **Draft Expense**): < 1 second response time.
* Receipt image capture and storage: < 3 seconds.
* **Core OCR processing time (target): < 5-10 seconds (clarify if sync/background process).**
* Sync operation: Background process with status indicator.

## Success Criteria for MVP

The **Core MVP** will be considered successful if it meets the following criteria:

1.  **User Adoption:** Initial user base of at least 50 active landscaping businesses within 3 months of launch, with positive feedback on **core ease of input and Deferred Processing workflow**.
2.  **Core Functionality:** Users can successfully:
    * Capture receipts via photo with >80% accuracy on **core** fields via OCR (target).
    * Quickly associate/split expenses to jobs using core smart suggestions and simple UI.
    * Track core expenses offline (manual/photo capture, saving as **Draft Expense**, basic association).
    * Resume and complete **Draft Expenses**.
    * Add and manage basic client and contractor information.
    * Track payments made to contractors, including splitting costs.
    * Generate core invoices (without tax) with correct details.
    * View basic core profitability reports.
    * Access the system bilingually (English/French).
3.  **Technical Performance (Core):**
    * 99% successful sync rate for core data (including drafts).
    * < 1% of users reporting core data loss.
    * Average app rating > 4.2 (out of 5), reflecting improved core ease of use.
    * < 5% of users requiring support for basic core expense logging functions (including resuming drafts).
4.  **Business Metrics (Core):**
    * Users report spending at least **40%** less time on core expense administration.
    * Positive user feedback validating the "effortless core input" value proposition.
    * (Post conditional release): Track activation rate of conditional tax module among target users (e.g., registered businesses).

*(Success criteria for the Conditional Tax Module will be defined closer to its development phase.)*

## Product Roadmap Preview (Post-MVP)

While not part of the MVP, the following features are planned for subsequent releases, building upon the **validated Core MVP** and **integrated Conditional Tax Module**.

### Near-term Additions (Phase 2: 3-6 months post-Conditional Release)
* Multi-user access with permissions
* Client portal for invoice access
* Online payment acceptance
* Advanced reporting and analytics (building on core & conditional data)
* Mileage tracking (dedicated feature)
* Advanced Tax Reporting (building on conditional module)

### Mid-term Roadmap (Phase 3: 6-12 months post-Conditional Release)
* Integration with accounting software (e.g., QuickBooks Online)
* Job scheduling and crew management features
* Expanded offline capabilities (e.g., editing core data)
* Mobile app versions (iOS/Android native)
* Custom invoice templates
* Contract Management

### Long-term Vision (Phase 4+: 12+ months)
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

## Appendix: Feature Prioritization Matrix

*(Note: Priority score is a combination of the four factors, with 1 being highest priority. This matrix reflects prioritization for the initial **Core MVP** delivery, with conditional features deferred).*

| Feature                           | Business Value | User Value | Implementation Complexity | Risk   | Priority Score (CORE MVP) | Phase (Core/Conditional) |
| :-------------------------------- | :------------- | :--------- | :-------------------------- | :----- | :------------------------ | :----------------------- |
| **Receipt OCR (Basic Core Data)** | High           | High       | High                        | High   | **1** | Core                     |
| **Context-Aware Job Suggestions** | High           | High       | Medium                      | Medium | **2** | Core                     |
| **Simple Expense Splitting UI** | Medium         | High       | Medium                      | Low    | **3** | Core                     |
| Expense Tracking Core & Capture   | High           | High       | Medium                      | Medium | **4** | Core                     |
| Job Profitability Calculation     | High           | High       | Medium                      | Low    | **5** | Core                     |
| Offline Expense Entry (Core/Draft)| High           | High       | High                        | Medium | **6** | Core                     |
| **Draft Expense Access/Resume UI**| Medium         | High       | Low                         | Low    | **7** | Core                     |
| Invoice Management (Core)         | High           | Medium     | Low                         | Low    | **8** | Core                     |
| Contractor Payment Tracking       | Medium         | High       | Low                         | Low    | **9** | Core                     |
| Client Management                 | Medium         | Medium     | Low                         | Low    | **10** | Core                     |
| Weekly Financial Summary          | Medium         | High       | Low                         | Low    | **11** | Core                     |
| Contractor Management (Basic)     | Medium         | High       | Low                         | Low    | **12** | Core                     |
| Account Settings & Profile        | Medium         | Low        | Low                         | Low    | **13** | Core                     |
| Data Utilities (Export Core)      | Low            | Medium     | Low                         | Low    | **14** | Core                     |
| UI Language Toggle                | Medium         | High       | Low                         | Low    | **15** | Core                     |
| Expense Listing (inc. Drafts)     | Medium         | High       | Low                         | Low    | **16** | Core                     |
| --- Conditional Features ---      | ---            | ---        | ---                         | ---    | ---                       | ---                      |
| Tax Features (Reporting/Guidance) | Medium         | High       | Medium                      | High   | **Deferred** | Conditional              |
| Tax Calculation on Invoices       | Medium         | High       | Medium                      | Medium | **Deferred** | Conditional              |
| Tax Detail Capture (Expenses)     | Medium         | High       | Medium                      | Medium | **Deferred** | Conditional              |


## Change Log
| Date             | Version | Changed By   | Changes Made                                                                                                                                                                                                                                 |
| :--------------- | :------ | :----------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ...              | ...     | ...          | ...                                                                                                                                                                                                                                          |
| April 8, 2025    | 1.4     | Gemini Model | Major revision: Incorporated "Ideal Onboarding" features (OCR, Smart Suggestions, Easy Splitting) into MVP scope based on stakeholder feedback. Updated Principles, Feature Scope (Expense/Contractor Mgmt), Phasing, Technical Notes, Success Criteria, Prioritization Matrix. Acknowledged increased complexity and potential offline limitations for new features. |
| April 9, 2025    | 1.5     | Gemini Model | **Refactored based on core vs. conditional prioritization instructions:** Added Guiding Principles; Restructured Feature Categories/Scope Definition (Sec 2-11) for Core vs. Conditional; Explicitly separated Conditional Tax Module; Applied conditional language; Adjusted Phasing (Sec 12), Success Criteria (Sec 13), Prioritization Matrix (Appendix). Ensured full document output. |
| **April 9, 2025** | **1.6** | **Gemini Model** | **Updated for Standardized Terminology:** Replaced various terms related to incomplete expenses with "Draft Expense" and the workflow with "Deferred Processing" for consistency. Added specific mention of "Draft Expense Access/Resume UI" and filtering for drafts in listings. Updated version number. |