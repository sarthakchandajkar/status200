---
title: Virtual Machines
aliases:
  - Virtual Machines
draft: false
tags:
  - AZ-104
  - Cloud
author:
  - Sarthak Chandajkar
---
**Virtual Machines (VMs)** are software-based emulations of physical computers, enabling multiple operating systems to run on a single physical host. They provide isolated environments for running applications, testing software, or deploying [[Machine Learning]] workloads, making them essential in cloud computing, development, and system administration. This note explores VM architecture, use cases, and their role in [[Deep Learning]], with backlinks to related concepts.

## Definition

A VM is a virtualized computing environment that mimics a physical computer, including its CPU, memory, storage, and network interfaces. It runs an operating system and applications in isolation from the host system, managed by a **hypervisor** (e.g., VMware, VirtualBox, KVM).

### Key Components

- **Guest OS**: The operating system running inside the VM (e.g., Ubuntu, Windows).
- **Hypervisor**: Software that creates and manages VMs, allocating resources between the host and guests.
    - **Type 1 (Bare-Metal)**: Runs directly on hardware (e.g., VMware ESXi, Hyper-V).
    - **Type 2 (Hosted)**: Runs on top of a host OS (e.g., VirtualBox, VMware Workstation).
- **Virtual Hardware**: Emulated CPU, RAM, disk, and network interfaces assigned to the VM.

> [!NOTE] Intuition  
> Think of a VM as a computer within a computer, like a self-contained apartment in a larger building, with its own resources but sharing the host’s infrastructure.

## How VMs Work

The hypervisor abstracts physical hardware, creating virtualized resources for each VM:

1. **Resource Allocation**: The hypervisor assigns CPU cores, memory, and storage to VMs.
2. **Isolation**: Each VM operates independently, ensuring crashes or security issues in one don’t affect others.
3. **Execution**: The guest OS runs as if on physical hardware, interacting with virtualized devices.

VMs use virtualization technologies like Intel VT-x or AMD-V for efficient CPU performance and can leverage GPU passthrough for [[Deep Learning]] tasks.

### Real-World Example

In a cloud provider like AWS, an EC2 instance (a VM) runs a [[Neural Network]] training job on Ubuntu with [[TensorFlow]]. The hypervisor (AWS Nitro) isolates the instance, ensuring secure, scalable computation.

## Use Cases

1. **Development and Testing**:
    - Create isolated environments to test software across different OS versions.
    - Example: Testing a web app on Windows and Linux VMs without physical hardware.
2. **Cloud Computing**:
    - VMs power cloud services like AWS EC2, Azure VMs, or Google Compute Engine for scalable workloads.
    - Example: Deploying a [[Convolutional Neural Network]] on a cloud VM for image recognition.
3. **Server Consolidation**:
    - Run multiple VMs on a single server to optimize resource usage.
    - Example: Hosting web, database, and [[Machine Learning]] servers on one physical machine.
4. **Machine Learning Workloads**:
    - VMs provide reproducible environments for training models like [[BERT]] or [[Faster R-CNN]].
    - Example: A VM with a GPU runs [[PyTorch]] to train a model on the CIFAR-10 dataset.

### Real-World Example

In a data science team, VMs are used to create identical environments for training [[Transformers]] models. Each team member’s VM runs [[TensorFlow]] with pre-installed dependencies, ensuring consistent results across experiments.

## Advantages

- **Isolation**: VMs prevent interference between applications or users.
- **Flexibility**: Run multiple OS types (e.g., Linux, Windows) on one host.
- **Scalability**: Easily replicate or scale VMs in cloud environments.
- **Portability**: VMs can be exported as images and deployed elsewhere.

## Challenges

1. **Resource Overhead**: VMs require significant CPU, memory, and storage compared to containers (e.g., Docker).
    - **Solution**: Use lightweight containers for simple apps or optimize VM resource allocation.
2. **Performance**: Virtualization introduces latency compared to bare-metal execution.
    - **Solution**: Use Type 1 hypervisors or GPU passthrough for [[Deep Learning]] tasks.
3. **Management Complexity**: Managing multiple VMs requires robust tools.
    - **Solution**: Use orchestration platforms like Kubernetes or VMware vSphere.

> [!TIP] Practical Tip  
> For [[Machine Learning]] workloads, configure VMs with GPU support and pre-install frameworks like [[TensorFlow]] or [[PyTorch]]. Use cloud VMs with auto-scaling to handle varying compute demands.

## Implementation Example

Below is a Bash script to create a VM using **QEMU/KVM** on a Linux host for a [[Machine Learning]] task:

```bash
#!/bin/bash
# Create a VM with Ubuntu 20.04
qemu-img create -f qcow2 ubuntu-vm.qcow2 20G
qemu-system-x86_64 \
  -m 4G \
  -cpu host \
  -enable-kvm \
  -hda ubuntu-vm.qcow2 \
  -cdrom ubuntu-20.04.iso \
  -boot d \
  -net nic -net user \
  -vga virtio

# After setup, install TensorFlow inside the VM
# sudo apt update && sudo apt install python3-pip
# pip install tensorflow
```

This script creates a VM with 4GB RAM and a 20GB disk, boots from an Ubuntu ISO, and sets up a network. Post-setup, [[TensorFlow]] can be installed for training [[Neural Networks]].

## Comparison with Containers

- **VMs vs. Containers**:
    - VMs emulate full systems (OS + apps), providing strong isolation but higher overhead.
    - Containers (e.g., Docker) share the host OS, offering lightweight deployment but less isolation.
    - **Example**: Use VMs for secure, multi-OS environments (e.g., Windows for testing, Linux for [[BERT]] training); use containers for microservices.

## Applications

- **Machine Learning**: VMs host training environments for [[Convolutional Neural Networks]] or [[Transformers]] with GPU support.
- **Cloud Services**: Power cloud instances for scalable [[Deep Learning]] tasks.
- **Development**: Create sandboxes for testing [[Python]] scripts or [[PyTorch]] models.
- **Security**: Run untrusted applications in isolated VMs to prevent system compromise.

### Real-World Example

In a research lab, a VM on Google Cloud with an NVIDIA GPU trains a [[Faster R-CNN]] model for object detection on medical images, using [[TensorFlow]] and an [[Adam Optimizer]] to minimize the [[Objective Function]], ensuring reproducible results across experiments.


