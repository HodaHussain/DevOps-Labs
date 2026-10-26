# Lab 11: Namespace Management and Resource Quota Enforcement

## Objective
Create a Kubernetes namespace named `ivolve` to isolate application resources and enforce a limit of three Pods using a ResourceQuota.

## Environment
- Kubernetes Playground
- Namespace: `ivolve`
- ResourceQuota: `ivolve-quota`
- Maximum Pods: `3`

## Step 1: Create the Namespace

```bash
kubectl create namespace ivolve
```

Verify:

```bash
kubectl get namespaces
```

Expected result: The `ivolve` namespace is listed with status `Active`.

## Step 2: Create the ResourceQuota

Kubernetes resource names must use lowercase letters. Therefore, `ivolve-quota` is used instead of the requested mixed-case name `ivolveQuota`.

```bash
kubectl create quota ivolve-quota --hard=pods=3 -n ivolve
```

Verify:

```bash
kubectl describe resourcequota ivolve-quota -n ivolve
```

Expected result:

```text
Resource    Used  Hard
--------    ----  ----
pods        0     3
```

## Step 3: Create Three Pods

```bash
kubectl run pod1 --image=nginx -n ivolve
kubectl run pod2 --image=nginx -n ivolve
kubectl run pod3 --image=nginx -n ivolve
```

Verify:

```bash
kubectl get pods -n ivolve
```

All three Pods reached the `Running` state.

## Step 4: Test the ResourceQuota

Attempt to create a fourth Pod:

```bash
kubectl run pod4 --image=nginx -n ivolve
```

Kubernetes rejected the request with the following error:

```text
Error from server (Forbidden): pods "pod4" is forbidden:
exceeded quota: ivolve-quota, requested: pods=1,
used: pods=3, limited: pods=3
```

## Step 5: Verify the Final State

```bash
kubectl get namespace ivolve
kubectl get resourcequota -n ivolve
kubectl get pods -n ivolve
```

Final verification:
- Namespace status: `Active`
- ResourceQuota usage: `3/3`
- `pod1`: `Running`
- `pod2`: `Running`
- `pod3`: `Running`
- `pod4`: Rejected because the quota limit was reached

## Conclusion

Successfully created the `ivolve` namespace and enforced a maximum of three Pods using a Kubernetes ResourceQuota. The fourth Pod creation request was denied, confirming that quota enforcement works correctly.

<img width="900" height="872" alt="Screenshot 2026-10-27 002436" src="https://github.com/user-attachments/assets/d413958e-9b15-4261-896a-4be768c8753d" />

