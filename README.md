# TITAN
### A Bare-Metal Distributed Systems Research Testbed

TITAN is a distributed systems testbed under active development, designed to study fault tolerance semantics and distributed workload behavior under controlled infrastructure-level failure conditions.

The system is being built on commodity hardware to preserve full observability across every layer of the stack — from the hypervisor to the scheduler. The goal is to create an environment where infrastructure-induced failures can be introduced deliberately and analyzed with minimal abstraction.

The platform is intentionally minimal: three nodes, no managed cloud services, and no hidden control planes. This constraint is a design choice to ensure that system behavior remains fully traceable during failure scenarios.

---

## Architecture

| Node | Role | Hypervisor |
|------|------|------------|
| titan-cp-01 | Kubernetes Control Plane | KVM / libvirt |
| titan-worker-01 | Worker Node | KVM / libvirt |
| titan-worker-02 | Worker Node | KVM / libvirt |

**Host:** Single bare-metal machine (64GB RAM, 4GHz+, 1TB) running Ubuntu, with KVM/libvirt managing all nodes as virtual machines.

**Orchestration:** Kubernetes (single control plane — high availability is treated as an outcome of system design, not a starting assumption).

**Planned extensions:**
- Raspberry Pi worker nodes for edge failure simulation  
- Cloud-based GPU nodes for AI workload experimentation  

---

## Research Objective

The central question guiding TITAN is:

> *How do correctness guarantees and execution semantics in distributed task-parallel systems behave when the failure domain is the underlying infrastructure, rather than the application layer?*

Most fault tolerance research assumes a stable execution substrate and models failures at the task or message level. TITAN approaches the problem from the infrastructure layer, introducing failures such as node loss, network partition, and resource contention, and observing how higher-level system behavior responds.

The focus is on:
- Execution behavior under partial failure  
- Recovery characteristics and failure propagation  
- Interaction between scheduling decisions and infrastructure instability  

This direction aligns with ongoing research areas in distributed data processing, asynchronous execution, and system-level fault tolerance.

---

## Methodology

TITAN is being structured around a phase-gated experimental approach. Each phase introduces a specific class of failure, documents system behavior, and progresses based on analysis of observed outcomes.

**Failure classes under investigation:**
- Node failure (graceful and ungraceful)
- Network partition
- Resource contention (CPU, memory, I/O)
- Control plane degradation

Each experiment is intended to produce:
- A defined procedure (runbook)
- Observed system behavior
- A structured incident-style analysis

---

## Artifact Trail

| ID | Type | Description | Status |
|----|------|------------|--------|
| Phase(-1)-RB-001 | Runbook | Cluster bootstrap and baseline validation | In progress |
| INC-001 | Incident Report | Initial fault injection scenario | Pending |

Artifacts are published incrementally as the system evolves. The repository serves as a record of both system construction and experimental observation.

---

## Repository Structure
