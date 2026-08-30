# Hardware and platform

## Host platform

| Component | Observed configuration |
| --- | --- |
| System | Dell Inspiron 14 5410 2-in-1 |
| Chassis | Convertible laptop |
| CPU | 11th-generation Intel Core i7-1165G7 |
| Topology | 4 physical cores, 8 threads |
| Memory | 16 GB installed |
| Disk | 512 GB SK hynix NVMe SSD |
| Root filesystem | ext4 |
| Boot | UEFI system partition |
| Network uplink | Wi-Fi |

## Operating system

- Ubuntu 22.04.5 LTS
- Linux 5.15 LTS kernel series
- x86-64 architecture
- systemd service manager
- systemd-networkd and systemd-resolved
- journald and rsyslog logging

The hardware is a good fit for a compact learning lab: the mobile CPU provides hardware-efficient compute, the integrated battery acts as a short-duration power buffer, and the form factor minimizes incremental equipment cost.

## Capacity snapshot

At discovery time:

- Approximately half of the root filesystem was in use.
- Normal workloads consumed less than one-third of physical memory.
- Swap was actively used, despite substantial available cached memory.

These measurements are a point-in-time snapshot rather than performance benchmarks. The next observability phase should record CPU temperature, memory pressure, disk health, disk latency, and application response time over a longer window.

## Platform trade-offs

| Choice | Benefit | Cost |
| --- | --- | --- |
| Repurposed laptop | Low cost, quiet, compact, integrated battery | Limited expansion and cooling |
| Single NVMe disk | Simple and fast | No disk redundancy |
| Wi-Fi uplink | Flexible placement | Less predictable than wired Ethernet |
| Ubuntu LTS | Stable package base and broad support | Current release requires planned upgrade before end of standard support |
| Single host | Low operational complexity | Shared failure domain for every service |
