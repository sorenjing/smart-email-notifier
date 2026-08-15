# Smart Email Notifier

**ChatGPT-first AI 重要邮件智能提醒｜告诉 ChatGPT 你不想错过什么，剩下能安全自动完成的交给它。**

[中文文档](./README.zh-CN.md) · English

![Privacy-safe QQ Mail → Gmail → ChatGPT demo](./assets/qqmail-gmail-chatgpt-demo.svg)

Smart Email Notifier is a **ChatGPT-first Skill** for turning important emails into actionable reminders. It is designed to use ChatGPT's existing connected apps, Tasks/automations, and browser/computer capabilities when those capabilities are available in the current environment.

## The intended experience

```text
Install the Skill
      ↓
Tell ChatGPT what you cannot afford to miss
      ↓
ChatGPT discovers available capabilities
      ↓
Automates everything it can safely perform
      ↓
You only take over for login / 2FA / verification / consent
      ↓
Ongoing email checking becomes automatic
```

Example:

```text
帮我配置秋招邮件提醒。
```

The Skill should not respond with a long manual by default. It should inspect the available ChatGPT capabilities, perform supported actions directly, and guide only the missing provider-specific steps.

See [`CHATGPT.md`](./CHATGPT.md) for the runtime contract.

## Why two filtering layers?

Important messages are mixed with newsletters, promotions, and routine notifications. A keyword filter alone is brittle: an urgent email may say `下一轮安排` without saying `面试`, while a recruiting advertisement may contain every recruiting keyword without requiring action.

The architecture therefore separates recall from judgment:

```text
Source mailbox
    ↓
Broad mailbox rule / selective forwarding
    ↓
ChatGPT-accessible mailbox
    ↓
AI semantic classification
    ↓
Action / deadline extraction
    ↓
Task / conditional notification
```

> **Mailbox rules maximize recall. AI decides whether the message deserves your attention.**

## Automation levels

The exact experience depends on the tools available in the user's current ChatGPT environment.

| Level | What happens |
| --- | --- |
| Guide | ChatGPT generates the exact configuration and guides unsupported provider steps |
| Assisted setup | ChatGPT directly uses connected mail + Tasks; the user handles source-mail login/verification |
| Connector-driven | Source and destination providers are both controllable, so more setup can be executed directly |

Authentication, CAPTCHA, SMS/2FA, passwords, recovery codes, and sensitive consent remain human checkpoints.

Read [`docs/automation-model.md`](./docs/automation-model.md) for the detailed capability model.

## ChatGPT-first behavior

When the runtime provides the necessary capabilities, the Skill should prefer:

1. connected mailbox/app tools over manual instructions;
2. direct Task/automation creation over asking the user to copy a prompt;
3. browser/computer interaction for ordinary provider configuration when supported;
4. human takeover only at authentication, verification, CAPTCHA, or sensitive consent boundaries;
5. a guided fallback only for capabilities the runtime genuinely lacks.

A Skill does **not** itself grant browser or mailbox permissions. Availability can differ by ChatGPT client, plan, workspace, region, and provider behavior.

## Real example: QQ Mail → Gmail → ChatGPT

The project was initially inspired by campus recruiting: important coding tests and interviews arrived in QQ Mail among large amounts of recruiting mail.

In a capable ChatGPT environment, the desired flow is:

```text
User: “帮我配置秋招邮件提醒”

AUTO  choose job-search preset
AUTO  inspect Gmail / Tasks / browser capabilities
AUTO  navigate QQ Mail configuration when browser control is available
USER  login / phone verification when required
AUTO  find the forwarding verification message in Gmail
USER  approve sensitive provider consent when required
AUTO  verify Gmail retrieval
AUTO  create the recurring semantic check
AUTO  verify the end-to-end path
```

If QQ Mail cannot be controlled, only that portion degrades to guided setup. Gmail retrieval and Task creation should still be automated when available.

Privacy-safe walkthrough: [`docs/qqmail-gmail-chatgpt.md`](./docs/qqmail-gmail-chatgpt.md).

ChatGPT-first recruiting preset: [`presets/job-search-chatgpt.md`](./presets/job-search-chatgpt.md).

## Supported scenarios

| Scenario | Examples of actionable mail |
| --- | --- |
| Job search | assessment, coding test, interview, HR action, offer, signing deadline |
| School | exam, assignment deadline, administrative notice, course change |
| Billing | invoice, renewal, failed payment, cancellation deadline |
| Meetings | invitation, reschedule, preparation request |
| Orders | delivery exception, pickup deadline, refund update |
| Security | login warning, verification request, account action |

## Skill structure

```text
SKILL.md                       Agent orchestration rules
CHATGPT.md                     ChatGPT runtime contract
presets/                       Scenario-specific policies
docs/automation-model.md       Capability / fallback model
docs/qqmail-gmail-chatgpt.md   Provider-specific example
assets/                        Privacy-safe public visuals
```

## Privacy

Do not publish or feed public examples with real email addresses, phone numbers, verification codes, candidate/account IDs, private assessment/interview links, meeting links, tokens, cookies, app passwords, QR codes, authorization codes, or URLs containing personal identifiers.

Use synthetic values such as `example@qq.com` and `yourname@example.com`. Fictional recruiting cards should be explicitly marked `演示数据 · 非真实招聘通知`.

## Current scope

The repository currently provides the ChatGPT-first orchestration Skill, runtime contract, presets, and provider guidance. It does **not** ship a custom QQ Mail connector or bypass provider authentication/security controls.

A future ChatGPT App / MCP layer can add stable provider-specific tools where native ChatGPT capabilities are insufficient. Current OpenAI frontier models support Skills, computer use, and MCP at the model/tooling layer, which makes this a viable evolution path; actual ChatGPT surface availability still needs to be checked at runtime.

## License

No license has been selected yet. Add one before encouraging third-party redistribution or modification.
