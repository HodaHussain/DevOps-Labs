# Lab 5: Trivy Security Scanning

## Objective
Scan Docker images for security vulnerabilities using Trivy and compare the results before and after improving the image.

## 1. Install and Verify Trivy
Installed Trivy and verified the installation using:

```bash
trivy --version
```

## 2. Scan the Original Image
Scanned the original image and filtered the results to show HIGH and CRITICAL vulnerabilities:

```bash
trivy image --scanners vuln --severity HIGH,CRITICAL --format table trivy-lab:v1
```

The original image scan reported 27 Node.js vulnerabilities: 26 HIGH and 1 CRITICAL. The scan also displayed operating-system findings and an unsupported Debian version warning.

## 3. Save the Original Scan Report

```bash
trivy image --scanners vuln --severity HIGH,CRITICAL --format json --output trivy-before.json trivy-lab:v1
```

## 4. Build the Updated Image
Updated the application image to use `node:24-alpine`, configured Express as a dependency, and used `npm ci --omit=dev` in the Dockerfile.

Built the updated image:

```bash
docker build --network=host -t ivolve-app:v2 .
```

## 5. Test the Updated Container

```bash
docker run -d --name trivy-test-v2 -p 3001:3000 ivolve-app:v2
```

Verified that the application responded successfully from inside the container with HTTP status 200.

## 6. Scan the Updated Image

```bash
trivy image --scanners vuln --severity HIGH,CRITICAL --format json --output trivy-after.json ivolve-app:v2
```

The updated image scan reported:
- Alpine operating system: 0 HIGH and 0 CRITICAL vulnerabilities.
- Node.js packages: 4 HIGH and 0 CRITICAL vulnerabilities.

The updated image therefore reduced the reported vulnerabilities, but it was not completely free of HIGH vulnerabilities.

## 7. Generate an HTML Report

Downloaded the Trivy HTML template and generated the report:

```bash
trivy image --scanners vuln --severity HIGH,CRITICAL --format template --template "@html.tpl" --output trivy-report.html ivolve-app:v2
```

The generated HTML report was opened in a browser for review.

## Result
Trivy was used to scan the original and updated Docker images, save JSON scan reports, and generate an HTML report. The updated image had fewer reported vulnerabilities, with four HIGH findings remaining in Node.js packages.

## Screenshots
Screenshots will be added to this repository separately.


<img width="1391" height="912" alt="Screenshot 2026-10-23 184024" src="https://github.com/user-attachments/assets/af51cb4a-00fc-4457-89a1-bbb6cd2b2698" />
<img width="1007" height="205" alt="Screenshot 2026-10-23 182440" src="https://github.com/user-attachments/assets/f5b9d48c-49b6-48ed-b449-ee48161aef6c" />
<img width="1002" height="108" alt="Screenshot 2026-10-23 182348" src="https://github.com/user-attachments/assets/46cb3f9f-6c59-4b52-a84f-428ad22b4247" />
<img width="988" height="402" alt="Screenshot 2026-10-23 182234" src="https://github.com/user-attachments/assets/aaa322c8-3af3-49ad-b723-4c2228fce5d4" />


