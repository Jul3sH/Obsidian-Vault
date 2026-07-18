---
title: "Integrate Apollo with Claude"
source: "https://knowledge.apollo.io/hc/en-us/articles/43827318678541-Integrate-Apollo-with-Claude?_gl=1*yxmwpr*_gcl_aw*R0NMLjE3NzY4NjMwNDcuQ2p3S0NBanc0NkhQQmhBTUVpd0FTWnBMUk14RlQyMWZuaHdDZmkxRmFSUFVVbjdfUkZmSDVNbVFlZHliYWRFQ0RlSm4zVlROUHVoMVZCb0NkdVlRQXZEX0J3RQ..*_gcl_au*MTEyODU4NjE5LjE3NzI2NzE4MTk.*_ga*MzE2MTc2NjAwLjE3NzI2NzE4MTk.*_ga_76XXTC73SP*czE3Nzc0NDA1MzEkbzUkZzEkdDE3Nzc0NDA1NzQkajE3JGwwJGgzMjE5OTM3NTA."
author:
published: 2026-03-27
created: 2026-04-29
description: "Overview             In Beta     The Claude integration is in beta. Product functionality and pricing may change during the beta.     If..."
tags:
  - "clippings"
---
## Overview

In Beta

The Claude integration is in beta. Product functionality and pricing may change during the beta.

If you use Claude from Anthropic, add Apollo as a connector and do real Apollo work without leaving the chat: search for people and companies, enrich records, and take action across Apollo.

In one conversation, you can:

- Find prospects using natural language
- Enrich people or companies
- Create or update contacts
- Add contacts to an existing sequence
- Analyze your team's performance

Everything runs on your existing Apollo permissions, plan limits, and credit balance. Setup is simple: connect Apollo in Claude, then start using Apollo in any Claude conversation.

Check out the following sections to connect and use Apollo with Claude.

## Connect Apollo to Claude

No Strings Attached

Apollo works on any Claude subscription, including free accounts!

To connect Apollo to Claude:

1. Launch **[Claude](https://claude.ai/new)**, and log in or create a new account.
2. In a chat, click **Connect your tools to Claude**.
[![[ab1f3cb2dba0e593caf3319c1de64cc0_MD5.png]]](https://storage.googleapis.com/apollo-public-assets/kb_images/integrate_apollo_with_claude/i1.png)
3. Alternatively, click **Customize** > [**Connectors**](https://claude.ai/directory).
4. Click **+**.
5. Search for `Apollo.io` and click **\+ Apollo.io**.
[![[de763535ae231042f82d7d8ff1516f9c_MD5.png]]](https://storage.googleapis.com/apollo-public-assets/kb_images/integrate_apollo_with_claude/i2.png)

Claude and You

The Claude integration is user-specific and must be set up separately by each person rather than at the team or admin-level.

6. Review the terms and conditions, and click **Authorize**.
[![[441cfd1d6b267537567eb1908e8bbad1_MD5.png]]](https://storage.googleapis.com/apollo-public-assets/kb_images/integrate_apollo_with_claude/i3.png)
7. Next, in Claude, navigate back to **Customize** > [**Connectors**](https://claude.ai/directory).
8. Click **Configure** beside `Apollo.io`.9. Review the permissions for each action to ensure Claude works the way you expect with your Apollo account.
10. Set each action to one of the following permission levels:
- **✓⃝ Always allow**: Claude always has permission to perform the action in Apollo and won't seek your approval first.
	- **✋ Approval required**: Claude asks permission before completing the action in Apollo. Apollo recommends you require approval from Claude on actions that require .
	- **⊗ Blocked**: Claude does not have permission to perform the action on your behalf in Apollo.

| Action | Description | Requires Credits? |
| --- | --- | --- |
| Search for Contacts | Search people and contacts with natural language. | No |
| Get a List of Email Accounts | List connected mailboxes used for sending, sequences, and tracking across your team. | No |
| Search for Sequences | Find existing [sequences](https://knowledge.apollo.io/hc/en-us/articles/4409237165837-Sequences-Overview) to enroll and manage outreach. | No |
| People API Search | Search Apollo's people data programmatically using the [Apollo API](https://knowledge.apollo.io/hc/en-us/articles/4416173158541-Use-Apollo-API). | No |
| Profile | Edit your user settings like email preferences and custom fields in [profile settings](https://knowledge.apollo.io/hc/en-us/articles/34010120281613-Configure-Your-Profile-Settings-in-Apollo). | No |
| Create an Account | Create a [company record](https://knowledge.apollo.io/hc/en-us/articles/4413032484493-Save-Contacts-and-Accounts) to save and manage in Apollo. | No |
| Update an Account | Update fields on an [existing account](https://knowledge.apollo.io/hc/en-us/articles/5995865049229-View-and-Edit-Accounts). | No |
| Create Contact | Create a [contact record](https://knowledge.apollo.io/hc/en-us/articles/4413032484493-Save-Contacts-and-Accounts) to save and engage in Apollo. | No |
| Update Contact | Update details on a [saved contact](https://knowledge.apollo.io/hc/en-us/articles/5995459280525-View-and-Edit-Contacts). | No |
| Add Contacts to a Sequence | Enroll contacts into a [sequence](https://knowledge.apollo.io/hc/en-us/articles/4409396985741-Add-Contacts-to-a-Sequence) to start outreach steps. | No |
| Remove Contacts from Sequences | [Remove contacts from a sequence](https://knowledge.apollo.io/hc/en-us/articles/4409396985741-Add-Contacts-to-a-Sequence) to stop future outreach steps. | No |
| Organization Search | Search for companies using filters like industry, headcount, and buying intent. | Yes |
| Bulk Organization Enrichment | Enrich multiple company records at once using the [Enrichment API](https://knowledge.apollo.io/hc/en-us/articles/33699917233293-Enrichment-Overview). | Yes |
| Organization Enrichment | Enrich a single company with fresh firmographic data. | Yes |
| Organization Job Postings | Retrieve company job posting data to identify hiring signals. | Yes |
| Bulk People Enrichment | Enrich multiple people records at once, including verified email data. | Yes |
| People Enrichment | Enrich a single person record with updated contact and employment data. | Yes |
| Query Analytics Data | Retrieve analytics data on sequences, emails, and engagement to measure performance and activity. | No |

Missing an Action?

If an action isn't working or doesn't appear in Claude, try disconnecting and reconnecting Apollo.You have now connected Apollo to Claude, and you're ready to [use the Claude integration](#use).

## Use Apollo on Claude

Once connected, using Apollo in Claude is as simple as having a conversation. There are no special commands or complex prompts required. Just describe what you want to do, and Claude uses your Apollo account to complete the action.

Permission Reflection

Claude can only perform actions in Apollo that you can perform yourself based on your [permission profile](https://knowledge.apollo.io/hc/en-us/articles/4409154208269-Create-and-Assign-Permission-Profiles) and [Apollo plan](https://app.apollo.io/#/settings/plans/upgrade). If you can't do it, Claude can't either.

To use Apollo on Claude:

1. Start a new chat, and use natural language to describe your request or goal. Claude translates your request into action based on the permissions you configured.
2. Follow these best practices to get the best results:
- Be specific about titles, industries, locations, and company size to improve search accuracy.
	- Review returned results before enrolling large groups into sequences.
	- Orchestration is key! Use follow-ups to refine searches and chain actions, for example: "Narrow this to companies using Sumware Software, then find decision makers."3. Here are a few example requests to help get you started:

<table><tbody><tr><th colspan="2">Examples</th></tr><tr><td><a href="#search-for-people">Search for people</a></td><td><a href="#search-for-companies">Search for companies</a></td></tr><tr><td><a href="#create-or-update-contacts-and-accounts">Create or update contacts and accounts</a></td><td><a href="#enrich-contacts-and-accounts">Enrich contacts and accounts</a></td></tr><tr><td><a href="#add-contacts-to-sequences">Add contacts to sequences</a></td><td><a href="#analyze-your-performance">Analyze your performance</a></td></tr></tbody></table>

### Search for people

```
Find VP-level marketing leaders at SaaS companies in North America.
```
```
Show me IT directors in healthcare companies.
```
```
Search for founders in fintech companies based in New York.
```

Claude returns matching prospects. People search results show names and job titles but don't include email addresses or phone numbers. [Save contacts](#create-or-update-contacts-and-accounts), and [use enrichment](#enrich-contacts-and-accounts) to reveal contact details.

### Search for companies

### Create or update contacts and accounts

### Enrich contacts and accounts

### Add contacts to sequences

### Analyze your performance

Pipeline on Autopilot

For power users, Apollo also offers a dedicated [MCP Cowork plugin](https://github.com/apolloio/apollo-mcp-plugin) for Claude that chains search, enrichment, and sequence management into single-command workflows, allowing you to go from ideal customer profile (ICP) to sequenced prospects without orchestrating each step:

- `/apollo:enrich-lead`: Paste a name, LinkedIn URL, or email and get a complete contact card, plus suggested next actions.
- `/apollo:prospect`: Describe your ICP in plain English and get a ranked table of enriched decision-maker leads.
- `/apollo:sequence-load`: Find leads, enrich them, dedupe, create contacts, and bulk-add them to an existing Apollo sequence with a preview before enrollment.

You have now used Apollo on Claude.

## Next Steps

Now that Apollo is running inside Claude, here are a few ways to level up how you search, enrich, and automate what happens next.

| [Use the AI Assistant On Apollo To Sell Smarter](https://knowledge.apollo.io/hc/en-us/articles/39359204112397-Use-the-AI-Assistant-on-Apollo-to-Sell-Smarter) | Want to use AI inside Apollo? [Use the AI assistant](https://knowledge.apollo.io/hc/en-us/articles/39359204112397-Use-the-AI-Assistant-on-Apollo-to-Sell-Smarter) on Apollo to refine ICP filters, surface better-fit prospects, and take action faster across your workflows directly in Apollo. |
| --- | --- |
| [Enrichment Overview](https://knowledge.apollo.io/hc/en-us/articles/33699917233293-Enrichment-Overview) | If you need cleaner data before you enroll prospects, [enrich contacts and accounts](https://knowledge.apollo.io/hc/en-us/articles/33699917233293-Enrichment-Overview) on Apollo to verify emails, refresh firmographics, and keep your team's outreach accurate and up to date. |
| [Sequences Overview](https://knowledge.apollo.io/hc/en-us/articles/4409237165837-Sequences-Overview) | Ready to automate follow-up? [Build and manage sequences](https://knowledge.apollo.io/hc/en-us/articles/4409237165837-Sequences-Overview) to turn Claude-powered prospecting into consistent, multi-step outreach that actually drives replies. |
| [Create and Assign Permission Profiles](https://knowledge.apollo.io/hc/en-us/articles/4409154208269-Create-and-Assign-Permission-Profiles) | Rolling Apollo ↔ Claude out to your team? [Create and assign permission profiles](https://knowledge.apollo.io/hc/en-us/articles/4409154208269-Create-and-Assign-Permission-Profiles) to control who can search, enrich, and enroll prospects when working through Claude. |
| [What Are Credits?](https://knowledge.apollo.io/hc/en-us/articles/9527776320781-What-Are-Credits) | If you plan to scale enrichment and automation (and you should), [understand how credits work](https://knowledge.apollo.io/hc/en-us/articles/9527776320781-What-Are-Credits) on Apollo to manage usage, avoid surprises, and keep your Claude-driven workflows running smoothly. |