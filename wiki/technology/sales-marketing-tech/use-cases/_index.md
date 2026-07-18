# Cold Email Outreach — Use Cases

Six core use cases that map the full cold email lifecycle. Each file defines the job, inputs, outputs, and what to evaluate in a vendor.

| Use Case | File | Job to Be Done |
|----------|------|----------------|
| Prospecting | [[prospecting]] | Find and build a verified contact list |
| Email Verification | [[email-verification]] | Confirm addresses are safe to send to |
| Email Warm-up & Infrastructure | [[email-warmup]] | Build sender reputation before campaigns |
| Personalisation & Content | [[personalisation]] | Create content that doesn't look like spam |
| Campaign & Sequence Management | [[campaign-sequence]] | Build, send, and optimise multi-step campaigns |
| Unified Inbox & Reply Management | [[inbox-reply-management]] | Manage replies at scale across multiple accounts |

## ⚠️ Use Case Dependencies

Use cases are not independent — some require upstream steps to be in place first. Always check dependencies before recommending vendors.

| Use Case | Depends On |
|----------|-----------|
| Personalisation | Requires enriched data: **reverse email lookup** (email → LinkedIn URL) + **LinkedIn profile scraping** (URL → profile data). See [[personalisation]] for full prerequisites. |
| Campaign & Sequence | Requires verified email list + warmed-up sending domains |
| Inbox & Reply Management | Requires Campaign & Sequence to be running |

> ✅ Validation check: When a user states they want personalisation, always ask — or confirm — how they plan to get from their contact list to enriched LinkedIn data. Do not assume the sequencing tool handles this.
