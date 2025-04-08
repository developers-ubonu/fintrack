# Interview Findings Summary

## Metadata
**Interview Date:** 2025-04-07
**Participant:** Simulated Montreal Landscaper/Snow Remover (Based on provided text)
**Business Type:** Small Crew (Implied - mentions helpers/subcontractors)
**Services Offered:** Landscaping + Snow Removal
**Language of Interview:** English (Based on provided text)
**Interviewer:** [Interviewer Name]

## Key Insights Summary
This interview strongly validated the core need for a simple, mobile-first financial tool tailored to Quebec small landscaping/snow removal businesses. Key pain points include managing receipts, accurately tracking job profitability (especially differentiating seasonal work), and handling GST/QST efficiently. The user desires simplicity over complex features, requires offline capability, and confirmed a price sensitivity around $10-$20/month. Significant time (5-10 hrs/wk) is spent on admin, and money is lost through missed deductions and inaccurate job costing.

## Problem Domain Model Impacts
Information gathered that affects our understanding of the business domain.

| Finding | Impact on Problem Domain Model | Priority |
|---------|--------------------------------|---------|
| Different workflows, contracts, and financial tracking needed for Landscaping vs. Snow Removal. | Refine `Job`, `Service`, `Contract` entities to include attributes differentiating seasons, billing models (per-visit, project, flat-rate, monthly, per storm), and associated tracking needs (e.g., `Storm Event`). | High |
| Receipt loss is a significant pain point leading to missed deductions. | Add `Receipt Image/Link` attribute to `Expense` entity. Ensure key categories (`Fuel`, `Equipment`, `Labour`, `Materials`) are well-defined. | High |
| GST/QST handling is mandatory and involves tracking supplier numbers and quarterly remittance. | Refine `TaxInfo` entity/attributes. Ensure `Invoice` and `Expense` entities correctly link to tax information and calculations. | High |
| Recurring clients are treated differently (pricing, priority) from one-time jobs. | Add `Client Type` attribute (Recurring/One-Time) to `Client` entity. | Medium |
| Common payment methods include e-transfer and cheque. | Ensure `Payment` entity includes `Payment Method` attribute covering these options. | Medium |

## Scope Definition Impacts
Information that affects project boundaries, constraints, or assumptions.

| Finding | Impact on Scope Definition | Priority |
|---------|---------------------------|---------|
| User emphasized simplicity and abandoned tools deemed too complex (Wave, FreshBooks). | Reinforce 'Simplicity' and 'Ease of Use' (especially for field use) as core design principles and constraints. Define as a key non-functional requirement. | High |
| Field work occurs in areas with potentially spotty internet. | Mandate 'Offline Capability' with reliable data sync as a core technical requirement and constraint. | High |
| User needs job costing, invoicing, tax help but not full accounting or payroll. | Confirm project boundaries: *Exclude* full payroll processing, personal budgeting/finance, complex accounting suite features. *Include* job-level profitability, expense tracking, invoicing, payment status, GST/QST management. | High |
| Field access to information (pricing, invoices, payments) is crucial for on-site decisions. | Prioritize 'Mobile-First' development (iOS initially based on user device) with essential features available on the mobile app. Web access likely needed for office tasks. | High |
| Seasonal differences require distinct handling within the tool. | Scope must include functionality to manage both landscaping (per visit/project) and snow removal (seasonal/monthly/per storm) financial logic. | High |

## Business Case Impacts
Information that affects value proposition, ROI analysis, pricing strategy, etc.

| Finding | Impact on Business Case | Priority |
|---------|------------------------|---------|
| User spends 5-10 hours/week on financial administration. | Quantify potential time savings as a key value proposition and ROI element. | High |
| User estimates $500-$1000/year lost via missed deductions (lost receipts) and ~$200-300 per instance on underbid jobs. | Quantify potential financial recovery (deductions) and risk mitigation (accurate bidding) as key value propositions and ROI elements. | High |
| Existing tools (QB Self-Employed, Wave, FreshBooks) perceived as either too complex or lacking specific Quebec support. | Strengthen competitive positioning by emphasizing simplicity, specific Quebec focus (GST/QST), and tailored workflow for landscapers/snow removers. | High |
| User considers $10-$20/month a fair price. User pays ~$240/yr for QB Self-Employed + $600-800/yr for accountant. | Validate proposed pricing strategy ($10-$20/month). FinTrack cost can be positioned favorably against current combined costs, especially if accountant time is reduced. | Medium |

## Stakeholder Requirements Impacts
Information that affects success criteria, feature prioritization, etc.

| Finding | Impact on Stakeholder Requirements | Priority |
|---------|-----------------------------------|---------|
| User provided clear "Must-Haves": Track jobs (time, materials), Calc profit/job, GST/QST manage, Invoice/payment track, Mobile app w/ offline. | Define the Minimum Viable Product (MVP) feature set based directly on these user needs. | High |
| User provided clear "Deal-Breakers": No Quebec tax support, Too complex, Requires constant internet. | Document these as critical constraints and failure conditions. Must be addressed by the solution. | High |
| User desires simplicity and quick operation, especially in the field. | Add/Prioritize 'High Usability' and 'Efficiency' as key Non-Functional Requirements. | High |
| User identified "Nice-to-Haves": Integrations (Square, Interac, QB, RQ APIs, Calendar), Invoice reminders, Routing, CNESST tracking. | Populate product backlog with these features for future consideration post-MVP. | Medium |
| User measures success by less tax stress, less admin time, profit visibility, fewer errors, faster payments. | Define User Acceptance Criteria (UAC) and success metrics based on these desired outcomes. | High |

## New Requirements Discovered
Requirements that weren't previously identified but should be considered.

| Requirement | Rationale | Priority | Affected Artifact(s) |
|------------|-----------|----------|---------------------|
| Mobile Receipt Capture | Addresses major pain point of lost receipts and facilitates accurate expense tracking for deductions. | High | PDM, Scope, Req, BC |
| Distinct Handling for Seasonal Contract Types | Reflects the fundamentally different billing and operational models for landscaping vs. snow removal, essential for accurate tracking. | High | PDM, Scope, Req |
| Storm Event Tracking (for Snow Removal) | Needed to manage client visits/service delivery against flat-rate seasonal snow contracts and resolve potential disputes. | Medium | PDM, Scope, Req |
| Simple GST/QST Remittance Summary | To directly support the user's quarterly tax obligations beyond just calculating tax on invoices/expenses. | Medium | Req, Scope |

## Challenged Assumptions
Previously held assumptions that were challenged by this interview.

| Original Assumption | Challenge | Recommended Action | Priority |
|--------------------|-----------|-------------------|---------|
| Generic small business finance tools might be "good enough". | User explicitly abandoned tools (Wave, FreshBooks) due to complexity or lack of specific Quebec tax support. | Prioritize simplicity and dedicated Quebec GST/QST features over breadth of generic accounting features. | High |
| Reliable internet connectivity can be assumed in the work environment. | User highlighted spotty internet in some areas and the need to work offline. | Design and build with an offline-first approach for mobile field use. | High |
| Users might desire a comprehensive, all-in-one accounting suite. | User explicitly wants to keep some tasks (personal budgeting, potentially payroll) separate and avoids overly complex tools. | Maintain focus on core job costing, invoicing, expense tracking, and tax simplification; avoid scope creep into full accounting. | High |

## Quebec-Specific Insights
Information specific to operating in the Quebec market.

| Finding | Impact | Affected Artifact(s) |
|---------|--------|---------------------|
| GST/QST handling (collection, supplier numbers, quarterly remittance via Revenu Québec) is mandatory and a pain point. | Requires dedicated, accurate GST/QST calculation, tracking, and reporting features. Core requirement. | PDM, Scope, Req, BC |
| Awareness/need to manage CNESST compliance for subcontractors. | Potential value-add/differentiator ("Nice-to-Have" feature). | Req, Scope |
| Common use of Interac e-transfer for payments. | Ensure payment tracking supports this method; consider integration if feasible. | PDM, Req |
| Need for French language support (Implicit, given location). | UI/UX must support French. | Req |

## Seasonal Considerations
Information about differences between summer (landscaping) and winter (snow removal) operations.

| Finding | Impact | Affected Artifact(s) |
|---------|--------|---------------------|
| Different workflows (scheduled landscaping vs. reactive snow removal). | May influence scheduling/routing features (if added) and UI/UX design to easily switch context or manage different job types. | PDM, Req |
| Different billing models (per visit/project vs. flat-rate/monthly/per storm). | Requires flexible invoicing, contract management, and profitability calculation logic within the tool. | PDM, Scope, Req |
| Different equipment and materials used seasonally. | Expense categorization should accommodate items specific to each season (e.g., mulch vs. salt). | PDM |

## Technical Environment Findings
Information about devices, connectivity, and technical constraints.

| Finding | Impact | Affected Artifact(s) |
|---------|--------|---------------------|
| Uses iPhone (field) / Windows laptop (office). | Requires robust iOS mobile app and complementary web application. | Scope, Req |
| Uses QuickBooks Self-Employed, Square, Google Calendar, Google Sheets, WhatsApp. | Identifies direct competitor (QB SE), key integration opportunities (Square, Calendar), and current manual workarounds (Sheets). | BC, Req, Scope |
| Needs offline capability due to potentially unreliable internet in work areas. | Core technical requirement impacting architecture and design. | Scope, Req |
| Prefers simple and quick mobile apps. | Emphasizes usability and performance requirements for the mobile application. | Req |

## Direct Quotes
Notable quotes that provide valuable insight or context.

| Quote | Context | Relevance |
|-------|---------|-----------|
| "Reconciling payments and categorizing expenses at tax time. I tend to procrastinate and rush near deadlines." | Describing the most frustrating part of financial management. | Highlights key pain points (reconciliation, categorization, tax stress) and user behavior. |
| "Misplaced receipts likely cost me $500–$1,000 in deductions last year." | Quantifying losses from poor tracking. | Provides concrete data for the value proposition (financial recovery). |
| "[Deal-breakers?] No Quebec tax support. Too complex for on-site use. Requires constant internet access." | Defining absolute requirements/failure conditions. | Sets critical constraints for the product design and MVP. |
| "$10–$20/month if it saves time and simplifies taxes." | Stating a fair price point. | Provides a benchmark for pricing strategy linked directly to core value props. |
| "Very important. I make many decisions on-site and often need quick access to pricing, invoices, and payment records." | On the importance of field access. | Justifies the need for a robust, accessible mobile application with key data available. |

## Follow-up Actions
Specific actions needed based on this interview.

| Action | Owner | Due Date | Priority |
|--------|-------|----------|---------|
| Update Problem Domain Model with identified entities/attributes/relationships. | [BA/Product Owner Name] | 2025-04-14 | High |
| Update Scope Definition Document (boundaries, constraints, core scope). | [BA/Product Owner Name] | 2025-04-14 | High |
| Integrate quantitative findings (time/cost savings) into Business Case value proposition. | [BA/Product Owner Name] | 2025-04-14 | High |
| Refine Stakeholder Requirements list (Must-Haves, Nice-to-Haves, Non-Functionals). | [BA/Product Owner Name] | 2025-04-14 | High |
| Schedule next 4-6 interviews targeting mix of solo/small crew, snow/no snow operators to validate findings. | [Researcher/BA Name] | 2025-04-11 | High |
| Draft initial user stories for core MVP features based on Must-Haves. | [BA/Product Owner Name] | 2025-04-18 | Medium |

## Validation Status
Track which findings have been validated across multiple interviews.

| Finding | Validation Status | Corroborating Interviews |
|---------|------------------|--------------------------|
| Need for specific Quebec GST/QST handling | Needs Validation | [This Interview ID] |
| Need for simplicity & mobile-first w/ offline | Needs Validation | [This Interview ID] |
| Core pain points: Job profitability, receipt/expense tracking, admin time | Needs Validation | [This Interview ID] |
| Significant differences in managing landscaping vs. snow removal | Needs Validation | [This Interview ID] |
| Price sensitivity around $10-$20 / month | Needs Validation | [This Interview ID] |

## Notes for Problem Domain Model
Incorporate: `Job` (w/ JobType, Season, Duration, MaterialsUsed, TeamMembers), `Service` (linked to Job), `Client` (w/ ClientType), `Expense` (w/ Category, ReceiptImage), `Invoice` (w/ GST, QST, PaymentStatus), `Payment` (w/ PaymentMethod), `TaxInfo` (GST/QST rates, supplier #s), `Contract` (linking Client to seasonal/recurring Services, e.g., `SnowContract`), potentially `StormEvent`. Ensure relationships support tracking job profitability linking revenue (Invoice/Contract) to costs (Expense, Time/Labour).

## Notes for Scope Definition Document
Reiterate Core Scope: Job Costing (Time, Material, Labour tracking -> Profitability), Expense Management (incl. receipt capture), Invoicing (w/ QC Tax), Payment Tracking, Mobile & Offline access. Explicit Exclusions: Full Payroll, Personal Finance, Complex Accounting features (e.g., depreciation schedules, full balance sheet). Critical Constraints: Must support Quebec GST/QST, Must be Simple/Intuitive (esp. mobile), Must work Offline. Assumptions: Users have Smartphone (iOS/Android TBD), basic tech comfort. Boundary: Focus on financial tracking directly related to job execution and basic business health, not comprehensive business management (e.g., marketing, advanced CRM).

------