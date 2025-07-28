# NAS Machine

This device serves as the primary storage node in the network. All outbound traffic is routed through the Pi 3 gateway (`brian-pi-3`).

## Machine Specs: Raspberry Pi 5

Model: Raspberry Pi 5

* **Architecture**: `64-bit` (`aarch64`, `ARMv8`)
* **CPU**: Quad-core ARM Cortex-A76 @ 2.4GHz
* **RAM**: 8 GB
* **Storage**:
    * **OS Drive**: 120 GB microSD
        - /boot: 512 MiB
        - /: ~118.9 GB
    * **External Drive**: 1 TB HDD mounted at /mnt/storage
    * Additional drives will be attached for network storage
* **Kernel Features**: Supports `32-bit` and `64-bit` modes
* **Caches**:
    - L1d: 256 KiB × 4
    - L1i: 256 KiB × 4
    - L2: 2 MiB × 4
    - L3: 2 MiB shared

## Operating System

* **Distro**: Ubuntu Server
* **Version**: 25.04 (64-bit, ARM)
* **Kernel**: 6.14.0 (Raspberry Pi optimized build)
* **Package Manager**: `apt`
* **Installed Services**:
    - `docker` – For running self-hosted services
    - `nfs-kernel-server` – Exposes directories over NFS for other machines on the LAN

## Storage Node Configuration

* **Hostname**: `brian-pi-5`
* **Static IP**: `192.168.100.89` (assigned via DHCP from gateway)
* **Primary Role**: Network-attached storage (NAS) and media streaming
* **Network Access**: All outbound and inbound traffic routes through the gateway (`192.168.100.1`)
* **Mounted Storage**: External 1 TB HDD at `/mnt/storage`, with plans for additional drives
* **File Sharing**: Exposes storage via NFS for LAN-wide access

