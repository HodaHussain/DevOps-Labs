# Lab 4: Docker Image Optimization

## Objective
Optimize a Docker image using a multi-stage build, reduce image size, and run the application using a non-root user.

## Steps Performed

### 1. Create the Original Image
Built the original Docker image using the Maven base image and saved it as `image1`.

### 2. Optimize the Dockerfile
Used a multi-stage build to separate the build environment from the runtime environment.

- Build stage: `maven:3.9.15-eclipse-temurin-17-alpine`
- Runtime stage: `eclipse-temurin:17-jre-alpine`
- Copied only the generated JAR file into the final image.
- Created a non-root user named `appuser`.
- Configured the application to run on port `8080`.

### 3. Build the Optimized Image
Built the optimized image and tagged it as `image2`.

### 4. Compare Image Sizes

| Image | Size on Disk |
|---|---:|
| Original (`image1`) | 671 MB |
| Optimized (`image2`) | 294 MB |

The optimized image reduced disk usage by approximately 56%.

### 5. Run and Test the Application
Ran the original and optimized containers on separate host ports.

- Original container: port `18081`
- Optimized container: port `18082`
- Verified the optimized container runs as `appuser`.
- Tested the application and received HTTP 200 with the response: `Hello from Dockerized Spring Boot!`

### 6. Save the Image
Exported the optimized image to a TAR archive using `docker save`.

## Result
The multi-stage build reduced image size and allowed the application to run as a non-root user.

## Screenshots
Screenshots will be added to this repository after uploading them.
