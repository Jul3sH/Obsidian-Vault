---
name: Email Verification
category: cold-email-outreach
---

# Email Verification

**Job to be done:** Check that the email addresses you have found are real and safe to send to before launching a campaign.

## Inputs
- Single email address (one-off check)
- CSV file of email addresses (bulk check)
- Email addresses returned from a prospecting tool (inline verification)

## Outputs
- Verification status: valid / risky / invalid / catch-all / unknown
- Bounce risk classification
- Deliverability risk score
- Cleaned list ready for campaign upload

## Key Capabilities to Evaluate
- **Accuracy** — claimed accuracy rate and bounce guarantee (some offer money-back if >4% hard bounce)
- **Catch-all detection** — identifying domains that accept all email regardless of whether the mailbox exists
- **Greylisting bypass** — retrying on 4xx codes to avoid false negatives
- **Spam trap / honeypot detection** — filtering addresses that will damage sender reputation
- **Disposable / role-based detection** — removing throwaway and shared inboxes
- **Credit model** — do you pay for unknowns/catch-alls or only verified valid?
- **Bulk volume limits** — max rows per file / per day
- **API access** — for inline verification in pipelines
- **CRM sync** — auto-verify records when syncing to CRM

## Vendors in This Category
Snov.io, Apollo, Clay, HubSpot, Prospeo, SalesQL, ProxyCurl, Lix, MillionVerifier

## Key Takeaways
- MillionVerifier offers the strongest catch-all resolution and credits only charged on good/bad (not unknowns)
- Prospeo pre-verifies every email at discovery — no separate verification step needed
- Lix credits only charged for validated emails (1 credit = 1 valid email)
- Apollo provides automatic credit refunds on bounces — propagates to all customers
- Clay allows waterfall verification across multiple providers in a single workflow
