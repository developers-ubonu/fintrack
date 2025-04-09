# Level 0: Problem Definition & User Needs Analysis - FinTrack
*(Reflecting Enhanced MVP Scope v1.4)*

## Core Problem Statement

### Question 1: What is the core problem we're trying to solve?
**Answer:** Small landscaping and lawn care business owners struggle to **efficiently and accurately** track job profitability, manage seasonal cash flow, organize expenses (**especially with time-consuming manual capture and allocation**), and handle client invoicing efficiently, leading to financial uncertainty, missed tax deductions, and administrative burdens that take time away from their core work.

**Evidence:** Direct feedback from landscaping business owners, industry surveys showing high administrative burden in small service businesses, high failure rate of small trade businesses due to financial mismanagement.

**Assumptions Made:**
- [x] Target users have low to moderate financial expertise
- [x] Users prefer mobile-first solutions due to field-based work
- [x] Users prioritize **simplicity and effortless input** over comprehensive accounting features
- [x] Most users currently use inadequate tools (spreadsheets, paper, generic software)
- [x] **Users will accept ~80-90% OCR accuracy with easy correction.**
- [x] **Users will grant context permissions (GPS/Calendar) if value is clear.**

**Information Gaps:**
- [x] Exact percentage of time spent on financial management vs. core work (Goal: Reduce significantly via automation)
- [x] Quantified financial impact of poor job cost tracking
- [x] Regional variations in financial management needs (Quebec-specific requirements identified)
- [ ] Integration requirements with existing tools (Calendar/GPS read-only needed for suggestions)
- [ ] User price sensitivity and willingness to pay for different feature tiers (including automation)
- [ ] Specific accessibility requirements for field conditions

**Validation Required:**
- [x] User interviews with 5-7 additional landscaping/gardening business owners
- [x] Analysis of existing financial management processes
- [x] Competitive analysis of current solutions and their shortcomings
- [ ] Verification by accounting professional with Quebec GST/QST expertise
- [ ] **Proof-of-concept for OCR accuracy, smart suggestions, splitting UI**
- [ ] **Re-validation of offline functionality feasibility considering automation limitations**
- [ ] User testing of bilingual interface
- [ ] **Validation of user acceptance for context permissions (GPS/Calendar)**

## User Analysis

### Question 2: Who are the primary users and what is their context?
**User Personas:** *(Refined goals/pain points)*
1. **Solo Operator:** Handles all aspects of the business themselves; minimal financial training; works primarily in the field; limited time for administrative tasks (**needs automation**); needs to track GST/QST for Quebec tax compliance.
2. **Small Business Owner with Crew:** Manages 2-10 employees/contractors; handles finances personally or with minimal support; balances field work with business management; requires visibility into multiple concurrent jobs; **needs efficient expense/contractor cost allocation**.
3. **Office Manager/Admin:** Works for a small landscaping business; responsible for invoicing and expense tracking; may have slightly more financial knowledge but not formal accounting training; **would benefit from streamlined data capture**.
4. **Prospective/Early-Stage Operator:** Individual planning to start or who recently started a small service business; needs guidance on tax obligations and thresholds (GST/QST); primarily operates through mobile devices; limited or no prior business administration experience; **needs extreme simplicity from day one**.

**Usage Environment:**
- Primarily mobile (in trucks, at job sites)
- Occasionally desktop (evenings/weekends for catch-up work)
- Often in areas with limited connectivity (**impacts real-time automation features**)
- May be accessing while physically tired or with dirty hands
- Bilingual environment requiring both English and French support (Quebec market)

**User Constraints:**
- **Technical:** Limited technical skills; need for intuitive interface; may have older devices; intermittent internet connectivity (**requires offline manual fallback**); **acceptance of camera/location/calendar permissions**.
- **Time:** Extremely time-constrained; needs **minimal time for data entry** and quick review; works long physical hours.
- **Resource:** Budget-sensitive; reluctant to pay for multiple specialized tools.
- **Language:** Requires bilingual support (English/French) to serve Quebec market.
- **Regulatory:** Needs to comply with Quebec's GST/QST requirements and reporting.
- **Other:** Seasonal work patterns; high variability in workload; limited accounting knowledge; paper receipt management (**target for OCR**).

**Success Criteria (User Perspective):**
1. [x] Can determine profitability of individual jobs **accurately and easily**.
2. [x] Can track and categorize expenses **with minimal manual effort** on-the-go.
3. [x] Can create and manage invoices efficiently.
4. [x] Can monitor cash flow and anticipate seasonal fluctuations.
5. [x] Can prepare for tax obligations without extensive manual work, **leveraging captured data**.
6. [x] Can separate business and personal finances clearly.
7. [x] **Spends significantly less time on financial admin due to automation.**

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

**Minimum Viable Solution:** *(Revised to align with MVP Scope v1.4)*
1. **User & Account Management:**
   - User account creation and authentication
   - Basic user profile with business information
   - Language preference setting (English/French)
   - Priority: Medium

2. **Client Management:**
   - Client database with basic information
   - Client listing with search and filter
   - Client access in offline mode (read-only)
   - Why essential: Foundation for job tracking and invoicing
   - Impact: Organizes business relationships and enables proper job attribution
   - Priority: High

3. **Job/Work Tracking:**
   - Job creation with basic details and client association
   - Job listing with search and filter
   - Job profitability calculation
   - Job access in offline mode (read-only)
   - Why essential: Core unit for measuring profitability
   - Impact: Enables linking expenses and revenue to specific work
   - Priority: Critical

4. **Mobile-friendly Expense Tracking (Automated):**
   - **Receipt Capture with basic OCR** (Vendor, Date, Amount, Tax)
   - **Manual entry fallback**
   - **Context-aware job suggestions**
   - **Simple expense splitting UI**
   - Offline *manual* expense entry & photo capture capability with sync
   - Expense listing with search and filter
   - Quebec-specific GST/QST tracking (aided by OCR)
   - Why essential: Drastically reduces manual effort and improves accuracy, core value proposition.
   - Impact: Improves accuracy, saves significant time, reduces administrative burden.
   - Priority: **Critical**

5. **Basic Invoicing:**
   - Invoice creation with client/job association
   - GST/QST tax calculations for Quebec compliance
   - PDF invoice generation
   - Email invoice sending capability
   - Why essential: Required for receiving payment and maintaining cash flow
   - Impact: Accelerates payment cycle and professionalizes business image
   - Priority: High

6. **Financial Reporting:**
   - Job profitability report (based on potentially automated data)
   - Weekly profit summary view
   - GST/QST summary report for tax filing (leveraging captured data)
   - Export reports to CSV/PDF
   - Why essential: Provides actionable insights into business health
   - Impact: Enables informed business decisions and pricing adjustments
   - Priority: Medium-High

7. **Contractor Management & Payment (with Allocation):**
    - Basic Contractor contact management (Add/Edit/View)
    - Contractor payment recording
    - **Context-aware job suggestions for payment allocation**
    - **Simple splitting UI for allocating payments across jobs**
    - Why essential: Accurately tracks major cost component for many users.
    - Impact: Ensures contractor costs are correctly factored into job profitability.
    - Priority: High

**Phased Implementation Approach:** *(Revised based on MVP Scope v1.4)*
The enhanced MVP development will follow these phases:

**Phase 1: Core Foundation & Smart Input**
1. User account system and authentication
2. Basic client management
3. Core **expense tracking framework** with receipt **photo capture**
4. **OCR Implementation (Basic)** for key receipt data
5. Offline storage architecture & basic sync mechanism

**Phase 2: Job Context & Linking**
1. Job management and tracking (including offline list access)
2. **Context-Aware Job Suggestions** (basic location/recency)
3. Manual Job-Expense Association (fallback/correction)
4. Basic Contractor Management (Add, Edit, View, List)
5. Contractor Payment Recording (manual association initially)

**Phase 3: Profitability & Allocation**
1. **Simple Splitting UI** implementation (for expenses & contractor pay)
2. Job profitability calculation logic
3. Weekly financial summary view
4. Basic Tax Features integration (GST/QST tracking)
5. Job list profitability indicators

**Phase 4: Invoicing, Reporting & Refinement**
1. Invoice generation with tax calculation
2. Email sending capability
3. Core financial reports (Job Profitability, Tax Summary)
4. Data Utilities (export functionality)
5. UI refinements, localization, performance optimization, offline robustness improvements.

**Development Prioritization:** *(Revised)*
The critical delivery path for initial implementation focuses on:
1. Core expense tracking framework with **OCR and smart suggestions**.
2. **Simple splitting/allocation UI**.
3. Job-expense association capabilities (leveraging automation).
4. Basic job profitability calculation and reporting.
5. Contractor payment tracking with allocation.
6. Client management and invoice generation to follow/parallel.

**Technical Platform Requirements:** *(Revised)*
- Mobile-first design approach essential
- Progressive Web App (PWA) architecture for optimal cross-platform compatibility
- Clear offline capability scope for MVP:
  - Must work offline:
    - **Manual** expense entry with **photo capture** (image stored locally)
    - Basic client/job list access for manual expense association (read-only)
    - Reliable data synchronization with queue-based approach when back online
    - Clear sync status indicators
  - Likely requires connectivity:
    - **OCR processing** (unless using robust on-device models)
    - **Smart job suggestions** (based on real-time context like GPS/Calendar)
    - Invoice creation/sending
    - Report generation
    - Historical data access beyond cache
- Responsive design for occasional desktop use
- Storage strategy that accounts for mobile browser storage limitations
- Support for bilingual interface (English/French)
- Emphasis on reliability in areas with spotty connectivity, **with graceful degradation for online-only features**.
- Architecture must support both summer (landscaping) and winter (snow removal) service tracking.
- **Requires user permissions for Camera, potentially Location/Calendar for suggestions.**
- **Consideration for OCR service integration (cloud or on-device).**

**Revenue Model Direction:**
- Intended as a commercial product (not internal-only tool)
- Subscription-based pricing model preferred
- Potentially tiered based on clients/jobs tracked or feature access (Automation features likely in paid tier)
- Freemium approach possible (basic manual tracking free, automation paid)
- Pricing must be affordable for small businesses and sole proprietors ($10-20/month range validated)

**Budget Approach:**
- Cost-effective development with focus on core functionality **and key automation differentiators**.
- Strict prioritization of MVP features **(scope significantly increased)**.
- Need to balance development investment against potential market returns, **potentially requiring increased budget/timeline for enhanced MVP**.
- Budget range to be defined based on technical approach for automation and overall MVP scope.

## Dependencies to Level 1
List of critical information needed by Level 1 (Business Requirements):
1. [x] Target user demographic details and market size
2. [x] Competitive landscape analysis
3. [x] Primary user pain points and priorities (**emphasizing automation needs**)
4. [x] **Enhanced** core functional scope boundaries
5. [x] Rough project timeline expectations (**potentially revised**)
6. [x] Budget constraints for development (**potentially revised**)
7. [x] Revenue model expectations
8. [x] Technical platform constraints (**including automation/offline limitations**)

## Sign-off Checklist
Before proceeding to Level 1:
- [x] All critical questions answered
- [x] Assumptions documented (**including new ones for automation**)
- [x] Information gaps identified
- [x] Validation plan created (**including automation features**)
- [x] Stakeholder review completed
- [x] Dependencies to Level 1 identified

## Notes
- Focus must remain on **effortless input** and job-profitability tracking
- Consider potential future integrations with scheduling and payment processing
- Must balance offline functionality (manual core) with cloud-based automation features
- Must accommodate seasonal business patterns in financial reporting
- Should design with potential expansion to similar service industries in mind, leveraging flexible automation core

## Change Log *(Added Section)*
| Date          | Version | Changed By   | Changes Made                                                                                                                               |
| :------------ | :------ | :----------- | :----------------------------------------------------------------------------------------------------------------------------------------- |
| April 7, 2025 | 0.1     | FinTrack PM  | Initial draft based on problem definition.                                                                                                 |
| April 8, 2025 | 0.2     | Gemini Model | **Major Revision:** Incorporated automation features (OCR, Smart Suggestions, Splitting) into MVP definition based on stakeholder feedback & updated scope documents (MVP Scope v1.4). Revised Problem Statement, User Analysis, MVP Definition, Phasing, Prioritization, Technical Req's, Assumptions. Added Change Log section. |