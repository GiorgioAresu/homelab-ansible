# :construction: homelab-ansible

Ansible repository for my homelab. I'm currently learning Ansible so this is a way to practice it. With time, more and more of my homelab config will land here.

To use this, you need to setup:

- Ansible Vault, save the key in `~/.ansible/vault_pass.txt`.  
- [bitwarden-cli (bw)](https://github.com/bitwarden/clients/tree/master/apps/cli) installed and logged in.

The playbook badges highlight compatibility with a device.

## :notebook: Notes

### Odroid HC4

![playbook: odroidhc4.yml](https://img.shields.io/badge/playbook-odroidhc4.yml-brightgreen?style=flat&logo=ansible) ![playbook: upgrade.yaml](https://img.shields.io/badge/playbook-upgrade.yaml-blue?style=flat&logo=ansible)

This device is used for offsite backup, and it's a bit delicate to make it work with ZFS reliably due to Armbian kernel trickery.

*TL;DR*: at the moment, flash [latest Jammy with 5.15.y](https://imola.armbian.com/archive/odroidhc4/archive/Armbian_22.02.1_Odroidhc4_jammy_edge_5.15.25.img.xz).

As a general guideline, you need to cross check 3 things:

- Kernel version included in the image you're downloading from [here](https://imola.armbian.com/archive/odroidhc4/archive/) (eg. 5.19.y).
- Packages in repos ([debian](https://packages.debian.org/search?searchon=names&keywords=zfsutils-linux)).
- Supported kernels by [OpenZFS version](https://github.com/openzfs/zfs/releases).

In Armbian, kernel versions are named by branch and not by version. It tends to be very old on *current* and very new on *edge*, but the issue with edge is that other packages might still be old.

Once installed, the trick is to install the correct headers and then freeze the firmware to avoid ZFS breaking on the first kernel update. This is taken care of by the playbook.
