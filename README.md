# Smart Email Notifier

A reusable ChatGPT Skill for important-email triage and actionable reminders.

> **Tell ChatGPT what you don't want to miss. The Skill designs the filtering strategy, uses available tools where possible, and asks for your help only when authentication or consent is required.**

[中文说明](./README.zh-CN.md) · [Skill](./SKILL.md) · [QQ Mail → Gmail → ChatGPT example](./docs/qqmail-gmail-chatgpt.md)

## Why

Important messages are often buried among newsletters, promotions, and routine notifications. Keyword filters alone are also imperfect: an urgent message may say only “the next-round schedule has been updated”, while a promotional email may contain many high-signal keywords.

Smart Email Notifier uses a two-stage approach:

```text
mailbox recall rule → AI semantic triage → actionable reminder
```

**Mailbox rules reduce misses; AI reduces noise.**

## Quick start

Install or provide [`SKILL.md`](./SKILL.md), then describe what matters in natural language:

```text
帮我配置秋招重要邮件提醒。
```

```text
工作会议有改期、取消或者需要我提前准备时提醒我。
```

```text
学校邮件里有考试、作业或需要我处理的通知时提醒我。
```

The Skill will adapt the setup to the scenario and to the capabilities currently available. It can propose mailbox rules, generate the semantic triage policy, use connected mail/task capabilities when available, and guide the remaining provider-specific steps.

Authentication, CAPTCHA, SMS/2FA and sensitive consent always remain user-controlled.

## What it can help configure

Depending on the mailbox and available tools, the Skill can help with:

- mailbox folders or labels;
- subject/body/sender matching;
- any-match / all-match / exclusion logic;
- recall keywords and exclusions;
- selective forwarding or routing;
- AI semantic triage rules;
- extraction of deadlines, event times and next actions;
- recurring or conditional checks;
- end-to-end verification.

It does **not** grant itself mailbox or browser permissions. Automation depends on the ChatGPT environment, connected services and user authorization.

## Example: job-search email

This project started from a job-search workflow: recruiting promotions, assessments, interviews, HR requests and offer-related messages all arrived in the same mailbox.

One working setup was:

```text
QQ Mail
→ broad recall rule
→ selective forwarding to Gmail
→ ChatGPT semantic triage
→ notify only when action is required
```

The reusable Skill is provider- and scenario-oriented; the QQ Mail workflow is only one example. See the [sanitized walkthrough](./docs/qqmail-gmail-chatgpt.md) and the job-search preset in [`presets/`](./presets/).

## Use cases

Job search, work and meeting notices, school deadlines, billing and renewals, order exceptions, account/security notices, or any custom class of email where missing an actionable message has a real cost.

## Repository

```text
SKILL.md      reusable Skill instructions
presets/      scenario-specific policies and examples
docs/         provider examples and automation notes
assets/       sanitized public demo assets
```

Start with [`SKILL.md`](./SKILL.md). The supporting files explain examples; they are not required reading before using the Skill.

## Privacy and safety

Prefer selective forwarding over forwarding an entire private inbox. Never provide mailbox passwords, SMS codes, recovery codes, app passwords, tokens or cookies to the Skill.

Public examples should use synthetic identities and links. Remove real email addresses, phone numbers, candidate/account IDs, private assessment or meeting links, authorization data, QR codes and URLs containing identifying parameters.

## Status

V1 focuses on a reusable Skill rather than a standalone email application. Provider capabilities vary, so the Skill deliberately degrades from automation to guided setup when a required tool is unavailable.

## License

No license has been selected yet. Until a license is added, the repository is publicly viewable but no open-source reuse rights are granted by default.
