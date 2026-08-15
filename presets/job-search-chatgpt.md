# Job Search — ChatGPT-first preset

## Trigger examples

- 帮我配置秋招邮件提醒
- 帮我盯笔试和面试通知
- 有需要我操作的招聘邮件时提醒我
- Don't let me miss recruiting deadlines

## Desired setup

Prefer the following without asking the user to manually reproduce steps ChatGPT can execute:

1. Detect connected mailbox and Tasks capabilities.
2. Determine whether the source mailbox needs forwarding.
3. Use browser tooling for provider setup when available; otherwise guide only that missing portion.
4. Verify destination-mailbox access.
5. Create the recurring task directly.
6. Verify the path with non-sensitive mail.

## Recall signals for source mailbox

```text
面试
笔试
测评
在线测评
人才测评
初试
复试
校招
秋招
招聘
录用
offer
签约
背调
候选人
下一轮
```

These maximize recall; they do **not** determine whether the user gets notified.

## Semantic policy

Notify when a new message creates a candidate action, explicit deadline, attendance requirement, meaningful application-status change, or decision.

Typical positives:

- coding/written test or assessment;
- interview or interview reschedule;
- HR request requiring reply/submission;
- offer, signing, background check, onboarding;
- explicit candidate deadline;
- material application-status change.

Typical negatives:

- employer branding;
- recruiting launch announcement with no personal action;
- generic job recommendations;
- newsletter;
- duplicate forward;
- repeated reminder whose urgency has not materially changed.

## Extract

```text
Company
Role
Category
Event time
Explicit deadline
Relevant link
Required action
Urgency
Reason for notification
```

Unknown fields remain unknown. Never guess.

## Default task instruction

```text
Check my connected mailbox for new messages since the previous check. Identify job-search and recruiting messages that require action or materially change my application status, including coding tests, written tests, assessments, interviews, HR requests, offers, signing, background checks, onboarding, and explicit candidate deadlines.

For each actionable new item, extract the company, role, category, event time, explicit deadline, relevant link, required action, urgency, and reason for notification. Suppress ads, newsletters, generic recruiting promotions, duplicate forwards, and informational messages with no action. Notify me only when something new requires attention. If an explicit deadline exists, highlight remaining time and the next step. Never invent dates, deadlines, links, or application status.
```

Choose the check cadence from the user's urgency and timezone rather than hard-coding one schedule for everyone.
