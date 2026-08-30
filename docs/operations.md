# Operations

## Current operating model

The homelab has demonstrated long-running stability on a single Ubuntu host. Core infrastructure services start through systemd, while several media applications run as user-owned processes. Administration is performed over SSH, with Tailscale available as the private overlay.

## Operational signals

The private operating view tracks uptime, time synchronization, package maintenance, reboot state, filesystem utilization, journal growth, backup freshness, container health, and Hermes gateway availability. The public repository intentionally omits live counts and remediation status.

## Service ownership

| Layer | Current supervisor |
| --- | --- |
| SSH, Docker, containerd, Tailscale, WARP | systemd system services |
| Hermes Agent | systemd user service |
| Home Assistant | Docker |
| Jellyfin and supporting media tools | User-level process supervision |
| Package maintenance | unattended-upgrades and systemd timers |
| Logs | journald and rsyslog |

## Backup model

Application-local backups protect against some configuration mistakes; they do not protect against disk failure, theft, ransomware, or full-host loss. The recovery design therefore separates local recovery points from encrypted off-host copies.

A complete backup design should classify:

- Home Assistant configuration and database
- Hermes configuration, non-secret policy, and restorable state
- Jellyfin configuration, metadata, and rebuildable cache
- Supporting media-tool configuration and metadata
- Infrastructure definitions and system service units
- Irreplaceable media versus reproducible content

The target should follow a 3-2-1 pattern where practical: three copies, two storage types, and one copy off-site. Restore verification is part of the backup, not a separate optional task.

## Maintenance runbook

### Monthly

1. Review disk, memory, temperature, and journal growth.
2. Review failed systemd units, Hermes gateway health, and container restart counts.
3. Check available operating-system and application updates.
4. Review Tailscale devices and remove stale access.
5. Confirm the most recent backup and test a small restore.

### Before a reboot

1. Record currently running applications and container state.
2. Confirm a recent configuration backup.
3. Apply updates and review package errors.
4. Keep local-console access available.

### After a reboot

1. Verify SSH and Tailscale connectivity.
2. Verify Hermes responds only to the intended Telegram identity.
3. Verify Docker and Home Assistant.
4. Verify Jellyfin and supporting media services.
5. Check failed units, disk mounts, DNS, and system time.
6. Confirm application endpoints from an intended client.

## Observability target

The next iteration should add lightweight host and service monitoring with:

- CPU, memory, swap, temperature, disk use, and disk health
- Service availability and response latency
- Hermes gateway availability, tool failures, approval outcomes, and provider latency
- Container health and restart count
- Backup age and last restore-test result
- Pending updates and reboot-required state
- Alerts delivered outside the homelab failure domain
