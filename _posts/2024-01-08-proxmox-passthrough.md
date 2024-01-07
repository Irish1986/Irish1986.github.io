---
layout: post
title: "Proxmox VE 8.1 Device Passthrough"
author: irish1986
date: 2024-01-08 00:00:00 +0000
categories:
  - proxmox
  - tutorial
tags:
  - core system
  - gpu
  - proxmox
  - proxmox 8
  - setup
  - tutorial
---

This guide is a complete step by step configuration for devices passthrough under Proxmox.

## Device Passthrough (Optional)

### Intel iGPU (Optional)

```bash
nano /etc/default/grub
GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on"

update-grub

nano /etc/modules
vfio
vfio_iommu_type1
vfio_pci
vfio_virqfd
update-initramfs -u -k all

reboot
```

### nvidia GPU (Optional)

### AMD GPU (Optional)

### Google Coral TPU (Optional)

A very popular NVR solution that integrates well with Home Assistant is Frigate. It provides fantastic object and person detection from your camera streams. The Frigate project is a container, so it’s easy to deploy.

Special hardware can be used in order to improve the image detection and general performance.  A Google Coral Tensor Processing Unit (TPU) is a very common fairly affordable option.  This device is availabe for purchase in a few configuration sch as USB, PCI-E and m.2 (A+E Key) PCI-E.  Two of my Proxmox host have m.2 (A+E Key) Google Coral TPU installed so here how to enable this device passthrough.

First on the Proxmox host, we need to modify the configuration of the Proxmox host where the Coral TPU is installed.  Login to Proxmox and open a shell.

1. Modify the GRUB configuration by running the following command:

```bash
nano /etc/default/grub
GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on iommu=pt pcie_aspm=off initcall_blacklist=sysfb_init"
```

```bash
nano /etc/default/grub
update-grub
```

```bash
nano /etc/modules
vfio
vfio_iommu_type1
vfio_pci

kvmgt
xengt
vfio-mdev
```

```bash
update-initramfs -u -k all
```

```bash
nano /etc/modprobe.d/blacklist-apex.conf
blacklist gasket
blacklist apex
options vfio-pci ids=1ac1:089a
```

```bash
update-initramfs -u -k all
lsmod | grep apex
reboot
```

### PCI-E Device (Optional)

I don't have any other devices at the moment to passthrought from the host but soon I shall have a HBA adapter.  I am not certain if I'll run TrueNAS bare metal or under Proxmox.
