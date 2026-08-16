---
name: smart-email-notifier
description: Help users set up reliable important-email triage and reminders. Use when a user wants to avoid missing actionable email such as job-search, school, work, billing, order, or security notices, especially when important messages are buried in noise or arrive in a mailbox that needs routing to an AI-accessible inbox.
---

# Smart Email Notifier

## Goal

Turn a natural-language intent such as:

> “帮我配置秋招重要邮件提醒。”

into a practical workflow that maximizes recall at the mailbox layer and uses semantic judgment to reduce unnecessary notifications.

Target experience:

```text
tell ChatGPT what matters
→ understand the scenario
→ design mailbox recall + AI triage
→ use available capabilities
→ ask for user action only where required
→ verify the workflow
→ notify only when attention is needed
```

## Core principle

Use two stages instead of treating keyword matching as the final decision:

> **mailbox rule maximizes recall → AI semantic triage improves precision**

Mailbox rules should catch plausible candidates. Semantic triage should decide whether a message creates a meaningful action, deadline, status change, risk, or decision.

## Workflow

### 1. Understand the scenario

Infer the user's goal from context when it is clear. Ask only for information that is necessary to design the workflow.

Typical scenarios include job search, school, work/meetings, billing, orders, security notices, and custom high-priority email.

### 2. Check available capabilities

Determine which parts can actually be performed in the current environment, such as:

- reading/searching a connected mailbox;
- creating scheduled or conditional checks;
- accessing the source mailbox;
- navigating provider settings;
- performing a harmless end-to-end test.

Tool availability varies by client, plan, region, provider and authorization. Never represent an unavailable or unperformed action as completed.

### 3. Design the mailbox recall rule

Adapt the rule to the provider's actual filtering model. When supported, consider:

- folder or label;
- subject, body and sender fields;
- any-match / all-match / exclusion logic;
- recall keywords and useful exclusions;
- move, label, retain or selective-forwarding actions.

Prefer broad recall when false negatives are costly. An OR / any-match rule is often more appropriate than requiring every signal to appear. Use stricter matching only when the scenario warrants it.

Provider- and scenario-specific values belong in presets or examples rather than being hard-coded into the core workflow.

### 4. Configure or guide the mailbox setup

Use available provider or browser capabilities when they can safely perform the setup. Otherwise provide the shortest exact manual path and the values the user should enter.

Prefer selective forwarding over forwarding an entire private inbox.

Authentication, CAPTCHA, SMS/2FA, passwords, security codes and sensitive consent remain user-controlled. Resume the workflow after the user completes the required checkpoint.

### 5. Create the semantic triage policy

Generate a policy appropriate to the scenario. For each candidate message, identify relevant fields such as:

- sender or organization;
- category;
- required action;
- event time;
- explicit deadline;
- relevant link;
- urgency;
- recommended next action.

Notify only when a new message creates a meaningful action, deadline, status change, risk, or decision. Suppress advertisements, newsletters, duplicate forwards, generic promotions and informational messages that require no action. Never invent missing dates, links, deadlines or status.

A useful base policy is:

> Check new messages since the previous check. Identify messages related to the user's scenario that create an action, deadline, status change, risk, or decision. Extract the organization/sender, category, required action, event time, explicit deadline, relevant link, urgency, and next action. Suppress advertisements, newsletters, duplicate forwards, generic promotions, and informational messages that require no action. Notify only when something new requires attention. Highlight explicit deadlines and the recommended next step. Never invent missing information.

### 6. Set up ongoing checks when available

When task or automation capabilities are available, create the recurring or conditional check directly. Choose the cadence according to the consequence and time sensitivity of the scenario rather than applying one fixed schedule to every user.

If automation is unavailable, provide the generated policy so the user can use it in an environment that supports recurring checks.

### 7. Verify the workflow

Verify as much of the chain as the available tools allow:

```text
source inbox
→ recall rule / routing
→ AI-accessible inbox
→ semantic triage
→ reminder
```

A harmless test message can be used when appropriate. Clearly distinguish between verified steps, configured-but-unverified steps, and remaining user actions.

## Provider examples

Provider-specific behavior should remain outside the core Skill whenever possible.

For the QQ Mail → Gmail → ChatGPT example, see:

- `docs/qqmail-gmail-chatgpt.md`
- the relevant scenario preset under `presets/`

The example demonstrates selective forwarding, provider verification and semantic triage; it is not a requirement that every user follow the same architecture.

## Progress reporting

Keep setup progress concise and useful. For example:

```text
Smart Email Notifier
✓ Scenario understood
✓ Recall strategy generated
✓ Destination mailbox available
✓ Semantic policy generated
→ Source-mail verification needs your action
○ End-to-end test pending
```

## Privacy and safety

- Prefer selective forwarding over forwarding an entire private inbox.
- Do not request mailbox passwords, SMS codes, recovery codes, app passwords, tokens or cookies.
- Do not bypass authentication, CAPTCHA, 2FA or provider consent.
- Do not fabricate provider URLs, capabilities or completed actions.
- Minimize the amount of private email exposed to downstream services.
- Avoid noisy notifications for every keyword match.

When preparing public screenshots, examples or logs, replace personal data with synthetic values rather than relying on blur alone. Remove real email addresses, phone numbers, verification data, unnecessary names, candidate/student/account IDs, private assessment/interview/application links, meeting links, tokens, cookies, authorization codes, QR codes, message IDs and URLs containing identifying parameters.

## Boundaries

This Skill orchestrates capabilities that are available in the current environment; it does not grant new mailbox, browser or task permissions by itself. When a required capability is unavailable, fall back to concise guided setup instead of claiming full automation.
