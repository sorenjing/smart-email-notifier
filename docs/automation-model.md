# Automation Model / 自动化模型

Smart Email Notifier is designed around a simple rule:

> **Automate what the runtime can do; turn everything else into the shortest possible human checkpoint.**

It is not a browser macro and it does not gain mailbox permissions merely because `SKILL.md` is installed.

## Three levels of automation

### Level 1 — Guide

The runtime has no mailbox or task connector. The Skill can still:

- choose an appropriate preset;
- generate mailbox filter values;
- route the user to provider settings when a verified route is available;
- provide the semantic policy;
- explain the minimum manual setup.

### Level 2 — Assisted setup

The runtime can access the destination mailbox and/or create tasks, but cannot control the source mailbox.

Typical QQ Mail → Gmail → ChatGPT flow:

```text
USER: create QQ Mail folder/rule
USER: complete SMS verification
AUTO: find forwarding verification in Gmail
USER: approve provider consent if required
AUTO: verify Gmail access
AUTO: create recurring semantic check
AUTO: classify and notify thereafter
```

This is the expected mode for many real deployments.

### Level 3 — Connector-driven setup

If the runtime also has a supported source-mailbox connector capable of rule/folder writes, more initialization can be automated. Authentication, 2FA, sensitive consent, and security boundaries remain human checkpoints.

## Why not automate every click?

Email forwarding changes where private communications are delivered. Providers intentionally protect these operations with authentication, verification, and consent. A trustworthy Skill should respect those boundaries instead of attempting to bypass them.

The goal is therefore not “zero clicks”. The goal is:

> **minimum safe setup effort + zero repetitive inbox checking.**

## Capability matrix

| Capability | Without connector | With read connector | With read/write connector |
| --- | --- | --- | --- |
| Generate filter policy | Auto | Auto | Auto |
| Create source folder/rule | Manual | Manual | Potentially auto |
| SMS / 2FA | Human | Human | Human |
| Approve forwarding consent | Human | Human unless supported safely | Human unless supported safely |
| Verify destination inbox | Manual | Auto | Auto |
| Create recurring AI task | Depends on runtime | Depends on runtime | Depends on runtime |
| Semantic classification | When AI can read mail | Auto | Auto |
| Deadline/action extraction | When AI can read mail | Auto | Auto |
| Ongoing notification | With task support | Auto | Auto |

## Completion criteria

A setup should only be called **complete** when the system has verified the available portions of the end-to-end path. If the source rule has not yet delivered a message, report it as “configured, awaiting verification” rather than claiming success.
