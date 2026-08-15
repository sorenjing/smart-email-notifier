---
name: smart-email-notifier
description: Use when a user wants important email to be detected and surfaced automatically, especially when mail arrives in an unsupported or secondary mailbox, important messages are buried in noise, deadlines are easy to miss, or a reusable email-to-AI notification workflow is needed.
---

# Smart Email Notifier

## Overview

Act as a **capability-aware setup wizard**, not a static tutorial.

> Automate every step the current runtime can safely perform; guide the user only through steps that require unavailable provider access, browser interaction, authentication, verification, or explicit consent.

Target experience: **tell ChatGPT what matters → generate the right mailbox rule and semantic policy → configure what can be configured → ask for human action only at security boundaries → ongoing automatic notification.**

## When to use

Use for job-search notices, school deadlines, work/meeting notices, bills and renewals, orders, account/security notices, or any custom class of email the user cannot afford to miss.

Do not use merely to summarize one already-open email.

## Execution contract

Do not dump the README first. Progress through setup interactively.

### 1. Discover capabilities

Check which actions the runtime can actually perform now:

- read/search the destination mailbox;
- create scheduled or conditional tasks;
- access the source mailbox;
- open/navigate provider setup pages;
- send a harmless test email;
- access calendar/to-do integrations if needed.

Classify each relevant step as **AUTO**, **USER ACTION**, or **OPTIONAL**. Prefer a real capability check over asking whether something is connected. Never claim an action was automated unless it was actually performed.

### 2. Resolve the scenario

Infer the scenario from context when clear; otherwise ask only for the minimum missing information. Common scenarios: `job-search`, `school`, `work/meetings`, `billing`, `orders`, `security`, `custom`.

The scenario determines both:

1. the **mailbox recall rule** used to catch likely candidates;
2. the **AI semantic policy** used to decide whether the user should actually be interrupted.

### 3. Generate the mailbox rule, not just keywords

Before asking the user to configure a provider, translate the scenario into the provider's actual rule model. Recommend, when supported:

- folder/label name;
- field(s) to match, e.g. subject, body, sender;
- match operator;
- include terms;
- exclude terms if useful;
- actions such as move/label, forward, retain original;
- forwarding destination when already known and appropriate.

Choose the operator intentionally. For broad recall, prefer an **OR / any-match** operator such as `包含任一` rather than requiring every keyword to appear. Use `包含全部` only when all terms are genuinely required; use `不包含任一` / `不包含全部` only when exclusions improve precision without creating unacceptable false negatives.

For QQ Mail job-search recall, a typical starting recommendation is:

```text
条件关系：任一条件
主题：包含任一 → 面试 / 笔试 / 测评 / offer / Offer / 录用 / 初试 / 复试 / 校招 / 补录 / 签约 / 背调
正文：包含任一 → 面试 / 笔试 / 测评 / offer / Offer / 录用 / 参加 / 初试 / 复试 / 校招 / 补录 / 签约 / 背调 / 候选人 / 下一轮
动作：移动到「求职」 + 自动转发到 AI 可访问邮箱 + 保留原邮件
```

This is a recall layer, not the notification policy. Tune suggestions to the user's scenario and provider instead of blindly reusing this example.

### 4. Configure the source mailbox

If the source mailbox is controllable, create the folder/label and routing rule after any required approval.

If it is not controllable:

1. open the verified provider settings route when the runtime supports it;
2. tell the user exactly which UI values to select, using the generated rule;
3. stop only at authentication, SMS/2FA, CAPTCHA, consent, or unsupported UI actions;
4. resume when the user confirms completion.

Prefer selective forwarding over forwarding an entire private inbox.

### 5. Handle verification as a human checkpoint

Never request or handle mailbox passwords, SMS codes, app passwords, recovery codes, or authorization tokens. If mobile verification or forwarding consent is required, explain only the immediate action and wait. If the confirmation email arrives in a connected destination mailbox, locate it automatically when possible.

### 6. Verify destination-mailbox connectivity

If the destination mailbox connector is available, perform a harmless search/read test. If unavailable, direct the user to connect it and verify afterward.

### 7. Generate the semantic policy

Generate a scenario-specific instruction rather than forcing the user to write one. For each candidate email, extract relevant fields such as sender/organization, category, required action, event time, explicit deadline, relevant link, urgency, and next action.

Notify only when the message creates a meaningful action, deadline, status change, risk, or decision. Suppress advertisements, newsletters, duplicate forwards, generic promotions, and FYI messages with no action. Never invent missing facts.

Base template:

> Check my connected mailbox for new messages since the previous check. Identify messages related to [SCENARIO] that create an action, deadline, status change, risk, or decision. Extract the sender/organization, category, event or action, event time, explicit deadline, relevant link, urgency, and next action. Suppress advertisements, newsletters, duplicate forwards, generic promotions, and informational messages that require no action. Notify me only when something new requires attention. If a deadline is explicit, highlight remaining time and the recommended next step. Never invent missing dates, deadlines, links, or status.

### 8. Create the automation

If task/automation tooling is available, create the recurring or conditional check directly instead of asking the user to copy a prompt. Choose cadence from consequence, latency, and the user's timezone rather than hard-coding one schedule for every scenario.

### 9. Verify end to end

Verify as much as tools allow:

`source inbox → rule/folder → destination inbox → AI retrieval → semantic classification → scheduled notification`

Use a harmless test when possible. Report separately what is verified automatically, what is configured but awaiting real mail, and what still requires user action.

## Provider adapter: QQ Mail → Gmail → ChatGPT

Use when QQ Mail is the source and Gmail is the AI-accessible destination.

1. Generate the scenario-specific QQ Mail folder and receive-rule values.
2. If QQ Mail is not controllable, guide/open the settings and let the user enter only the required values.
3. Configure move-to-folder + selective forwarding + retain-original where appropriate.
4. **USER ACTION:** complete QQ Mail mobile verification if prompted.
5. **AUTO when Gmail is connected:** locate the QQ Mail forwarding verification message.
6. **USER ACTION:** approve forwarding if the consent click cannot be safely executed.
7. **AUTO:** verify Gmail retrieval.
8. **AUTO when Tasks exist:** create the semantic check.
9. Verify the chain.

The architecture is deliberately two-stage:

> **mailbox rule maximizes recall → AI classification improves precision.**

## Setup status format

Keep progress concise, for example:

```text
Smart Email Notifier
✓ Scenario understood
✓ Recommended mailbox rule generated
✓ Destination mailbox connected
✓ Semantic policy generated
✓ Recurring check created
→ Source-mail forwarding: waiting for your verification
○ End-to-end test: pending
```

## Privacy and safety

Before publishing screenshots, examples, logs, or documentation, replace rather than merely blur full email addresses, phone numbers, verification codes, unnecessary personal names, candidate/student/account IDs, private assessment/interview/application links, meeting links that grant access, tokens, authorization codes, cookies, app passwords, QR codes, message IDs, and URLs containing identifiers or secrets.

Use synthetic values such as `example@qq.com` and `yourname@example.com`. Mark fictional recruiting cards as `演示数据 · 非真实招聘通知`.

## Boundaries

- A Skill does not itself grant mailbox or browser permissions.
- Never fabricate a provider settings URL.
- Never bypass authentication, 2FA, forwarding consent, CAPTCHA, or provider security controls.
- Never ask for secrets that should remain between the user and provider.
- Do not forward the entire private inbox by default.
- Do not create noisy notifications for every matching email.
- Provider-specific UI behavior belongs in adapters; scenario policy remains reusable.
