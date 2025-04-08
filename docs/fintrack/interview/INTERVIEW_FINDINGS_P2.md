# Interview Findings Summary

## Metadata
**Interview Date:** 2025-04-07
**Participant:** Simulated Informal Landscaper (Participant 2)
**Business Type:** Solo Operator / Very Small Crew (Pays friends/extra workers informally)
**Services Offered:** Landscaping Only (Considering Snow Removal)
**Language of Interview:** English (Based on provided text)
**Interviewer:** [Interviewer Name]

## Key Insights Summary
This interview represents a segment operating informally (cash-based, door-to-door sales, currently avoiding taxes/formal reporting). The primary need is for an extremely simple, mobile-only tool to gain basic visibility into weekly profit (cash in minus cash out for gas/helpers). Current financial tracking is minimal ("gut feeling," memory). There's an aspiration to potentially formalize the business if the process (especially taxes) can be simplified. Simplicity, mobile-only access, and low cost ($10-15/month) are critical.

## Problem Domain Model Impacts
Information gathered that affects our understanding of the business domain.

| Finding | Impact on Problem Domain Model | Priority |
|---------|--------------------------------|---------|
| Business operates primarily on cash, immediate payment. | Need entities/attributes to track `Cash Income` per job/day. `Payment Status` needs to handle "paid on the spot" effectively. | High |
| Expense tracking is very basic (gas, helpers, maintenance, dump fees) and informal. | Define simple `Expense` categories. `Expense` tracking needs to be extremely quick/easy. May need a specific `Helper Payment` type. | High |
| Profitability is currently assessed by "gut feeling". | Core need is for a simple `Profit Calculation` (e.g., Weekly Cash In - Weekly Cash Out). Less emphasis on per-job initially. | High |
| Minimal job data tracked (maybe address for recurring). | `Job` entity can be simpler for this user type initially, focusing on basic service description and income received. | Medium |
| GST/QST currently not handled (cash operations). | `TaxInfo` / GST/QST handling is *not* a current requirement for this user segment but represents a *future need* if they formalize. Model should allow for this future state. | Low (Current) / Medium (Future) |

## Scope Definition Impacts
Information that affects project boundaries, constraints, or assumptions.

| Finding | Impact on Scope Definition | Priority |
|---------|---------------------------|---------|
| User requires extreme simplicity and speed; avoids paperwork/admin. | Reinforce 'Extreme Simplicity' and 'Minimal Data Entry' as paramount design principles. The tool must be faster than their current non-system. | High |
| User operates entirely via mobile phone; no office/computer. | Mandate 'Mobile-Only' access as a critical constraint for this user segment. A web app is not required initially for them. | High |
| User currently avoids taxes but sees value in a tool that *could* help if they formalize. | Define initial MVP scope focused *only* on basic income/expense/profit tracking. Tax features (GST/QST) should be designed as optional/future modules activated when needed. | High |
| User finds remembering who owes money difficult. | Include simple 'Payment Tracking' (even just marking a client/job as paid/unpaid) in scope. | Medium |
| User explicitly separates personal finance. | Confirm boundary: Exclude personal finance tracking. | High |

## Business Case Impacts
Information that affects value proposition, ROI analysis, pricing strategy, etc.

| Finding | Impact on Business Case | Priority |
|---------|------------------------|---------|
| User currently spends $0 on financial tools. | Represents a market segment currently unserved by paid tools. Value proposition must be compelling enough to warrant *starting* to pay. | High |
| Primary value driver is gaining basic profit visibility and control ("know if I actually profited"). | Position the tool as providing essential financial clarity and control for informal businesses, potentially as a first step towards growth/formalization. | High |
| User loses money ($200-$300 instances) due to poor cost awareness. | Quantify potential savings from better expense awareness, even basic tracking. | Medium |
| User expresses interest in future formalization/tax handling *if simplified*. | Add "Pathway to Legitimacy/Growth" as a potential value proposition for this segment. | Medium |
| Price sensitivity confirmed at $10-$15/month (monthly preference). | Validates potential for a lower-priced entry tier focused on core simplicity. | Medium |

## Stakeholder Requirements Impacts
Information that affects success criteria, feature prioritization, etc.

| Finding | Impact on Stakeholder Requirements | Priority |
|---------|-----------------------------------|---------|
| Must-Haves: Easy phone use, shows profit, tracks payments to others, quick input. | Define ultra-simple MVP: Record Cash In (link to basic job/client), Record Cash Out (gas, helpers), Display Weekly Profit Summary. | High |
| Deal-Breakers: Complicated, time-consuming, computer-only. | Reinforce usability, performance, and mobile-only constraints as critical pass/fail criteria for this segment. | High |
| Nice-to-Haves: Job reminders, invoicing (future), team hours, Maps integration. | Add these to backlog. Note invoicing/team hours are linked to potential future formalization. | Low (MVP) / Medium (Future) |
| Success defined by clear profit view, feeling in control, confidence to potentially grow/register. | Align UAC and long-term product goals with these user outcomes, including enabling growth. | High |
| User uses basic apps (Maps, WhatsApp, Notes). | Interface should be intuitive for users familiar with standard mobile app conventions, but not necessarily business software. | Medium |

## New Requirements Discovered
Requirements that weren't previously identified but should be considered.

| Requirement | Rationale | Priority | Affected Artifact(s) |
|------------|-----------|----------|---------------------|
| Ultra-Simple 'Cash In' Recording | To match the user's current cash-based, immediate payment workflow with minimal friction. | High | PDM, Scope, Req |
| Basic 'Helper Payment' Expense Tracking | To easily track informal payments to day laborers/friends, a key expense category mentioned. | High | PDM, Scope, Req |
| Weekly Profit Summary View | User specifically asked for a weekly breakdown, reflecting their operational rhythm. | High | Req |
| Optional/Future Tax Module Activation | To cater to users currently operating informally but considering future formalization, without burdening them initially. | Medium | Scope, Req, BC |

## Challenged Assumptions
Previously held assumptions that were challenged by this interview.

| Original Assumption | Challenge | Recommended Action | Priority |
|--------------------|-----------|-------------------|---------|
| Most small businesses engage in some form of formal financial tracking or tax reporting. | This user represents a segment operating entirely informally (cash, no reporting). | Acknowledge and potentially target this informal segment with an entry-level, simplified offering focused on basic visibility and enabling future formalization. | High |
| GST/QST handling is a universal requirement for all Quebec businesses using the tool. | Informal cash businesses may not need/want this initially. | Design tax features as optional or part of a higher tier/module, not mandatory for basic use. | High |
| Users will have access to/use a computer for some business tasks. | This user is mobile-only. | Ensure the core functionality is fully accessible and usable via the mobile app. | High |

## Quebec-Specific Insights
Information specific to operating in the Quebec market.

| Finding | Impact | Affected Artifact(s) |
|---------|--------|---------------------|
| User currently avoids GST/QST and formal reporting (operates "under the table"). | Confirms the existence of an informal economy segment. The tool could potentially facilitate transition *towards* compliance if desired by the user. | Scope, BC, Req |
| User perceives future tax compliance/paperwork as stressful and time-consuming. | Emphasizes the need for any tax-related features (future) to be extremely simple and efficient. | Req, BC |

## Seasonal Considerations
Information about differences between summer (landscaping) and winter (snow removal) operations.

| Finding | Impact | Affected Artifact(s) |
|---------|--------|---------------------|
| User only does landscaping currently but is considering snow removal. | Confirms interest in year-round income. Financial tracking needs for snow are currently hypothetical for this user. | PDM, Scope (Future) |
| User anticipates snow removal might require more formal contracts than current landscaping. | Suggests that as businesses grow/diversify (add snow), their needs for features like contract management and potentially invoicing may increase. | PDM (Future), Req (Future) |

## Technical Environment Findings
Information about devices, connectivity, and technical constraints.

| Finding | Impact | Affected Artifact(s) |
|---------|--------|---------------------|
| Uses mobile phone exclusively for business tasks. | Reinforces mobile-only requirement for this segment. | Scope, Req |
| Has reliable LTE internet connection. | Offline capability might be slightly less critical *for this specific user* than for Interview 1, but remains best practice. | Scope, Req |
| Uses basic consumer apps (Maps, WhatsApp, Notes), no finance apps. | Sets baseline for user's technical familiarity; UI must be very intuitive. Integration with Maps could be useful. | Req |

## Direct Quotes
Notable quotes that provide valuable insight or context.

| Quote | Context | Relevance |
|-------|---------|-----------|
| "We don’t charge tax since we mostly work under the table. It’s all cash." | Explaining GST/QST handling. | Defines the user's current informal operating model and lack of need for tax features *now*. |
| "It’s more like gut feeling... If we made good money that day... then we’re good." | On determining job profitability. | Highlights the lack of quantitative tracking and the core need for basic profit visibility. |
| "[Most frustrating?] Honestly, just keeping track of how much I made or spent. By the end of the season, it’s hard to know if I actually profited." | Describing financial pain points. | Clearly states the primary problem the tool needs to solve: basic profit/loss tracking. |
| "[Ideal tool?] Something that tells me how much I made each week, after paying workers and gas." | Defining the core desired function. | Provides a clear, simple requirement for the primary output/view. |
| "[Deal-breaker?] If it’s too complicated, takes too long to input stuff, or only works on a computer." | Setting critical constraints. | Emphasizes extreme usability, speed, and mobile-only necessity. |
| "[Hope to see in 6 months?] Better idea of my profit... and maybe confidence to register and grow legit." | Describing desired outcomes. | Links tool usage to potential business growth and formalization aspirations. |

## Follow-up Actions
Specific actions needed based on this interview.

| Action | Owner | Due Date | Priority |
|--------|-------|----------|---------|
| Validate the size and needs of this "informal operator" segment through further interviews. | [Researcher/BA Name] | 2025-04-21 | High |
| Define requirements for an "ultra-simple" MVP targeting basic cash in/out and weekly profit for mobile-only users. | [BA/Product Owner Name] | 2025-04-18 | High |
| Analyze feasibility/design for optional/phased introduction of features like invoicing and tax support. | [BA/Product Owner Name] | 2025-04-25 | Medium |
| Update Business Case to reflect potential targeting of the informal segment and value prop around enabling formalization. | [BA/Product Owner Name] | 2025-04-18 | Medium |
| Compare/contrast findings rigorously with Interview 1 to understand needs across different operational styles. | [BA/Product Owner Name] | 2025-04-14 | High |

## Validation Status
Track which findings have been validated across multiple interviews.

| Finding | Validation Status | Corroborating Interviews |
|---------|------------------|--------------------------|
| Existence of informal, cash-based landscapers avoiding tax | Needs Validation | [Participant 2 ID] |
| Core need is basic profit visibility (Cash In - Cash Out) | Needs Validation (Likely High overlap w/ P1 need) | [Participant 2 ID, P1 ID (Implicitly)] |
| Mobile-only operation (no computer) | Needs Validation | [Participant 2 ID] |
| Desire for extreme simplicity | Needs Validation (Stronger emphasis than P1) | [Participant 2 ID, P1 ID] |
| Price sensitivity $10-$15/month | Needs Validation (Overlaps with P1 range) | [Participant 2 ID, P1 ID] |
| Aspiration to use tool to help formalize business | Needs Validation | [Participant 2 ID] |

## Notes for Problem Domain Model
Initial model for this segment needs: `Income` (cash, date, basic description/client link), `Expense` (category - Gas, Helper Pay, Maintenance, Dump Fee, date, amount), `Client` (name/address, maybe phone, paid status tracking). Relationship to calculate `Weekly Profit`. Needs structure to easily add `Job` details, `Invoice`, `TaxInfo` later if user formalizes/needs upgrade.

## Notes for Scope Definition Document
Define potential tiered approach: Tier 1 (MVP for Informal Segment) - Mobile-only, basic cash in/out tracking, weekly profit summary, extreme simplicity. Tier 2 (Adds features for Formalized Small Biz like P1) - Includes per-job profitability, invoicing, GST/QST handling, web access, integrations. Explicitly state Tier 1 constraints: mobile-only, no mandatory tax features.

------