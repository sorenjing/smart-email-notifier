# ChatGPT App / MCP Roadmap

This document defines when Smart Email Notifier should evolve beyond a Skill.

## Decision

**Do not build an MCP server merely to duplicate capabilities ChatGPT already provides.**

The Skill remains the orchestration layer. Add a ChatGPT App / MCP server only when a stable provider-specific capability is missing from the user's ChatGPT environment.

## Primary archetype

If/when an app is added, start with a **tool-only** ChatGPT App unless a real inline UI need emerges.

Why:

- the product is primarily orchestration and background actions;
- a widget is not required to classify email;
- fewer moving parts make permissions and privacy easier to audit;
- ChatGPT itself remains the user interface.

## Candidate MCP tools

Only implement tools that close real capability gaps.

### Provider configuration

```text
get_provider_setup_capabilities(provider)
```

Read-only. Reports whether the adapter can create folders, filters, forwarding rules, or only provide navigation.

```text
prepare_forwarding_rule(provider, scenario, destination)
```

Returns a proposed configuration. It must not expose secrets and should remain reviewable before mutation.

```text
apply_forwarding_rule(provider, rule)
```

Mutating. Only for providers with a supported authenticated API. Never bypass 2FA or consent.

### Verification

```text
verify_forwarding(source_provider, destination_provider)
```

Read-only/idempotent where possible. Confirms whether a privacy-safe test message reached the destination.

### Presets

```text
get_notification_preset(name)
```

Returns the semantic policy and suggested recall signals for job search, school, billing, meetings, orders, security, or custom scenarios.

## What should remain native ChatGPT behavior

Do not reimplement these in MCP if ChatGPT already exposes them safely:

- Gmail search/read;
- Task/automation creation;
- general semantic classification;
- deadline/action extraction;
- ordinary browser/computer navigation.

The Skill should discover and use native capabilities first.

## Security properties

Any future app must preserve these invariants:

1. No mailbox passwords, SMS codes, recovery codes, or app passwords are accepted as tool inputs.
2. Forwarding mutations require explicit user intent and provider authorization.
3. The default is selective forwarding, not full-inbox forwarding.
4. Public examples use synthetic identities and URLs.
5. Tool results minimize message content and personal data.
6. Logs must not store raw sensitive email bodies by default.
7. Retryable mutations must be idempotent or guarded against duplicate rule creation.

## Minimum repo contract for the future app

When implementation begins:

```text
server/
  src/
    index.ts
    tools/
    providers/
  package.json
README.md
```

The MCP server should expose `/mcp`, use one user intent per tool, set accurate read-only/destructive/idempotent annotations, and include a local validation command.

No widget should be added until a concrete interaction requires one.

## Validation ladder

1. Static contract review.
2. TypeScript compile/lint.
3. Local `/mcp` runtime sanity.
4. MCP Inspector test.
5. ChatGPT Developer Mode end-to-end test.
6. Only then consider production hosting or public submission.

## Product milestones

### v0.1 — Skill

- ChatGPT-first orchestration
- Gmail + Tasks when available
- QQ Mail guided/browser-assisted setup
- job-search preset

### v0.2 — More presets

- school
- billing
- meetings
- orders
- security

### v0.3 — Provider adapters

Add adapter code only for providers whose configuration cannot be reliably completed with native ChatGPT capabilities.

### v1.0 — Optional ChatGPT App

A tool-only MCP app with audited provider actions, stable auth, privacy documentation, and end-to-end verification.

## Public positioning

Current:

> 安装一次，只告诉 ChatGPT 你不想错过什么；剩下能安全自动完成的，都交给它。

Future App version:

> Skill 负责判断和编排，Provider Adapter 负责执行，ChatGPT 仍然是唯一交互入口。
