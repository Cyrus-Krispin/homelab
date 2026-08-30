# Improvement roadmap

The roadmap is ordered to reduce risk before expanding the platform. It describes target engineering work; live completion status is maintained privately.

## Phase 1 — Recoverable access

- Rotate administrative credentials on a defined schedule.
- Verify dedicated SSH-key access from a second session.
- Document local-console recovery.
- Store an encrypted recovery copy of the SSH public-key setup instructions.

**Acceptance:** key-based access works, credential rotation is verified, and a local recovery path is documented privately.

## Phase 2 — Host security baseline

- Define and test a default-deny host policy with explicit LAN and tailnet allowances.
- Enforce key-only SSH with minimal optional features.
- Disable direct root SSH login.
- Review Tailscale access and remove stale devices.
- Verify upstream router exposure privately.

**Acceptance:** only intended clients can reach administration and application endpoints; key-only SSH survives a reboot.

## Phase 3 — Agent control-plane hardening

- Use a dedicated Hermes service identity without unnecessary administration groups.
- Record an explicit allowlist of required tools, paths, network destinations, and Home Assistant actions.
- Require confirmation for shell, file mutation, scheduling, and other consequential operations.
- Apply systemd protections such as `NoNewPrivileges`, filesystem restrictions, private temporary storage, and a constrained system-call/address-family policy where compatible.
- Deny or explicitly review unauthorized Telegram messages.
- Protect agent state, redact logs, define bot/API token rotation, and bound request consumption.
- Link approved Telegram requests to tool executions without storing secrets.

**Acceptance:** Hermes retains its intended Telegram and automation flows while compromise of the agent process cannot directly administer the host.

## Phase 4 — Reproducible services

- Capture the Home Assistant container in a sanitized Compose definition.
- Pin deployable versions and document update procedures.
- Create systemd units or containers for Jellyfin and supporting media tools.
- Remove temporary services when they are not required.
- Document data paths and dependencies without committing secrets.

**Acceptance:** every persistent workload starts automatically, has a health check, and can be rebuilt from documented definitions plus restored data.

## Phase 5 — Backup and recovery

- Use an encrypted off-host backup target.
- Back up application configuration and irreplaceable data.
- Add retention and failure alerts.
- Perform and document recovery drills.

**Acceptance:** a clean host can recover critical services from documented steps and verified backups.

## Phase 6 — Observability and lifecycle

- Add host and service metrics.
- Add external availability and backup-age alerts.
- Maintain a predictable update and reboot cadence.
- Plan Ubuntu LTS lifecycle upgrades.
- Evaluate wired Ethernet and storage-health monitoring.

**Acceptance:** failures, capacity pressure, stale backups, and pending maintenance are visible before users discover them.

## Phase 7 — Portfolio integration

- Review every tracked file using the redaction policy.
- Maintain a polished architecture image for GitHub and the homepage.
- Publish only sanitized architecture and target-state security material.
- Add the project card and case-study summary to the personal homepage.

**Acceptance:** the portfolio demonstrates architectural reasoning and operational maturity without exposing actionable infrastructure details.
