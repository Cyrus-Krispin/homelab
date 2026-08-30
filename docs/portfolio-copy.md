# Portfolio copy

## Project card

**Homelab — Private infrastructure on repurposed hardware**

Designed and operated a compact Ubuntu homelab centered on a Telegram-controlled Hermes Agent. Combined agentic orchestration, Docker, systemd, Tailscale, Home Assistant, and Linux operations on repurposed hardware, then documented the architecture and developed a risk-prioritized hardening roadmap.

Suggested tags: `Linux`, `Docker`, `Tailscale`, `Home Assistant`, `Networking`, `Security`, `Self-hosting`

## Case-study introduction

I built this homelab to turn an unused laptop into a practical, conversational infrastructure environment. Hermes Agent acts as the control plane: I send requests through an allowlisted Telegram bot, and the gateway coordinates approved tools, local services, and Home Assistant. Tailscale provides private administrative access, while Ubuntu, Docker, and systemd provide the operating foundation.

The first version grew organically. I documented the live system through a read-only SSH inventory, separated observed behavior from assumptions, and converted the findings into an explicit architecture and security roadmap. That process identified the next engineering priorities: key-only administration, a default-deny firewall, declarative service definitions, off-host backups, and external monitoring.

## Resume-style bullets

- Designed and operated an Ubuntu homelab supporting automation and media workloads with Docker, systemd, Tailscale, and Cloudflare WARP.
- Deployed a persistent Hermes Agent gateway to control homelab workflows through a single-user Telegram interface and local tool integrations.
- Converted an organically grown server into a documented architecture with service, network, trust-boundary, and recovery models.
- Threat-modeled an agentic control plane and prioritized least-privilege identities, tool authorization, confirmation gates, auditability, and secret isolation.
- Sustained more than 13 weeks of continuous availability on repurposed consumer hardware while identifying the platform's single-host resilience trade-offs.

## Interview talking points

- Why Tailscale was preferable to publishing administrative services directly.
- Why Telegram works well as a mobile control surface but cannot be the only authorization boundary.
- How to constrain an AI agent that can invoke local tools without removing its usefulness.
- Why Home Assistant benefits from host networking and what security trade-off that creates.
- How mixed native/container deployment affects reproducibility.
- Why a backup is not complete until restoration is tested.
- How to enable firewall and SSH hardening without locking out remote administration.
- How documenting existing infrastructure revealed more value than immediately adding another service.

## Recommended homepage layout

1. One-sentence project outcome
2. Sanitized architecture diagram
3. Technology stack
4. Three engineering decisions or trade-offs
5. Security and reliability improvements
6. Link to the GitHub repository
