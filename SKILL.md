---
name: smart-email-notifier
description: Use when a user wants important email to be detected and surfaced automatically, especially when mail arrives in an unsupported or secondary mailbox, important messages are buried in noise, deadlines are easy to miss, or a reusable email-to-AI notification workflow is needed.
---

# Smart Email Notifier

## Overview

Act as a **capability-aware setup wizard**, not a static tutorial.

Core principle:

> Automate every step the current runtime can safely perform; guide the user only through steps that require unavailable provider access, browser interaction, authentication, verification, or explicit consent.

The target experience is **one-time setup → automatic ongoing classification and notification**.

## When to use

Use for workflows such as job-search notices, school deadlines, bills and renewals, meetings, orders, account/security notices, or any custom class of email the user cannot afford to miss.

Do not use merely to summarize one already-open email.

## Execution contract

When invoked, do not dump the whole README first. Progress through setup interactively.

### 1. Discover capabilities before instructing

Determine which actions the runtime can actually perform now:

- read/search the destination mailbox;
- create scheduled or conditional tasks;
- access the source mailbox;
- open/navigate provider setup pages;
- send a harmless test email;
- access calendar/to-do integrations if the requested preset needs them.

Prefer a real capability check over asking the user whether something is connected.

Classify each setup step as:

- **AUTO** — perform it directly;
- **USER ACTION** — user must authenticate, verify, consent, or click in an unsupported provider;
- **OPTIONAL** — useful but not required.

Never claim an action was automated unless the runtime actually performed it.

### 2. Resolve the scenario

Infer the preset from context when clear. Otherwise ask only for the minimum missing information.

Examples:

- `job-search`
- `school`
- `billing`
- `meetings`
- `orders`
- `security`
- `custom`

Mailbox keyword rules are only a coarse recall layer. AI semantic classification remains the final decision layer.

### 3. Configure the source mailbox

If the source mailbox is directly controllable, create the folder/label and broad routing rule after obtaining any required user approval.

If it is not controllable:

1. provide the shortest provider-specific route to the relevant settings page when a reliable URL is known;
2. tell the user exactly what to create, using copyable values;
3. stop at authentication/SMS/2FA/consent boundaries and ask the user to complete them;
4. resume from the next step when the user confirms completion.

Prefer selective forwarding of a dedicated folder/rule over forwarding an entire private inbox.

For a job-search preset, a starter recall set can include:

`面试 / 笔试 / 测评 / 在线测评 / 人才测评 / 初试 / 复试 / 校招 / 秋招 / 录用 / offer / 签约 / 背调 / 候选人 / 下一轮`

Tune it from observed false negatives/positives. Do not treat it as the notification policy.

### 4. Handle verification as a human checkpoint

Never request or handle mailbox passwords, SMS codes, app passwords, recovery codes, or authorization tokens.

If the provider requires mobile verification or forwarding consent, explain only the immediate action and wait for completion.

If a confirmation email arrives in a connected destination mailbox, locate it automatically when possible. The user must perform any consent click that the runtime cannot safely execute.

### 5. Verify destination-mailbox connectivity

If the destination mailbox connector is available, perform a harmless search/read test. Do not merely tell the user to test it.

If it is unavailable, direct the user to connect it, then verify after connection.

### 6. Create the semantic policy

For each candidate email, extract when available:

- sender/company/organization;
- scenario/category;
- event or required action;
- event time;
- explicit deadline;
- relevant link;
- urgency;
- next action.

Notify only when the message creates a meaningful action, deadline, status change, risk, or decision.

Suppress advertisements, newsletters, duplicate forwards, generic promotions, and FYI messages with no action.

Never invent missing dates, deadlines, links, status, or urgency.

### 7. Create the automation when the runtime supports it

Do not make the user manually copy a prompt if a task/automation tool is available.

Choose cadence based on consequence and latency, using the user's timezone. Time-sensitive recruiting or school workflows may warrant multiple checks during waking hours; low-urgency billing/newsletter workflows may be daily or weekly.

Base automation instruction:

> Check my connected mailbox for new messages since the previous check. Identify messages related to [SCENARIO] that create an action, deadline, status change, risk, or decision. Extract the sender/organization, category, event or action, event time, explicit deadline, relevant link, urgency, and next action. Suppress advertisements, newsletters, duplicate forwards, generic promotions, and informational messages that require no action. Notify me only when something new requires attention. If a deadline is explicit, highlight remaining time and the recommended next step. Never invent missing dates, deadlines, links, or status.

### 8. Verify end to end

Do not declare setup complete merely because configuration exists.

Verify as much of this chain as tools allow:

`source inbox → rule/folder → destination inbox → AI retrieval → semantic classification → scheduled notification`

If a harmless test can be generated, use one. Otherwise verify against an existing non-sensitive message.

Report separately:

- verified automatically;
- configured but awaiting real mail;
- still requires user action.

## Provider adapter: QQ Mail → Gmail → ChatGPT

Use this adapter when QQ Mail is the source and Gmail is the AI-accessible destination.

1. **USER ACTION if QQ Mail is not controllable:** open QQ Mail settings and create a dedicated folder such as `求职` or `Important-AI`.
2. Create a receiving rule using broad preset signals.
3. Set actions to move matching mail into the dedicated folder and forward it to Gmail while retaining the original message.
4. **USER ACTION:** complete QQ Mail mobile verification if prompted.
5. **AUTO when Gmail is connected:** search Gmail for the QQ Mail forwarding verification message.
6. **USER ACTION:** approve forwarding if the consent link cannot be safely clicked by the runtime.
7. **AUTO:** verify that Gmail is readable by the AI runtime.
8. **AUTO when task tooling exists:** create the recurring semantic check instead of asking the user to copy the prompt.
9. Verify the complete chain.

The architecture is deliberately two-stage:

> mailbox rule maximizes recall → AI classification improves precision.

An important email may say `下一轮安排` without saying `面试`; a recruiting newsletter may contain every keyword while requiring no action.

## Setup status format

Keep progress concise. A useful status summary is:

```text
Smart Email Notifier
✓ Destination mailbox connected
✓ Semantic policy ready
✓ Recurring check created
→ Source-mail forwarding: waiting for your verification
○ End-to-end test: pending
```

Only show steps relevant to the user's current state.

## Privacy and safety

Before publishing screenshots, examples, logs, or documentation, replace rather than merely blur:

- full email addresses;
- phone numbers;
- verification codes;
- personal names when unnecessary;
- candidate/student/account IDs;
- private assessment/interview/application links;
- meeting links that grant access;
- tokens, authorization codes, cookies, app passwords, QR codes;
- message IDs and URLs containing identifiers or secrets.

Use synthetic values such as `example@qq.com` and `yourname@example.com`. Mark fictional recruiting cards as `演示数据 · 非真实招聘通知`.

## Boundaries

- A Skill does not itself grant mailbox or browser permissions.
- Never fabricate a provider settings URL. Use a verified route when available; otherwise give navigation labels.
- Never bypass authentication, 2FA, forwarding consent, or provider security controls.
- Never ask for secrets that should remain between the user and provider.
- Do not forward the entire private inbox by default.
- Do not create noisy notifications for every matching email.
- Provider-specific behavior belongs in adapters; semantic policy belongs in presets.
