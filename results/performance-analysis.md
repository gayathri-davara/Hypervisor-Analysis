# Hypervisor Performance Analysis

## 1. Objective

To compare the CPU performance of a Type-1 hypervisor and a Type-2 hypervisor using the same Sysbench CPU benchmark.

- **Type-1 Hypervisor:** Proxmox VE
- **Type-2 Hypervisor:** VMware Workstation
- **Guest Operating System:** Ubuntu 22.04
- **Benchmark Tool:** Sysbench 1.0.20
- **Benchmark Workload:** CPU benchmark with a prime number limit of 20,000

The experiment compares execution time, total events, events per second, and latency between the two virtualization environments.

---

## 2. Hypervisor Overview

### 2.1 Type-1 Hypervisor — Proxmox VE

Proxmox VE is a virtualization platform based on a Type-1, or bare-metal, hypervisor architecture.

In this experiment, Proxmox VE was used to run an Ubuntu 22.04 virtual machine. The VM was configured with 2 virtual CPUs and 2 GB of RAM.

### 2.2 Type-2 Hypervisor — VMware Workstation

VMware Workstation is a hosted virtualization platform that runs on top of a host operating system.

In this experiment, VMware Workstation was used to run an Ubuntu 22.04 virtual machine. The VM was configured with 2 virtual CPUs and 2 GB of RAM.

---

## 3. Experimental Configuration

The virtual machines were configured with comparable CPU and memory resources so that their CPU performance could be compared using the same benchmark workload.

| Parameter | Proxmox VE | VMware Workstation |
|---|---|---|
| Hypervisor Type | Type-1 | Type-2 |
| Guest OS | Ubuntu 22.04 | Ubuntu 22.04 |
| CPU | 2 vCPU | 2 vCPU |
| CPU Configuration | 1 Socket × 2 Cores | 1 Processor × 2 Cores |
| RAM | 2 GB | 2 GB |
| Disk | 20 GB | 30 GB |
| Network | VirtIO / vmbr0 | NAT |
| Sysbench Version | 1.0.20 | 1.0.20 |
| Number of Threads | 1 | 1 |
| Prime Number Limit | 20,000 | 20,000 |

---

## 4. VMware Configuration Deviation

The laboratory configuration specified a **20 GB virtual disk**.

The VMware Workstation virtual machine used during the experiment had a **30 GB virtual disk**.

This deviation was documented rather than rebuilding the virtual machine.

Since the benchmark used in this experiment is focused on CPU computation, the additional disk capacity was not directly involved in the benchmark calculation.

The actual configuration has been retained in this report for transparency.

---

## 5. Experimental Procedure

The experiment was performed on both virtualization environments using the same CPU benchmark.

### Step 1 — Virtual Machine Setup

An Ubuntu 22.04 virtual machine was configured on each hypervisor.

### Step 2 — Resource Configuration

The virtual machines were configured with:

- 2 vCPUs
- 2 GB RAM
- Virtual disk
- Ubuntu 22.04 guest operating system

### Step 3 — Sysbench

Sysbench 1.0.20 was used for CPU performance testing.

### Step 4 — Benchmark Execution

The following benchmark command was executed on both virtual machines:

```bash
sysbench cpu --cpu-max-prime=20000 run
