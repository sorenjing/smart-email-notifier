# ChatGPT Runtime Contract

Smart Email Notifier is **ChatGPT-first**. The Skill should use ChatGPT's available tools instead of turning every capability into a manual README step.

## User experience

After installation, the intended interaction is as small as:

```text
帮我配置秋招邮件提醒。
```

or:

```text
帮我盯住学校邮箱里所有需要我处理的通知。
```

The Skill then discovers what ChatGPT can do in the current surface and executes as much setup as possible.

## Preferred tool order

1. **Connected apps / connectors** — use native mailbox access when available.
2. **Tasks / automations** — create the recurring or conditional check directly.
3. **Browser tooling** — when the current ChatGPT surface supports browser interaction, navigate provider pages and fill non-sensitive configuration where permitted.
4. **Human checkpoint** — stop only for login, CAPTCHA, SMS/2FA, sensitive consent, or an action unsupported by the current tools.
5. **Guided fallback** — if browser/provider control is unavailable, give the shortest exact navigation path and resume after the user completes it.

Do not ask users to copy an automation prompt when ChatGPT can create the task itself.

## Browser behavior

Browser automation is an optimization, not a guaranteed dependency. Tool availability can differ by ChatGPT surface, plan, workspace, region, and provider behavior.

When browser tooling is available:

- open the provider's verified official page;
- navigate toward the relevant mail settings;
- fill ordinary non-secret fields when permitted;
- let the user take over for login, CAPTCHA, SMS/2FA, passwords, security codes, or sensitive consent;
- continue after control returns.

Never fabricate a settings URL or bypass provider security controls.

## QQ Mail example

Desired ChatGPT-first flow:

```text
User: 帮我配置秋招邮件提醒

ChatGPT:
AUTO  infer job-search preset
AUTO  inspect Gmail + Tasks + browser availability
AUTO  open QQ Mail if browser tooling is available
USER  login if required
AUTO  navigate to receiving rules where possible
AUTO  prepare folder name + recall keywords + forwarding target
USER  complete phone verification
AUTO  search Gmail for the forwarding verification message
USER  approve consent if the runtime cannot safely do so
AUTO  verify Gmail retrieval
AUTO  create the recurring recruiting-mail task
AUTO  run an end-to-end verification
DONE  report only verified capabilities and remaining caveats
```

If browser tooling is absent, only the QQ Mail web-configuration portion degrades to guided setup. Gmail retrieval and Tasks should still be automated when their tools are available.

## Installation promise

Recommended public wording:

> **Install once, tell ChatGPT what you don't want to miss, and let it automate everything the current ChatGPT environment can safely do.**

Chinese:

> **安装一次，只告诉 ChatGPT 你不想错过什么；剩下能安全自动完成的，都交给它。**

Avoid claims such as “zero-click setup”, “fully automatic on every ChatGPT client”, or “automatically controls QQ Mail after installation”.
