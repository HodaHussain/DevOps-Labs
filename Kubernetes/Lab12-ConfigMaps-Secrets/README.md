# Lab 12: Managing Configuration and Sensitive Data with ConfigMaps and Secrets

## Objective

Create a ConfigMap to store non-sensitive MySQL configuration and a Secret to store sensitive MySQL credentials in the `ivolve` namespace.

## Environment

- Kubernetes Playground
- Namespace: `ivolve`
- ConfigMap: `ivolve-cm`
- Secret: `ivolve-secret`

> Note: Kubernetes resource names must be lowercase. The names `ivolve-cm` and `ivolve-secret` are used instead of the mixed-case names specified in the lab.

## Step 1: Verify the Namespace

```bash
kubectl get namespace ivolve
```

The namespace was successfully created and its status was `Active`.

## Step 2: Create the ConfigMap

The ConfigMap stores non-sensitive configuration values:

- `DB_HOST`: `mysql` (expected headless Service name; the Service has not yet been created or verified).
- `DB_USER`: `ivolveUser` (example application database username).

```bash
kubectl create configmap ivolve-cm \
  --from-literal=DB_HOST=mysql \
  --from-literal=DB_USER=ivolveUser \
  -n ivolve
```

Verify the ConfigMap:

```bash
kubectl describe configmap ivolve-cm -n ivolve
```

The output confirmed that both `DB_HOST` and `DB_USER` were present.

## Step 3: Create the Secret Manifest

Create a YAML file named `ivolve-secret.yaml`:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: ivolve-secret
  namespace: ivolve
type: Opaque
data:
  MYSQL_ROOT_PASSWORD: cm9vdDEyMw==
  DB_PASSWORD: aXZvbHZlMTIz
```

The example values are Base64-encoded:

- `MYSQL_ROOT_PASSWORD`: `root123`
- `DB_PASSWORD`: `ivolve123`

These are demonstration credentials only and must not be used in production.

Apply the manifest:

```bash
kubectl apply -f ivolve-secret.yaml
```

## Step 4: Verify the Secret

```bash
kubectl get secret ivolve-secret -n ivolve
kubectl describe secret ivolve-secret -n ivolve
```

The verification output confirmed:
- Type: `Opaque`
- Data entries: `2`
- `MYSQL_ROOT_PASSWORD`: 7 bytes
- `DB_PASSWORD`: 9 bytes

The password values were not displayed in the verification output.

## Step 5: Final Verification

```bash
kubectl get configmap ivolve-cm -n ivolve
kubectl get secret ivolve-secret -n ivolve
kubectl get namespace ivolve
```

All three resources were verified successfully.

## Security Notes

- Base64 is an encoding method, not encryption.
- Do not use real passwords in demonstration manifests or commit real credentials to GitHub.
- Production environments should use stronger secret-management practices and appropriate access controls.

## Conclusion

Successfully created and verified a ConfigMap containing two non-sensitive MySQL configuration values and a Secret containing two Base64-encoded credential values in the `ivolve` namespace.

The MySQL StatefulSet and headless Service were not created as part of these steps. The `DB_HOST` value must be checked against the actual Service name when MySQL is deployed.



<img width="900" height="802" alt="Screenshot 2026-10-27 003831" src="https://github.com/user-attachments/assets/a6c1d326-7e14-4d96-b54e-a22e4a954cfa" />
<img width="762" height="500" alt="Screenshot 2026-10-27 004059" src="https://github.com/user-attachments/assets/c9ed03de-c747-49ed-9197-796df10c39f9" />
<img width="741" height="360" alt="Screenshot 2026-10-27 003948" src="https://github.com/user-attachments/assets/71d6b378-fa31-4f9d-8818-6371ad06fafa" />
