# Smart Email Notifier

A reusable AI Skill for important-email triage and actionable reminders.

> **Tell your AI assistant what you do not want to miss. The Skill generates filtering and triage strategies and, when the current environment already provides the required capability and you authorize it, can help carry out supported setup steps. Authentication and sensitive consent remain user-controlled.**

[中文说明](./README.zh-CN.md) · [Skill](./SKILL.md) · [QQ Mail → Gmail → ChatGPT example](./docs/qqmail-gmail-chatgpt.md)

## Why

Important messages are often buried among newsletters, promotions and routine notifications. Keyword filters alone are imperfect: an urgent message may say only “the next-round schedule has been updated”, while a promotional email may contain many high-signal keywords.

Smart Email Notifier uses two stages:

```text
mailbox recall rule → AI semantic triage → actionable reminder
```

**Mailbox rules reduce misses; AI reduces noise.**

## Quick start

Install or provide [`SKILL.md`](./SKILL.md), then describe what matters in natural language, for example:

```text
帮我配置秋招重要邮件提醒。
```

```text
工作会议有改期、取消或者需要我提前准备时提醒我。
```

The Skill generates a mailbox filtering strategy and semantic triage policy for the scenario. If the user's AI environment already provides authorized mailbox, task or related capabilities, it may use those capabilities to assist with supported steps. Otherwise it provides the necessary manual setup guidance.

## What it can help with

Depending on the provider, AI environment and user authorization, the Skill can help:

- design mailbox folders, labels and routing;
- generate subject/body/sender matching rules;
- choose any-match, all-match and exclusion logic;
- generate recall keywords and exclusions;
- design selective forwarding;
- generate semantic triage policies;
- extract explicit deadlines, event times, links and next actions;
- configure recurring or conditional checks when supported;
- assist with end-to-end verification.

## Example: job-search email

This project started from a job-search workflow in which recruiting promotions, assessments, interviews, HR requests and offer-related messages arrived in the same mailbox.

One working setup was:

```text
QQ Mail
→ broad recall rule
→ selective forwarding to Gmail
→ ChatGPT semantic triage
→ notify only when action is required
```

The reusable Skill **does not require QQ Mail, Gmail or ChatGPT**. This is only a sanitized example. See the [walkthrough](./docs/qqmail-gmail-chatgpt.md) and [`presets/`](./presets/).

## Scope and limitations

Please understand the following before use:

- this is a reusable AI workflow Skill, **not a standalone email application or background service**;
- the Skill does not grant itself mailbox, browser, account or task permissions;
- executable capabilities depend on the AI assistant, client, region, email provider, connected services and user authorization;
- unsupported steps fall back to guided manual setup;
- provider interfaces and third-party AI capabilities may change over time;
- AI classification and extraction can be wrong or incomplete, so important items should be verified against the original email;
- no specific message is guaranteed to be recalled, classified or delivered as a timely reminder;
- do not use this Skill as the sole notification channel for legal, medical, financial, security-critical or other high-risk matters.

## Privacy and safety

Prefer selective forwarding over forwarding an entire private inbox. Grant only the access needed for the intended workflow and review the terms and privacy policies of the email provider, AI assistant and any other service you choose to connect.

**Never provide mailbox passwords, SMS codes, recovery codes, app passwords, tokens, cookies, private keys or other secret credentials to the Skill.** The Skill must not bypass authentication, CAPTCHA, 2FA, permission controls or provider security mechanisms.

Public examples should use synthetic identities and links. Remove real email addresses, phone numbers, candidate/account IDs, private assessment/interview/meeting links, authorization data, QR codes and identifying URL parameters.

## Third-party services

Names such as QQ Mail, Gmail and ChatGPT are used only to describe compatible scenarios and example workflows. This project is not affiliated with, endorsed by or sponsored by those service providers. Users remain responsible for complying with applicable third-party terms and authorization requirements.

## Repository

```text
SKILL.md      reusable Skill instructions
presets/      scenario-specific policies and examples
docs/         provider examples and automation notes
assets/       sanitized public demo assets
```

Start with [`SKILL.md`](./SKILL.md). Supporting files explain examples and design decisions.

## License

Released under the [MIT License](./LICENSE). Third-party services, trademarks and platform content remain subject to their respective terms and rights.
