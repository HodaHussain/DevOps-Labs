# Lab 10: Kubernetes Taints and Labels

## Objective
The objective of this lab is to apply a taint to a Kubernetes worker node, assign a label to the node, and verify how taints affect pod scheduling.

## Environment
- Kubernetes Playground (Killercoda)
- Kubernetes
- kubectl
- Container Runtime: containerd

## Tasks Performed

### 1. Apply a Taint to the Worker Node

```bash
kubectl taint nodes node01 workload=ivolveApp:NoSchedule
```

This taint prevents pods from being scheduled on `node01` unless they have a matching toleration.

### 2. Apply a Label to the Worker Node

```bash
kubectl label nodes node01 project=ivolve
```

The label identifies the node as part of the `ivolve` project.

### 3. Verify the Node Configuration

```bash
kubectl describe node node01
kubectl get nodes --show-labels
```

The output confirmed that the node had the label `project=ivolve` and the taint `workload=ivolveApp:NoSchedule`.

### 4. Test Pod Scheduling

A test pod was created:

```bash
kubectl run taint-test --image=nginx
```

The pod was scheduled on `controlplane`, where scheduling was permitted.

A second pod was forced to target `node01`:

```bash
kubectl run taint-test-worker --image=nginx --overrides='{"apiVersion":"v1","spec":{"nodeSelector":{"kubernetes.io/hostname":"node01"}}}'
```

The second pod remained in the `Pending` state because the taint on `node01` prevented scheduling without a matching toleration.

## Results
- Successfully applied the taint
<img width="1732" height="916" alt="Screenshot 2026-10-26 212911" src="https://github.com/user-attachments/assets/3e023919-a707-4de8-8b82-a42fe20ce2e1" />
<img width="1790" height="950" alt="Screenshot 2026-10-26 212948" src="https://github.com/user-attachments/assets/52e44aaa-3600-4e04-aaed-23c36903f145" />
<img width="1868" height="867" alt="Screenshot 2026-10-26 212932" src="https://github.com/user-attachments/assets/7a4e59c4-5628-4543-91f1-4a6e439e6161" />
