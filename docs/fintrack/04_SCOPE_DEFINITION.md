# Scope Definition Document - FinTrack

## Metadata
**Version:** 0.5 *(Updated for Enhanced MVP Scope v1.4 & Core/Conditional Prioritization)*.
**Status:** Draft.
**Last Updated:** April 9, 2025.
**Owner:** FinTrack Project Manager.
**Reviewers:** [To be determined].

## Dependencies
**Required Artifacts:**
- Problem Statement Document *(Reflecting enhanced MVP & Core/Conditional)*
- User Needs Analysis *(v1.6 or later)*
- Problem Domain Model *(v0.5 or later)*
- **MVP Feature Scope Document (v1.4 or later)** *(Aligns with enhanced scope)*

**Dependent Artifacts:**
- Business Case Document
- Solution Vision Document
- Project Timeline and Budget
- Technical Specifications Document

## **Guiding Principles**

1.  ***Core Experience Priority:*** The primary user experience focuses on effortless core features (jobs, expenses, profitability), remaining simple and functional independently of conditional modules.
2.  ***Integrated Conditional Design:*** While core workflow is primary, design core components anticipating logical integration points for optional conditional features (like taxes) to ensure smooth user transitions and efficient development.

## Purpose
This document clearly defines the boundaries, constraints, and assumptions of the FinTrack project to establish a shared understanding of what is and is not included in the solution. It emphasizes the priority of the **core workflow** while defining the scope of the **optional, conditional tax module**. It serves as a reference point for scope management throughout the project lifecycle and sets realistic expectations for all stakeholders. This version reflects an enhanced MVP scope focused on effortless input via automation within the core framework.

## Success Criteria
- [x] Project boundaries are clearly defined and agreed upon, **distinguishing core and conditional scope**.
- [x] In-scope and out-of-scope items are explicitly documented, **aligned with core/conditional model**.
- [x] Key constraints are identified and analyzed, **considering core and conditional aspects**.
- [x] Critical assumptions are documented and validated, **reflecting core/conditional approach**.
- [x] Acceptance criteria for minimum viable solution are established, **focusing on core validation first**.
- [x] Phased implementation approach **prioritizing core delivery** is outlined.

## Content Requirements
1. Project Boundaries
2. In-Scope/Out-of-Scope Items
3. Key Constraints
4. Critical Assumptions
5. Minimum Viable Solution Definition **(Structured Core vs. Conditional)**
6. Future Phase Considerations

## Validation Methods
- [ ] Review with key stakeholders
- [x] Consistency check with Problem Statement, User Needs, Problem Domain Model, **MVP Feature Scope v1.4 (interpreted through core/conditional lens)**
- [x] Verification of alignment with project goals **(Core Experience Priority)**
- [x] Assessment of scope feasibility (**given enhanced core MVP and deferred conditional module**)
- [ ] Stakeholder sign-off

## Content

### 1. Project Boundaries *(Revised for Core/Conditional Emphasis)*

#### 1.1 Solution Scope
FinTrack is a financial management application specifically designed for small landscaping, lawn care, and related service businesses (e.g., snow removal, cleaning) in Quebec. The solution focuses on providing **effortless core** financial tracking features essential for these businesses, including **automated expense capture via OCR**, context-aware job suggestions, simple expense splitting, job profitability tracking, client management, and basic contractor management (add/edit/view/track payments). **Optional, conditional features** activated by the user (based on their tax registration status) handle Quebec-specific tax handling (GST/QST calculation and informational guidance). The solution will not address comprehensive accounting needs, payroll processing, or detailed scheduling/dispatching functionality in the MVP.

#### 1.2 User Scope
The solution targets three primary user personas:
- Solo Operators (individuals who handle all aspects of their business themselves) - **Primarily needs core features, may optionally enable tax features.**
- Small Crew Owners (businesses with 2-10 employees or contractors) - **Needs core features, likely enables conditional tax features based on status.**
- Prospective/Early-Stage Operators (individuals planning to start or who recently started a service business) - **Needs simple core features, may enable tax features later.**

The solution does not target medium or large enterprises, franchises, or businesses significantly outside the field service industry focus in the initial phases.

#### 1.3 Functional Scope *(Revised for Core/Conditional)*
The **core functional scope** includes:
- User account settings and basic business profile (including **Tax Registration Status setting** for conditional activation)
- Client information management (add/edit/view)
- Job/work tracking and profitability calculation (**core basis**)
- **Mobile-friendly expense tracking with automated OCR receipt capture (core data: Vendor/Date/Amount) & smart job suggestions**
- **Simple expense splitting UI (for consumables & contractor pay)**
- Basic invoicing (**core: no tax**)
- Basic contractor management (add/edit/view) and payment tracking (incl. splitting)
- Simple financial reporting (**core: profit summary**)
- Offline capability for essential **core** functions (manual entry, photo capture, basic data view)
- Bilingual interface (English/French)

The **conditional functional scope (Tax Module)**, activated by user setting, includes:
- Quebec-specific GST/QST support (calculation on invoices, tracking on expenses - potentially via enhanced OCR)
- Tax status monitoring & informational guidance links
- Basic tax reporting summaries

#### 1.4 Technical Scope *(Revised for Core/Conditional)*
The solution will be developed as a Progressive Web App (PWA) with:
- Mobile-first design approach
- Responsive design for occasional desktop use
- **Offline capabilities for essential core manual functions & data viewing**
- **Cloud integration for advanced core features (OCR, potentially sync logic)**
- **Consideration for context data access (GPS/Calendar permissions for core suggestions)**
- Cross-platform compatibility
- Secure cloud data storage
- Bilingual support
- **Architecture supporting activation/deactivation of conditional tax features based on the Tax Registration Status setting.**

#### 1.5 Organizational Scope
The solution impacts the core financial management processes of small service businesses, including:
- Expense tracking and categorization (**streamlined via core automation**)
- Revenue tracking and client management (**core**)
- Job costing and profitability analysis (**core**)
- Invoice generation and payment tracking (client payments - **core**)
- Contractor payment tracking (**with core allocation**)
- **Optional:** Tax management (GST/QST calculation, reporting preparation, informational guidance - **conditional**)

### 2. In-Scope/Out-of-Scope Items *(Revised for Core/Conditional)*

#### 2.1 In-Scope Items (Core MVP)

| Category | Item | Description | Priority | Justification |
|----------|------|-------------|----------|--------------|
| Account Settings & Profile | User Authentication | Secure login and account management | High | Foundation for secure data access |
| Account Settings & Profile | Business Profile | Basic business information storage, **incl. Tax Registration Status setting** | Medium | Required for invoicing and context, activation trigger |
| Account Settings & Profile | Language Preference | Toggle between English and French | Medium | Essential for Quebec market |
| Client Management | Add/Edit/View Clients | Create, update, and view client contact information | High | Foundation for job tracking and invoicing |
| Client Management | Client Type Tracking | Differentiate one-time vs. recurring clients | Medium | Supports business relationship management |
| Client Management | Client Search & Filter | Find clients quickly | Medium | Improves efficiency in the field |
| Job Management | Job Creation & Tracking | Record job details and status | Critical | Core unit for measuring profitability |
| Job Management | Job-Client Association | Link jobs to specific clients | Critical | Essential for organization and tracking |
| Job Management | Job Profitability Calculation | Calculate profit/loss per job (incl. contractor costs, **core basis**) | Critical | Key business insight demanded by users |
| **Expense Tracking (Core)** | **Mobile Expense Entry with OCR (Core Data) & Smart Suggestions** | **Quick expense logging via OCR (Vendor/Date/Amount)/manual, with context-aware job suggestions** | **Critical** | **Core "ease of use" value prop** |
| **Expense Tracking (Core)** | **Receipt Image Capture & Storage** | **Photograph and store receipt images (source for OCR)** | **Critical** | **Supports compliance & OCR** |
| **Expense Tracking (Core)** | **Simple Expense Splitting UI** | **Allocate single expense across multiple jobs intuitively** | **High** | **Handles shared costs accurately** |
| Expense Tracking (Core) | Expense Categorization | Organize expenses by type (Fuel, Materials, etc.) | High | Supports financial analysis |
| Expense Tracking (Core) | Job-Expense Association | Link expenses to specific jobs (facilitated by suggestions) | Critical | Required for accurate job costing |
| Invoicing (Core) | Invoice Creation | Generate professional invoices (**no tax**) | High | Professionalizes business image |
| Invoicing (Core) | PDF Export | Export invoices as PDF | Medium | Client delivery method |
| Invoicing (Core) | Email Sending | Send invoices via email | Medium | Client delivery method |
| Payment Tracking (Client) | Payment Recording | Track client payments against invoices or jobs | High | Cash flow monitoring |
| Payment Tracking (Client) | Payment Method Tracking | Track cash, e-transfer, check payments | Medium | Reflects business reality |
| Contractor Management | Basic Contractor Management | Add, edit, and view basic contractor contact info | Medium | Foundation for tracking payments |
| **Contractor Management** | **Contractor Payment Tracking with Splitting** | **Record & allocate payments to contractors across jobs** | **High** | **Needed for accurate job costing & expense tracking** |
| Financial Reporting (Core) | Job Profitability Report | Show profit/loss by job (**core basis**) | High | Informs business decisions |
| Financial Reporting (Core) | Weekly/Monthly Summary | Show overall financial health (**core basis**) | Medium-High | Quick business health check |
| Financial Reporting (Core) | Export to CSV/PDF | Export core data for external use | Medium | Integration with accountant workflows |
| **Technical Features (Core)** | **Offline Expense Entry (Manual/Photo Capture)** | **Record basic core expense info & photo without internet** | **Critical** | **Field usage requirement** |
| Technical Features (Core) | Data Synchronization | Sync core data when connectivity returns | Critical | Ensures data integrity |
| Technical Features (Core) | Bilingual Interface | Support English and French | Medium | Quebec market requirement |

#### 2.2 In-Scope Items (Conditional Tax Module - Enabled by User Setting)

| Category | Item | Description | Priority | Justification |
|----------|------|-------------|----------|--------------|
| **Tax Features** | GST/QST Calculation & Tracking | Monitor collected and paid taxes accurately (aided by OCR tax capture if enabled) | High (Conditional) | Compliance requirement for registered users |
| **Tax Features** | Tax Status Monitoring & Guidance | Track revenue against tax thresholds; provide informational alerts & links to official resources | High (Conditional) | Supports growing/formalizing businesses; addresses key user anxiety |
| **Tax Features** | Tax Filing Reports | Generate basic summary reports for tax filing preparation | Medium-High (Conditional) | Reduces administrative burden for registered users |
| Invoicing (Conditional) | Tax Calculation on Invoices | Apply appropriate taxes when required/enabled | High (Conditional) | Extends core invoicing for compliance |
| Expense Tracking (Conditional) | Tax Detail Capture (OCR/Manual) | Capture/track GST/QST paid on expenses | High (Conditional) | Enables ITC tracking for registered users |

#### 2.3 Out-of-Scope Items

*(Reviewed and adjusted based on core/conditional split)*

| Category | Item | Description | Rationale for Exclusion | Future Consideration? |
|----------|------|-------------|--------------------------|----------------------|
| Advanced Accounting | Full Accounting Suite | Double-entry accounting, balance sheets, etc. | Exceeds user needs, adds complexity | No |
| Advanced Accounting | Depreciation Tracking | Complex asset depreciation calculation | Beyond MVP needs (Core or Conditional) | Yes (Phase 3+) |
| Financial Management | Payroll Processing | Employee payroll management | Outside contractor focus for MVP | Yes (Phase 3+) |
| Financial Management | Personal Finance | Personal expense/income tracking | Outside business focus | No |
| Financial Management | Bank Integration | Direct bank account connections | Adds complexity, security concerns (Postponed) | Yes (Phase 2+) |
| Operations | Detailed Crew/Contractor Scheduling | Staff/contractor scheduling and dispatch | Outside financial focus | Yes (Phase 3+) |
| Operations | Route Optimization | Job location mapping and routing | Outside financial focus | Yes (Phase 3+) |
| Operations | Equipment Tracking | Detailed equipment management | Outside core financial needs | Yes (Phase 3+) |
| Client Management | CRM Features | Advanced customer relationship management | Beyond MVP needs | Yes (Phase 3+) |
| Client Management | Client Portal | Client self-service portal | Adds significant complexity | Yes (Phase 3+) |
| Contractor Management | Advanced Contractor Features | Contract management, onboarding, communication tools, time tracking | Beyond basic payment tracking/splitting for MVP | Yes (Phase 2+) |
| Marketing | Marketing Tools | Lead tracking, campaign management | Outside financial focus | No |
| Integrations | Full Accounting Software Integration | QuickBooks, Xero, etc. integration | Adds complexity to MVP | Yes (Phase 2+) |
| Integrations | Calendar Integration | Sync with Google/Apple calendars *(Note: Read-only access might be needed for core suggestions)* | Outside core financial *tracking* focus | Yes (Phase 2+) |
| Integrations | Payment Processing | Direct payment acceptance | Additional regulatory requirements | Yes (Phase 2+) |
| Technical | Native Mobile App | iOS/Android native applications | PWA meets initial core needs more cost-effectively | Yes (Phase 3+) |
| Technical | **Complex Offline Operations** | **Full OCR, smart suggestions offline, conditional tax features offline** | **Significant technical complexity, storage limitations** | Partial (Phase 2+) |
| **Expense Tracking** | **Advanced OCR (Line items, validation)** | **Increases complexity beyond basic core data capture** | Yes (Phase 2+) |
| **Expense Tracking** | **Automatic Mileage Tracking** | **Dedicated feature, adds complexity** | Yes (Phase 2+) |

### 3. Key Constraints *(Revised for Core/Conditional)*

#### 3.1 Business Constraints

| ID | Constraint | Description | Impact | Mitigation Strategy |
|----|------------|-------------|--------|---------------------|
| BC-1 | Budget Limitations | Development budget must be managed carefully, **prioritizing core MVP features** | Limits feature scope and development time for core; defers conditional module build | Strict prioritization, focus on core value, phased rollout |
| BC-2 | Price Sensitivity | Target users can only afford $10-20/month | Limits revenue potential; **core features must provide value; conditional features may influence tiering** | Tiered pricing model, focus on high-value core features first, validate perceived value of automation & conditional module |
| BC-3 | Market Size | Initial focus on Quebec service businesses | Limited initial market | Design core for future expansion |
| BC-4 | Time to Market | Need to release **core MVP** for upcoming busy season | Compressed development timeline for core | Phased approach (Core first), focus on most critical core automation |
| BC-5 | Competitive Landscape | Competing with established accounting tools | Challenging market entry | Focus on niche pain points (effortless core input, job costing, seamless conditional QC tax handling) |

#### 3.2 Technical Constraints

| ID | Constraint | Description | Impact | Mitigation Strategy |
|----|------------|-------------|--------|---------------------|
| TC-1 | Mobile-First Requirement | Primary use on mobile devices in field | Limits UI complexity and screen space for core workflows | Simplified core workflows, progressive disclosure of features |
| TC-2 | Offline Functionality | Must work offline **for core manual entry/capture**; **Advanced automation (OCR, suggestions) & conditional tax features likely require connectivity** | Increases complexity of core data management; manage user expectations for online features | Robust offline-first architecture for *core manual* entry/capture; clear sync mechanisms; graceful degradation of advanced/conditional features offline |
| TC-3 | Mobile Storage Limitations | Limited storage on mobile devices | Restricts amount of offline data (esp. images) | Prioritize essential core offline data, clear cache strategies, image compression |
| TC-4 | Bilingual Support | Must support English and French | Increases content management complexity for core & conditional UI | Standardized translation framework, separated content |
| TC-5 | Cross-Platform Compatibility | Must work across iOS/Android/desktop | Development and testing complexity for core PWA | PWA approach, responsive design principles |
| TC-6 | Quebec GST/QST Rules | **Conditional module** must implement accurate Quebec tax calculations & provide appropriate guidance links; **OCR must accurately capture tax fields if enabled** | Increases conditional tax logic complexity; requires careful design for integration | Consult with tax expert, separate tax module, curated official links, user disclaimers, OCR validation for tax |
| **TC-7** | **OCR Accuracy & Reliability (Core)** | **OCR technology is not perfect for core data capture** | **Potential user frustration if accuracy is low for core tasks** | **Set realistic accuracy targets, provide easy editing, potentially use hybrid OCR (cloud/device)** |
| **TC-8** | **Context Data Permissions (Core)** | **Core smart suggestions require user permission for GPS/Calendar** | **Feature utility reduced if permissions denied** | **Clear explanation of value exchange, privacy policy, alternative manual selection** |
| **TC-9** | **Conditional Feature Activation** | Architecture must reliably enable/disable tax features based on user setting | Adds complexity to UI rendering and data handling | Clear state management based on "Tax Registration Status" setting |

#### 3.3 Resource Constraints

| ID | Constraint | Description | Impact | Mitigation Strategy |
|----|------------|-------------|--------|---------------------|
| RC-1 | Development Team Size | Limited development resources | Extends timeline or limits features; **increased pressure for core automation** | Prioritize core features, focus on core value delivery, potentially augment team |
| RC-2 | Subject Matter Expertise | Limited access to Quebec tax experts for rules & guidance content **(for conditional module)** | Risk of tax errors or misinfo in conditional module | Partner with accounting advisors, thorough validation, use official sources for links |
| RC-3 | User Testing Resources | Limited access to target users for testing | Risk of usability issues (esp. with core automation & conditional flow) | Early prototype testing (core first), phased rollout to beta users |
| RC-4 | Support Capabilities | Limited capacity for user support | Potential user experience issues (e.g., OCR errors, conditional feature confusion) | Self-service help resources, simple intuitive core design, clear error handling, separate guidance for conditional features |
| RC-5 | Marketing Budget | Limited funds for user acquisition | Slower initial adoption | Focused marketing to specific niche, referral incentives, highlight core automation benefits |
| **RC-6** | **Expertise in AI/ML/OCR (Core)** | **Implementing core OCR & smart suggestions requires specific skills** | **May require external expertise or library reliance** | **Choose reliable third-party services or libraries, allocate time for integration/tuning** |

#### 3.4 Schedule Constraints

| ID | Constraint | Description | Impact | Mitigation Strategy |
|----|------------|-------------|--------|---------------------|
| SC-1 | Seasonal Business | Must launch **core MVP** before peak landscaping season | Compressed timeline for core MVP | Phased approach (Core first), focus on most critical core automation first |
| SC-2 | Tax Deadline Alignment | Align **conditional tax reports** with tax filing periods | Timing pressure for conditional tax features | Ensure basic tax reports are stable *when released* post-core |
| SC-3 | Development Capacity | Limited developer hours available | Extended timeline or reduced scope; **significant impact from core automation scope** | Clear prioritization (core first), avoid scope creep |
| SC-4 | Testing Requirements | Offline/sync features require extensive testing; **Core OCR/suggestions add new testing dimensions; Conditional tax features add another layer** | Additional QA time needed | Incremental testing throughout development (core first), specific test cases for automation & conditional logic |
| SC-5 | Localization Time | Bilingual support adds translation time | Extended timeline | Parallel translation work, modular content structure |

### 4. Critical Assumptions *(Revised for Core/Conditional)*

| ID | Assumption | Description | Validation Method | Impact if Invalid | Owner |
|----|------------|-------------|-------------------|-------------------|-------|
| A-1 | Technical Skills | Users have basic smartphone proficiency **for core tasks** | User interviews, market research | UX redesign for lower technical skill | UX Designer |
| A-2 | Mobile Device Access | Target users have smartphones with cameras **for core OCR** | User interviews, market research | May need alternative input methods | Product Manager |
| A-3 | Category Commonality | Most expenses fit into standard categories **for core tracking** | User interviews, industry research | Expanded categories, custom categories | Product Manager |
| A-4 | Offline Priority | **Core manual** expense entry/capture & core data viewing are highest priority for offline use | User interviews, usage analytics | Reprioritize offline features; manage expectations for online-only advanced/conditional features | Product Manager |
| A-5 | Tax Guidance Need | Users **who enable tax features** require informational guidance (links, alerts), not advice | User interviews, legal review | Adjust conditional tax information approach | Product Manager |
| A-6 | Value Proposition | **Effortless core input (OCR/suggestions)** & Job profitability tracking are key value drivers | User interviews, market testing | Reprioritize core features based on value | Product Manager |
| A-7 | Price Point | $10-20/month is viable pricing range **for core automation value + optional tax features** | User interviews, market analysis | Revise business model or feature scope/tiering | Business Analyst |
| A-8 | Language Needs | English/French covers language requirements | Quebec market research | Add additional languages if needed | Product Manager |
| A-9 | Customer Growth | Users may grow from informal to formal operations (**triggering need for conditional tax features**) | User interviews, market research | Ensure smooth activation of conditional features | Product Manager |
| A-10 | Feature Progression | Proposed **core-first** phased approach aligns with user needs | User validation, beta testing | Reprioritize feature roadmap | Product Manager |
| A-11 | Contractor Terminology | Using "Contractor" is acceptable and understood by users | Beta testing, user feedback | Revert/adjust terminology if confusing | Product Manager |
| **A-12** | **OCR Accuracy Acceptance (Core)** | **Users will accept ~80-90% OCR accuracy for core data with easy correction** | **Beta testing, market analysis of OCR tools** | **Need higher accuracy (more cost/time) or core feature may cause frustration** | **Technical Lead** |
| **A-13** | **Context Permission Acceptance (Core)** | **Users will grant GPS/Calendar permissions for core smart suggestions** | **Beta testing, privacy review** | **Core suggestion feature less effective, need strong manual selection fallback** | **UX Designer/PM** |
| **A-14** | **Conditional Activation Viability** | Users will understand and utilize the "Tax Registration Status" setting to enable tax features when needed | Beta testing, onboarding design | Redesign activation flow if confusing; simplify conditional logic | UX Designer/PM |

### 5. Minimum Viable Solution Definition *(Revised for Core vs. Conditional)*

#### 5.1 Core MVP Workflow Criteria
The Minimum Viable Solution for FinTrack's **core workflow** must:
- Enable users to track expenses with **automated OCR receipt capture (core data)** and minimal manual input.
- Provide **smart suggestions** for associating expenses and payments with jobs.
- Offer an **intuitive UI for splitting** shared costs (consumables, contractor pay) across jobs.
- Allow users to add, edit, and view basic client and contractor information.
- Calculate job profitability based on income and expenses (including contractor costs) using a **core calculation basis**.
- Provide basic invoicing capabilities (**without tax calculations**).
- Support offline **core manual expense entry & photo capture** with reliable synchronization.
- Offer a simple weekly profit summary view (**core basis**).
- Support both English and French interfaces.
- Work efficiently on mobile devices.
- Include the **Tax Registration Status** setting in the Business Profile as the trigger for the conditional module.

#### 5.2 Conditional Tax Module (MVP Add-on) Criteria
The **conditional tax module**, activated via the user's Tax Registration Status setting, must:
- Add GST/QST calculations to invoices.
- Enable tracking of GST/QST paid on expenses (potentially enhancing OCR).
- Provide basic tax summary reports for filing periods.
- Offer tax threshold monitoring alerts and links to official guidance.
- Integrate seamlessly with the core UI when activated.

#### 5.3 MVP Features **(Core vs. Conditional)**

*(Reflecting the structure from MVP Feature Scope v1.4, now categorized)*

**Core MVP Features (Always Active):**

| Feature Area | Description | Must-Have Functionality | Could-Have Functionality |
|--------------|-------------|--------------------------|-----------------------|
| Account Settings & Profile | Account creation and authentication | Basic registration, login, password reset, language preference, **Tax Registration Status setting** | Business profile customization |
| Client Management | Tracking client information | **Add/Edit/View basic client details** (name, contact, address), client listing | Client type (recurring/one-time), notes, search/filter |
| Job Tracking | Recording job details and status | Job creation with client association, basic details, status tracking | Job categories, detailed job notes |
| **Expense Tracking (Core)** | Recording business expenses | **Expense entry (OCR-Core/Manual), Receipt photo capture, Basic categories, Context-aware job suggestions, Simple splitting UI, Offline manual/capture capability, Job association** | Vendor management, custom categories |
| Invoice Creation (Core) | Generating client invoices | Basic invoice creation, job association, PDF export | Email sending, basic templates |
| Payment Tracking (Client) | Recording payments received | Basic payment recording (date, amount, method) against invoice/job, payment status | Payment history, partial payments |
| **Contractor Management** | Basic contractor tracking | **Add/Edit/View contractor contacts**, contractor listing, **Basic payment recording with job suggestions & splitting UI** | Contractor list/search |
| Financial Reporting (Core) | Business financial insights | Job profitability calculation (**core basis**), weekly profit summary | Historical comparisons, graphical reports |
| **Offline Functionality (Core)** | Working without internet | **Offline manual expense entry, receipt capture, offline view of client/job list (read-only), data synchronization** | Conflict resolution UI |
| Bilingual Support | English and French interface | Core interface elements in both languages | Complete help documentation in both languages |
| **Data Utilities (Core)** | Basic data handling | Export core data (CSV), basic backup concept | Import data |

**Conditional Tax Module Features (Activated by Setting):**

| Feature Area | Description | Must-Have Functionality | Could-Have Functionality |
|--------------|-------------|--------------------------|-----------------------|
| **Tax Features (Conditional)** | Quebec GST/QST handling | Basic tax calculation on invoices, tax paid tracking on expenses (aided by OCR), Tax threshold alerts, Links to official tax guidance | Tax report generation for filing prep |
| Invoice Creation (Conditional Enhancement) | Adding tax to invoices | GST/QST calculation added to existing core invoice | N/A (enhances core) |
| Expense Tracking (Conditional Enhancement) | Tracking tax on expenses | Capture/Track GST/QST paid (OCR/Manual) | N/A (enhances core) |

#### 5.4 MVP Success Measures *(Revised for Core Focus)*
The **Core MVP** will be considered successful if:
1. Users can track core expense data with >80% OCR accuracy for Vendor/Date/Amount (target).
2. Users successfully utilize core smart suggestions and splitting features with high satisfaction.
3. Core job profitability calculations are accurate based on linked data.
4. Offline *core manual* expense entry works reliably with >95% sync success.
5. Users report spending at least **40%** less time on core financial administration.
6. Users can successfully add/edit/view clients and contractors.
7. Users can successfully navigate core functions in their preferred language.
8. Beta users confirm the value of core automation features.
9. 70% of beta users express willingness to pay within the $10-$20/month range **for the core automated features alone**.

*(Success measures for the conditional tax module will be defined closer to its development phase.)*

### 6. Future Phase Considerations *(Revised for Core/Conditional Phasing)*

*(Phase 1 is now the Conditional Tax Module integration)*

| Feature/Item | Description | Tentative Phase | Prerequisites | Business Value |
|--------------|-------------|-----------------|---------------|---------------|
| **Conditional Tax Module Integration** | **Full build, test, and release of the tax features defined in MVP scope** | **Phase 1 (Post-Core)** | **Stable Core MVP, Activation Trigger** | **High for registered businesses** |
| Advanced Tax Reporting | Comprehensive GST/QST reports for filing | Phase 2 | Conditional Tax Module | High for registered businesses |
| Contract Management | Creating and managing service contracts | Phase 2 | Basic client management | Medium for recurring clients |
| Bank Integration | Connecting to bank accounts for transaction import | Phase 2 | Secure data architecture | High for reducing manual entry |
| **Advanced Receipt Management** | **Line-item OCR, validation, auto-categorization** | **Phase 2/3** | **Basic Core OCR in MVP** | **Medium for efficiency** |
| **Mileage Tracking (Dedicated)** | **Automated GPS mileage logging & calculation** | **Phase 2/3** | **Basic GPS context in MVP** | **High for relevant businesses** |
| Advanced Contractor Mgmt | Time tracking, communication, contracts | Phase 3 | Basic Contractor Management | High for businesses with crews |
| Calendar Integration (Full Sync) | Sync with business calendars | Phase 3 | Job scheduling (Future) | Medium for organization |
| Quote/Estimate Creation | Create professional quotes before jobs | Phase 2/3 | Basic invoicing | Medium for sales process |
| Customer Portal | Client self-service for invoices/payments | Phase 3 | Invoicing system | Low-Medium for client convenience |
| Native Mobile Apps | iOS and Android native applications | Phase 3 | Proven PWA success | Medium for user experience |
| Additional Service Industries | Support for other service types beyond initial focus | Phase 2+ | Flexible core service model | High for business growth |
| Route Optimization | Efficient job routing and scheduling | Phase 4 | Job location tracking | Medium for efficiency |
| Equipment/Inventory Management | Track equipment, maintenance, inventory | Phase 4 | Expense tracking | Medium for asset management |
| Advanced Business Analytics | Predictive insights, benchmarking | Phase 4 | Baseline reporting | Medium for business planning |

## Assumptions *(Revised for Core/Conditional)*
- [x] The primary user base consists of small service businesses with 1-10 workers/contractors.
- [x] Users prioritize **effortless core input** and simplicity over comprehensive features.
- [x] Mobile functionality is more important than desktop functionality for **core tasks**.
- [x] Both informal and formal business operations exist in the target market, **necessitating the core/conditional split**.
- [x] Quebec GST/QST regulations will remain relatively stable **for the conditional module**.
- [x] **An enhanced Core MVP with core automation is feasible within adjusted project constraints.** *(Assumption carried over)*
- [x] **The conditional tax module can be effectively integrated post-core validation.**

## Risks *(Revised for Core/Conditional)*
- [x] Risk 1: **Offline functionality limitations for advanced core automation features (OCR, suggestions) may cause confusion.**
   - Impact: User frustration if expectations aren't managed.
   - Mitigation: Clear UI indicators for online/offline status and feature availability; robust core manual fallbacks.
- [x] Risk 2: **Conditional module:** Quebec tax rules/guidance may be implemented incorrectly or misinterpreted; **OCR tax capture errors (if enabled).**
   - Impact: Legal and financial exposure for users *who enable the module*, loss of trust.
   - Mitigation: Tax expert consultation, clear disclaimers, use official sources, user verification/editing of OCR data, thorough testing *of the module*.
- [x] Risk 3: **Enhanced core feature scope significantly exceeds development capacity/timeline/budget, delaying core or conditional release.**
   - Impact: Delayed launch, quality issues, budget overruns.
   - Mitigation: Strict prioritization within core MVP, realistic timeline adjustment, potential need for more resources for core.
- [x] Risk 4: User adoption may be slower than anticipated if core automation isn't reliable or permissions are denied.
   - Impact: Reduced revenue, failing to reach critical mass.
   - Mitigation: Focus on core pain points, thorough beta testing of core automation, clear value prop for permissions.
- [x] Risk 5: Competitors may release similar targeted solutions.
   - Impact: Market share pressure, price competition.
   * Mitigation: Accelerate development of differentiating core features (automation), build strong local presence.
- [x] **Risk 6: Core OCR accuracy may not meet user expectations.**
    - Impact: Frustration, manual correction negates time savings.
    - Mitigation: Set clear accuracy targets, choose reliable OCR tech, design easy correction workflow for core data.
- [x] **Risk 7: Conditional feature activation/deactivation flow is confusing.**
    - Impact: Users struggle to enable/disable tax features correctly, leading to errors or frustration.
    - Mitigation: Intuitive design for the "Tax Registration Status" setting and clear indication of feature status in the UI.

## Review Notes
- [ ] Review 1
   - Reviewer: [Name]
   - Date: [Date]
   - Comments: [Comments]
   - Status: [Status]

## Change Log
| Date          | Version | Changed By   | Changes Made |
| :------------ | :------ | :----------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| April 7, 2025 | 0.1     | FinTrack PM  | Initial creation of Scope Definition Document |
| April 7, 2025 | 0.2     | FinTrack PM  | Incorporated review suggestions: Standardized terminology ("Contractor"); Clarified scope of Tax Guidance (informational links/alerts) in MVP; Ensured consistency with MVP Feature Scope details. Added A-11 assumption. Updated Risk 2. |
| April 8, 2025 | 0.3     | Gemini Model | Aligned feature names (Tax Features) & scope details (Contractor Add/Edit) with MVP Feature Scope v1.3. Updated MVP Features table for clarity. Minor wording consistency adjustments. |
| April 8, 2025 | 0.4     | Gemini Model | **Major Revision:** Updated scope definition to align with enhanced MVP (MVP Feature Scope v1.4) incorporating OCR, smart suggestions, and expense splitting into the core MVP based on stakeholder feedback. Updated Boundaries, In/Out Scope, Constraints, Assumptions, MVP Definition, Future Phases, Risks. |
| **April 9, 2025** | **0.5** | **Gemini Model** | **Refactored based on core vs. conditional prioritization instructions:** Added Guiding Principles; Restructured MVP Definition (Sec 5) for Core vs. Conditional; Explicitly categorized In-Scope items; Applied conditional language and emphasis throughout; Adjusted phasing/priorities. Ensured full document output. |

## Sign-off
- [ ] Technical Review
- [ ] Business Review
- [ ] Stakeholder Review
- [ ] Final Approval

## Next Steps
- **Re-validate revised scope definition (v0.5) with key stakeholders, emphasizing core-first approach and conditional module plan.**
- **Re-assess technical feasibility & timeline for enhanced Core MVP features (OCR, suggestions, offline limitations).**
- Refine phased implementation timeline for Core MVP delivery, followed by Conditional Tax Module.
- Develop detailed requirements based on **updated Core MVP scope**.
- Establish scope change management process.
- Proceed with solution design within **updated defined boundaries (Core first)**.