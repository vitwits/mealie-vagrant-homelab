# Homelab Virtual Machines Setup

This repository is a part of my MEALIE_HOMELAB project, that is aimed to practice and replicate an infrastructure and practices used in devops in real life projects, but considering limitations of a home lab setup. 

This configuration was created for a **personal homelab setup** consisting of **4 virtual machines distributed across 2 physical servers**. Each physical server hosts 2 virtual machines, which can be chosen according to your needs.  

The setup has been **tested on Debian 12 (Bookworm)**. Resources (CPU, memory, disk) for each VM can be adjusted depending on your server capacity.  

BRIDGE_IFACE variable should be set accrdint to host network interface of your machine, so we can get an IP in your local network.


```bash
ip link show
```
e.g. BRIDGE_IFACE = "enp1s0"

Also rename the secrets example file and populate it with your public SSH key

```bash
mv secrets.yml.example secrets.yml
```

> **Requirements:**  
> - Vagrant  
> - libvirt (QEMU/KVM)  

**Note:** Each virtual machine requires **a static IP address and a hostname** to be configured in each `Vagrantfile`.

---

# Setting up Vagrant with QEMU/KVM on Linux

This guide will show how to prepare a Linux server to run **Vagrant** with **QEMU/KVM**, so you can use `vagrant up` to start VMs.

## 1️⃣ Install QEMU/KVM and Dependencies

```bash
sudo apt update
sudo apt install -y qemu-system libvirt-daemon-system libvirt-clients bridge-utils virt-manager virtinst cpu-checker vagrant
```

Verify installation:

```bash
vagrant --version
```

Check if KVM is available:

```bash
sudo kvm-ok
# or
virsh list --all
```

---

## 2️⃣ Enable libvirt Service and Add Your User to libvirt and kvm Groups

```bash
sudo systemctl enable --now libvirtd
sudo usermod -aG libvirt $USER
```

Log out and log back in for the group changes to apply.

---

## 5️⃣ Vagrant Commands

Use only the following commands in your Vagrant setup:

```bash
vagrant up
vagrant halt
vagrant suspend
vagrant reload
vagrant destroy
vagrant destroy -f
vagrant ssh
vagrant ssh-config
vagrant provision
vagrant status
vagrant global-status
vagrant box list
vagrant box add <box-name>
vagrant box remove <box-name>
```
