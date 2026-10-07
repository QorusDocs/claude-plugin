# Set up and use the QorusDocs plugin for Claude

The QorusDocs plugin brings AI-powered proposal and pursuit management into Claude. Bid, proposal, and sales teams can work with live pursuit data, approved answer content, and company knowledge in the same conversation where they are already thinking and drafting. You can track your pipeline, answer RFP questions, find approved content, and take a pursuit from set-up to a delivered document, such as a proposal, pitch, or capability statement, without copying and pasting between systems.

The plugin bundles two things: the **QorusDocs connector**, which connects Claude to your hub and powers everything described in this article, and a **Pursuit skill**, which adds a guided, step-by-step workflow for creating a Pursuit. All other work, including drafting other documents from your templates, runs through the connector. If you don't need the create Pursuit workflow, the connector can be added on its own; the plugin includes it, so you never need both.

This article explains what the plugin can do, what it can access and change, how authentication and permissions work, and how to install it. It is written for both end users and the IT administrators who review plugins and connectors before approving them for their organization.

## What's in the plugin

| Component | What it does |
| --- | --- |
| QorusDocs connector | Connects Claude to your QorusDocs hub (`https://agent-mcp.qorushub.com`) so you can work with pursuits, content, documents, and reporting. Sign-in uses OAuth, so there are no API keys. |
| Pursuit skill | Step-by-step guidance Claude follows to take a pursuit from set-up, through your hub's Assignments, to a drafted and completed Pursuit. |

## What you can do

- **Track your pipeline:** ask which pursuits are due this week, what stage a bid is at, who is assigned, and what is outstanding.
- **Answer RFP and security questionnaire questions:** answers are drafted from your organization's approved QorusDocs answer library, with the source content behind every answer.
- **Search company content:** find the case studies, boilerplate, past proposals, and reference material your hub already curates.
- **Create and progress pursuits:** create a pursuit, add members, attach documents, and move it through its stages to start your hub's Assignments, always with your confirmation.
- **Build pursuit documents:** draft any document from your hub's templates, such as a proposal, pitch, or RFP response, merge in the bios and experience selected for the pursuit, and deliver the finished document in Word or PowerPoint format (depending on the template used) or as a PDF.
- **Create a Pursuit with guided steps:** the Pursuit skill walks you through each stage, from setting up the pursuit to delivering a PDF with a draft covering email.
- **Work with pursuit documents:** summarize, compare, and pull key points from the documents attached to a named pursuit.
- **Review adoption and activity:** see usage and activity across your teams, scoped to what you are entitled to see.

Answers are grounded in your organization's own approved content rather than a general-purpose model's recollection, and Claude will state plainly when nothing relevant was found. Bios and experience for a pursuit are selected based on your pursuit criteria or chosen by your hub's own Assignments, not invented by Claude.

## Prerequisites

- An active **QorusDocs subscription** and a **QorusDocs user account** on your organization's hub. There is no self-serve or trial path without an account. Contact your QorusDocs administrator, or visit [qorusdocs.com](https://www.qorusdocs.com), if your organization is not yet subscribed.
- A **Claude plan that supports plugins** (see Anthropic's documentation for current plan requirements).
- **Claude tools enabled on your QorusDocs hub.** The pursuit tools are switched on per hub. If Claude reports that pursuit tools are unavailable, contact QorusDocs support.
- To build pursuit documents: a **template** for that document in one of your document libraries. To have bios and experience selected automatically: a **Pursuit Type with Assignments** that select them or use the tools available to select the bios and experiences.
- No administrator role is needed to install the plugin. Your Claude administrator is only involved if your organization restricts which plugins or connectors members may enable, or wants to install the plugin for everyone.

## Authentication

- Connection uses **OAuth 2.0 with dynamic client registration**. There are no API keys, tokens, or URLs for users to enter, and no configuration is needed on the QorusDocs side before connecting. The plugin itself contains no credentials.
- Users sign in with their **existing QorusDocs credentials**, including Microsoft Entra single sign-on where your organization uses it. Neither the plugin nor the connector sees or stores passwords. Sign-in happens on the QorusDocs (or your identity provider's) hosted login page.
- Access can be revoked at any time by disconnecting QorusDocs or uninstalling the plugin in Claude.

## Data access and permissions

The connector reads your QorusDocs data and, **when you ask it to**, can create and update pursuits and the documents on them. Claude asks for your approval before running an action that changes data, unless you have chosen to always allow it.

Every request runs **as the signed-in QorusDocs user** and honors existing hub, team, pursuit, and content permissions. Each tool runs the same business logic the QorusDocs application uses, so it cannot surface or change anything that user cannot already see or change in QorusDocs. There is no service account or elevated access path.

| Data | Access |
| --- | --- |
| Pursuits (status, stages, members, field values, assignments, dates) | Read and write |
| Pursuit documents and attachments | Read and write |
| Bios, experience, and other Smart Layout records | Read |
| A pursuit's selected bios and experience | Read and write |
| Approved answer library (Q&A content) | Read |
| Content sources (case studies, boilerplate, past proposals) | Read |
| User names and roles on your hub (to resolve people) | Read |
| Adoption, activity, and user reporting | Read |

### Changes the connector can make

- Create a pursuit
- Add members to a pursuit
- Copy documents from a library onto a pursuit
- Move a pursuit to another stage, update its field values, or close it
- Change the bios and experience selected for a pursuit
- Draft a document from a template
- Merge a pursuit's selected records into a document
- Convert a pursuit document to PDF

No tool deletes a pursuit, a document, or library content. Two actions overwrite rather than add: updating a pursuit's field values or status, and saving a selection, which replaces the previous selection for that record type.

Some tools are resolved per hub from what that hub has published, so the exact tool list a user sees reflects their organization's QorusDocs configuration.

## Install the plugin

### Claude apps (web, desktop)

1. In Claude, go to **Customize > Plugins** and open **Discover**.
2. Find **QorusDocs** and select **Install**.
3. The first time Claude uses a QorusDocs tool, a QorusDocs sign-in page opens. Sign in with your normal QorusDocs credentials (or your organization's single sign-on).
4. Review and accept the consent prompt listing the requested scopes.

### Claude Code

Install QorusDocs from the plugin directory, or add it directly:

```
/plugin marketplace add QorusDocs/claude-plugin
/plugin install qorusdocs@qorusdocs
```

Then run `/mcp`, select **qorusdocs**, and sign in.

### For your whole organization

A Claude organization administrator can install the plugin for all members, so it is available without each user installing it.

### Already using the QorusDocs connector?

The plugin includes the same connector. After installing the plugin, disconnect the standalone QorusDocs connector in **Settings > Connectors** so the QorusDocs tools do not appear twice.

## Using the plugin

### Tracking pursuits and finding content

Ask Claude about your pipeline, RFP questions, or company content in plain language. For example:

- *"What pursuits are due this week, and what's still outstanding on each?"*
- *"Answer these RFP questions from our knowledge base: …"*
- *"Find case studies about cloud migration projects for financial services clients."*

Claude shows the source content behind each answer, so you can check it before using it.

### Building a pursuit document

You can take any pursuit from set-up to a delivered document, using whichever templates your hub provides. Claude shows you the result of each stage and asks before making changes:

1. **Create the pursuit:** Claude asks for the details your Pursuit Type needs. Adding the first member restricts the pursuit to its members, and members may be emailed; Claude tells you this before it happens.
2. **File the client's documents:** the RFP, brief, or background, copied onto the pursuit from your document libraries.
3. **Start the Assignments:** moving the pursuit to its next stage starts the Assignments your hub has configured for that stage. Agents read the pursuit's documents and choose the bios and experience.
4. **Review the selection:** Claude shows what was chosen and can add or swap individual bios or experience records.
5. **Draft:** from the template you choose, with the pursuit's details and selected records merged in.
6. **Deliver:** once you approve the draft, it is ready on the pursuit in Word or PowerPoint format (depending on the template used), and Claude can also convert it to PDF.

For example: *"Set up a pursuit for Acme Corp's IT services RFP, file the RFP on it, and draft our standard proposal once the Assignments finish."*

### Creating a Pursuit

For Pursuits, the Pursuit skill guides Claude through a fuller workflow, including a draft covering email. Ask Claude to create a Pursuit, for example *"Create a Pursuit for Acme Corp's commercial litigation RFP."* Claude works through the pursuit one stage at a time, shows you the result of each stage, and asks before moving on:

1. **Create the pursuit:** Claude asks what the pursuit is about and who should be involved. Adding people as members restricts the pursuit to its members, and members may be emailed; Claude tells you this before it happens.
2. **File the client's documents:** the RFP, brief, or background, copied onto the pursuit from your document libraries.
3. **Start the Assignments:** your hub's agents read those documents and choose the bios and experience. This usually takes a few minutes; Claude can do client research or draft the covering email while you wait, and checks progress when you ask.
4. **Review the selection:** Claude shows what was chosen and can add or swap individual bios or experience records.
5. **Draft:** from your firm's template.
6. **Deliver:** once you approve the draft (including any edits you make to it), Claude converts it to PDF and drafts a covering email for you to review. Claude never sends email.
7. **Close:** Claude sets the closing status and outcome, with your confirmation.

You can pick up a pursuit already under way: *"Where are we with the Acme Pursuit?"*

### Long-running work

Some QorusDocs tools are long-running: they start a job and Claude retrieves the result when it is ready, typically within 10 to 60 seconds. Assignments take longer, usually a few minutes, and run in the background. Claude can carry on with other work while you wait, and does not claim an Assignment is finished without checking its status.

### Example prompts

**Pipeline and reporting**
- *"What pursuits are due this week?"*
- *"How are the Assignments on the Acme pursuit going?"*
- *"Show QorusDocs user activity for the last 30 days."*

**Answers and content**
- *"Answer these RFP questions from our knowledge base: …"*
- *"Find our boilerplate on information security and data privacy."*
- *"Summarize the documents in the Acme Corp pursuit."*

**Pursuits and documents**
- *"Create a pursuit for Acme Corp's IT services RFP, due March 14."*
- *"Swap Jane Smith's bio for John Doe's."*
- *"Draft our standard proposal for the Acme pursuit and convert it to PDF."*
- *"Create a pursuit for Acme Corp's commercial litigation RFP."*
- *"Convert the approved proposal to PDF and draft the covering email."*

As with any AI assistant, Claude can make mistakes. Review drafts, and verify important answers against the source content the connector cites, before sending anything to a client.

## Uninstall or disconnect

- **Uninstall the plugin:** in Claude, go to **Customize > Plugins**, find QorusDocs, and uninstall it. In Claude Code, run `/plugin uninstall qorusdocs@qorusdocs`.
- **Revoke access but keep the plugin:** disconnect QorusDocs in Claude's connector settings. Access is revoked immediately, and you can reconnect at any time.

## Frequently asked questions

**Can the connector change or delete data in QorusDocs?**
It can create and update pursuits and the documents on them, when you ask and with your approval before each change. It cannot delete pursuits, documents, answers, or library content. See *Changes the connector can make* above.

**Can a user see or change data through Claude that they can't in QorusDocs?**
No. Every tool call executes as the signed-in user, runs the same permission checks as the QorusDocs application, and is filtered by that user's hub, team, pursuit, and content permissions.

**Do I need the plugin if I already use the connector?**
Only if you want the guided create Pursuit workflow. The connector on its own handles everything else in this article, including building other pursuit documents from your templates. The plugin adds the Pursuit skill. Don't run both: disconnect the standalone connector after installing the plugin.

**What documents can I create?**
Any document your hub has a template for. Claude can draft from any template in your hub's document libraries, merge in the bios and experience selected for the pursuit, and deliver the result in Word or PowerPoint format (depending on the template used) or as a PDF. The Pursuit skill only adds guided steps for creating a Pursuit.

**Does QorusDocs need any setup before our users can connect?**
No credentials need to be exchanged: authorization uses OAuth 2.0 with dynamic client registration, so no client IDs, secrets, or server URLs are provisioned. The pursuit tools must be enabled on your hub, and building pursuit documents needs templates and, for automatic selection of bios and experience, a Pursuit Type with Assignments. See *Prerequisites*.

**Does the plugin support single sign-on?**
Yes. Users sign in through your existing QorusDocs login flow, including Microsoft Entra SSO where configured.

**How do we control who in our organization can use the plugin?**
A QorusDocs license is required, so only your QorusDocs users can connect. In addition, Claude organization administrators can restrict which plugins and connectors members may enable, or install the plugin for everyone, through Claude's own admin controls.

**Can we see what the skill tells Claude to do?**
Yes. The skill is plain text in the public plugin repository, [github.com/QorusDocs/claude-plugin](https://github.com/QorusDocs/claude-plugin). It is licensed for use with a QorusDocs subscription only.

**Does the plugin handle personal health data?**
No.

## Support

- Help and support requests: [QorusDocs Help Center](https://helpcenter.qorusdocs.com/hc/en-us/requests/new)
- Privacy policy: [qorusdocs.com/privacy-policy/proposalhub](https://www.qorusdocs.com/privacy-policy/proposalhub)
