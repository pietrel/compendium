# Virtual Machines

Virtual machines (VMs) rely on host hardware to establish connections with other devices and locations within a network.
This document outlines how VM networking functions and explains the default VM network configuration.

Virtual networking is built around the concept of a virtual network switch—a software-based construct running on the
host machine. VMs access the network via this virtual switch. Depending on its configuration, the virtual switch enables
VMs to connect to an existing virtual network managed by the hypervisor or use an alternative network connection method.

`libvirtd` is a popular virtualization daemon that provides a virtual network switch for VMs. It is used by hypervisors
like KVM and QEMU to manage VM networking. The `virsh` command-line tool can be used to interact with `libvirtd` and
manage VMs.

The default network interface for VMs is `vibr0`. This interface is created by `libvirtd` and acts as a bridge between
the VMs and the host network. VMs can communicate with each other and the host machine through this interface. By
default, all VMs are connected to the same virtual network, allowing them to communicate with each other without any
additional configuration.

