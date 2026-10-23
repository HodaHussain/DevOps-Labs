# Lab 6: Docker Environment & Resource Management

## Objective
The objective of this lab is to build Docker images, configure containers using environment variables, and manage container CPU and memory resources.

## 1. Build the First Docker Image

Created a Dockerfile using `python:3.12-slim` as the base image, installed the required Python dependencies, and copied the application files into the image.

**Image name:** `ivolve1`

## 2. Run the First Container

Ran the first container with environment variables and resource limits.

- **Container:** `lab6-container1`
- **Application:** `iVolveApp1`
- **Environment:** `stg`
- **CPU limit:** 1 CPU
- **Memory limit:** 256 MB
- **Host port:** 15000
- **Container port:** 5000

## 3. Configure Environment Variables Using a File

Created an `env.txt` file containing:

```text
APP_NAME=iVolveApp2
APP_ENV=prod
```

Ran the second container using the `--env-file` option.

- **Container:** `lab6-container2`
- **Host port:** 15001
- **Container port:** 5000

## 4. Build the Second Docker Image

Created `Dockerfile.ivolve2` based on the first image and configured the default environment variables.

```dockerfile
FROM ivolve1

ENV APP_NAME=iVolveApp3
ENV APP_ENV=dev
```

Built the image named `ivolve2`.

## 5. Run the Third Container

Ran a container from `ivolve2` using the default environment variables.

- **Container:** `lab6-container3`
- **Application:** `iVolveApp3`
- **Environment:** `dev`
- **Host port:** 15002
- **Container port:** 5000

## 6. Verification

Verified the application response from inside each container. All three containers returned the expected application name and environment.

Tested the `/health` endpoint in all three containers. Each returned:

```json
{"status":"healthy"}
```

## Conclusion

Successfully built two Docker images and ran three containers with different environment configurations. Practiced using environment variables, environment files, and CPU and memory resource limits.


<img width="1025" height="646" alt="Screenshot 2026-10-23 191402" src="https://github.com/user-attachments/assets/920ffa2b-39f1-4a18-bb00-d0edf4674b21" />
<img width="1048" height="778" alt="Screenshot 2026-10-23 192519" src="https://github.com/user-attachments/assets/d9dec7d5-1063-4bb3-b57d-d983de69f97b" />
<img width="1061" height="485" alt="Screenshot 2026-10-23 191917" src="https://github.com/user-attachments/assets/31a6e537-28b6-45b2-b10e-343a461a52e9" />
