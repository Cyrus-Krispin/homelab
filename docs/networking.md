# Networking

## Topology

The server has four relevant logical interfaces:

| Interface class | Function |
| --- | --- |
| Wi-Fi | Default LAN route through the home router |
| Docker bridge | Container networking; currently unused by the host-networked Home Assistant container |
| Tailscale | Encrypted private overlay for authenticated devices |
| Cloudflare WARP | Outbound tunnel and resolver path |

The Tailscale overlay connects the Linux server to authorized personal clients without publishing their identities, addresses, or roles in this repository.

Hermes introduces a separate application-layer path: the mobile client communicates with Telegram, and the local gateway maintains outbound connectivity to Telegram and configured model providers. This does not require a documented public inbound port on the home router, but it makes external account security and bot-token protection part of the homelab perimeter.

## DNS

DNS resolution is coordinated by systemd-resolved. The LAN router supplies local-network DNS, Tailscale supplies its overlay resolver, and WARP exposes a local resolver endpoint. Multiple resolver domains make troubleshooting order and split-DNS behavior an important operational concern.

## Service exposure

Administrative and application endpoints are grouped by intended audience rather than published with live bindings:

| Audience | Examples | Intended boundary |
| --- | --- | --- |
| Administration | SSH and host maintenance | Tailnet and restricted management path |
| Automation | Home Assistant and device integrations | Authorized LAN and tailnet clients |
| Media | Jellyfin and supporting tools | Authorized household clients |
| Agent control | Hermes gateway | Outbound Telegram session plus local policy layer |

Exact ports, interface bindings, firewall rules, and upstream router settings are intentionally private.

## Trust-boundary observations

- Tailscale provides identity-aware private connectivity, but it does not automatically restrict services reached directly over the LAN.
- Telegram sender authorization protects the Hermes message boundary, while local tool authorization must independently constrain what an accepted message can cause.
- Host networking gives Home Assistant broad LAN visibility, which is useful for discovery but increases the importance of host controls.
- Temporary tooling should bind to the narrowest practical interface and be removed when no longer needed.
- Router forwarding and automatic mapping settings belong in the private operational review, not the public portfolio.

## Target network policy

The target state is:

1. Default-deny unsolicited inbound traffic at the host.
2. Permit SSH administration from the tailnet and, if needed, a restricted LAN management range.
3. Permit Home Assistant and media endpoints only from intended LAN/tailnet clients.
4. Bind management interfaces to the smallest practical address scope.
5. Confirm router port forwards and UPnP mappings are absent unless explicitly required.
6. Record Tailscale ACL intent without publishing device identities or addresses.
