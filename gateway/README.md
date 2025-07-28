# Gateway Machine

This device serves as the central gateway, handling NAT, DNS, and DHCP for the internal network (`.brian.lan` domain). It is responsible for routing all traffic from connected devices.

## Machine Specs: Raspberry Pi 3

* **Model**: Raspberry Pi 3
* **Architecture**: 64-bit (`aarch64`, `ARMv8`)
* **CPU**: Quad-core ARM Cortex-A53 @ 1.2GHz
* **RAM**: 1 GB
* **Storage**: 32 GB microSD
    - /boot: 512 MiB
    - /: ~29 GB
* **Kernel Features**: Supports `32-bit` and `64-bit` modes
* **CPU Flags**: `fp`, `asimd`, `evtstrm`, `crc32`, `cpuid`
* **Caches**:
    - L1d: 128 KiB × 4
    - L1i: 128 KiB × 4
    - L2: 512 KiB shared

## Operating System

* **Distro**: Ubuntu Server
* **Version**: 22.04 LTS (64-bit, ARM)
* **Kernel**: 6.14.0 (Raspberry Pi optimized build)
* **Package Manager**: `apt`
* **Installed Services**:
    - `dnsmasq` – Lightweight DNS and DHCP server
    - `iptables` – NAT and packet forwarding
    - `docker` – For isolated service deployment (optional)

## Gateway Configuration

* **Hostname**: `brian-pi-3`
* **Static IP**: `192.168.100.1`
* **Domain**: All connected devices resolve via the `.brian.lan` DNS suffix
* **DHCP & DNS**: Handled via dnsmasq (authoritative DHCP + local DNS)
* **Routing**: Acts as a NAT gateway, forwarding traffic from LAN (`eth0`) to WLAN (`wlan0`)
* **Firewall**: iptables NAT rules isolate and forward outbound traffic

## Reverse Proxy (Traefik)

* **Entrypoint**: Traefik listens on LAN interfaces and routes all service traffic
* **TLS/SSL**: Supports HTTPS (local or external certs)
* **Routing Strategy**:
    - Internal apps mapped to subdomains like `jellyfin.brian.lan`, `media.brian.lan`
* TODO: **Cloudflare Tunnel**: Can securely expose internal services over the internet without port forwarding

