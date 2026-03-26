# Cluster Overview

## Objective

This document describes the initial system architecture for TITAN, a small-scale distributed testbed designed to study system behavior under infrastructure-level failure conditions.

The goal is not to build a production cluster, but to create a controlled environment where failure scenarios can be introduced and observed with full visibility.

---

## System Topology

TITAN is designed as a three-node cluster running on a single bare-metal host.

| Node | Role | Description |
|------|------|------------|
| titan-cp-01 | Control Plane | Kubernetes API server, scheduler, controller manager |
| titan-worker-01 | Worker | Runs application workloads |
| titan-worker-02 | Worker | Runs application workloads |

---

## Host Environment

- **Hardware:** Single bare-metal machine (64GB RAM, multi-core CPU, 1TB storage)
- **Operating System:** Ubuntu (LTS)
- **Virtualization:** KVM / libvirt

Each node runs as a virtual machine to simulate a distributed environment while maintaining centralized control.

---

## Networking Model

- Nodes communicate over a virtual network managed by libvirt
- Each node has a static internal IP
- All inter-node communication occurs over this virtual network

Planned failure scenarios:
- Network partition between worker nodes
- Loss of connectivity to control plane
- Partial packet loss / latency injection (future phase)

---

## Orchestration Layer

- **Platform:** Kubernetes
- **Topology:** Single control plane (non-HA)
- **Reasoning:**  
  High availability is intentionally not configured at this stage.  
  The goal is to observe how system behavior degrades under control plane instability.

---

## Observability (Planned)

The system is being instrumented with:

- Prometheus (metrics collection)
- Grafana (visualization)

Target signals:
- Node health and availability
- Pod scheduling behavior
- Resource utilization (CPU, memory)
- Recovery timelines after failure events

---

## Design Constraints

The following constraints are intentional:

- No managed cloud services  
- No external orchestration layers  
- Minimal node count (3 nodes)  

These constraints ensure:
- Full control over failure injection  
- Clear attribution of system behavior  
- Reduced noise in observation  

---

## Future Extensions

- Addition of edge nodes (e.g., Raspberry Pi) for heterogeneous environments  
- Integration of GPU-backed nodes for ML workload testing  
- Expansion to multi-host deployment  

---

## Status

- VM topology defined  
- Base environment provisioning in progress  
- Kubernetes cluster bootstrap in progress  

This document will be updated as the system moves from design to execution.
