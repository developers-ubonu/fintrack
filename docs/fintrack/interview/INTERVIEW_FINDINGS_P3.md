# Interview Findings Summary

## Metadata
**Interview Date:** 2025-04-07
**Participant:** Peter (Participant 3)
**Business Type:** Solo Operator (Exploring hiring/formalizing)
**Services Offered:** Landscaping Only (Considering Snow Removal)
**Language of Interview:** English (Speaks some French)
**Interviewer:** [Interviewer Name]

## Key Insights Summary
Peter represents a solo, informal landscaper operating on a cash basis, similar to Participant 2, but actively contemplating formalization and hiring. Key pain points mirror P2: lack of profit visibility, difficulty tracking payments and jobs, and minimal expense tracking. He is explicitly nervous and confused about tax obligations (GST/QST, deductions, registration), viewing this complexity as a barrier to making his business official. He requires an extremely simple, mobile-only (iPhone) tool, is comfortable with basic apps but failed with spreadsheets, seeking something more 'automatic'. His price sensitivity is $10-$15/month, and core value drivers are basic tracking, time savings, and crucially, help/confidence navigating taxes to enable growth.

## Problem Domain Model Impacts
Information gathered that affects our understanding of the business domain.

| Finding | Impact on Problem Domain Model | Priority |
|---------|--------------------------------|---------|
| Current operation is cash-based, informal, similar to P2. | Reinforces need for simple `Cash Income`, basic `Expense` (Gas, Oil, Repairs, Tools), simple `Job`/`Client` tracking for initial stage. | High |
| Explicit confusion/nervousness about tax rules (GST/QST, deductions, registration). | Underscores the need for any future `TaxInfo` features to be clear, simple, and potentially provide guidance. It's a future state need driven by growth aspiration. | Medium (Future) |
| Considers hiring friends; nice-to-have is tracking helper pay. | Suggests future need for simple `Helper/Employee Payment` tracking within `Expense` or linked entities as business formalizes. | Low (MVP) / Medium (Future) |
| Considers snow removal, anticipates need for contracts (monthly). | Reinforces need for flexible `Contract` structures (per visit vs. monthly) in later stages/tiers. | Low (MVP) / Medium (Future) |

## Scope Definition Impacts
Information that affects project boundaries, constraints, or assumptions.

| Finding | Impact on Scope Definition | Priority |
|---------|---------------------------|---------|
| Requires extreme simplicity; abandoned spreadsheets as "too much writing", wants "automatic" feel. | High priority on 'Ease of Use', 'Minimal Data Entry', and efficient UX. Explore quick-add features for expenses/income. | High |
| Operates mobile-only (iPhone). | Reinforce 'Mobile-Only' as sufficient for base tier/MVP targeting this segment. | High |
| Tax handling seen as a future need tied to formalization, and a current source of confusion. | Validate approach of optional/future tax module activation. Scope for tax features should include simplification/guidance. | High |
| Needs basic tracking of clients, payments, expenses. | Confirm core MVP scope aligns with these fundamental tracking needs. | High |
| Nice-to-have: Quotes/Contracts, GPS/Map, Helper Pay tracking. | Add to backlog, aligning with features needed for growth/formalization beyond basic solo cash operation. | Medium (Future) |

## Business Case Impacts
Information that affects value proposition, ROI analysis, pricing strategy, etc.

| Finding | Impact on Business Case | Priority |
|---------|------------------------|---------|
| Currently spends $0 on tools; validates the market segment. | Confirms addressable market at $0 current spend. | High |
| Explicitly links tool value to "making tax season easier" and giving "confidence to grow and maybe hire". | Strengthen "Pathway to Legitimacy/Growth" value prop. Position tool as enabler overcoming complexity barrier. | High |
| Loses money ($50-$100+) through poor tracking/undercharging; aware of missed deductions (lost receipts). | Quantify ROI through reduced losses, better pricing decisions, and capturing legitimate deductions upon formalization. | High |
| Price sensitivity $10-$15/month (monthly preference). | Further validates target price range for an entry-level tier. | High |
| Current admin time (2-3 hrs/wk) feels "messy" and "not helpful". | Value prop includes not just time saving, but making time spent *effective* and providing clarity. | Medium |

## Stakeholder Requirements Impacts
Information that affects success criteria, feature prioritization, etc.

| Finding | Impact on Stakeholder Requirements | Priority |
|---------|-----------------------------------|---------|
| Must-Haves: Job log (client), Payment tracking, Easy expense log, Mobile access. | Confirms core MVP feature set, consistent with P2. Emphasize "Easy" expense logging UX. | High |
| Deal-Breakers: Complicated, Computer-only. | Reinforces critical NFRs: Simplicity, Mobile-Only access (for base tier). | High |
| Nice-to-Haves align with growth: Reminders, Maps, Quotes/Contracts, Helper Pay. | Populate backlog, consider these for Tier 2 / growth-focused features. | Medium (Future) |
| Success includes feeling "ready for tax season" and having "confidence to grow/hire". | Define UAC and long-term success metrics tied to enabling formalization and expansion. | High |
| Wants something more "automatic" than spreadsheets. | Prioritize streamlined workflows and potentially investigate smart features (e.g., remembering common expenses) for ease of use. | Medium |

## New Requirements Discovered
Requirements that weren't previously identified but should be considered.

| Requirement | Rationale | Priority | Affected Artifact(s) |
|------------|-----------|----------|---------------------|
| Streamlined/ "Automatic" Feel Expense Logging | User explicitly contrasted with difficult spreadsheet experience; needs very low friction data entry. | High | Req (UX/NFR) |
| Simple Quote/Contract Generation (Nice-to-Have) | Supports user's growth path towards more formal client agreements, especially if adding snow removal. | Medium (Future) | Req, Scope |
| Helper Payment Tracking (Nice-to-Have) | Supports user's explicit interest in hiring friends and needing to track payments fairly. | Medium (Future) | Req, PDM |
| Potential for In-App Guidance on Tax Basics (Future) | Addresses user's expressed confusion/nervousness about QC tax rules as a barrier to formalization. | Low (MVP) / Medium (Future) | Req, Scope, BC |

## Challenged Assumptions
Previously held assumptions that were challenged by this interview.

| Original Assumption | Challenge | Recommended Action | Priority |
|--------------------|-----------|-------------------|---------|
| Users primarily need tracking for *current* operations. | This user (like P2) needs tracking, but a key value driver is enabling/simplifying *future* formalization and growth. | Position and design the tool not just for current tracking but as a bridge to becoming a more formal business. | High |
| Lack of formal tracking is due to laziness or lack of need. | Peter indicates confusion and nervousness about regulations are significant factors preventing formal tracking/registration. | Acknowledge complexity as a real barrier; emphasize simplification as a core product benefit. | High |

## Quebec-Specific Insights
Information specific to operating in the Quebec market.

| Finding | Impact | Affected Artifact(s) |
|---------|--------|---------------------|
| Expressed confusion/nervousness about GST/QST registration thresholds and deductible expenses in Quebec. | Highlights opportunity for the tool (in future versions) to provide clarity/guidance specific to Revenu Québec rules, reducing barriers. | Req (Future), BC |
| Operates informally now but acknowledges need to deal with taxes if official. | Reinforces the "informal-to-formal" pathway as a relevant user journey in this market. | BC, Scope |

## Seasonal Considerations
Information about differences between summer (landscaping) and winter (snow removal) operations.

| Finding | Impact | Affected Artifact(s) |
|---------|--------|---------------------|
| Wants to add snow removal, potentially teaming up. | Confirms landscaping-only operators see snow as a growth path for year-round income. | BC |
| Anticipates snow requires better planning (costs) and monthly contracts; needs help setting up contracts. | Future versions/tiers should support contract management and potentially different planning views for seasonal services. | PDM (Future), Req (Future) |

## Technical Environment Findings
Information about devices, connectivity, and technical constraints.

| Finding | Impact | Affected Artifact(s) |
|---------|--------|---------------------|
| Uses iPhone exclusively for business. | Confirms mobile-only approach is viable and necessary for this segment. | Scope, Req |
| Has reliable LTE connection. | Consistent with P2; offline capability remains good practice but maybe less acutely critical than for P1. | Scope, Req |
| Uses basic apps (Calendar, Notes, WhatsApp); failed with spreadsheets. | Need intuitive UI suitable for basic app users; must be significantly easier than manual spreadsheet entry. | Req (NFR/UX) |

## Direct Quotes
Notable quotes that provide valuable insight or context.

| Quote | Context | Relevance |
|-------|---------|-----------|
| "I get paid in cash, and it’s all under the table for now. But if I register officially, I know I’ll need to deal with GST and QST." | On tax handling. | Describes current informal status and awareness of future obligations. |
| "[Tax challenges?] I’m not sure what I can deduct... I don’t know when I have to register... It’s confusing... makes me nervous about making it official." | On tax reporting challenges. | Explicitly links confusion/fear about tax complexity to hesitation in formalizing. Key opportunity for the tool. |
| "Honestly, if I have money left after gas and supplies, I feel like it was good. I go by feeling, not numbers." | On determining profitability. | Highlights the need for basic, quantitative financial visibility. |
| "I tried a spreadsheet once but gave up. Too much writing. I want something that feels more automatic." | On past solutions. | Sets a clear UX benchmark: must be easier and feel more automated than spreadsheets. |
| "[Success?] I’d... feel ready for tax season... Feeling confident to grow and maybe hire a friend." | On measuring success/desired outcomes. | Directly links tool usage to overcoming tax anxiety and enabling business growth/hiring. |

## Follow-up Actions
Specific actions needed based on this interview.

| Action | Owner | Due Date | Priority |
|--------|-------|----------|---------|
| Consolidate findings from P2 & P3 to define the "Informal Operator / Aspiring Formalizer" persona and MVP needs. | [BA/Product Owner Name] | 2025-04-14 | High |
| Prioritize requirements for MVP focusing on extreme simplicity, mobile-only, core tracking (income, expense, payment, profit). | [BA/Product Owner Name] | 2025-04-14 | High |
| Brainstorm/prototype UX concepts for "easy/automatic" expense logging. | [UX Designer/BA] | 2025-04-21 | High |
| Refine "Pathway to Legitimacy" value proposition in Business Case using P2/P3 insights. | [BA/Product Owner Name] | 2025-04-18 | High |
| Plan specific questions for future interviews to probe deeper into tax confusion points and desired "guidance". | [Researcher/BA Name] | 2025-04-11 | Medium |

## Validation Status
Track which findings have been validated across multiple interviews.

| Finding | Validation Status | Corroborating Interviews |
|---------|------------------|--------------------------|
| Existence of informal, cash-based solo operators | Validated | [P2 ID, P3 ID] |
| Core need is basic profit visibility & payment tracking | Validated | [P2 ID, P3 ID, P1 ID (Implicitly)] |
| Mobile-only operation (no computer) for this segment | Validated | [P2 ID, P3 ID] |
| Desire for extreme simplicity, frustration with complexity/manual entry | Validated | [P2 ID, P3 ID, P1 ID] |
| Price sensitivity $10-$15/month | Validated | [P2 ID, P3 ID, P1 ID (Similar range)] |
| Tax complexity/confusion as barrier to formalization | Needs Validation (Explicit in P3, hinted in P2) | [P3 ID] |
| Aspiration to use tool to help formalize/grow | Needs Validation (Explicit in P3, hinted in P2) | [P3 ID] |

## Notes for Problem Domain Model
Reinforces need for very simple base model: `Income` (Cash), `Expense` (Simple Cats: Gas, Repair, Tool, HelperPay), `Client` (Basic info + Payment Status), `Job` (Basic Desc). Key relationships for weekly/monthly `Profit Summary`. Structure must easily accommodate future additions: `TaxInfo`, `Invoice`, `Contract`, detailed `Job Costing`, `Employee` links as user grows/formalizes.

## Notes for Scope Definition Document
Strongly supports a tiered approach. Tier 1 (MVP): Mobile-only, ultra-simple UI, Cash In/Out, basic Expense Cats, Payment Status, Profit Summary. NO mandatory tax features. Tier 2: Adds per-job profit, Invoicing, GST/QST module (optional activation?), potentially Quotes/Contracts, web access. Clearly define NFRs for Tier 1: Extreme Ease of Use, Speed, Mobile-Only.

------