---
layout: post
title: "Proxmox VE 8.1 Advanced"
author: irish1986
date: 2024-01-06 00:00:00 +0000
categories:
  - proxmox
  - tutorial
tags:
  - core system
  - proxmox
  - proxmox 8
  - setup
  - tutorial
---

This guide is a complete step by step guide for Proxmox advance features.

## Proxmox Post-Install Configuration

### AMD/Intel Microcode Update (Optional)

AMD and Intel releases new microcode for their processors from time to time. This is different from BIOS firmware, as the microcode runs inside the processor. It can fix CPU bugs or make other changes, as needed. You can use the following tteck script to download the latest AMD/Intel microcode and install it. A full system reboot will be needed for the microcode to take effect.

```bash
bash -c "$(wget -qLO - https://github.com/tteck/Proxmox/raw/main/misc/microcode.sh)"
```

After the Proxmox host reboots you can run the following command to see if any microcode update is active. Not all CPUs need microcode updates, so you may well not see anything listed.

```bash
journalctl -k | grep -E "microcode" | head -n 1
```

### Optimize CPU Power (Optional)

## Storage

### Local vs Local-LVM

1. Navigate to "datacenter -> storage"
2. Delete the "local-lvm" storage
3. SSH into your server and run the follwing commands

```shell
lvremove /dev/pve/data
lvresize -l +100%FREE /dev/pve/root
resize2fs /dev/mapper/pve-root
```

### Wake On Lan

1. Create HA Groups
2. Create Disable HA

## Monitoring

### Metric Server

### Notifications (Optional)

### SMART Monitoring (Optional)
