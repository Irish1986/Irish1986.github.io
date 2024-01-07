---
layout: post
title: "Proxmox VE 8.1 Clustering"
author: irish1986
date: 2024-01-08 00:00:00 +0000
categories:
  - proxmox
  - tutorial
tags:
  - core system
  - clustering
  - proxmox
  - proxmox 8
  - setup
  - tutorial
---

This guide is a complete step by step guide on how to setup Proxmox Cluster.

## Network

### Realtek R8125B (Optional)

```bash
cd /tmp
wget <https://github.com/awesometic/realtek-r8125-dkms/releases/download/9.012.03-2/realtek-r8125-dkms_9.012.03-2_amd64.deb>
sudo dpkg -i realtek-r8125-dkms*.deb
sudo apt install --fix-broken

lsmod | grep -i r8169
lspci -k

sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y
```

### VLAN Enable Proxmox (Optional)

## Storage

### CEPH Storage

1. Wipe disk
    ceph-volume lvm zap /dev/nvme0n1 --destroy

## Clustering

1. Log in to the first Proxmox server, select Datacenter, then Cluster, and select Create Cluster.
2. Give the cluster a name, then select create. The cluster will then be created and you’ll be able to join it from other Proxmox instances.
3. We will create three total rules for UDP ports 5404, 5405, and TCP port 22. (optional)
4. On the device you just set up the cluster with (pve-test in my example), select Join Information under Cluster.
5. The join information will be displayed. You will need both, the Fingerprint and Join Information to join the cluster. Select Copy Information, then open your second Proxmox node.
6. On the second Proxmox node, select Datacenter, Cluster, and Join Cluster.
7. Create external quorum devices

pvecm create pve-cluster
pvecm status
pvecm join <ip-address-of-the-main-node>

### High Availability

1. Create HA Groups
2. Create Disable HA

### Create Pools

1. Create HA Groups
2. Create Disable HA
