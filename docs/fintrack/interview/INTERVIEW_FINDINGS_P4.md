# Interview Findings Summary

## Metadata
**Interview Date:** 2025-04-07
**Participant:** Carlos (Participant 4)
**Business Type:** Prospective / Very Early Stage Solo Operator
**Services Offered:** Planning Landscaping, Snow Removal, potentially House Cleaning
**Language of Interview:** English (Implied)
**Interviewer:** [Interviewer Name]

## Key Insights Summary
Carlos represents a prospective entrepreneur planning to start a small service business (landscaping, snow removal, potentially cleaning). He wants to start organized and look professional, avoiding the pitfalls of poor tracking from the beginning. Key needs include an extremely simple, mobile-only tool for tracking per-job profitability, basic income/expenses, and crucially, *guidance* on Quebec tax rules (GST/QST thresholds, deductions) which he finds confusing. He has tried and abandoned QuickBooks as too complex. Price sensitivity is $10-20/month. Core value drivers are organization, professionalism, profit visibility, and avoiding tax stress/errors.

## Problem Domain Model Impacts
Information gathered that affects our understanding of the business domain.

| Finding | Impact on Problem Domain Model | Priority |
|---------|--------------------------------|---------|
| Plans diverse services (Landscaping, Snow, Cleaning). | `Service` / `Job` entities need flexibility to accommodate different service types beyond just landscaping/snow. | Medium |
| Wants per-job profitability tracking from the start. | Reinforces need for linking `Income` and `Expense` records to specific `Job` entities, even in a simple model. | High |
| Needs guidance on tax rules (thresholds, deductions). | `TaxInfo` model may need to support storing/presenting basic rule guidance, not just rates/calculations. Impacts how tax compliance status is determined/displayed. | Medium |
| Aims for recurring clients but has none yet; wants scheduling help. | Need for `Client` entity to support recurring status and link to potential future scheduling features. | Medium |
| Plans to accept e-transfer alongside cash. | Confirm `Payment` entity supports tracking various methods. | Medium |

## Scope Definition Impacts
Information that affects project boundaries, constraints, or assumptions.

| Finding | Impact on Scope Definition | Priority |
|---------|---------------------------|---------|
| Requires extreme simplicity; found QuickBooks too complex. | Reinforce 'Simplicity' and 'Intuitive UI' as critical NFRs, essential for user adoption, especially for those starting out. | High |
| Operates mobile-only. | Confirm 'Mobile-Only' is a valid approach for the base tier/MVP. | High |
| Explicitly needs basic tax *guidance* (not just calculation) as a Must-Have. | Scope needs to carefully consider feasibility/liability of providing tax guidance (e.g., linking to official resources vs. giving advice). Potentially a differentiator or higher-tier feature. | High |
| Wants "automatic" tracking feel. Nice-to-have: auto mileage. | Explore features reducing manual entry (e.g., quick adds, templates, potential for mileage tracking integration/estimation). | Medium |
| Nice-to-have: Estimate/Invoice Templates. | Add to backlog; supports goal of looking professional from the start. | Medium (Future) |

## Business Case Impacts
Information that affects value proposition, ROI analysis, pricing strategy, etc.

| Finding | Impact on Business Case | Priority |
|---------|------------------------|---------|
| Represents "prospective / early-stage" segment seeking tools *before* significant operations. | Identifies a target segment aiming to "start right." Value prop includes preventing future problems, establishing professionalism early. | High |
| Explicitly links tool value to avoiding high accountant fees ($2k mentioned) for basic needs. | Position the tool as a cost-effective solution for foundational financial tracking and tax prep support for startups/sole props. | High |
| Confirms $10-$20/month price range (monthly preferred initially). | Validates target pricing, including potential for slightly higher end ($20) if value (esp. tax help) is strong. | High |
| Value prop includes helping user grow faster and "not stress about taxes." | Emphasize confidence, organization, and reduced anxiety as key benefits alongside financial metrics. | High |
| Tried and failed with QuickBooks (complexity). | Reinforces competitive advantage of simplicity tailored to this user type. | High |

## Stakeholder Requirements Impacts
Information that affects success criteria, feature prioritization, etc.

| Finding | Impact on Stakeholder Requirements | Priority |
|---------|-----------------------------------|---------|
| Must-Haves: Track income/expense per job, Show profit, *Help with taxes (GST/QST)*, Mobile, Simple. | Define MVP feature set. Note the inclusion of basic tax help/guidance as essential *for this user*. | High |
| Deal-Breakers: Complicated, too many menus, desktop-only, no support for solo biz. | Confirm critical constraints, especially around UI complexity and platform access. | High |
| Nice-to-Haves support growth/professionalism: Scheduling/reminders, Estimate/invoice templates, Auto mileage, Tax preparer reports, E-transfer track, Calendar/Maps integration. | Populate backlog; consider these for tiered offering or post-MVP roadmap. | Medium (Future) |
| Success includes feeling in control, knowing profitable jobs, less tax stress, looking professional, tax readiness. | Align UAC and success metrics with these outcomes, focusing on confidence and organization for early-stage users. | High |

## New Requirements Discovered
Requirements that weren't previously identified but should be considered.

| Requirement | Rationale | Priority | Affected Artifact(s) |
|------------|-----------|----------|---------------------|
| Basic In-App Tax Guidance (QC Specific) | User explicitly needs help understanding thresholds, deductions etc. to start correctly and avoid stress/errors. | High (for this user type) | Req, Scope, BC, PDM |
| Flexibility for Diverse Service Types (e.g., Cleaning) | User plans multiple service types; tool shouldn't be rigidly limited to only landscaping/snow. | Medium | PDM, Scope, Req |
| Automatic Mileage Tracking (Nice-to-Have) | Addresses a common business expense/deduction; user mentioned wanting things "automatic". | Medium (Future) | Req, Scope |
| Estimate/Invoice Templates (Nice-to-Have) | Supports user's goal of appearing professional from the start. | Medium (Future) | Req, Scope |
| Tax Preparer Report Sharing (Nice-to-Have) | Facilitates collaboration with accountants if/when user seeks professional help, potentially reducing accountant costs. | Low (MVP) / Medium (Future) | Req |

## Challenged Assumptions
Previously held assumptions that were challenged by this interview.

| Original Assumption | Challenge | Recommended Action | Priority |
|--------------------|-----------|-------------------|---------|
| Users adopt tools primarily reactively (after facing problems). | Carlos seeks a tool proactively to *prevent* problems and start organized. | Target marketing/messaging towards prospective entrepreneurs emphasizing "starting right." | Medium |
| Basic tax knowledge (e.g., GST/QST threshold) is common among those starting a business. | Carlos explicitly lacks this knowledge and seeks guidance from the tool. | Do not assume baseline tax knowledge. Ensure any tax features are clear and potentially provide links/basic info responsibly. | High |
| Target market is strictly landscaping/snow removal. | Carlos includes "House Cleaning," suggesting related home services might be part of the user base. | Consider flexibility in service definition/categorization. Evaluate if focus should broaden slightly. | Medium |

## Quebec-Specific Insights
Information specific to operating in the Quebec market.

| Finding | Impact | Affected Artifact(s) |
|---------|--------|---------------------|
| Uncertainty about $30k GST/QST registration threshold is a key concern. | Providing clear info (or link) on this threshold within the tool would directly address a stated need. | Req (Future/Guidance) |
| Desire for guidance on Quebec-specific deductible expenses. | High potential value if tool can responsibly highlight common deductions for this type of business in Quebec. | Req (Future/Guidance), BC |
| Wants to avoid issues with Revenu Québec / tax authorities. | Tool's value prop includes peace of mind and compliance support. | BC |

## Seasonal Considerations
Information about differences between summer (landscaping) and winter (snow removal) operations.

| Finding | Impact | Affected Artifact(s) |
|---------|--------|---------------------|
| Plans both services; anticipates different contract/payment models (per visit vs. monthly/per storm). | Reinforces need for the system to flexibly handle different billing cycles and service agreements. | PDM, Req |
| Wants to track landscaping and snow removal financials separately. | Requires ability to categorize income/expenses/jobs by service type for reporting. | PDM, Req |

## Technical Environment Findings
Information about devices, connectivity, and technical constraints.

| Finding | Impact | Affected Artifact(s) |
|---------|--------|---------------------|
| Uses mobile phone exclusively. | Confirms mobile-only is a critical requirement for this segment. | Scope, Req |
| Has reliable LTE connection (Montreal). | Offline capability good but perhaps less critical than for users in potentially rural areas (like P1). | Scope, Req |
| Comfortable with easy mobile apps; failed with QuickBooks (complexity). | UI must be extremely simple and intuitive, benchmarked against consumer apps, not complex business software. | Req (NFR/UX) |

## Direct Quotes
Notable quotes that provide valuable insight or context.

| Quote | Context | Relevance |
|-------|---------|-----------|
| "I’d like something that helps me look professional and keep track of everything." | Initial goal. | Sets the tone: organization and professionalism are key drivers from the start. |
| "I think if I stay under $30,000, I don’t have to [charge tax]. But I’m not 100% sure. I’d need something to guide me." | On GST/QST handling. | Explicitly states need for tax rule guidance due to uncertainty. |
| "I don’t want problems, but I also don’t want to pay an accountant $2,000 just to file basic stuff." | On tax reporting challenges. | Positions the tool as a cost-effective alternative/complement to expensive accounting services for basic needs. |
| "Show me exactly how much money I made from each job after expenses—and keep track of everything automatically." | Ideal tool description. | Highlights core needs: per-job profit visibility and low-friction ("automatic") tracking. |
| "I tried QuickBooks but it felt too complicated. I just need something simple." | On past solutions. | Direct feedback reinforcing simplicity as a critical requirement and competitive differentiator. |
| "[Must Haves?] ... Help with taxes (GST/QST)... Simple to use." | Defining essential features. | Notably includes tax help alongside simplicity and core tracking, reflecting his proactive stance. |

## Follow-up Actions
Specific actions needed based on this interview.

| Action | Owner | Due Date | Priority |
|--------|-------|----------|---------|
| Validate needs/size of "prospective/early-stage entrepreneur" segment. | [Researcher/BA Name] | 2025-04-21 | High |
| Define requirements & scope for MVP, considering Carlos's need for basic tax guidance (feasibility/approach TBD). | [BA/Product Owner Name] | 2025-04-18 | High |
| Research responsible ways to implement basic tax guidance (e.g., info links, standard deduction lists) vs. giving advice. | [BA/Product Owner Name] | 2025-04-25 | High |
| Evaluate flexibility of PDM/Scope to handle adjacent service types (e.g., cleaning). | [BA/Product Owner Name] | 2025-04-18 | Medium |
| Refine Business Case value prop for "starting right," professionalism, and tax anxiety reduction. | [BA/Product Owner Name] | 2025-04-18 | High |

## Validation Status
Track which findings have been validated across multiple interviews.

| Finding | Validation Status | Corroborating Interviews |
|---------|------------------|--------------------------|
| Desire for extreme simplicity / Failure with complex tools (QB) | Validated | [P4 ID, P3 ID, P2 ID, P1 ID] |
| Mobile-only operation for solo/small operators | Validated | [P4 ID, P3 ID, P2 ID, P1 ID (Field)] |
| Price sensitivity $10-$20/month (monthly preferred) | Validated | [P4 ID, P3 ID, P2 ID, P1 ID] |
| Core need for basic profit visibility & payment/expense tracking | Validated | [P4 ID, P3 ID, P2 ID, P1 ID] |
| Confusion/Anxiety about Quebec tax rules | Validated (Explicit in P4, P3) | [P4 ID, P3 ID] |
| Need for tool to handle distinct seasonal operations (Landscaping vs Snow) | Validated | [P4 ID (Planning), P3 ID (Planning), P1 ID (Doing)] |
| Interest in tool as enabler for formalization/growth | Validated | [P4 ID, P3 ID, P2 ID (Hinted)] |
| Need for explicit tax *guidance* (not just calculation) | Needs Validation (Strongest in P4) | [P4 ID] |

## Notes for Problem Domain Model
Model needs flexibility for `ServiceType` (Landscaping, Snow, Cleaning?). `TaxInfo` might need attributes related to thresholds or links to guidance resources. `Quote`/`Invoice` entities needed for future state/professionalism goal. Relationships must clearly support per-job `Profit` calculation (linking `Job`, `Income`, `Expense`). Consider `MileageLog` entity for future Nice-to-Have.

## Notes for Scope Definition Document
Tiered approach essential. Tier 1 (MVP): Ultra-simple, mobile-only, core tracking (Income, Expense, Profit per Job), basic Payment status. *Consider* including links to official QC tax threshold info. Tier 2: Adds Invoicing/Quotes, full GST/QST calculation/reporting, potential advanced features (Scheduling, Mileage, Reports). Clearly define what "tax guidance" means within scope (likely informational links, not advice). Confirm flexibility for different service types.

------