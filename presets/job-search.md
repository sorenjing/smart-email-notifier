# Job Search Preset

Use this preset for internship, campus recruiting, graduate recruiting, and experienced-hire workflows.

## Source-mailbox coarse filter

Suggested starter signals:

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
Offer
签约
背调
候选人
下一轮
笔试邀请
面试邀请
```

Tune this list based on false negatives and false positives. Do not treat it as the final notification policy.

## Semantic notification policy

Notify for new messages that contain one or more of:

- a coding test, written test, assessment, or interview that needs attendance;
- an explicit deadline or validity window;
- a request from HR/recruiting that requires a reply or submission;
- an offer, signing, background-check, onboarding, or document action;
- a meaningful status change that affects the candidate's next step.

Usually suppress:

- generic employer-branding campaigns;
- campus recruiting launch announcements with no personal action;
- newsletters and job recommendations;
- repeated reminders for an already-known event unless urgency has materially changed;
- duplicate forwarded copies.

## Extraction schema

```text
Company:
Role:
Category:
Event time:
Deadline:
Link:
Required action:
Urgency:
Reason for notification:
```

If a field is absent, mark it as unknown rather than guessing.

## Suggested reminder prompt

```text
Check my connected mailbox for new messages since the previous check. Focus on job-search and recruiting messages that require action or materially change my application status. Include coding tests, written tests, assessments, interviews, HR requests, offers, signing, background checks, onboarding, explicit deadlines, and other candidate actions.

For each actionable new item, extract the company, role, category, event time, deadline, relevant link, required action, urgency, and why it deserves a notification. Suppress ads, newsletters, generic recruiting promotions, duplicate forwards, and informational messages with no action. If an explicit deadline exists, highlight remaining time and the next step. Never invent dates, deadlines, or links.
```
