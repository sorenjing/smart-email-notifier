# Smart Email Notifier

**AI 重要邮件智能提醒｜自动识别重要邮件、截止时间与下一步行动。**

[中文文档](./README.zh-CN.md) · English

![Privacy-safe QQ Mail → Gmail → ChatGPT demo](./assets/qqmail-gmail-chatgpt-demo.svg)

A reusable AI-assisted workflow for turning important emails into actionable reminders.

Instead of forwarding an entire inbox and generating more noise, this project uses a two-stage design:

**mailbox rule for broad routing → AI for semantic judgment and reminders**

## What problem does it solve?

Important messages are often mixed with newsletters, promotions, and routine notifications. A keyword filter alone is too brittle: an urgent email may say “next-round arrangement” without using the word “interview”, while a recruiting advertisement may contain “interview” and “assessment” without requiring any action.

Smart Email Notifier separates the problem:

- **Source mailbox:** broadly collects potentially important messages.
- **Destination mailbox:** provides an inbox that your AI assistant can access.
- **AI layer:** decides whether a message actually requires attention and extracts deadlines/actions.
- **Automation layer:** checks on an appropriate cadence and notifies only when necessary.

## Architecture

```text
Source mailbox
    ↓
Folder / receiving rule
    ↓
Selective forwarding
    ↓
AI-accessible mailbox
    ↓
Semantic classification
    ↓
Action / deadline extraction
    ↓
Scheduled or conditional reminder
```

## Supported scenarios

| Scenario | Examples of actionable mail |
| --- | --- |
| Job search | assessment, coding test, interview, HR action, offer, signing deadline |
| School | exam, assignment deadline, administrative notice, course change |
| Billing | invoice, renewal, failed payment, cancellation deadline |
| Meetings | invitation, reschedule, preparation request |
| Orders | delivery exception, pickup deadline, refund update |
| Security | login warning, verification request, account action |

## Quick start

1. Decide which class of emails you cannot afford to miss.
2. Create a dedicated folder/label in the source mailbox (recommended, not required).
3. Add broad receiving rules and selectively forward matches to a supported destination mailbox.
4. Complete any manual forwarding verification required by the providers.
5. Connect the destination mailbox to your AI assistant.
6. Create a semantic policy that extracts actions and deadlines while suppressing noise.
7. Schedule checks at a cadence appropriate for the scenario.
8. Test the full path end to end.

See [`SKILL.md`](./SKILL.md) for reusable agent instructions and [`docs/qqmail-gmail-chatgpt.md`](./docs/qqmail-gmail-chatgpt.md) for the privacy-safe QQ Mail → Gmail → ChatGPT walkthrough.

## Real example: QQ Mail → Gmail → ChatGPT for recruiting notifications

This repository was initially inspired by a real campus-recruiting problem: coding tests and interview invitations arrive in QQ Mail among many recruiting messages, making deadlines easy to miss.

Recommended setup:

```text
Create a dedicated “求职” folder
→ create broad receiving rules
→ move matches to the folder + selectively forward to Gmail
→ complete QQ Mail verification
→ approve forwarding in Gmail
→ connect Gmail to ChatGPT
→ create semantic reminder checks
```

The keyword list is a **coarse filter**, not the final intelligence layer. AI performs the final semantic decision because important mail may use wording such as `下一轮安排` without saying `面试`, while a marketing email may contain many recruiting keywords without requiring action.

Job-search preset: [`presets/job-search.md`](./presets/job-search.md).

## Reusable automation prompt

```text
Check my connected mailbox for new messages since the previous check.
Identify messages related to [SCENARIO] that create an action, deadline,
status change, risk, or decision.

Extract the sender/organization, category, event or action, event time,
deadline, relevant link, and the next action I need to take.

Suppress advertisements, newsletters, duplicate forwards, generic promotions,
and informational messages that require no action. Notify me only when something
new requires attention. If a deadline is explicit, highlight the remaining time
and recommended next step. Never invent missing dates or deadlines.
```

## Privacy before publishing

Do not publish real screenshots until you have removed or replaced full email addresses, phone numbers, verification codes, candidate/account IDs, private assessment/interview links, meeting links, tokens, cookies, app passwords, QR codes, authorization codes, and URLs containing personal identifiers.

Use synthetic values such as `example@qq.com`, `yourname@gmail.com`, and `https://example.com/...` in documentation. Prefer a sanitized demonstration over placing a weak translucent blur on secrets.

## Design principles

1. **Important ≠ contains a keyword.** Final classification should be semantic.
2. **Do not forward everything by default.** Minimize unnecessary exposure of private mail.
3. **Notify on actionability.** A good notifier reduces interruptions rather than creating them.
4. **Human verification stays human.** Authentication and sensitive confirmation steps should not be delegated.
5. **Provider-specific setup is an adapter.** The core Skill remains reusable across mail providers and scenarios.

## Status

Early version based on a working QQ Mail → Gmail → ChatGPT recruiting-notification workflow. More provider adapters and scenario presets can be added over time.

## License

No license has been selected yet. Add one before encouraging third-party redistribution or modification.
