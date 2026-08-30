# ADR-001: Use Hermes Agent with Telegram as the homelab control plane

## Status

Accepted and documented after implementation.

## Date

2026-08-31

## Context

The homelab contains automation, media, host, and network services with different administrative interfaces. Routine operation should be accessible from a mobile device without publishing each dashboard or requiring an interactive SSH session for every request.

The control layer must preserve a separate recovery path, avoid embedding secrets in documentation, and constrain the effect of messages and model-generated actions.

## Decision

Use Hermes Agent as the conversational orchestration layer and Telegram as its primary mobile interface. Restrict the bot to an explicit sender allowlist, retain Tailscale and SSH as the direct administrative and recovery plane, and treat tool authorization as a separate boundary from Telegram identity.

## Alternatives considered

### Direct SSH for every operation

- Strong and flexible administrative interface
- Poor fit for quick mobile workflows
- Retained for maintenance and recovery, not as the primary conversational interface

### A custom public web dashboard

- Purpose-built user experience
- Requires hosting, authentication, patching, and a new inbound application surface
- Not selected as the primary interface

### Home Assistant automations only

- Excellent for device-centric deterministic workflows
- Too narrow for host operations, research, files, and cross-service tasks
- Remains an execution target behind Hermes

## Consequences

- Routine homelab workflows are accessible through a familiar mobile interface.
- One agent can coordinate tools across multiple services and retain task context.
- Telegram account security and the bot token become part of the infrastructure perimeter.
- Prompt injection and excessive agency become first-class threats.
- The agent requires a dedicated least-privilege identity, explicit tool policies, confirmation gates, and auditable execution.
- Tailscale and SSH remain necessary as an independent recovery path if Hermes or Telegram is unavailable.
