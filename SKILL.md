---
name: smart-email-notifier
description: Build an AI-assisted important-email notification workflow. Use when a user wants to route important messages from an unsupported or secondary mailbox into an AI-accessible mailbox, classify actionable emails semantically, extract deadlines and required actions, and create scheduled reminders. Supports job-search, school, billing, meetings, orders, account/security, and custom scenarios. Never expose mailbox addresses, phone numbers, verification codes, private application links, candidate IDs, tokens, or other secrets in public examples.
---

# Smart Email Notifier

Turn an inbox from a passive message store into an actionable notification workflow.

## Core architecture

`Source mailbox → coarse mail rule → AI-accessible mailbox → semantic classification → scheduled/conditional notification`

Keep the two filters separate:

1. **Mailbox rules optimize recall.** They should broadly route potentially important mail.
2. **AI classification optimizes precision.** It decides whether a message actually requires attention or action.

Do not rely on keywords alone for final notification decisions.

## Workflow

### 1. Define the scenario

Ask what the user cannot afford to miss. Examples:

- job search: assessments, interviews, HR actions, offers, signing deadlines
- school: course notices, exams, deadlines, administrative actions
- billing: invoices, renewals, payment failures
- meetings: invitations, reschedules, required preparation
- orders: delivery exceptions, pickup deadlines, refunds
- account/security: login warnings, verification requests, policy changes

Create a broad keyword set only as a first-stage routing rule.

### 2. Create a dedicated folder/label in the source mailbox

Prefer a scenario-specific folder such as `求职`, `学校`, `账单`, or `Important-AI` rather than forwarding the entire inbox.

### 3. Create a receiving rule

Configure the source mailbox rule to match broad subject/body/sender signals, then:

- move or copy matching messages to the dedicated folder;
- forward matching messages to the AI-accessible destination mailbox when supported;
- keep the original message unless the user explicitly wants otherwise.

Warn that some providers require phone/SMS verification when saving forwarding rules.

### 4. Verify forwarding

Forwarding may require a second confirmation in the destination mailbox. Tell the user to open the provider-generated confirmation email and approve forwarding manually. Never ask the user to paste SMS codes, passwords, app passwords, or mailbox authorization codes into chat.

### 5. Connect the destination mailbox to the AI product

Use the product's supported mailbox connector. Confirm connectivity with a harmless search before claiming the workflow works.

### 6. Build the semantic notification policy

For every new candidate email, extract when available:

- sender/company/organization
- scenario/category
- event or required action
- event time
- deadline
- relevant link
- urgency
- next action

Notify only when the email creates a meaningful action, deadline, status change, risk, or decision. Suppress ads, newsletters, duplicated forwards, generic recruiting promotions, and FYI messages with no action.

If a deadline exists, highlight remaining time and the next action. Do not infer a deadline that is not present.

### 7. Schedule checks

Choose cadence based on consequence and latency. For time-sensitive recruiting or school workflows, several checks during waking hours may be appropriate. For bills or newsletters, daily or weekly checks may be enough. Use the user's timezone.

### 8. Test end to end

Send or wait for a harmless test message that matches the rule. Verify:

`source inbox → folder/rule → destination inbox → AI retrieval → classification → reminder`

Do not treat setup as complete until the forwarding path is verified.

## Reusable automation prompt

Use this as a base and customize the scenario:

> Check my connected mailbox for new messages since the previous check. Identify messages related to [SCENARIO] that create an action, deadline, status change, risk, or decision. Extract the sender/organization, category, event or action, event time, deadline, relevant link, and the next action I need to take. Suppress advertisements, newsletters, duplicate forwards, generic promotions, and informational messages that require no action. Notify me only when something new requires attention. If a deadline is explicit, highlight the remaining time and recommended next step. Never invent missing dates or deadlines.

## Example: QQ Mail → Gmail → ChatGPT for campus recruiting

A real deployment can use QQ Mail as the source mailbox and Gmail as the AI-accessible mailbox.

1. In QQ Mail, create a folder such as `求职`.
2. Create receiving rules with broad signals such as `面试`, `笔试`, `测评`, `在线测评`, `校招`, `秋招`, `录用`, `offer`, `签约`, `背调` and similar phrases.
3. Configure matching mail to enter the `求职` folder and forward to Gmail.
4. Save the rule. QQ Mail may require manual mobile-phone verification.
5. Open Gmail and find the forwarding confirmation email sent by QQ Mail. Open it and manually approve/confirm automatic forwarding.
6. Connect Gmail to ChatGPT.
7. Create a recurring check for new recruiting mail. Let the AI distinguish actionable assessments/interviews/deadlines from ordinary recruiting promotions.
8. Test the complete chain before relying on it.

The important design choice is that the QQ Mail keyword rule is deliberately broad. The AI performs the final semantic decision, because important mail may use wording such as `下一轮安排` without saying `面试`, while a marketing email may contain many recruiting keywords without requiring action.

## Privacy and publication checklist

Before publishing screenshots, examples, videos, or documentation, redact or replace:

- full email addresses
- phone numbers
- verification codes
- names when unnecessary
- candidate/student/account IDs
- private assessment/interview/application links
- meeting links that grant access
- tokens, authorization codes, cookies, app passwords, QR codes
- message IDs or URLs containing secrets

Prefer synthetic examples such as `yourname@example.com`. If a screenshot has already captured a secret, create a sanitized screenshot rather than relying only on a translucent blur.

## Boundaries

- Do not claim universal mailbox support. Provider capabilities differ.
- Do not ask for passwords or verification codes.
- Do not automatically forward an entire private inbox unless the user explicitly accepts that privacy tradeoff.
- Do not convert every email into a notification; the value is reducing noise.
- Keep the workflow provider-agnostic. Provider-specific instructions belong in examples or docs.
