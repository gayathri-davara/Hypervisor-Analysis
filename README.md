# Performance Analysis of Type-1 and Type-2 Hypervisors

[![Course](https://img.shields.io/badge/Course-Cloud%20Computing-blue.svg)](#)
[![Hypervisors](https://img.shields.io/badge/Hypervisors-Proxmox%20VE%20%7C%20VMware%20Workstation-orange.svg)](#)
[![Benchmark](https://img.shields.io/badge/Benchmark-Sysbench%20CPU%2020k%20Primes-green.svg)](#)
[![Status](https://img.shields.io/badge/Status-Completed-brightgreen.svg)](#)

---

## Executive Summary

This experiment evaluates the CPU performance of a **Type-1 hypervisor (Proxmox VE)** and a **Type-2 hypervisor (VMware Workstation)** using Ubuntu virtual machines and the Sysbench CPU benchmark.

Both environments were configured with **2 vCPU and 2 GB RAM** and tested using the same Sysbench workload:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

The benchmark results recorded during the experiment were:

| Metric | Proxmox VE | VMware Workstation |
|---|---:|---:|
| Total Execution Time | 10.0006 s | 10.0018 s |
| Total Events | 16,903 | 8,738 |
| Events per Second | 1,690.43 | 873.50 |
| Average Latency | 0.59 ms | 1.14 ms |

These results represent the specific hardware, software, virtual machine configurations, and experimental conditions used in this laboratory exercise.

---

## Table of Contents

1. [Objectives](#1-objectives)
2. [Hypervisor Architecture](#2-hypervisor-architecture)
3. [Virtual Machine Configuration](#3-virtual-machine-configuration)
4. [Experimental Procedure](#4-experimental-procedure)
5. [Benchmark Results](#5-benchmark-results)
6. [Performance Analysis](#6-performance-analysis)
7. [Screenshots](#7-screenshots)
8. [Conclusion](#8-conclusion)
9. [Repository Structure](#9-repository-structure)
10. [Reproduction](#10-reproduction)

---

## 1. Objectives

The objectives of this experiment are:

1. To understand Type-1 and Type-2 hypervisor architectures.
2. To configure Ubuntu virtual machines on both hypervisors.
3. To allocate comparable CPU and memory resources.
4. To execute a common CPU benchmark using Sysbench.
5. To collect execution time, total events, events per second, and latency.
6. To compare the measured CPU performance of both virtualization environments.

---

## 2. Hypervisor Architecture

### 2.1 Type-1 Hypervisor — Proxmox VE

Proxmox VE is a bare-metal virtualization platform based on Linux and KVM.

The general architecture used in this experiment can be represented as:

```text
+--------------------------------------+
|       Ubuntu Virtual Machine         |
+--------------------------------------+
|        Proxmox VE / KVM              |
+--------------------------------------+
|       Physical Host Hardware         |
+--------------------------------------+
```

The virtualization platform runs directly on the physical host rather than as an application inside a conventional desktop operating system.

---

### 2.2 Type-2 Hypervisor — VMware Workstation

VMware Workstation is a hosted hypervisor that runs on a host operating system.

The general architecture can be represented as:

```text
+--------------------------------------+
|       Ubuntu Virtual Machine         |
+--------------------------------------+
|       VMware Workstation             |
+--------------------------------------+
|       Host Operating System          |
+--------------------------------------+
|       Physical Host Hardware         |
+--------------------------------------+
```

The host operating system provides the underlying environment in which VMware Workstation operates.

---

## 3. Virtual Machine Configuration

The virtual machines were configured with comparable CPU and memory resources for the benchmark.

| Parameter | Proxmox VE | VMware Workstation |
|---|---|---|
| Hypervisor Type | Type-1 | Type-2 |
| Guest Operating System | Ubuntu 22.04 | Ubuntu 22.04 |
| CPU | 2 vCPU | 2 vCPU |
| CPU Configuration | 1 Socket × 2 Cores | 1 Processor × 2 Cores |
| RAM | 2 GB | 2 GB |
| Disk | 20 GB | 30 GB |
| Network | VirtIO / vmbr0 | NAT |
| Sysbench Version | 1.0.20 | 1.0.20 |

### Configuration Note

The VMware virtual machine used a **30 GB virtual disk** instead of the **20 GB disk** specified in the laboratory configuration.

This difference was documented rather than rebuilding the VM. The benchmark performed in this experiment is CPU-focused, so the additional virtual disk capacity was not directly involved in the CPU computation.

---

## 4. Experimental Procedure

### Step 1 — Virtual Machine Configuration

The virtual machines were configured with:

- Ubuntu 22.04
- 2 vCPU
- 2 GB RAM
- Virtual disk
- Network connectivity

The CPU topology was verified using:

```bash
lscpu
```

Memory allocation was verified using:

```bash
free -h
```

Disk allocation was checked using:

```bash
df -h
```

System activity was monitored using:

```bash
top
```

---

### Step 2 — Sysbench Installation

Sysbench was installed on the Ubuntu virtual machines using:

```bash
sudo apt update
sudo apt install sysbench -y
```

The installed version was verified using:

```bash
sysbench --version
```

The experiment used **Sysbench 1.0.20**.

---

### Step 3 — CPU Benchmark

The same benchmark command was executed on both virtual machines:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

The benchmark calculates prime numbers up to 20,000 and runs for approximately 10 seconds under the default configuration.

The following values were recorded:

- Total execution time
- Total events
- Events per second
- Average latency

---

## 5. Benchmark Results

### 5.1 Proxmox VE — Type-1

The verified Proxmox VE benchmark produced:

| Metric | Result |
|---|---:|
| Total Execution Time | **10.0006 s** |
| Total Events | **16,903** |
| Events per Second | **1,690.43** |
| Average Latency | **0.59 ms** |

---

### 5.2 VMware Workstation — Type-2

The verified VMware Workstation benchmark produced:

| Metric | Result |
|---|---:|
| Total Execution Time | **10.0018 s** |
| Total Events | **8,738** |
| Events per Second | **873.50** |
| Average Latency | **1.14 ms** |

---

### 5.3 Performance Comparison

| Performance Metric | Proxmox VE | VMware Workstation |
|---|---:|---:|
| Total Execution Time | 10.0006 s | 10.0018 s |
| Total Events | 16,903 | 8,738 |
| Events per Second | 1,690.43 | 873.50 |
| Average Latency | 0.59 ms | 1.14 ms |

The measured execution times were almost identical because the Sysbench CPU benchmark runs for approximately 10 seconds.

---

## 6. Performance Analysis

### 6.1 Total Execution Time

The measured execution times were:

- Proxmox VE: **10.0006 seconds**
- VMware Workstation: **10.0018 seconds**

The difference between the two measurements is very small.

The benchmark uses an approximately fixed 10-second execution period, so execution time alone is not sufficient to distinguish the CPU throughput of the two environments.

---

### 6.2 Total Events

The measured total events were:

- Proxmox VE: **16,903**
- VMware Workstation: **8,738**

The total event count represents the amount of benchmark work completed during the test period.

---

### 6.3 Events per Second

The measured throughput was:

- Proxmox VE: **1,690.43 events/sec**
- VMware Workstation: **873.50 events/sec**

For these particular experimental configurations, the Proxmox VE environment completed more Sysbench CPU events per second.

---

### 6.4 Average Latency

The measured average latency was:

- Proxmox VE: **0.59 ms**
- VMware Workstation: **1.14 ms**

The measured Proxmox VE environment therefore recorded a lower average latency in this particular benchmark run.

---

### 6.5 Interpretation

The measured results show a performance difference between the two tested virtualization environments.

However, these measurements should be interpreted within the context of the specific experimental setup.

Performance can be affected by factors such as:

- Physical CPU
- Host operating system
- Background processes
- Virtual CPU configuration
- Hypervisor configuration
- Memory configuration
- Virtualization technology
- System load during the benchmark

Therefore, these results should not be treated as a universal performance ranking of Proxmox VE and VMware Workstation.

---

## 7. Screenshots

All experimental evidence is organized inside the `screenshots` directory.

### 7.1 Type-1 — Proxmox VE

The Proxmox VE evidence includes:

1. Proxmox dashboard
2. VM configuration
3. VM running state
4. Ubuntu console
5. System configuration
6. Sysbench result
7. Resource monitoring

Location:

```text
screenshots/type1-proxmox/
```

Files:

```text
01-proxmox-dashboard.png
02-proxmox-vm-configuration.png
03-proxmox-vm-running.png
04-proxmox-ubuntu-console.png
05-proxmox-system-configuration.png
06-proxmox-sysbench-result.png
07-proxmox-resource-monitoring.png
```

---

### 7.2 Type-2 — VMware Workstation

The VMware Workstation evidence includes:

1. VM configuration
2. VM running state
3. System configuration
4. Sysbench result

Location:

```text
screenshots/type2-vmware/
```

Files:

```text
01-vmware-vm-configuration.png
02-vmware-vm-running.png
03-vmware-system-configuration.png
04-vmware-sysbench-result.png
```

---

### 7.3 Performance Comparison

The final comparison screenshot is stored in:

```text
screenshots/comparison/
```

File:

```text
01-hypervisor-performance-comparison.png
```

---

## 8. Conclusion

This experiment provided a practical comparison of Type-1 and Type-2 virtualization using a common CPU benchmarking workload.

Under the tested configurations, the recorded Sysbench results were:

### Proxmox VE

- **1,690.43 events/sec**
- **0.59 ms average latency**

### VMware Workstation

- **873.50 events/sec**
- **1.14 ms average latency**

The Proxmox VE environment recorded higher measured CPU throughput and lower measured average latency in this particular experiment.

The experiment demonstrates that virtualization architecture and configuration can affect measured performance. However, the results are specific to the hardware, software versions, VM configurations, and system conditions used during the experiment.

---

## 9. Repository Structure

```text
Experiment-01-Hypervisor-Analysis/
│
├── README.md
│
├── screenshots/
│   │
│   ├── comparison/
│   │   └── 01-hypervisor-performance-comparison.png
│   │
│   ├── type1-proxmox/
│   │   ├── 01-proxmox-dashboard.png
│   │   ├── 02-proxmox-vm-configuration.png
│   │   ├── 03-proxmox-vm-running.png
│   │   ├── 04-proxmox-ubuntu-console.png
│   │   ├── 05-proxmox-system-configuration.png
│   │   ├── 06-proxmox-sysbench-result.png
│   │   └── 07-proxmox-resource-monitoring.png
│   │
│   └── type2-vmware/
│       ├── 01-vmware-vm-configuration.png
│       ├── 02-vmware-vm-running.png
│       ├── 03-vmware-system-configuration.png
│       └── 04-vmware-sysbench-result.png
│
└── results/
    └── performance-analysis.md
```

---

## 10. Reproduction

To reproduce the CPU benchmark, install Sysbench inside each Ubuntu virtual machine:

```bash
sudo apt update
sudo apt install sysbench -y
```

Verify the installed version:

```bash
sysbench --version
```

Run the benchmark:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

Record the following values from the output:

- Total time
- Total events
- Events per second
- Average latency

The same benchmark command should be used in both virtualization environments for comparison.

---

## Important Experimental Note

An additional test using a lower prime limit (`--cpu-max-prime=2000`) was performed during the setup process. Those results are **not included** in the final analysis because the laboratory benchmark specification uses:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

Only the results from the specified **20,000-prime benchmark** are reported above.

---

*Cloud Computing Laboratory — Experiment 01*
