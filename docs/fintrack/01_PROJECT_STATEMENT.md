# Level 0: Problem Definition & User Needs Analysis - FinTrack
*(Reflecting Enhanced MVP Scope v1.4 and Core/Conditional Prioritization)*

## **Guiding Principles**

1.  ***Core Experience Priority:*** The primary user experience focuses on effortless core features (jobs, expenses, profitability), remaining simple and functional independently of conditional modules.
2.  ***Integrated Conditional Design:*** While core workflow is primary, design core components anticipating logical integration points for optional conditional features (like taxes) to ensure smooth user transitions and efficient development.

## Core Problem Statement

### Question 1: What is the core problem we're trying to solve?
**Answer:** Small landscaping and lawn care business owners struggle to **efficiently and accurately** track job profitability, manage seasonal cash flow, organize expenses (**especially with time-consuming manual capture and allocation**), and handle client invoicing efficiently, leading to financial uncertainty, missed tax deductions (if applicable), and administrative burdens that take time away from their core work.

**Evidence:** Direct feedback from landscaping business owners, industry surveys showing high administrative burden in small service businesses, high failure rate of small trade businesses due to financial mismanagement.

**Assumptions Made:**
- [x] Target users have low to moderate financial expertise.
- [x] Users prefer mobile-first solutions due to field-based work.
- [x] Users prioritize **simplicity and effortless input** over comprehensive accounting features.
- [x] Most users currently use inadequate tools (spreadsheets, paper, generic software).
- [x] **Users will accept ~80-90% OCR accuracy with easy correction**.
- [x] **Users will grant context permissions (GPS/Calendar) if value is clear**.
- [x] The conditional tax module is activated based on a specific user setting (e.g., "Tax Registration Status" in Business Profile).

**Information Gaps:**
- [x] Exact percentage of time spent on financial management vs. core work (Goal: Reduce significantly via automation).
- [x] Quantified financial impact of poor job cost tracking.
- [x] Regional variations in financial management needs (Quebec-specific requirements identified).
- [ ] Integration requirements with existing tools (Calendar/GPS read-only needed for suggestions).
- [ ] User price sensitivity and willingness to pay for different feature tiers (including automation and conditional tax module).
- [ ] Specific accessibility requirements for field conditions.

**Validation Required:**
- [x] User interviews with 5-7 additional landscaping/gardening business owners.
- [x] Analysis of existing financial management processes.
- [x] Competitive analysis of current solutions and their shortcomings.
- [ ] Verification by accounting professional with Quebec GST/QST expertise for the conditional tax module.
- [ ] **Proof-of-concept for OCR accuracy, smart suggestions, splitting UI**.
- [ ] **Re-validation of offline functionality feasibility considering automation limitations**.
- [ ] User testing of bilingual interface.
- [ ] **Validation of user acceptance for context permissions (GPS/Calendar)**.
- [ ] Validation of the conditional tax module activation mechanism and workflow.

## User Analysis

### Question 2: Who are the primary users and what is their context?
**User Personas:** *(Refined goals/pain points for core vs. conditional)*
1.  **Solo Operator:** Handles all aspects of the business themselves; minimal financial training; works primarily in the field; limited time for administrative tasks (**needs automation for core tasks**). May need to track GST/QST for Quebec tax compliance **if registered/applicable**.
2.  **Small Business Owner with Crew:** Manages 2-10 employees/contractors; handles finances personally or with minimal support; balances field work with business management; requires visibility into multiple concurrent jobs; **needs efficient expense/contractor cost allocation (core)**. Likely requires tax tracking based on business status.
3.  **Office Manager/Admin:** Works for a small landscaping business; responsible for invoicing and expense tracking; may have slightly more financial knowledge but not formal accounting training; **would benefit from streamlined data capture (core)**. Requires tax features based on business registration status.
4.  **Prospective/Early-Stage Operator:** Individual planning to start or who recently started a small service business; needs guidance on tax obligations and thresholds (GST/QST) **if considering registration**; primarily operates through mobile devices; limited or no prior business administration experience; **needs extreme simplicity from day one (core)**.

**Usage Environment:**
- Primarily mobile (in trucks, at job sites).
- Occasionally desktop (evenings/weekends for catch-up work).
- Often in areas with limited connectivity (**impacts real-time automation features**).
- May be accessing while physically tired or with dirty hands.
- Bilingual environment requiring both English and French support (Quebec market).

**User Constraints:**
- **Technical:** Limited technical skills; need for intuitive interface; may have older devices; intermittent internet connectivity (**requires offline manual fallback for core tasks**); **acceptance of camera/location/calendar permissions for core automation**.
- **Time:** Extremely time-constrained; needs **minimal time for data entry (core)** and quick review; works long physical hours.
- **Resource:** Budget-sensitive; reluctant to pay for multiple specialized tools.
- **Language:** Requires bilingual support (English/French) to serve Quebec market.
- **Regulatory:** Needs to comply with Quebec's GST/QST requirements and reporting **if registered**.
- **Other:** Seasonal work patterns; high variability in workload; limited accounting knowledge; paper receipt management (**target for core OCR**).

**Success Criteria (User Perspective):**
1.  [x] Can determine profitability of individual jobs **accurately and easily (core)**.
2.  [x] Can track and categorize expenses **with minimal manual effort** on-the-go **(core)**.
3.  [x] Can create and manage invoices efficiently **(core, with optional tax if enabled)**.
4.  [x] Can monitor cash flow and anticipate seasonal fluctuations **(core)**.
5.  [x] Can prepare for tax obligations without extensive manual work, **leveraging captured data (conditional, if enabled)**.
6.  [x] Can separate business and personal finances clearly **(core)**.
7.  [x] **Spends significantly less time on financial admin due to core automation**.

## Problem Scope

### Question 3: What are the boundaries of the solution?
**Scale:**
- [x] Personal
- [x] Organizational (Small Business)
- [ ] Enterprise
- [ ] Other: [Specify]

**Target Industry Focus:**
- Primary: Landscaping, lawn care, and gardening services
- Future expansion potential: Similar field service businesses (pressure washing, window cleaning, pool maintenance, cleaning)
- Note: Initial focus primarily on landscaping/lawn care/snow removal; features designed for flexibility.

**Minimum Viable Solution (MVP Definition):**

*(Structured to prioritize Core MVP with Conditional Add-on)*

**Core MVP Workflow (Always Active):**
The following features represent the essential, standalone functionality providing value to all users, regardless of tax status.

1.  **User & Account Management:**
    * User account creation and authentication
    * Basic user profile with business information
    * Language preference setting (English/French)
    * Priority: Medium

2.  **Client Management:**
    * Client database with basic information (Name, Contact, Address)
    * Client listing with search and filter
    * Client access in offline mode (read-only)
    * Why essential: Foundation for job tracking and invoicing
    * Impact: Organizes business relationships and enables proper job attribution
    * Priority: High

3.  **Job/Work Tracking:**
    * Job creation with basic details (Name/Desc, Location, Service Type) and client association
    * Job listing with search and filter
    * Job profitability calculation (based on recorded revenue and costs)
    * Job access in offline mode (read-only)
    * Why essential: Core unit for measuring profitability
    * Impact: Enables linking expenses and revenue to specific work
    * Priority: Critical

4.  **Mobile-friendly Core Expense Tracking (Automated):**
    * **Receipt Capture with basic OCR** (Vendor, Date, Amount)
    * **Manual entry fallback**
    * **Context-aware job suggestions**
    * **Simple expense splitting UI**
    * Offline *manual* expense entry & photo capture capability with sync
    * Expense listing with search and filter
    * Why essential: Drastically reduces manual effort and improves accuracy, core value proposition.
    * Impact: Improves accuracy, saves significant time, reduces administrative burden.
    * Priority: **Critical**

5.  **Basic Invoicing (Core):**
    * Invoice creation with client/job association
    * PDF invoice generation
    * Email invoice sending capability
    * Why essential: Required for receiving payment and maintaining cash flow
    * Impact: Accelerates payment cycle and professionalizes business image
    * Priority: High

6.  **Core Financial Reporting:**
    * Job profitability report (based on potentially automated data)
    * Weekly profit summary view
    * Export reports to CSV/PDF
    * Why essential: Provides actionable insights into business health
    * Impact: Enables informed business decisions and pricing adjustments
    * Priority: Medium-High

7.  **Contractor Management & Payment (Core Allocation):**
    * Basic Contractor contact management (Add/Edit/View)
    * Contractor payment recording
    * **Context-aware job suggestions for payment allocation**
    * **Simple splitting UI for allocating payments across jobs**
    * Why essential: Accurately tracks major cost component for many users.
    * Impact: Ensures contractor costs are correctly factored into job profitability.
    * Priority: High

**Conditional Tax Module (MVP Add-on):**
This module provides features related to tax handling, activated by a user setting (e.g., "Tax Registration Status: Registered" in the Business Profile). It builds upon the Core MVP.

1.  **Tax-Enabled Invoicing:**
    * GST/QST tax calculations for Quebec compliance added to invoices **(if enabled)**
    * Priority: High (Conditional)

2.  **Tax-Enabled Expense Tracking:**
    * Quebec-specific GST/QST tracking on expenses (aided by OCR) **(if enabled)**
    * Input Tax Credit (ITC) identification support **(if enabled)**
    * Priority: High (Conditional)

3.  **Tax Reporting:**
    * GST/QST summary report for tax filing (leveraging captured data) **(if enabled)**
    * Priority: Medium-High (Conditional)

4.  **Tax Settings & Guidance:**
    * Configuration for tax registration status and numbers **(defines activation)**
    * Tax threshold monitoring and informational alerts **(if enabled)**
    * Links to official Quebec tax resources
    * Priority: Medium (Conditional)

**Phased Implementation Approach:** *(Revised for Core-First Validation)*
The enhanced MVP development will prioritize delivering and validating the complete Core MVP Workflow first. Design considerations and groundwork for the Conditional Tax Module integration points can occur during core development where efficient, but the main build and testing of the conditional module are reserved for later phases after the core is stable.

**Phase 1: Core Foundation & Smart Input**
1.  User account system and authentication
2.  Basic client management
3.  Core **expense tracking framework** with receipt **photo capture**
4.  **OCR Implementation (Basic)** for key core receipt data (Vendor, Date, Amount)
5.  Offline storage architecture & basic sync mechanism

**Phase 2: Core Job Context & Linking**
1.  Job management and tracking (including offline list access)
2.  **Context-Aware Job Suggestions** (basic location/recency)
3.  Manual Job-Expense Association (fallback/correction)
4.  Basic Contractor Management (Add, Edit, View, List)
5.  Contractor Payment Recording (manual association initially)

**Phase 3: Core Profitability & Allocation**
1.  **Simple Splitting UI** implementation (for expenses & contractor pay)
2.  Job profitability calculation logic
3.  Weekly financial summary view
4.  *Design/Prep:* Define data points needed for conditional tax module integration (e.g., tax fields in expense/invoice).
5.  Job list profitability indicators

**Phase 4: Core Invoicing, Reporting & Refinement**
1.  Core Invoice generation (no tax initially)
2.  Email sending capability
3.  Core financial reports (Job Profitability)
4.  Data Utilities (export functionality)
5.  UI refinements, localization, performance optimization, offline robustness improvements.
6.  *Build/Test:* Implement conditional tax activation trigger ("Tax Registration Status" setting).

**Phase 5 (Post-Core Validation): Conditional Tax Module Build & Test**
1.  Implement GST/QST calculation logic for invoices **(conditional)**.
2.  Implement GST/QST capture/tracking for expenses (incl. OCR enhancements) **(conditional)**.
3.  Build Tax Reporting features **(conditional)**.
4.  Implement Tax Settings & Guidance features **(conditional)**.
5.  Integrate conditional features into UI, controlled by activation trigger.
6.  End-to-end testing of Core + Conditional workflows.

**Development Prioritization:** *(Revised)*
The critical delivery path for initial implementation focuses on the **Core MVP Workflow**:
1.  Core expense tracking framework with **OCR and smart suggestions**.
2.  **Simple splitting/allocation UI**.
3.  Job-expense association capabilities (leveraging automation).
4.  Basic job profitability calculation and reporting.
5.  Contractor payment tracking with allocation.
6.  Client management and core invoice generation to follow/parallel.
7.  **Conditional tax features are explicitly de-prioritized until the core is validated.**

**Technical Platform Requirements:** *(Revised for Core/Conditional)*
- Mobile-first design approach essential.
- Progressive Web App (PWA) architecture for optimal cross-platform compatibility.
- Clear offline capability scope for MVP **(focused on Core tasks)**:
    - Must work offline:
        - **Manual** core expense entry with **photo capture** (image stored locally).
        - Basic client/job list access for manual expense association (read-only).
        - Reliable data synchronization with queue-based approach when back online.
        - Clear sync status indicators.
    - Likely requires connectivity:
        - **OCR processing** (unless using robust on-device models).
        - **Smart job suggestions** (based on real-time context like GPS/Calendar).
        - Invoice creation/sending.
        - Report generation.
        - Historical data access beyond cache.
        - **Conditional Tax Module features (calculations, specific reporting)**.
- Responsive design for occasional desktop use.
- Storage strategy that accounts for mobile browser storage limitations.
- Support for bilingual interface (English/French).
- Emphasis on reliability in areas with spotty connectivity, **with graceful degradation for online-only features**.
- Architecture must support both summer (landscaping) and winter (snow removal) service tracking.
- **Requires user permissions for Camera, potentially Location/Calendar for core suggestions**.
- **Consideration for OCR service integration (cloud or on-device)**.
- Architecture must support enabling/disabling the conditional tax module based on the user's activation trigger.

**Revenue Model Direction:**
- Intended as a commercial product (not internal-only tool).
- Subscription-based pricing model preferred.
- Potentially tiered based on clients/jobs tracked or feature access (Automation features likely in paid tier, Conditional Tax Module potentially included in paid tier or separate add-on).
- Freemium approach possible (basic manual core tracking free, automation/conditional paid).
- Pricing must be affordable for small businesses and sole proprietors ($10-20/month range validated).

**Budget Approach:**
- Cost-effective development with focus on core functionality **and key automation differentiators**.
- Strict prioritization of **Core MVP** features **(conditional features deferred)**.
- Need to balance development investment against potential market returns, **potentially requiring increased budget/timeline for enhanced Core MVP**.
- Budget range to be defined based on technical approach for automation and Core MVP scope.

## Dependencies to Level 1
List of critical information needed by Level 1 (Business Requirements):
1.  [x] Target user demographic details and market size.
2.  [x] Competitive landscape analysis.
3.  [x] Primary user pain points and priorities (**emphasizing core automation needs**).
4.  [x] **Refined** core functional scope boundaries, **explicitly separating conditional tax module**.
5.  [x] Rough project timeline expectations (**revised for core-first phasing**).
6.  [x] Budget constraints for development (**potentially revised for core focus**).
7.  [x] Revenue model expectations (considering core vs. conditional features).
8.  [x] Technical platform constraints (**including core automation/offline limitations**).

## Sign-off Checklist
Before proceeding to Level 1:
- [x] All critical questions answered.
- [x] Guiding principles stated.
- [x] Assumptions documented (**including new ones for automation & conditional activation**).
- [x] Information gaps identified.
- [x] Validation plan created (**including core automation features & conditional approach**).
- [ ] Stakeholder review completed *(Pending for this revised version)*
- [x] Dependencies to Level 1 identified.

## Notes
- Focus must remain on **effortless core input** and job-profitability tracking.
- Consider potential future integrations with scheduling and payment processing.
- Must balance core offline functionality (manual) with cloud-based automation features.
- Must accommodate seasonal business patterns in financial reporting.
- Should design core with potential expansion to similar service industries in mind, leveraging flexible automation.
- The **conditional tax module** is secondary to delivering a robust, simple core experience.

## Change Log
| Date          | Version | Changed By   | Changes Made                                                                                                                                                                                                                               |
| :------------ | :------ | :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| April 7, 2025 | 0.1     | FinTrack PM  | Initial draft based on problem definition.                                                                                                                                                                                       |
| April 8, 2025 | 0.2     | Gemini Model | **Major Revision:** Incorporated automation features (OCR, Smart Suggestions, Splitting) into MVP definition based on stakeholder feedback & updated scope documents (MVP Scope v1.4). Revised sections. Added Change Log section. |
| **April 9, 2025** | **0.3** | **Gemini Model** | **Refactored based on core vs. conditional prioritization instructions:** Added Guiding Principles; Restructured MVP Definition and Phasing sections to clearly separate Core MVP and Conditional Tax Module; Applied conditional language; Refined emphasis in supporting sections. Adjusted dependencies and sign-off status. |