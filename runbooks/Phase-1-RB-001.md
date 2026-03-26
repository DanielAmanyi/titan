# Phase 1 Runbook — Node Failure Simulation

## Objective
Simulate worker node failure and observe system behavior.

## Environment
- Cluster: TITAN (3 nodes)
- Control Plane: titan-cp-01
- Target Node: titan-worker-01

## Procedure

1. Confirm cluster state
Command:
kubectl get nodes

2. Confirm workload placement
Command:
kubectl get pods -o wide

3. Simulate node failure
Command:
virsh destroy titan-worker-01

4. Observe node status
Command:
kubectl get nodes -w

5. Observe workload behavior
Command:
kubectl get pods -o wide -w

## Expected Behavior
- Node transitions from Ready to NotReady
- Pods on titan-worker-01 enter Unknown or Terminating
- Pods are rescheduled to titan-worker-02

## Post-conditions

Restore node:
virsh start titan-worker-01

Verify recovery:
kubectl get nodes
kubectl get pods -o wide

## Notes
Initial protocol draft — to be refined during execution.
